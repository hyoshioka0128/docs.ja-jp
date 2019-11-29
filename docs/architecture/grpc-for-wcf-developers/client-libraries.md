---
title: GRPC クライアントライブラリの作成-WCF 開発者向け gRPC
description: GRPC サービス用の共有クライアントライブラリ/パッケージについて説明します。
ms.date: 09/02/2019
ms.openlocfilehash: 2135fe8b24a2311a31cb2bed191d290b1112bc66
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73967884"
---
# <a name="create-grpc-client-libraries"></a>GRPC クライアントライブラリを作成する

GRPC アプリケーション用のクライアントライブラリを配布する必要はありません。 組織内に `.proto` ファイルの共有ライブラリを作成することができます。また、他のチームはこれらのファイルを使用して、独自のプロジェクトでクライアントコードを生成できます。 ただし、プライベート NuGet リポジトリがあり、他の多くのチームが .NET Core を使用している場合は、サービスプロジェクトの一部としてクライアント NuGet パッケージを作成して発行すると、サービスを共有して昇格させることができます。

クライアントライブラリを配布する利点の1つは、生成された gRPC および Protobuf クラスを、便利な "便利な" メソッドとプロパティを使用して拡張できることです。 クライアントコードでは、サーバーと同様に、すべてのクラスが `partial` として宣言されているため、生成されたコードを編集せずに、すべてのクラスを拡張できます。 これは、コンストラクター、メソッド、計算されたプロパティなどを基本型に簡単に追加できることを意味します。

> [!CAUTION]
> 重要な機能を提供するためにカスタムコードを使用し**ない**でください。これは、機能が、他の言語や Python や Java などのプラットフォームを使用しているチームではなく、共有ライブラリを使用して .net チームに限定されることを意味します。

複数のチームが頻繁に異なるプログラミング言語とフレームワークを使用している場合、または API に外部からアクセスできる場合は、`.proto` ファイルを共有するだけで、開発者が独自のクライアントを生成できるようになります。これは、可能な限り多くのチームが gRPC サービスにアクセスできるようにするための最善の方法です。

## <a name="useful-extensions"></a>便利な拡張機能

.NET には、オブジェクトのストリームを処理するために一般的に使用されるインターフェイスとして、<xref:System.Collections.Generic.IEnumerable%601> と <xref:System.IObservable%601>の2つがあります。 .NET Core 3.0 およびC# 8.0 以降では、ストリームを非同期処理するための <xref:System.Collections.Generic.IAsyncEnumerable%601> インターフェイスと、インターフェイスを使用するための `await foreach` 構文があります。 このセクションでは、これらのインターフェイスを gRPC ストリームに適用する再利用可能なコードを示します。

.NET Core gRPC クライアントライブラリには、`IAsyncEnumerable<T>`を作成する `IAsyncStreamReader<T>` の `ReadAllAsync` 拡張メソッドがあります。 事後対応型プログラミングを使用している開発者にとっては、`IObservable<T>` を作成するための同等の拡張メソッドは、次のようになります。

### <a name="iobservable"></a>IObservable

`IObservable<T>` インターフェイスは、`IEnumerable<T>`の "リアクティブな" 逆関数です。 ストリームから項目をプルするのではなく、事後対応型のアプローチによって、ストリームをサブスクライバーにプッシュすることができます。 これは gRPC ストリームとよく似ており、`IAsyncStreamReader<T>`の `IObservable<T>` を簡単にラップできます。

このコードは `IAsyncEnumerable<T>` コードC#よりも長くなっています。では observable を操作するためのサポートが組み込まれていないため、実装クラスを手動で作成する必要があります。 ただし、これはジェネリッククラスです。そのため、1つの実装がすべての型で動作します。

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;

namespace Grpc.Core
{
    public class GrpcStreamObservable<T> : IObservable<T>
    {
        private readonly IAsyncStreamReader<T> _reader;
        private readonly CancellationToken _token;
        private int _used;

        public Observable(IAsyncStreamReader<T> reader, CancellationToken token = default)
        {
            _reader = reader;
            _token = token;
            _used = 0;
        }

        public IDisposable Subscribe(IObserver<T> observer) =>
            Interlocked.Exchange(ref _used, 1) == 0
                ? new GrpcStreamSubscription(_reader, observer, _token)
                : throw new InvalidOperationException("Subscribe can only be called once.");

    }
}
```

> [!IMPORTANT]
> この観測可能な実装では、`Subscribe` メソッドを1回だけ呼び出すことができます。これは、複数のサブスクライバーがストリームからの読み取りを試みた場合に混乱が生じるためです。 Observable のバッファリングと反復可能な共有を有効にする、のよう `Replay` な演算子が[あります。](https://www.nuget.org/packages/System.Reactive.Linq)これは、この実装で使用できます。

`GrpcStreamSubscription` クラスは、`IAsyncStreamReader`の列挙体を処理します。

```csharp
public class GrpcStreamSubscription : IDisposable
{
    private readonly Task _task;
    private readonly CancellationTokenSource _tokenSource;
    private bool _completed;

    public Subscription(IAsyncStreamReader<T> reader, IObserver<T> observer, CancellationToken token)
    {
        Debug.Assert(reader != null);
        Debug.Assert(observer != null);
        _tokenSource = new CancellationTokenSource();
        token.Register(_tokenSource.Cancel);
        _task = Run(reader, observer, _tokenSource.Token);
    }

    private async Task Run(IAsyncStreamReader<T> reader, IObserver<T> observer, CancellationToken token)
    {
        while (!token.IsCancellationRequested)
        {
            try
            {
                if (!await reader.MoveNext(token)) break;
            }
            catch (RpcException e) when (e.StatusCode == Grpc.Core.StatusCode.NotFound)
            {
                break;
            }
            catch (OperationCanceledException)
            {
                break;
            }
            catch (Exception e)
            {
                observer.OnError(e);
                _completed = true;
                return;
            }

            observer.OnNext(reader.Current);
        }

        _completed = true;
        observer.OnCompleted();
    }

    public void Dispose()
    {
        if (!_completed && !_tokenSource.IsCancellationRequested)
        {
            _tokenSource.Cancel();
        }

        _tokenSource.Dispose();
        _task.Dispose();
    }

}
```

ここで必要なのは、ストリームリーダーから観測可能なを作成するための単純な拡張メソッドです。

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using System.Threading.Tasks;

namespace Grpc.Core
{
    public static class AsyncStreamReaderObservableExtensions
    {
        public static IObservable<T> AsObservable<T>(this IAsyncStreamReader<T> reader) =>
            new GrpcStreamObservable<T>(reader);
    }
}
```

## <a name="summary"></a>概要

`IAsyncEnumerable` モデルと `IObservable` モデルは、.NET でのデータの非同期ストリームを処理するための適切にサポートされ、適切に記述された方法です。 gRPC ストリームは、最新の .NET Core フレームワークとリアクティブ/非同期プログラミングスタイルとの密接な統合を実現するために、両方のパラダイムに適しています。

>[!div class="step-by-step"]
>[前へ](streaming-versus-repeated.md)
>[次へ](security.md)
