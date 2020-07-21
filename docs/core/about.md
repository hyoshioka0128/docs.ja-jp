---
title: .NET Core の概要
description: .NET Core の特性と構成について説明し、他の .NET 実装と比較します。
ms.date: 03/26/2020
ms.openlocfilehash: d5ef79fe5a8fbb56beae77edd01830fe6561fa51
ms.sourcegitcommit: 4ad2f8920251f3744240c3b42a443ffbe0a46577
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86100731"
---
# <a name="net-core-overview"></a>.NET Core の概要

> [!div class="button"]
> [.NET Core のダウンロード](https://dotnet.microsoft.com/download)

.NET Core には次の特徴があります。

- **クロス プラットフォーム:** Windows、macOS、Linux の[オペレーティング システム](https://github.com/dotnet/core/blob/master/os-lifecycle-policy.md)で実行されます。
- **オープン ソース:** .NET Core フレームワークは[オープン ソース](https://github.com/dotnet/core)であり、MIT および Apache 2 ライセンスを使用します。 .NET Core は [.NET Foundation](https://dotnetfoundation.org/) プロジェクトです。
- **最新:** 非同期プログラミング、構造体を使用したコピーなしのパターン、コンテナーのリソース管理など、最新のパラダイムを実装しています。
- **パフォーマンス:** [ハードウェア組み込み](https://devblogs.microsoft.com/dotnet/hardware-intrinsics-in-net-core/)、[階層化コンパイル](https://github.com/dotnet/coreclr/blob/master/Documentation/design-docs/tiered-compilation.md)、[Span\<T>](../standard/memory-and-spans/index.md) などの機能を使用して、[ハイ パフォーマンス](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-core-3-0/)を提供します。
- **環境全体での一貫性:** x64、x86、ARM を含めた複数のオペレーティング システムとアーキテクチャ上でコードが同じ動作で実行されます。
- **コマンドライン ツール:** ローカル開発と継続的インテグレーションで使用できる、使いやすいコマンドライン ツールが含まれます。
- **柔軟な展開:** アプリに .NET Core を含めたり、サイド バイ サイドでインストールしたりすること (ユーザー全体またはシステム全体のインストール) ができます。 [Docker コンテナー](docker/introduction.md)で使用できます。

## <a name="languages"></a>言語

.NET Core のアプリケーションとライブラリを記述するには、[C#](../csharp/index.yml)、[Visual Basic](../visual-basic/index.yml)、[F#](../fsharp/index.yml) 言語を使用できます。 これらの言語は、任意のテキスト エディターまたは統合開発環境 (IDE) で使用できます。これには次のものが含まれます。

- [Visual Studio](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link)
- [Visual Studio Code](https://code.visualstudio.com/download)

エディターの統合は、[OmniSharp](https://www.omnisharp.net/) および [Ionide](https://ionide.io) プロジェクトの共同作成者によって、一部提供されています。

## <a name="apis"></a>API

.NET Core では、あらゆる種類のアプリをビルドするためのフレームワークを公開しています。

* [ASP.NET Core](/aspnet/core/) を使用したクラウド アプリ
* [Xamarin](/xamarin) を使用したモバイル アプリ
* [System.Device.GPIO](https://docs.microsoft.com/archive/msdn-magazine/2019/august/net-core-cross-platform-iot-programming-with-net-core-3-0) を使用した IoT アプリ
* [WPF](../desktop-wpf/overview/index.md) と Windows フォームを使用した Windows クライアント アプリ
* 機械学習の [ML.NET](../machine-learning/index.yml)

次のような一般的なニーズを満たす多くの API が含まれます。

- <xref:System.Boolean?displayProperty=nameWithType> や <xref:System.Int32?displayProperty=nameWithType> などのプリミティブ型。
- <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> や <xref:System.Collections.Generic.Dictionary%602?displayProperty=nameWithType> などのコレクション。
- <xref:System.Net.Http.HttpClient?displayProperty=nameWithType> や <xref:System.IO.FileStream?displayProperty=nameWithType> などのユーティリティ型。
- <xref:System.Data.DataSet?displayProperty=nameWithType> や <xref:System.Data.Entity.DbSet?displayProperty=nameWithType> などのデータ型。
- <xref:System.Span%601?displayProperty=nameWithType>、<xref:System.Numerics.Vector?displayProperty=nameWithType>、[Pipelines](../standard/io/pipelines.md) などの高パフォーマンス型。

.NET core では [.NET Standard](../standard/net-standard.md) 仕様を実装することで .NET Framework や Mono の API との互換性を提供します。

## <a name="composition"></a>コンポジション

.NET Core は、次の部分で構成されます。

- 型システム、アセンブリ読み込み、ガベージ コレクター、ネイティブ相互運用機能、およびその他の基本的なサービスを提供する [.NET Core ランタイム](https://github.com/dotnet/runtime/tree/master/src/coreclr)。 [.NET Core フレームワーク ライブラリ](https://github.com/dotnet/runtime/tree/master/src/libraries)はプリミティブ データ型、アプリ コンポジションの種類、および基本的なユーティリティを提供します。
- Web アプリ、IoT アプリ、モバイル バックエンドなど、最新のクラウドベースのインターネットに接続されているアプリを構築するためのフレームワークを提供する [ASP.NET Core ランタイム](https://github.com/dotnet/aspnetcore)。
- .NET Core の開発者エクスペリエンスを実現する [.NET Core CLI](https://github.com/dotnet/sdk) および言語コンパイラ ([Roslyn](https://github.com/dotnet/roslyn) と [F#](https://github.com/microsoft/visualfsharp))。
- .NET Core アプリと CLI コマンドの起動に使用する [dotnet コマンド](./tools/dotnet.md)。 ランタイムの選択とホスト、アセンブリ読み込みポリシーの提供、アプリおよびツールの起動が行われます。

### <a name="open-source"></a>ソースを開く

[.NET Core](about.md) は、[オープンソース](https://github.com/dotnet/runtime/blob/master/LICENSE.TXT)の汎用開発プラットフォームです。 Windows、macOS、Linux 用の .NET Core アプリを、x64、x86、ARM32、ARM64 の各プロセッサ用に作成できます。 フレームワークと API は、[クラウド](/aspnet/core/)、[IoT](https://docs.microsoft.com/archive/msdn-magazine/2019/august/net-core-cross-platform-iot-programming-with-net-core-3-0)、[クライアント UI](../desktop-wpf/overview/index.md)、[機械学習](../machine-learning/index.yml)用に提供されています。

## <a name="support"></a>サポート

.NET Core は、Windows、macOS、Linux 上で [Microsoft によってサポート](https://dotnet.microsoft.com/platform/support/policy)されています。 セキュリティと品質に関する更新が定期的に行われます (毎月第 2 火曜日)。

Microsoft からの .NET Core のバイナリ配布は、Azure 内のマイクロソフトが管理するサーバーで構築されてテストされ、Microsoft のエンジニアリングおよびセキュリティ プラクティスに従っています。

Red Hat Enterprise Linux (RHEL) では [.NET Core は Red Hat によってサポート](https://developers.redhat.com/topics/dotnet/)されます。 Red Hat がソースから .NET Core をビルドして、[Red Hat ソフトウェア コレクション](https://developers.redhat.com/products/softwarecollections/overview/)で使用できるようにします。 Red Hat とマイクロソフトが共同して、.NET Core が RHEL 上で適切に動作するようにします。

Tizen プラットフォームでは、[Tizen によって .NET Core がサポートされています](https://developer.tizen.org/development/training/.net-application)。
