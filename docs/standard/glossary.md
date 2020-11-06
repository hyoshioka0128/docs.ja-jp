---
title: .NET 用語集
description: .NET のドキュメントで使われている用語からいくつか選択してその意味を説明します。
ms.date: 10/13/2020
ms.technology: dotnet-standard
ms.openlocfilehash: 3de9e0aea253b42d65199dc3d66f026dd023f4c7
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/20/2020
ms.locfileid: "92224405"
---
# <a name="net-glossary"></a>.NET 用語集

この用語集の主な目的は、.NET のドキュメントで定義なしに頻繁に出現する用語と頭字語の意味を明確にすることです。

## <a name="aot"></a>AOT

Ahead Of Time コンパイラ。

[JIT](#jit) と同様に、このコンパイラも [IL](#il) をマシン コードに変換します。 JIT コンパイルとは異なり、AOT コンパイルはアプリケーションが実行される前に行われ、通常は、別のコンピューターで実行されます。 AOT ツール チェーンは実行時にコンパイルされないので、コンパイルに費やされる時間を最小限に抑える必要はありません。 つまり、より多くの時間を最適化に費やすことができます。 AOT のコンテキストはアプリケーション全体であるため、AOT コンパイラはモジュール間のリンクとプログラム全体の分析も実行します。これは、すべての参照が追跡されて、1 つの実行可能ファイルが生成されることを意味します。

「[CoreRT](#corert)」と「[.NET Native](#net-native)」を参照してください。

## <a name="app-model"></a>アプリ モデル

[ワークロード](#workload)固有の API。 次に例をいくつか示します。

* ASP.NET
* ASP.NET Web API
* Entity Framework (EF)
* Windows Presentation Foundation (WPF)
* Windows Communication Foundation (WCF)
* Windows Workflow Foundation (WF)
* Windows フォーム (WinForms)

## <a name="aspnet"></a>ASP.NET

.NET Framework に付属している ASP.NET の元の実装。

ASP.NET は、ASP.NET Core を含む ASP.NET の両方の実装を指す包括的な用語として使われることがあります。 どちらを意味するかはコンテキストによって決まります。 両方の実装を意味するために ASP.NET を使っているのではないことを明確にしたい場合は、ASP.NET 4.x を参照してください。

[ASP.NET のドキュメント](/aspnet/#pivot=aspnet)をご覧ください。

## <a name="aspnet-core"></a>ASP.NET Core

ASP.NET のクロスプラットフォームで高パフォーマンスなオープンソースの実装。

[ASP.NET Core のドキュメント](/aspnet/#pivot=core)をご覧ください。

## <a name="assembly"></a>アセンブリ

アプリケーションまたは他のアセンブリから呼び出すことができる API のコレクションを含む *.dll*/ *.exe* ファイル。

アセンブリは、インターフェイス、クラス、構造体、列挙型、デリゲートなどの種類を含むことができます。 プロジェクトの *bin* フォルダー内のアセンブリは、" *バイナリ* " と呼ばれることもあります。 「[ライブラリ](#library)」もご覧ください。

## <a name="bcl"></a>BCL

基本クラス ライブラリ。 " *フレームワーク ライブラリ* " とも呼ばれます。

System.\* (および限られた範囲の Microsoft.\*) 名前空間を構成するライブラリのセット。 BCL は汎用の下位レベル フレームワークであり、ASP.NET Core などの上位レベル アプリケーション フレームワークはそれを基にして構築されています。

[.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)用の BCL のソース コードは、[.NET ランタイム リポジトリ](https://github.com/dotnet/runtime)に含まれています。 この新しい .NET の実装用の BCL API の大部分は、.NET Framework でも使用できるため、このソース コードは、.NET Framework BCL ソース コードがブランチしたものと考えることができます。

## <a name="clr"></a>CLR

共通言語ランタイム (Common Language Runtime)。

厳密な意味はコンテキストによって異なります。 共通言語ランタイムは、通常、[.NET Framework](#net-framework) のランタイム、または [.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)のランタイムを指します。

CLR によって、メモリの割り当てと管理が処理されます。 CLR は、アプリの実行だけでなく、[JIT](#jit) コンパイラを使って実行時にコードを生成してコンパイルする仮想マシンでもあります。

.NET Framework の CLR 実装は Windows のみです。

.NET 5 以降のバージョンの CLR 実装 (Core CLR とも呼ばれる) は、.NET Framework CLR と同じコード ベースから構築されます。 当初は、Core CLR は Silverlight のランタイムであり、複数のプラットフォーム (特に Windows と OS X) で実行するように設計されていました。これはまだ[クロスプラットフォーム](#cross-platform) ランタイムですが、多くの Linux ディストリビューションのサポートが含まれるようになりました。

「[ランタイム](#runtime)」も参照してください。

## <a name="core-clr"></a>Core CLR

[.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)の共通言語ランタイム。

「[CLR](#clr)」を参照してください

## <a name="corert"></a>CoreRT

[CLR](#clr) とは異なり、CoreRT は仮想マシンではありません。つまり、[JIT](#jit) が含まれないため、実行時にコードを生成して実行する機能はありません。 ただし、[GC](#gc) およびランタイム型識別 (RTTI) とリフレクションの機能は備えています。 ただ、CoreRT の型システムはリフレクション用のメタデータが必要ないように設計されています。 メタデータが必要ないと、[AOT](#aot) ツール チェーンで余分なメタデータのリンクを削除し、(さらに重要なこととして) アプリが使っていないコードを特定することができます。 CoreRT は開発中です。

[.NET Native と CoreRT の概要](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)をご覧ください。

## <a name="cross-platform"></a>クロスプラットフォーム

Linux、Windows、iOS など、複数の異なるオペレーティング システム上で使用できるアプリケーションを開発し、実行することができます。OS ごとに作成し直す必要はありません。 そのため、異なるプラットフォーム上のアプリケーション間でコードを再利用し、一貫性を保つことができます。

## <a name="ecosystem"></a>エコシステム

特定のテクノロジ用のアプリケーションを構築して実行するために使われるすべての実行時ソフトウェア、開発ツール、およびコミュニティ リソース。

".NET エコシステム" という用語は ".NET スタック" などの用語と似ていますが、サードパーティのアプリとライブラリを含む点が異なります。 文章での使用例を次に示します。

- "[.NET Standard](#net-standard) の背後にある意図は、.NET エコシステムの高度な統一性を確立することです。"

## <a name="framework"></a>フレームワーク

一般に、特定のテクノロジに基づくアプリケーションの開発と展開を容易にする API の包括的なコレクション。 この一般的な意味でのアプリケーション フレームワークの例としては、ASP.NET Core や Windows フォームなどがあります。 「[ライブラリ](#library)」もご覧ください。

以下の用語の "フレームワーク" という単語には、別の意味があります。

- [.NET Framework](#net-framework)
- [ターゲット フレームワーク](#target-framework)
- [TFM (ターゲット フレームワーク モニカー)](#tfm)
- [フレームワークに依存するアプリ](../core/deploying/index.md#publish-framework-dependent)

従来の .NET ドキュメントでは、"フレームワーク" は [.NET の実装](#implementation-of-net)を指している場合があります。 たとえば、ある記事では .NET 5 をフレームワークと呼んでいる場合があります。

## <a name="gc"></a>[GC]

ガベージ コレクター (Garbage Collector)。

ガベージ コレクターは、自動メモリ管理の実装です。  GC は、使われなくなったオブジェクトによって占有されているメモリを解放します。

「[ガベージ コレクション](garbage-collection/index.md)」をご覧ください。

## <a name="il"></a>IL

中間言語 (Intermediate Language)。

C# などの高レベル .NET 言語は、中間言語 (IL) と呼ばれるハードウェアに依存しない命令セットにコンパイルされます。 IL は、MSIL (Microsoft IL) や CIL (Common IL) などと呼ばれることもあります。

## <a name="jit"></a>JIT

Just-In-Time コンパイラ。

[AOT](#aot) と同様に、このコンパイラは [IL](#il) をプロセッサが理解するマシン コードに変換します。 AOT とは異なり、JIT のコンパイルはオンデマンドで行われ、コードを実行する必要があるコンピューター上で実行されます。 JIT コンパイルはアプリケーションの実行中に行われるため、コンパイル時間は実行時間の一部になります。 したがって、JIT コンパイラでは、コードの最適化に要する時間と、結果のコードによって得られる時間の節約のバランスを考える必要があります。 ただし、JIT は実際のハードウェアを認識するので、開発者はさまざまな実装を出荷する必要がなくなります。

## <a name="implementation-of-net"></a>.NET の実装

.NET の実装には次のものが含まれます。

- 1 つまたは複数のランタイム。 次に例を示します。 [CLR](#clr)、[CoreRT](#corert)。
- .NET Standard の 1 つのバージョンを実装し、他の API を含むことができるクラス ライブラリ。 たとえば、[.NET Framework](#net-framework) および [.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)の [BCL](#bcl) です。
- 必要に応じて、1 つまたは複数のアプリケーション フレームワーク。 次に例を示します。 .NET Framework と .NET 5 には、[ASP.NET](#aspnet)、Windows フォーム、WPF が含まれます。
- 必要に応じて、開発ツール。 一部の開発ツールは、複数の実装間で共有されます。

.NET の実装の例:

- [.NET Framework](#net-framework)
- [.NET 5 以降のバージョン (.NET Core 2.1 から 3.1 を含む)](#net-5-and-later-versions)
- [ユニバーサル Windows プラットフォーム (UWP)](#uwp)
- [Mono](#mono)

## <a name="library"></a>ライブラリ

アプリまたは他のライブラリで呼び出すことができる API のコレクション。 .NET ライブラリは 1 つ以上の[アセンブリ](#assembly)で構成されます。

ライブラリと[フレームワーク](#framework)は同義語として使われることがよくあります。

## <a name="mono"></a>Mono

Mono はオープン ソースであり、主に小規模なランタイムが必要な場合に使用される[クロスプラットフォーム](#cross-platform)の .NET 実装です。 Android、Mac、iOS、tvOS、および watchOS 上の Xamarin アプリケーションで利用されるランタイムであり、フットプリントの小さいアプリに重点が置かれています。

現在公開されているすべての .NET Standard バージョンをサポートしています。

これまで Mono は .NET Framework の多数の API を実装し、Unix で人気の高い機能の一部をエミュレートしていました。 また、Unix のそのような機能に依存する .NET アプリケーションを実行するために使用されることもあります。

一般的に Mono は、[Just-In-Time コンパイラ](#jit)と共に使用されますが、iOS のようなプラットフォームに使用される完全な[静的コンパイラ (Ahead Of Time コンパイル)](#aot) としても機能します。

[Mono のドキュメント](https://www.mono-project.com/docs/)を参照してください。

## <a name="net"></a>.NET

[.NET Standard](#net-standard) とすべての [.NET の実装](#implementation-of-net)およびワークロードを表す包括的な用語。 常にすべて大文字で表し、".Net" とは表記されません。

[.NET 5](#net-5-and-later-versions) (現在、プレビュー段階) がリリースされると、すべての新しい .NET 開発で推奨される .NET 実装となります。そのため、一部のコンテキストでは、".NET" は ".NET 5 以降のバージョン" を意味します。

[.NET の基礎](../fundamentals/index.yml)に関するページを参照してください

## <a name="net-5-and-later-versions"></a>.NET 5 以降のバージョン

.NET のクロスプラットフォームで高パフォーマンスなオープンソースの実装。 共通言語ランタイム ([CLR](#clr))、[AOT](#aot) ランタイム ([CoreRT](#corert)。開発中)、基本クラス ライブラリ ([BCL](#bcl))、および [.NET SDK](#net-sdk) が含まれます。

この .NET 実装の以前のバージョンは、.NET Core と呼ばれています。 .Net 5.0 は、.NET Core 3.1 の次のバージョンです。 バージョン 4 は、この .NET の新しい実装を、[.NET Framework](#net-framework) と呼ばれる古い実装と混同しないようにするためにスキップされました。 .NET Framework の現在のバージョンは 4.8 です。

[.NET の基礎](../fundamentals/index.yml)に関するページを参照してください。

## <a name="net-cli"></a>.NET CLI

[.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)用のアプリケーションとライブラリを開発するためのクロスプラットフォーム ツールチェーン。 .NET Core CLI とも呼ばれます。

[.NET CLI](../core/tools/index.md) に関するページを参照してください。

## <a name="net-core"></a>.NET Core

「[.NET 5.0 以降のバージョン](#net-5-and-later-versions)」を参照してください。

## <a name="net-framework"></a>.NET Framework

Windows でのみ動作する .NET の実装。 共通言語ランタイム ([CLR](#clr))、基本クラス ライブラリ ([BCL](#bcl))、および [ASP.NET](#aspnet)、Windows フォーム、WPF などのアプリケーション フレームワーク ライブラリが含まれます。

「[.NET Framework ガイド](../framework/index.yml)」をご覧ください。

## <a name="net-native"></a>.NET Native

Just-In-Time ([JIT](#jit)) ではなく、Ahead Of Time ([AOT](#aot)) でネイティブ コードを生成するコンパイラ ツール チェーン。

コンパイルは、C++ のコンパイラやリンカーと同様に、開発者のコンピューターで行われます。 未使用のコードが削除され、より多くの時間がコードの最適化に費やされます。 ライブラリからコードを抽出し、実行可能ファイルにそれらをマージします。 結果は、アプリ全体を表す 1 つのモジュールです。

UWP は、.NET Native によってサポートされる最初のアプリケーション フレームワークでした。 現在では、Windows、macOS、Linux 用のネイティブ コンソール アプリの構築がサポートされています。

「[Intro to .NET Native and CoreRT](https://github.com/dotnet/corert/blob/master/Documentation/intro-to-corert.md)」(.NET Native と CoreRT の概要) をご覧ください。

## <a name="net-sdk"></a>.NET SDK

[.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)用の .NET アプリケーションとライブラリを開発者が作成できるようにする、一連のライブラリとツール。 .NET Core SDK とも呼ばれます。

アプリ構築用の [.NET CLI](#net-cli)、アプリの構築および実行用の .NET ライブラリとランタイム、CLI コマンドとアプリケーションを実行する dotnet 実行可能ファイル ( *dotnet.exe* ) が含まれます。

[.NET SDK の概要](../core/sdk.md)に関するページを参照してください。

## <a name="net-standard"></a>.NET Standard

.NET の各実装で使用可能な .NET API の正式な仕様。

.NET Standard の仕様は、ドキュメントではライブラリとも呼ばれます。 ライブラリには仕様 (インターフェイス) だけでなく API の実装も含まれるため、.NET Standard を "ライブラリ" と呼ぶのは誤解を招きます。

「[.NET Standard](net-standard.md)」をご覧ください。

## <a name="ngen"></a>NGEN

ネイティブ (イメージ) 生成。

このテクノロジは、永続的な [JIT](#jit) コンパイラと考えることができます。 通常はコードが実行されるコンピューター上でコードをコンパイルしますが、一般にコンパイルはインストール時に行われます。

## <a name="package"></a>package

NuGet パッケージ &mdash; または単にパッケージ &mdash; は、同じ名前の 1 つまたは複数のアセンブリと、作成者名などの追加メタデータを含む、 *.zip* ファイルです。

*.zip* ファイルは、拡張子が *.nupkg* であり、複数のターゲット フレームワークとバージョンで使う *.dll* ファイルや *.xml* ファイルなどのアセットを含むことができます。 アプリまたはライブラリでインストールされるときに、アプリまたはライブラリで指定されているターゲット フレームワークに基づいて適切なアセットが選択されます。 インターフェイスを定義するアセットは *ref* フォルダーにあり、実装を定義するアセットは *lib* フォルダーにあります。

## <a name="platform"></a>platform

オペレーティング システムとそれが動作するハードウェア (Windows、macOS、Linux、iOS、Android)。

文章での使用例を次に示します。

- ".NET Core は、.NET のクロスプラットフォームの実装です。"
- "PCL プロファイルは Microsoft のプラットフォームを表し、.NET Standard はプラットフォームに依存しません。"

従来の .NET のドキュメントでは、[.NET の実装](#implementation-of-net)、またはすべての実装を含む .NET [スタック](#stack)の意味で ".NET プラットフォーム" が使われることがあります。 これらの使用法はどちらも本来の (OS およびハードウェア) の意味と紛らわしい場合があるので、これらの使用法は避けるようにしています。

"開発者プラットフォーム" という語句の "プラットフォーム" には、別の意味があります。これは、アプリをビルドして実行するためのツールとライブラリを提供するソフトウェアを指します。 .NET は、さまざまな種類のアプリケーションをビルドするためのクロスプラットフォームでオープンソースの開発者プラットフォームです。

## <a name="runtime"></a>ランタイム

一般的には、マネージド プログラムの実行環境です。 OS は、ランタイム環境の一部ですが、.NET ランタイムの一部ではありません。 この単語の意味での .NET ランタイムの例をいくつか以下に示します。

- 共通言語ランタイム ([CLR](#clr))
- .NET Native (UWP の場合)
- Mono ランタイム

以下のコンテキストでの "ランタイム" という単語には、別の意味があります。

* [.NET ダウンロード ページ](https://dotnet.microsoft.com/download)。

  ここでの "ランタイム" は、[CLR](#clr) と [BCL](#bcl) (フレームワーク ライブラリ) を合わせた意味となります。これは、コンピューター上で[フレームワークに依存する](../core/deploying/index.md#publish-framework-dependent)アプリを実行できるように、そのコンピューターにダウンロードしてインストールすることができます。

* [.NET 5 (および .NET Core) 以降のバージョン](#net-5-and-later-versions)の[ランタイム識別子 (RID)](../core/rid-catalog.md)。

  ここでの "ランタイム" は、.NET アプリが実行されている OS プラットフォームと CPU アーキテクチャを意味します (例: `linux-x64`)。

従来の .NET ドキュメントでは、次の例に示すように、[.NET の実装](#implementation-of-net)の意味で "ランタイム" を使用することがあります。

- "さまざまな .NET ランタイムで、.NET Standard の特定のバージョンが実装されます。"
- "複数のランタイムでの実行を意図したライブラリは、このフレームワークを対象とする必要があります。" (.NET Standard を指している場合)
- "さまざまな .NET ランタイムで、.NET Standard の特定のバージョンが実装されます。 … .NET ランタイムの各バージョンは、サポートしている .NET Standard の最高のバージョンをアドバタイズします …"

## <a name="stack"></a>スタック

全体としてアプリケーションの構築と実行に使われるプログラミング テクノロジのセット。

".NET スタック" は、.NET Standard および .NET のすべての実装を指します。 ".NET スタック" という語句が .NET の 1 つの実装を示すこともあります。

## <a name="target-framework"></a>ターゲット フレームワーク

.NET アプリまたはライブラリが依存する API のコレクション。

アプリまたはライブラリでは、.NET Standard の 1 つのバージョン (.NET Standard 2.0 など) をターゲットにできます。これは、.NET のすべての実装で標準化された API のセットの仕様です。 また、アプリまたはライブラリは、.NET の特定の実装のバージョンをターゲットにすることもでき、その場合は実装固有の API にアクセスできます。 たとえば、Xamarin.iOS をターゲットにするアプリは、Xamarin が提供する iOS API ラッパーにアクセスできます。

一部のターゲット フレームワーク (.NET Framework など) では、使用可能な API は .NET の実装がシステムにインストールするアセンブリによって定義され、アプリケーション フレームワーク API (たとえば ASP.NET、WinForms) を含む場合があります。 パッケージ ベースのターゲット フレームワーク (.NET Standard、.NET Core など) では、フレームワーク API はアプリまたはライブラリでインストールされるパッケージによって定義されます。 その場合、ターゲット フレームワークで、全体としてフレームワークを構成するすべてのパッケージを参照するパッケージが暗黙的に指定されます。

「[ターゲット フレームワーク](frameworks.md)」をご覧ください。

## <a name="tfm"></a>TFM

ターゲット フレームワーク モニカー (Target Framework Moniker)。

.NET アプリまたはライブラリのターゲット フレームワークを指定するための標準化されたトークン形式。 通常、ターゲット フレームワークは短い名前によって参照されます (`net462` など)。 長い形式の TFM (.NETFramework,Version=4.6.2 など) も存在しますが、一般に、ターゲット フレームワークの指定には使われません。

「[ターゲット フレームワーク](frameworks.md)」をご覧ください。

## <a name="uwp"></a>UWP

ユニバーサル Windows プラットフォーム (Universal Windows Platform)。

モノのインターネット (IoT) のために最新のタッチ対応の Windows アプリケーションとソフトウェアを構築するために使われる .NET の実装。 PC、タブレット、携帯電話、Xbox など、ターゲットにされる可能性があるさまざまな種類のデバイスを統一するように設計されています。 UWP は、一元的なアプリ ストア、実行環境 (AppContainer)、Win32 の代わりに使う Windows API のセット (WinRT) など、多くのサービスを提供します。 アプリは、C++、C#、Visual Basic、および JavaScript で記述することができます。 C# と Visual Basic を使用する場合は、.NET 5 (および .NET Core) 以降のバージョンで .NET API が提供されます。

## <a name="workload"></a>ワークロード

誰かがビルドしているアプリの種類。 [アプリ モデル](#app-model)よりも一般的です。 たとえば、これを含むすべての .NET ドキュメント ページの上部には、 **[ワークロード]** のドロップダウン リストがあります。これにより、 **[Web]** 、 **[モバイル]** 、 **[クラウド]** 、 **[デスクトップ]** 、 **[機械学習 \& データ]** 用のドキュメントに切り替えることができます。

コンテキストによっては、" *ワークロード* " は、特定の種類のアプリをサポートするために、インストールできる Visual Studio 機能のコレクションを指します。 例については、「[ワークロードを選択する](../core/install/windows.md#select-a-workload)」を参照してください。

## <a name="see-also"></a>関連項目

- [.NET の基礎](../fundamentals/index.yml)
- [.NET Framework ガイド](../framework/index.yml)
- [ASP.NET の概要](/aspnet/index#pivot=aspnet)
- [ASP.NET Core の概要](/aspnet/index#pivot=core)
