---
title: .NET Framework から .NET Core への移植
description: 移植プロセスを理解し、.NET Framework プロジェクトを .NET Core に移植する際に役立つツールを確認します。
author: cartermp
ms.date: 10/22/2019
ms.openlocfilehash: 74fe4519e41a07bc78a4dc346f8d1b52b5c7d092
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502770"
---
# <a name="overview-of-porting-from-net-framework-to-net-core"></a>.NET Framework から .NET Core への移植の概要

現在 .NET Framework で実行しているコードの .NET Core への移植を検討する場合があります。 この記事では、次について説明します。

* 移植プロセスの概要。
* コードを .NET Core に移植するときに役立つ場合があるツールの一覧。

## <a name="overview-of-the-porting-process"></a>移植プロセスの概要

多くのプロジェクトは、.NET Framework から .NET Core (または .NET Standard) に比較的簡単に移植できます。 多数の変更が必要ですが、その多くは次に示すパターンどおりです。 .NET Core にアプリ モデルがあるプロジェクト (ライブラリ、コンソール アプリ、デスクトップ アプリケーションなど) では、通常ほとんど変更することはありません。 ASP.NET から ASP.NET Core への移行など、新しいアプリケーション モデルを必要とするプロジェクトでは、多少の作業が必要になりますが、多くのパターンには変換時に使用できるアナログがあります。 このドキュメントでは、ユーザーがどのような主戦略を使用してコード ベースをターゲットの .NET Standard または .NET Core に正常に変換したか理解し、ソリューション全体とプロジェクト別の 2 つのレベルで変換を行う方法について説明します。 アプリ モデル固有の変換については、下部にあるリンクを参照してください。

ご自分のプロジェクトを .NET Core に移植する場合は、次の手順を使用することをお勧めします。 これらの各手順では、動作が変わってしまう可能性がある場所を示しています。それ以降の手順に進む前に、ご自分のライブラリまたはアプリケーションは十分にテストしてください。 最初の手順では、ご自分のプロジェクトを .NET Standard または .NET Core に切り替えられることができるように準備します。 単体テストがある場合は、最初にそれらを変換して、作業中の製品の変更のテストを継続できるようにすることをお勧めします。 .NET Core への移植はコードベースにとって大きな変更となるため、テスト プロジェクトを移植して、ご自分のコードの移植時にテストを実行できるようにすることを強くお勧めします。 MSTest、xUnit、NUnit はすべて .NET Core で動作します。

## <a name="getting-started"></a>作業の開始

このプロセスを通して、次のツールを使用します。

