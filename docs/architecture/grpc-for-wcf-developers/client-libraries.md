---
title: GRPC クライアントライブラリの作成-WCF 開発者向け gRPC
description: GRPC サービス用の共有クライアントライブラリ/パッケージについて説明します。
ms.date: 09/02/2019
ms.openlocfilehash: bb58cb3cda4b0cbb3a5d34129961349bcb0093e9
ms.sourcegitcommit: 5fb5b6520b06d7f5e6131ec2ad854da302a28f2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74711456"
---
# <a name="create-grpc-client-libraries"></a>GRPC クライアントライブラリを作成する

GRPC アプリケーション用のクライアントライブラリを配布する必要はありません。 組織内に `.proto` ファイルの共有ライブラリを作成することができます。また、他のチームはこれらのファイルを使用して、独自のプロジェクトでクライアントコードを生成できます。 ただし、プライベート NuGet リポジトリがあり、他の多くのチームが .NET Core を使用している場合は、サービスプロジェクトの一部としてクライアント NuGet パッケージを作成して発行することができます。 これは、サービスの共有と昇格に適した方法です。

クライアントライブラリを配布する利点の1つは、生成された gRPC および Protobuf クラスを、便利な "便利な" メソッドとプロパティを使用して拡張できることです。 クライアントコードでは、サーバーと同様に、すべてのクラスが `partial`として宣言されているため、生成されたコードを編集しなくても、それらを拡張できます。 これは、コンストラクター、メソッド、および計算されるプロパティを基本的な型に簡単に追加できることを意味します。

> [!CAUTION]
> カスタムコードを使用して、重要な機能を提供しないでください。 共有ライブラリを使用する .NET チームにこの重要な機能を制限するのではなく、Python や Java などの他の言語やプラットフォームを使用するチームに提供する必要はありません。

可能な限り多くのチームが gRPC サービスにアクセスできることを確認します。 これを行う最善の方法は、開発者が独自のクライアントを生成できるように `.proto` ファイルを共有することです。 これは、さまざまなチームがさまざまなプログラミング言語やフレームワークを頻繁に使用している場合や、API に外部からアクセスできる場合に、マルチプラットフォーム環境で特に当てはまります。

## <a name="useful-extensions"></a>便利な拡張機能

.NET には、オブジェクトのストリームを処理するために一般的に使用されるインターフェイスとして、<xref:System.Collections.Generic.IEnumerable%601> と <xref:System.IObservable%601>の2つがあります。 .NET Core 3.0 およびC# 8.0 以降では、ストリームを非同期処理するための <xref:System.Collections.Generic.IAsyncEnumerable%601> インターフェイスと、インターフェイスを使用するための `await foreach` 構文があります。 このセクションでは、これらのインターフェイスを gRPC ストリームに適用する再利用可能なコードを示します。

.NET Core gRPC クライアントライブラリには、`IAsyncEnumerable<T>` インターフェイスを作成する `IAsyncStreamReader<T>` の `ReadAllAsync` 拡張メソッドがあります。 事後対応型プログラミングを使用する開発者にとっては、`IObservable<T>` インターフェイスを作成するための同等の拡張メソッドが、次のセクションの例のようになります。

### <a name="iobservable"></a>IObservable

`IObservable<T>` インターフェイスは、`IEnumerable<T>`の "リアクティブな" 逆関数です。 ストリームから項目をプルするのではなく、事後対応型のアプローチによって、ストリームをサブスクライバーにプッシュすることができます。 これは gRPC ストリームとよく似ており、`IAsyncStreamReader<T>` インターフェイスの `IObservable<T>` インターフェイスをラップするのは簡単です。

このコードは `IAsyncEnumerable<T>` コードよりも長くなってC#います。には observable を操作するためのサポートが組み込まれていないためです。 実装クラスは手動で作成する必要があります。 ただし、これはジェネリッククラスであるため、1つの実装がすべての型で動作します。

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
> この監視可能な実装により、`Subscribe` メソッドを1回だけ呼び出すことができます。これは、複数のサブスクライバーがストリームから読み取ろうとすると混乱が生じるためです。 Observable の `Replay` などの演算子が[あります。](https://www.nuget.org/packages/System.Reactive.Linq)これにより、この実装で使用できるのバッファリングと反復可能な共有が可能になります。

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

## <a name="summary"></a>要約

`IAsyncEnumerable` モデルと `IObservable` モデルは、.NET でのデータの非同期ストリームを処理するための適切にサポートされ、適切に記述された方法です。 gRPC ストリームは、両方のパラダイムに適切にマップされ、.NET Core との密接な統合と、リアクティブおよび非同期のプログラミングスタイルを提供します。

>[!div class="step-by-step"]
>[前へ](streaming-versus-repeated.md)
>[次へ](security.md)