- Visual Studio 2019
- [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) をダウンロードします
- _省略可能_ [dotnet try-convert](https://github.com/dotnet/try-convert) をインストールします

## <a name="porting-a-solution"></a>ソリューションの移植

ソリューションに複数のプロジェクトがある場合は、特定の順序でプロジェクトに対応する必要があるため、移植が複雑に思える場合があります。 他のプロジェクトに依存しないソリューション内のプロジェクトを最初に変換してから、ソリューション全体を変換し続ける、ボトムアップ アプローチでこの変換プロセスは行う必要があります。

次のツールを使用すると、どのプロジェクトから移行するかを割り出すことができます。

- [Visual Studio の依存関係図](/visualstudio/modeling/create-layer-diagrams-from-your-code)に関する説明からは、ソリューション内のコードの有向グラフを作成できます。
- `msbuild _SolutionPath_ /t:GenerateRestoreGraphFile /p:RestoreGraphOutputPath=graph.dg.json` を実行すると、プロジェクト参照の一覧を含む json ドキュメントを生成できます。
- アセンブリの依存関係図を取得するには、`-r DGML` スイッチを使用して [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) を実行します。 詳細については、[このページ](../../standard/analyzers/portability-analyzer.md#solution-wide-view)を参照してください。

依存関係の情報を取得した後は、その情報を使用してリーフ ノードから開始し、次のセクションのステップを適用して依存関係ツリーを操作できます。

## <a name="per-project-steps"></a>プロジェクト別の手順

プロジェクトを .NET Core に移植する場合は、次の手順を使用することをお勧めします。

1. [Visual Studio の変換ツール](/nuget/consume-packages/migrate-packages-config-to-package-reference)を使用して、すべての `packages.config` の依存関係を [PackageReference](/nuget/consume-packages/package-references-in-project-files) 形式に変換します。

   この手順では、依存関係を従来の `packages.config` 形式から変換します。 `packages.config` は .NET Core では機能しないため、パッケージの依存関係がある場合は、この変換が必須です。 また、プロジェクトで直接使用される依存関係のみに対して実行します。これにより、管理する必要がある依存関係の数を減らせるので、後の手順を楽にできます。

1. ご自分のプロジェクト ファイルのファイル構造を新しい SDK 形式のものに変換します。 .NET Core 用の新しいプロジェクトを作成してソース ファイルをコピーするか、ツールを使ってお使いの既存のプロジェクト ファイルを変換することができます。

   .NET Core では、.NET Framework よりも簡素化された (異なる) [プロジェクト ファイル形式](../tools/csproj.md)が使用されます。 続行するには、プロジェクト ファイルをこの形式に変換する必要があります。 このプロジェクト形式では、この時点では、まだターゲットとしたい .NET Framework もターゲットにすることができます。

   [dotnet try-convert](https://github.com/dotnet/try-convert) ツールを使用すると、より小規模なソリューションや個々のプロジェクトを、1 回の操作で .NET Core プロジェクトのファイル形式に移植することが可能です。 `dotnet try-convert` がすべてのプロジェクトに対して動作する保証はありません。また、これが原因となって、依存していた動作に微妙な変更が生じる可能性があります。 これは、自動化できる基本的なことを自動化するための "_開始点_" としてお使いください。 SDK 形式のプロジェクトで使用されるターゲットと旧形式のプロジェクト ファイルで使用されるものとの間には違いが多数あるため、このソリューションではプロジェクトの移行は保証されません。

1. 移植するすべてのプロジェクトを、.NET Framework 4.7.2 以降をターゲットとするように再ターゲットします。

   この手順により、.NET Core で特定の API がサポートされない場合に、.NET Framework 固有のターゲットに対して API の代替を確実に使用できます。

1. すべての依存関係を最新バージョンに更新します。 プロジェクトで、.NET Standard でサポートされていない古いバージョンのライブラリが使用されている場合があります。 ただし、単純に切り替えれば以降のバージョンでサポートされるようにできる場合があります。 ライブラリに破壊的変更がある場合は、コードの変更が必要になることがあります。

1. [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) を使ってアセンブリを分析し、それらが .NET Core に移植可能かどうかを確認します。

   .NET Portability Analyzer ツールでは、ご自分のコンパイル済みのアセンブリを分析し、レポートを生成します。 このレポートには、移植性に関する大まかな概要と、使用している API のうち NET Core では利用できないものそれぞれについての内訳が表示されます。 このツールを使用する場合、変更する必要がある可能性がある API に集中して取り組めるよう、変更するプロジェクトを個々に送信してください。 .NET Core には、多くの API と同等の、ユーザーが切り替えたいと思うものが用意されています。

   Analyzer で生成されたレポートを確認するときの重要な情報は、使用されている実際の API です。必ずしもターゲットのプラットフォームのサポートのパーセンテージではありません。 .NET Standard と Core には、多くの API と同等の選択肢があります。そのため、お使いのライブラリまたはアプリケーションでの API の使われ方のシナリオを理解しておくと、移植において何をする必要があるかを判断することができます。

   同等の API がなく、コンパイラ プリプロセッサ ディレクティブ (つまり、`#if NET45`) を多少使用して、そのプラットフォームに特別対応をする必要がある場合もあります。 この時点では、あなたのプロジェクトでは、変わらず .NET Framework をターゲットにしています。 これらのターゲットがあるケースでは、シナリオとして理解できる広く知られた条件を都度使用することをお勧めします。  たとえば、.NET Core では限定的にしか AppDomain をサポートしていません。しかし、アセンブリを読み込みアンロードするシナリオ用に .NET Core では利用できない新しい API があります。 これをコードで処理するには、一般的に次のような方法を使用します。

   ```csharp
   #if FEATURE_APPDOMAIN_LOADING
   // Code that uses appdomains
   #elif FEATURE_ASSEMBLY_LOAD_CONTEXT
   // Code that uses assembly load context
   #else
   #error Unsupported platform
   #endif
   ```

1. [.NET API アナライザー](../../standard/analyzers/api-analyzer.md)をプロジェクトにインストールして、一部のプラットフォームで <xref:System.PlatformNotSupportedException> をスローする API と、発生する可能性のあるその他の互換性の問題を識別します。

   このツールは移植性アナライザーに似ていますが、.NET Core 上にコードをビルドできるかどうかが分析されるのではなく、実行時に <xref:System.PlatformNotSupportedException> をスローするような方法で API を使っているかどうかが分析されます。 .NET Framework 4.7.2 以上から移行する場合、これは一般的ではありませんが、確認することをお勧めします。 .NET Core で例外をスローする API の詳細については、「[.NET Core で常に例外をスローする API](../compatibility/unsupported-apis.md)」を参照してください。

1. この時点で、ターゲットを .NET Core (一般的にはアプリケーション用) または .NET Standard (ライブラリ用) に切り替えることができます。

   .NET Core と .NET Standard のどちらを選択するかは、プロジェクトの実行場所に大きく関係します。 他のアプリケーションで使用されたり、NuGet 経由で配布されるのがライブラリである場合は、通常は .NET Standard がターゲットとなります。 ただし、パフォーマンスやその他の理由で .NET Core にしかない API がある場合があります。そのような場合、パフォーマンスや機能が低い .NET Standard のビルドがあっても .NET Core をターゲットにする必要があります。 .NET Standard をターゲットにすると、(WebAssembly などの) 新しいプラットフォームでプロジェクトを実行できます。 プロジェクトが (ASP.NET Core など) 特定のアプリケーション フレームワークに依存している場合、ターゲットは依存関係がサポートする内容によって制限されます。

   .NET Framework または .NET Standard 用に条件付きでコードをコンパイルするプリプロセッサ ディレクティブがない場合は、プロジェクト ファイルで次を検索するのと同じくらいこれは簡単です。

   ```xml
   <TargetFramework>net472</TargetFramework>
   ```

   目的のフレームワークに切り替えます。 .NET Core 3.1 の場合、次のようになります。

   ```xml
   <TargetFramework>netcoreapp3.1</TargetFramework>
   ```

   ただし、このライブラリに .NET Framework の特定のビルドを引き続きサポートさせたい場合は、次のように置き換えて[マルチターゲット](../../standard/library-guidance/cross-platform-targeting.md)化させることができます。

   ```xml
   <TargetFrameworks>net472;netstandard2.0</TargetFrameworks>
   ```

   (レジストリ アクセスなどの) Windows 専用の API を使用する場合は、[Windows 互換機能パック](./windows-compat-pack.md)をインストールしてください。

## <a name="next-steps"></a>次の手順

> [!div class="nextstepaction"]
> [依存関係を分析する](third-party-deps.md)
> [NuGet パッケージのパッケージ化](../deploying/creating-nuget-packages.md)
> [ASP.NET から ASP.NET Core への移行](/aspnet/core/migration/proper-to-2x)
