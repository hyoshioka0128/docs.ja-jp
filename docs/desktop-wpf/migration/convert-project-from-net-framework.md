---
title: .NET Core 3.0 への WPF アプリの移行
description: Windows Presentation Foundation (WPF) アプリを .NET Core 3.0 に移行する方法について説明します。
author: mjrousos
ms.date: 09/12/2019
ms.author: mikerou
ms.openlocfilehash: fda4f618ddb4a3edbe6f2dd9fba0b10bc618e88d
ms.sourcegitcommit: 71b8f5a2108a0f1a4ef1d8d75c5b3e129ec5ca1e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84201566"
---
# <a name="migrating-wpf-apps-to-net-core"></a>.NET Core への WPF アプリの移行

この記事では、Windows Presentation Foundation (WPF) アプリを .NET Framework から .NET Core 3.0 に 移行するために必要な手順について説明します。 移植する WPF アプリが手元になくても、このプロセスを試してみたい場合は、[GitHub](https://github.com/dotnet/windows-desktop/tree/master/Samples/BeanTrader) で入手できる **Bean Trader** サンプル アプリを使用できます。 元のアプリ (.NET Framework 4.7.2 をターゲットとする) は、NetFx\BeanTraderClient フォルダーにあります。 まず、一般的にアプリの移植に必要な手順について説明し、次に **Bean Trader** サンプルに適用される特定の変更について説明します。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

.NET Core に移行するには、最初に以下を行う必要があります。

01. NuGet の依存関係を理解し、更新します。

    01. `<PackageReference>` 形式を使用するように NuGet の依存関係をアップグレードします。
    01. .NET Core または .NET Standard の互換性に関する最上位の NuGet の依存関係を確認します。
    01. NuGet パッケージを新しいバージョンにアップグレードします。
    01. [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) を使用して、.NET の依存関係を理解します。

01. プロジェクト ファイルを新しい SDK スタイルの形式に移行します。

    01. .NET Core と .NET Framework の両方をターゲットとするか、.NET Core のみをターゲットとするかを選択します。
    01. 関連するプロジェクト ファイルのプロパティと項目を新しいプロジェクト ファイルにコピーします。

01. ビルドの問題を修正します。

    01. [Microsoft.Windows.Compatibility](https://www.nuget.org/packages/Microsoft.Windows.Compatibility/) パッケージへの参照を追加します。
    01. API レベルの相違点を見つけて修正します。
    01. `appSettings` または `connectionStrings` 以外の *app.config* セクションを削除します。
    01. 必要に応じて、生成されたコードを再生成します。

01. ランタイムのテストを行います。

    01. 移植されたアプリが想定どおりに動作することを確認します。
    01. <xref:System.NotSupportedException> 例外に注意してください。

## <a name="about-the-sample"></a>サンプルについて

この記事では、[Bean Trader サンプル アプリ](https://github.com/dotnet/windows-desktop/tree/master/Samples/BeanTrader)を参照しています。これは、実際の WPF アプリのものと類似するさまざまな依存関係がそこで使用されているためです。 このアプリは大きくはありませんが、複雑さの点で "Hello World" からのステップアップを意図しています。 このアプリでは、ユーザーが実際のアプリを移植するときに発生する可能性のある問題が実証されます。 このアプリは WCF サービスと通信するので、これを適切に実行するためには、BeanTraderServer プロジェクト (同じ GitHub リポジトリで入手できます) を実行し、BeanTraderClient の構成が正しいエンドポイントを指していることを確認する必要があります。 (既定では、このサンプルではサーバーが `http://localhost:8090` の同じコンピューターで実行されていることが前提となっています。BeanTraderServer をローカルで起動した場合はこれが該当します。)

このサンプル アプリは、.NET Core の移植に関する課題と解決策を示すことを目的としている点に留意してください。 WPF のベスト プラクティスを示すことを目的としたものではありません。 実際、いくつかのアンチパターンが意図的に組み込まれており、移植中に少なくともいくつかの有用な課題が確実に発生するようになっています。

## <a name="getting-ready"></a>開発の準備

.NET Framework アプリを .NET Core に移行する際の主な課題は、その依存関係が異なる動作をする場合やまったく動作しない場合があることです。 移行は以前よりはるかに簡単になり、多くの NuGet パッケージが .NET Standard をターゲットにするようになっています。 .NET Core 2.0 以降、.NET Framework と .NET Core の領域が類似するようになっています。 それでも、相違点は (NuGet パッケージによるサポートと使用可能な .NET API の両方に) いくつか残っています 。 移行の最初の手順では、アプリの依存関係を確認し、参照が .NET Core に簡単に移行できる形式であることを確かめます。

### <a name="upgrade-to-packagereference-nuget-references"></a>`<PackageReference>` NuGet 参照へのアップグレード

通常、以前の .NET Framework プロジェクトでは、NuGet の依存関係は *packages.config* ファイルにリストされます。 新しい SDK スタイルのプロジェクト ファイル形式では、別の構成ファイルではなく、csproj ファイル自体の [`<PackageReference>`](/nuget/consume-packages/package-references-in-project-files) 要素として NuGet パッケージを参照します。

移行時に `<PackageReference>` スタイルの参照を使用する利点は 2 つあります。

- これは、新しい .NET Core プロジェクト ファイルに必要な NuGet 参照のスタイルです。 既に `<PackageReference>` を使用している場合、これらのプロジェクト ファイルの要素をコピーして、直接新しいプロジェクトに貼り付けることができます。
- packages.config ファイルとは異なり、`<PackageReference>` 要素は、プロジェクトが直接依存する最上位の依存関係のみを参照します。 他のすべての推移的な NuGet パッケージは復元時に判別され、自動生成された obj\project.assets.json ファイルに記録されます。 これにより、プロジェクトにどのような依存関係があるかを判断するのがはるかに簡単になり、必要な依存関係が .NET Core で動作するかどうかを判断するのに役立ちます。

.NET Framework アプリを .NET Core に移行する最初の手順は、それを、`<PackageReference>` NuGet 参照を使用するように更新することです。 Visual Studio を使用すると、これを簡単に行うことができます。 Visual Studio の**ソリューション エクスプローラー**で プロジェクトの *packages.config* ファイルを右クリックし、次に **[packages.config を PackageReference に移行する]** を選択します。

![PackageReference へのアップグレード](./media/convert-project-from-net-framework/package-reference-migration.png)

計算された最上位の NuGet 依存関係を表示し、他のどの NuGet パッケージを最上位に昇格する必要があるかを尋ねるダイアログが表示されます。 Bean Trader サンプルでは、これらの他のパッケージはいずれも最上位にする必要はないため、それらのボックスをすべてオフにすることができます。 次に、 **[OK]** をクリックすると、*packages.config* ファイルが削除され、`<PackageReference>` 要素がプロジェクト ファイルに追加されます。

`<PackageReference>` スタイルの参照では、NuGet パッケージはパッケージ フォルダーにローカルに格納されません。 代わりに、最適化としてグローバルに格納されます。 移行が完了したら、csproj ファイルを編集し、以前に *..\packages* ディレクトリから取得したアナライザーを参照するすべての `<Analyzer>` 要素を削除します。 ご心配は不要です。NuGet パッケージ参照は維持されるため、アナライザーはプロジェクトに含まれます。 必要なことは、以前の packages.config スタイルの `<Analyzer>` 要素をクリーンアップするだけです。

### <a name="review-nuget-packages"></a>NuGet パッケージの確認

プロジェクトが依存する最上位の NuGet パッケージが表示されるようになったので、それらのパッケージを .NET Core で使用できるかどうかを確認できます。 パッケージが .NET Core をサポートしているかどうかは、[nuget.org](https://www.nuget.org/) でその依存関係を調べることで判断できます。コミュニティによって作成された [fuget.org](https://www.fuget.org/) サイトでは、この情報がパッケージ情報ページの上部に目立つように表示されます。

.Net Core 3.0 をターゲットとする場合、.NET Core または .NET Standard をターゲットとするパッケージはすべて動作するはずです (.NET Core では .NET Standard の領域が実装されるため)。 場合によっては、使用されているパッケージの特定のバージョンで .NET Core または .NET Standard がターゲットにならないことがありますが、新しいバージョンではターゲットになります。 この場合は、最新バージョンのパッケージにアップグレードすることを検討してください。

.NET Framework をターゲットとするパッケージも使用できますが、それにはある程度のリスクが伴います。 .NET Core から .NET Framework への依存関係は許容されます。 .NET Core と .NET Framework の領域は類似しているので、このような依存関係は "*多くの場合*" 機能するためです。 ただし、パッケージで .NET Core に存在しない .NET API を使用しようとすると、ランタイム例外が発生します。 そのため、選択可能なオプションが他にない場合にのみ .NET Framework パッケージを参照し、これを行うことによってテストの負担が生じることを理解する必要があります。

.NET Core や .NET Standard をターゲットとしないパッケージが参照されている場合は、他の代替手段を検討する必要があります。

- 代わりに使用できる類似のパッケージは他にあるでしょうか。 NuGet の作成者が、特に .NET Core をターゲットとする別個の '.Core' バージョンのライブラリを公開している場合があります。 Enterprise Library パッケージは、コミュニティ発行 ".NetCore" の代替手段の例です。 他のケースとして、特定のサービス用の新しい SDK が (ときにより、異なるパッケージ名で) .NET Standard 用に用意されています。 使用できる他の代替手段がない場合は、.NET Framework をターゲットとするパッケージを使用して続行できますが、.NET Core で実行する際は、十分なテストが必要になることを念頭に置いてください。

Bean Trader サンプルには、次の最上位 NuGet 依存関係があります。

- [**Castle.Windsor、バージョン 4.1.1**](https://www.castleproject.org/projects/windsor/)  

  このパッケージは .NET Standard 1.6 をターゲットとしているため、.NET Core で動作します。

- [**Microsoft.CodeAnalysis.FxCopAnalyzers、バージョン 2.6.3**](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.3)  
  これはメタパッケージであるため、 どのプラットフォームがサポートされるかはすぐには明らかになりません。ただし、[ドキュメント](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisfxcopanalyzers)には、その最新バージョン (2.9.2) が .NET Framework と .NET Core の両方で動作することが示されています。

- [**Nito.AsyncEx、バージョン 4.0.1**](https://www.nuget.org/packages/Nito.AsyncEx/4.0.1)  

  このパッケージは .NET Core をターゲットとしていませんが、新しい 5.0 バージョンではターゲットとしています。 これは移行時によくあることです。多くの NuGet パッケージでは .NET Standard のサポートが最近追加されていますが、以前のバージョンのプロジェクトでは .NET Framework のみがターゲットになるためです。 バージョンの違いがマイナー バージョンの違いであれば、多くの場合、新しいバージョンに簡単にアップグレードできます。 これはメジャー バージョンの変更であるため、パッケージに破壊的変更が生じる可能性があるので、アップグレード時には注意が必要です。 しかし、前進できるので、それは望ましいことです。

- [**MahApps.Metro、バージョン1.6.5**](https://www.nuget.org/packages/MahApps.Metro/1.6.5)  

  このパッケージも .NET Core をターゲットとしていませんが、これをターゲットとする新しいプレリリース (2.0 アルファ版) があります。 この場合も、破壊的変更について注意する必要がありますが、新しいパッケージがあることは心強いものです。

Bean Trader サンプルの NuGet の依存関係はすべて .NET Standard または .NET Core をターゲットとしているか、これらをターゲットとする新しいバージョンを備えています。そのため、ここで障害となる問題が生じる可能性はほとんどありません。

### <a name="upgrade-nuget-packages"></a>NuGet パッケージのアップグレード

可能であれば、破壊的変更を早期に検出して対処するために、この時点 (プロジェクトが引き続き .NET Framework をターゲットとしている状態) で、.NET Core または .NET Standard のみをターゲットとするパッケージのバージョンをより新しいバージョンにアップグレードすることをお勧めします。

アプリの既存の .NET Framework バージョンに対して重大な変更を加えたくない場合は、.NET Core をターゲットとする新しいプロジェクト ファイルが作成されるまで待つことができます。 ただし、NuGet パッケージを前もって .NET Core の互換バージョンにアップグレードしておくと、新しいプロジェクト ファイルを作成したときの移行プロセスがより簡単になり、アプリの .NET Framework と .NET Core のバージョンの相違点が少なくなります。

Bean Trader サンプルを使用すると、(Visual Studio の NuGet パッケージ マネージャーを使用して) 必要なすべてのアップグレードを簡単に行うことができますが、1 つ例外があります。**MahApps.Metro 1.6.5** から **2.0** にアップグレードすると、テーマとアクセント管理の API に関する破壊的変更が発生します。

可能であれば、新しいバージョンのパッケージを使用するようにアプリを更新してください (その方が .NET Core で動作する可能性が高いためです)。 ただし、これが可能でない場合もあります。 このような場合は、**MahApps.Metro** をアップグレードしないでください。必要な変更が簡単ではないことと、このチュートリアルでは **MahApps.Metro 2** ではなく .NET Core 3 への移行に焦点を置いているからです。 また、Bean Trader アプリでは **MahApps.Metro** のわずかな部分のみが実行されるため、これはリスクの低い .NET Framework 依存関係です。 もちろん、移行が完了したら、すべてが正常に機能していることを確認するためのテストが必要になります。 これが実際のシナリオである場合は、**MahApps.Metro** バージョン 2.0 に移行する作業を追跡するために課題を提起することをお勧めします。移行を行わないと、今度は、技術的な問題点が残ったままになるためです。

NuGet パッケージが最新バージョンに更新されると、Bean Trader サンプルのプロジェクト ファイル内の `<PackageReference>` 項目グループは次のようになります。

```xml
<ItemGroup>
  <PackageReference Include="Castle.Windsor">
    <Version>4.1.1</Version>
  </PackageReference>
  <PackageReference Include="MahApps.Metro">
    <Version>1.6.5</Version>
  </PackageReference>
  <PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers">
    <Version>2.9.2</Version>
  </PackageReference>
  <PackageReference Include="Nito.AsyncEx">
    <Version>5.0.0</Version>
  </PackageReference>
</ItemGroup>
```

### <a name="net-framework-portability-analysis"></a>.NET Framework の移植性の分析

プロジェクトの NuGet 依存関係の状態を把握したら、次に考慮すべき点は、.NET Framework API の依存関係です。 [.NET Portability Analyzer](../../standard/analyzers/portability-analyzer.md) ツールは、プロジェクトで使用されている .NET API のうち、他の .NET プラットフォームで利用可能なものを理解するのに役立ちます。

このツールは、[Visual Studio プラグイン](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)や[コマンドライン ツール](https://github.com/Microsoft/dotnet-apiport/releases)として提供されるか、オプションを単純化する[シンプルな GUI](https://github.com/Microsoft/dotnet-apiport-ui) 内にラップされています。 GUI を使用した .NET Portability Analyzer (API Port) の使用の詳細については、「[.NET Core へのデスクトップ アプリの移植](https://devblogs.microsoft.com/dotnet/porting-desktop-apps-to-net-core/)」というブログ記事を参照してください。 コマンド ラインを使用する場合に必要な手順は次のとおりです。

1. [.NET Portability Analyzer](https://github.com/Microsoft/dotnet-apiport/releases) がまだない場合は、ダウンロードします。
1. 移植する .NET Framework アプリが正常にビルドされていることを確認します (移行前に必ずこれを行うことをお勧めします)。
1. 次のようなコマンド ラインを使用して API Port を実行します。

    ```console
    ApiPort.exe analyze -f <PathToBeanTraderBinaries> -r html -r excel -t ".NET Core"
    ```

    `-f` 引数は、分析するバイナリを含むパスを指定します。 `-r` 引数は、使用する出力ファイル形式を指定します。 `-t` 引数は、API の使用状況の分析対象である .NET プラットフォームを指定します。 この場合は .NET Core です。

HTML レポートを開くと、最初のセクションに、分析されたすべてのバイナリと、それらで使用される .NET API のうち何パーセントをターゲット プラットフォームで使用できるかが一覧表示されます。 このパーセントは、それ自体では意味がありません。 さらに役に立つのは、欠落している特定の API を確認することです。 これを行うには、アセンブリ名を選択するか、個々のアセンブリのレポートまで下にスクロールします。

ご自身がソース コードを所有しているアセンブリに注目してください。 たとえば、Bean Trader ApiPort レポートには多くのバイナリが一覧表示されますが、そのほとんどは NuGet パッケージに属しています。 `Castle.Windsor` は、.NET Core に存在しないいくつかの System.Web API に依存していることを示しています。 .NET Core が `Castle.Windsor` によってサポートされていることを事前に確認しているため、これは問題ではありません。 一般に、NuGet パッケージにはさまざまな .NET プラットフォームで使用する各種のバイナリがあるため、`Castle.Windsor` の .NET Framework バージョンで System.Web API が使用されるかどうかは、パッケージが、(この API が使用される) .NET Standard または .NET Core もターゲットとしている限り、重要ではありません。

Bean Trader サンプルでは、考慮する必要があるバイナリは **BeanTraderClient** のみであり、レポートでは、`System.ServiceModel.ClientBase<T>.Close` と `System.ServiceModel.ClientBase<T>.Open` の 2 つの .NET API だけが欠落していることが示されています。

![BeanTraderClient の移植性レポート](./media/convert-project-from-net-framework/portability-report.png)

これらが障害となる問題になる可能性はほとんどありません。WCF クライアント API は (ほとんどの場合) .NET Core でサポートされるので、これらの主要 API には代替手段が用意されているはずであるためです。 事実、(<https://apisof.net> を使用して) `System.ServiceModel` の .NET Core の領域を調べると、.NET Core では代わりに非同期の代替手段があることがわかります。

このレポートと以前の NuGet 依存関係分析に基づいて、Bean Trader サンプルを .NET Core に移行する際に大きな問題はないと考えられます。 これで、実際に移行を開始する次の手順の準備が整いました。

## <a name="migrating-the-project-file"></a>プロジェクト ファイルの移行

お使いのアプリで新しい [SDK スタイルのプロジェクト ファイル形式](../../core/tools/csproj.md)を使用していない場合は、.NET Core をターゲットとする新しいプロジェクト ファイルが必要になります。 既存の csproj ファイルを置き換えることも、既存のプロジェクトを現在の状態に維持する場合は、.NET Core をターゲットとする新しい csproj ファイルを追加することもできます。 [マルチターゲット](../../standard/library-guidance/cross-platform-targeting.md) (複数の `<TargetFrameworks>` ターゲットを指定すること) を使用すると、1 つの SDK スタイル プロジェクト ファイルで .NET Framework 用と .NET Core 用のアプリのバージョンをビルドできます。

新しいプロジェクト ファイルを作成する場合、Visual Studio で新しい WPF プロジェクトを作成することも、一時ディレクトリで `dotnet new wpf` コマンドを使用してプロジェクト ファイルを生成してから、それを適切な場所にコピー/名前変更することもできます。 また、コミュニティによって作成されたツール [CsprojToVs2017](https://github.com/hvanbakel/CsprojToVs2017) もあります。これを使用すると、プロジェクト ファイルの移行の一部を自動化できます。 このツールは便利ですが、それでも移行のすべての詳細が正しいことを確認するために、人間が結果をレビューする必要があります。 このツールで適切に処理できない特定の分野の 1 つは、*packages.config* ファイルからの NuGet パッケージの移行です。 NuGet パッケージを参照するためにまだ *packages.config* ファイルを使用しているプロジェクト ファイルでこのツールを実行すると、自動的に `<PackageReference>` 要素に移行されますが、最上位のパッケージだけでなく、"*すべての*" パッケージに対して `<PackageReference>` 要素が追加されます。 (このサンプルで行ったように) Visual Studio を使用して `<PackageReference>` 要素に既に移行している場合は、変換の残りの部分でこのツールが役立します。 Scott Hanselman 氏が [csproj ファイルの移行に関する彼のブログ記事](https://www.hanselman.com/blog/UpgradingAnExistingNETProjectFilesToTheLeanNewCSPROJFormatFromNETCore.aspx)で勧めているように、手操作で移植すると、そこから学ぶことができ、移植するプロジェクトが少数のみである場合は、より良い結果が得られます。 しかし、数十や数百ものプロジェクト ファイルを移植する場合は、[[CsprojToVs2017]](https://github.com/hvanbakel/CsprojToVs2017) などのツールが役に立ちます。

Bean Trader サンプル用に新しいプロジェクト ファイルを作成するには、一時ディレクトリで `dotnet new wpf` を実行し、生成された *.csproj* ファイルを *BeanTraderClient* フォルダーに移動して、その名前を **BeanTraderClient.Core.csproj** に変更します。

新しいプロジェクト ファイル形式には、そのディレクトリの中または下で見つかる C# ファイル、*resx* ファイル、XAML ファイルが自動的に含まれるため、プロジェクト ファイルは既にほぼ完成しています。 移行を完了するには、以前のプロジェクト ファイルと新しいプロジェクト ファイルを横に並べて開き、以前のプロジェクト ファイルを調べて、そこに含まれる情報に移行が必要なものがあるかどうかを確認します。 Bean Trader サンプルの場合、次の項目を新しいプロジェクトにコピーする必要があります。

- `<RootNamespace>`、`<AssemblyName>`、`<ApplicationIcon>` プロパティをすべてコピーする必要があります。

- また、`<GenerateAssemblyInfo>false</GenerateAssemblyInfo>` プロパティも新しいプロジェクト ファイルに追加する必要があります。Bean Trader サンプルでは、AssemblyInfo.cs ファイルにアセンブリ レベルの属性 (`[AssemblyTitle]` など) が含まれているためです。 既定では、新しい SDK スタイルのプロジェクトにより、csproj ファイルのプロパティに基づいてこれらの属性が自動生成されます。 ここでは、これが行われないようにしたいので (自動生成された属性は AssemblyInfo.cs のものと競合します)、`<GenerateAssemblyInfo>` を使用して自動生成される属性を無効にします。

- *resx* ファイルは埋め込みリソースとして自動的に含まれますが、イメージなどの他の `<Resource>` 項目は含まれません。 そのため、イメージとアイコンのファイルを埋め込むには `<Resource>` 要素をコピーしてください。 新しいプロジェクト ファイル形式での glob パターン (`<Resource Include="**\*.png" />`) のサポートを利用すると、png 参照を 1 行に簡略化できます。

- 同様に、`<None>` 項目は自動的に含まれますが、既定では出力ディレクトリにコピーされません。 Bean Trader プロジェクトには、(`PreserveNewest` の動作を使用して) 出力ディレクトリにコピー "*される*" `<None>` 項目が含まれているので、次のように、そのファイルに対して自動的に設定される `<None>` 項目を更新する必要があります。

  ```xml
  <None Update="BeanTrader.pfx">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
  ```

- Bean Trader サンプルには、XAML ファイル (Default.Accent.xaml) が (`Page` ではなく) `Content` として含まれます。このファイルで定義されているテーマとアクセントが、アプリ自体に埋め込まれるのではなく実行時にそのファイルの XAML から読み込まれるためです。 ただし、これは XAML ファイルであるため、新しいプロジェクト システムでは、このファイルは自動的に `<Page>` として組み込まれます。 そのため、XAML ファイルをページとして削除 (`<Page Remove="**\Default.Accent.xaml" />`) することと、コンテンツとして追加することが両方とも必要です。

  ```xml
  <Content Include="Resources\Themes\Default.Accent.xaml">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </Content>
  ```

- 最後に、すべての `<PackageReference>` 要素とともに `<ItemGroup>` をコピーして、NuGet 参照を追加します。 まだ NuGet パッケージを .NET Core 互換バージョンにアップグレードしていない場合は、パッケージ参照が .NET Core 固有のプロジェクトに含まれるようになったので、それを行うことができます。

この時点で、Bean Trader ソリューションに新しいプロジェクトを追加し、Visual Studio で開くことができます。 プロジェクトは**ソリューション エクスプローラー**で正しく表示され、`dotnet restore BeanTraderClient.Core.csproj` ではパッケージが正常に復元されているはずです (.NET Framework をターゲットとする、使用している MahApps.Metro バージョンに関連した 2 つの警告が出される可能性があります)。

両方のプロジェクト ファイルを並行して保持することは可能ですが (古いプロジェクトを以前とまったく同じようにビルドし続ける場合は、これが望ましい場合もあります)、これによって移行プロセスが複雑になり (2 つのプロジェクトが同じ bin と obj フォルダーを使用しようとします)、通常は必要ありません。 .NET Core と .NET Framework の両方のターゲット用にビルドする場合は、代わりに新しいプロジェクト ファイルの `<TargetFramework>netcoreapp3.0</TargetFramework>` プロパティを `<TargetFrameworks>netcoreapp3.0;net472</TargetFrameworks>` に置き換えることができます。 Bean Trader サンプルでは、以前のプロジェクト ファイル (BeanTraderClient.csproj) は不要になるため、削除します。 両方のプロジェクト ファイルを保持する場合は、必ず異なる出力パスと中間出力パスにビルドするようにしてください。

## <a name="fix-build-issues"></a>ビルドの問題の修正

移植プロセスの 3 番目の手順は、プロジェクトをビルドすることです。 プロジェクト ファイルが SDK スタイルのプロジェクトに変換されると、その時点で一部のアプリは既に正常にビルドされます。 使用しているアプリがそうであれば幸運です。 手順 4 に進むことができます。 その他のアプリでは、.NET Core 用にビルドするために、いくつかの更新を行う必要があります。 たとえば、この時点で Bean Trader サンプル プロジェクトで `dotnet build` を実行 (またはそれを Visual Studio でビルド) しようとすると、多くのエラーが発生しますが、すぐに修正できます。

### <a name="systemservicemodel-references-and-microsoftwindowscompatibility"></a>System.ServiceModel の参照と Microsoft.Windows.Compatibility

エラーの一般的な原因として、.NET Core で利用可能でありながら、.NET Core アプリのメタパッケージに自動的に含まれない API の参照が欠落していることが挙げられます。 これに対処するには、`Microsoft.Windows.Compatibility` パッケージを参照する必要があります。 この互換性パッケージには、WCF クライアント、ディレクトリ サービス、レジストリ、構成、ACL API など、Windows デスクトップ アプリに共通するさまざまな API のセットが含まれています。

Bean Trader サンプルでは、ビルド エラーのほとんどは <xref:System.ServiceModel> 型が欠落していることが原因です。 これらは、必要な WCF NuGet パッケージを参照することで対処できます。 ただし、WCF クライアント API は `Microsoft.Windows.Compatibility` パッケージに含まれるものの 1 つであるため、この互換性パッケージを参照すると、より効果的な解決策になります (これが、API に関連する問題の対策になり、この互換性パッケージによって提供される WCF の問題の解決策にもなるためです)。 `Microsoft.Windows.Compatibility` パッケージは、ほとんどの .NET Core 3.0 WPF と WinForms の移植のシナリオで役立ちます。 `Microsoft.Windows.Compatibility` への NuGet の参照を追加すると、残るビルド エラーは 1 つだけになります。

### <a name="cleaning-up-unused-files"></a>使用されていないファイルのクリーンアップ

移行に関して発生する問題の 1 つの種類として、以前はビルドに含まれていなかった C# と XAML のファイルが、"*すべての*" ソースが自動的に組み込まれる新しい SDK スタイルのプロジェクトによって取得されることに関連したものが多くあります。

Bean Trader サンプルで発生する次のビルド エラーは、*OldUnusedViewModel.cs* でのインターフェイスの不適切な実装を指しています。 このファイル名がヒントになりますが、検査時に、このソース ファイルが正しくないことがわかります。 以前は、それによって問題は発生しませんでした。それが元の .NET Framework プロジェクトには含まれていなかったためです。 ディスク上に存在していても以前の *csproj* に含まれていなかったソース ファイルは、自動的に含まれるようになっています。

このような 1 回限りの問題では、以前の *csproj* と比較してそのファイルが不要であることを確認し、それに対して `<Compile Remove="" />` を実行するか、そのソース ファイルがそれ以上どこにも必要でない場合は削除できます。 この場合は、単に *OldUnusedViewModel.cs* を削除すれば問題ありません。

この方法で除外する必要があるソース ファイルが多数ある場合は、プロジェクト ファイルで `<EnableDefaultCompileItems>` プロパティを false に設定して C# ファイルの自動組み込みを無効にすることができます。 その後に、以前のプロジェクト ファイルから新しいものに `<Compile Include>` 項目をコピーすると、含める必要があるソースのみをビルドできます。 同様に、`<EnableDefaultPageItems>` を使用すると XAML ページの自動組み込みをオフにすることができ、`<EnableDefaultItems>` によって 1 つのプロパティで両方を制御できます。

### <a name="a-brief-aside-on-multi-pass-compilers"></a>マルチパス コンパイラに関する簡単な説明

Bean Trader サンプルから問題のあるファイルを削除した後に、再ビルドできますが、4 つのエラーが発生します。 以前はこれが発生しなかった可能性があります。 エラーの数が増えたのはなぜでしょうか。 C# コンパイラは[マルチパス コンパイラ](https://docs.microsoft.com/archive/blogs/ericlippert/how-many-passes)です。 これは、各ソース ファイルが 2 回確認されることを意味します。 まずコンパイラでは、各ソース ファイルのメタデータと宣言が確認され、宣言レベルの問題が特定されます。 これらは先ほど修正したエラーです。 次に、C# ソースを IL にビルドするためにコードがもう一度確認されます。これらが、現在検討している 2 番目のエラー セットです。

> [!NOTE]
> C# コンパイラでは、[単なる 2 回のパス以上のこと](https://docs.microsoft.com/archive/blogs/ericlippert/how-many-passes)が行われますが、最終結果としては、このような大規模なコード変更でのコンパイラ エラーは 2 段階で発生する傾向にあります。

### <a name="third-party-dependency-fixes-castlewindsor"></a>サードパーティの依存関係の修正 (Castle.Windsor)

一部の移行シナリオで発生する別の種類の問題として、依存関係の .NET Framework と .NET Core バージョンの間の API の違いが挙げられます。 NuGet パッケージが .NET Framework と .NET Standard または .NET Core の両方をターゲットとしている場合でも、さまざまな .NET ターゲットで使用する各種のライブラリが存在する可能性があります。 これにより、パッケージではさまざまな .NET プラットフォームがサポートされますが、複数の異なる実装が必要になる場合があります。 さらに、異なる .NET プラットフォームをターゲットとする場合に、ライブラリ内にわずかな API の違いが存在する可能性もあります。

Bean Trader サンプルで確認される次のエラー セットは、`Castle.Windsor` API に関連するものです。 .NET Core の Bean Trader プロジェクトでは、.NET Framework ターゲット プロジェクト (4.1.1) と同じバージョンの `Castle.Windsor` が使用されますが、これら 2 つのプラットフォームの実装には若干の違いがあります。

この場合、修正が必要な次の問題が発生します。

1. `Castle.MicroKernel.Registration.Classes.FromThisAssembly` は .NET Core では使用できません。 ただし、類似の API `Classes.FromAssemblyContaining` を使用できるため、`Classes.FromThisAssembly()` の両方の使用を `Classes.FromAssemblyContaining(t)` の呼び出しに置き換えることができます。ここで、`t` は、呼び出しを行う型です。
1. 同様に、*Bootstrapper.cs* では、`Castle.Windsor.Installer.FromAssembly` です。これは .NET Core では使用できません。 代わりに、その呼び出しを `FromAssembly.Containing(typeof(Bootstrapper))` に置き換えることができます。

### <a name="updating-wcf-client-usage"></a>WCF クライアントの使用法の更新

`Castle.Windsor` の違いを修正したので、.NET Core の Bean Trader プロジェクトで最後に残ったビルド エラーは、`BeanTraderServiceClient` (`DuplexClientBase` から派生) に `Open` メソッドがないことです。 これは意外なことではありません。これが、この移行プロセスの最初の段階で .NET Portability Analyzer によって示された API であるためです。 ただし、`BeanTraderServiceClient` を調べることで、より大きな問題に注目することになります。 この WCF クライアントは、[Svcutil.exe](../../framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) ツールによって自動生成されました。

**Svcutil によって生成される WCF クライアントは .NET Framework での使用を想定しています。**

Svcutil で生成された WCF クライアントを使用するソリューションでは、.NET Core で使用するための .NET Standard 互換クライアントを再生成する必要があります。 以前のクライアントが動作しない主な理由の 1 つは、それらが、WCF バインドとエンドポイントを定義するためにアプリ構成に依存していることです。 .NET Standard の WCF API はクロスプラットフォームで動作できるため (この場合、System.Configuration API は使用できません)、.NET Core と .NET Standard のシナリオ用の WCF クライアントでは、バインドとエンドポイントを、構成内ではなくプログラムで定義する必要があります。

実際、`<system.serviceModel>` app.config セクションに依存する WCF クライアント (Svcutil によって作成されたか手動で作成されたかに関係なく) の使用法を、.NET Core で機能するように変更する必要があります。

.NET Standard 互換の WCF クライアントを自動生成するには、次の 2 つの方法があります。

- `dotnet-svcutil` ツールは、以前に Svcutil が動作していた方法と同様の方法で WCF クライアントを生成する .NET ツールです。
- Visual Studio では、その接続済みサービス機能の [[WCF Web Service Reference]](../../core/additional-tools/wcf-web-service-reference-guide.md) オプションを使用して、WCF クライアントを生成できます。

どちらの方法も適切に機能します。 または、当然のことながら、WCF クライアント コードをご自身で記述することもできます。 このサンプルでは、Visual Studio の接続済みサービス機能を使用します。 これを行うには、Visual Studio のソリューション エクスプローラーで *BeanTraderClient.Core* プロジェクトを右クリックし、 **[追加]**  >  **[接続済みサービス]** を選択します。 次に、WCF Web Service Reference Provider を選択します。 これによってイアログが表示され、そこでバックエンド Bean Trader Web サービスのアドレス (サーバーをローカルで実行している場合は `localhost:8080`) と、生成された型で使用する名前空間 (**BeanTrader.Service** など) を指定できます。

![WCF Web Service Reference の接続済みサービスのダイアログ](./media/convert-project-from-net-framework/connected-service-dialog.png)

**[完了]** ボタンを選択すると、新しい接続済みサービス ノードがプロジェクトに追加され、そのノードの下に、Bean Trader サービスにアクセスするための新しい .NET Standard WCF クライアントを含む Reference.cs ファイルが追加されます。 そのファイルの `GetEndpointAddress` または `GetBindingForEndpoint` メソッドを確認すると、バインドとエンドポイントが (アプリ構成によってではなく) プログラムで生成されるようになったことがわかります。 また、[接続済みサービスの追加] 機能を使用することで、プロジェクト ファイル内のいくつかの System.ServiceModel パッケージへの参照が追加される場合もあります。これは、必要なすべての WCF パッケージは Microsoft.Windows.Compatibility によって含まれるため、必要ありません。 csproj を調べて、他の System.ServiceModel `<PackageReference>` 項目が追加されているかどうかを確認し、追加されている場合は削除してください。

このプロジェクトには新しい WCF クライアント クラスが (*Reference.cs* 内に) 追加されていますが、以前のものも (BeanTrader.cs 内に) まだ存在します。 この時点で、次の 2 つのオプションがあります。

- 元の .NET Framework プロジェクトを (.NET Core ターゲットの新しいものとともに) ビルドできるようにする場合は、.NET Core プロジェクトの csproj ファイルの `<Compile Remove="BeanTrader.cs" />` 項目を使用して、アプリの .NET Framework と .NET Core バージョンで異なる WCF クライアントが使用されるようにすることができます。 これには、既存の .NET Framework プロジェクトが変更されないままになるという利点がありますが、生成された WCF クライアントを使用するコードが、.NET Core のケースでは場合によって .NET Framework プロジェクト内のときとは若干異なる必要があるという欠点もあります。そのため、`#if` ディレクティブを使用して、WCF クライアントの使用法 (たとえば、クライアントの作成) を条件付きでコンパイルして、.NET Core 用にビルドする際はある方法で動作し、.NET Framework 用にビルドする際は別の方法で動作するようにすることが必要になると考えられます。

- 一方、既存の .NET Framework プロジェクト内のコード チャーンを許容できる場合は、*BeanTrader.cs* をまとめて削除できます。 新しい WCF クライアントは .NET Standard 用にビルドされているため、.NET Core と .NET Framework の両方のシナリオで動作します。 .NET Core に加えて .NET Framework 用にビルドする (マルチターゲットにより、または 2 つの csproj ファイルを使用することにより) 場合は、この新しい *Reference.cs* ファイルを両方のターゲットに使用できます。 この方法には、2 つの異なる WCF クライアントをサポートするためにコードを 2 つに分ける必要がないという利点があります。同じコードがどこでも使われます。 欠点は、(安定していると想定される) .NET Framework プロジェクトの変更を伴うことです。

Bean Trader サンプルの場合、移行が簡単になるのであれば、元のプロジェクトにわずかな変更を加えることができます。そのため、次の手順に従って WCF クライアントの使用法を調整してください。

01. ソリューション エクスプローラーの [既存項目の追加] コンテキスト メニューを使用して、.NET Framework の *BeanTraderClient.csproj* プロジェクトに新しい Reference.cs ファイルを追加します。 両方のプロジェクトで同じファイルが使用されるように、必ず 'as link' を追加してください (C# ファイルをコピーするのとは異なります)。 (マルチターゲットを使用して) 1 つの csproj で .NET Core と .NET Framework の両方をビルドする場合、この手順は必要ありません。

01. *BeanTrader.cs* を削除します。

01. 新しい WCF クライアントは以前のものと似ていますが、生成されるコードの名前空間の数が異なります。 このため、BeanTrader.Model ではなく BeanTrader.Service (または任意に選択した名前空間) から、または名前空間なしで、WCF クライアント型が使用されるように、プロジェクトを更新する必要があります。 *BeanTraderClient.Core.csproj* を作成すると、これらの変更が必要な場所を特定するのに役立ちます。 修正は、C# と XAML の両方のソース ファイルで必要になります。

01. 最後に、*BeanTraderServiceClientFactory.cs* 内にエラーがあることがわかります。これは、`BeanTraderServiceClient` 型で使用可能なコンストラクターが変更されたためです。 以前は、`InstanceContext` 引数 (`Castle.Windsor` IoC コンテナーから `CallbackHandler` を使用して作成されました) を指定できました。 新しいコンストラクターでは、新しい `CallbackHandler` が作成されます。 ただし、`BeanTraderServiceClient` の基本型には、必要なものと一致するコンストラクターがあります。 自動生成された WCF クライアント コードはすべて部分クラスに存在するため、簡単に拡張できます。 これを行うには、*BeanTraderServiceClient.cs* という名前の新しいファイルを作成してから、(BeanTrader.Service 名前空間を使用して) それと同じ名前の部分クラスを作成します。 その後、次に示すように、1 つのコンストラクターを部分型に追加します。

    ```csharp
    public BeanTraderServiceClient(System.ServiceModel.InstanceContext callbackInstance) :
        base(callbackInstance, EndpointConfiguration.NetTcpBinding_BeanTraderService)
            { }
    ```

これらの変更を行うと、Bean Trader サンプルでは新しい .NET Standard 互換の WCF クライアントが使用されるようになり、*TradingService.cs* で、`await OpenAsync` を代わりに使用するように `Open` の呼び出しを変更するための最終的な修正を行うことができます。

WCF の問題が解決されたので、.NET Core バージョンの Bean Trader サンプルが正常にビルドされるようになりました。

## <a name="runtime-testing"></a>ランタイムのテスト

忘れがちですが、.NET Core に対してプロジェクトが正常にビルドされてすぐに移行作業が完了するわけではありません。 移植されたアプリをテストする時間を確保することも重要です。 ビルドが正常に完了したら、アプリが想定どおりに実行され、動作することを確認します (特に、.NET Framework をターゲットとするパッケージを使用している場合)。

移植された Bean Trader アプリを起動してみて、何が起こるか見ていきましょう。 まもなく、次の例外が発生してアプリが失敗します。

```output
System.Configuration.ConfigurationErrorsException: 'Configuration system failed to initialize'

Inner Exception
ConfigurationErrorsException: Unrecognized configuration section system.serviceModel.
```

これは当然の結果です。 WCF ではアプリ構成が使用されなくなったため、app.config ファイルの以前の system.serviceModel セクションは削除する必要があることを思い出してください。 更新された WCF クライアントでは、そのコード内に同じ情報がすべて含まれているため、構成セクションは不要になりました。 WCF エンドポイントを app.config で構成できるようにする場合は、それをアプリ設定として追加し、構成から WCF サービス エンドポイントを取得するように WCF クライアント コードを更新できます。

*app.config* の system.serviceModel セクションを削除すると、アプリは起動しますが、ユーザーがサインインするときに別の例外が発生して失敗します。

```output
System.PlatformNotSupportedException: 'Operation is not supported on this platform.'
```

サポートされていない API は `Func<T>.BeginInvoke` です。 [dotnet/corefx#5940](https://github.com/dotnet/corefx/issues/5940) で説明されているように、.NET Core では、基になるリモート処理の依存関係が原因で、デリゲート型で `BeginInvoke` と `EndInvoke` メソッドはサポートされません。 この問題とその修正方法については、「[.NET Core の Delegate.BeginInvoke 呼び出しの移行](https://devblogs.microsoft.com/dotnet/migrating-delegate-begininvoke-calls-for-net-core/)」ブログ記事で詳しく説明されていますが、要点としては、`BeginInvoke` と `EndInvoke` の呼び出しを `Task.Run` (または、可能な場合は非同期の代替手段) に置き換える必要があるということです。 ここで一般的な解決策を適用すると、`BeginInvoke` の呼び出しを `Task.Run` によって起動される `Invoke` の呼び出しに置き換えることができます。

```csharp
Task.Run(() =>
{
    return userInfoRetriever.Invoke();
}).ContinueWith(result =>
{
    // BeginInvoke's callback is replaced with ContinueWith
    var task = result.ConfigureAwait(false);
    CurrentTrader = task.GetAwaiter().GetResult();
}, TaskScheduler.Default);
```

`BeginInvoke` の使用を削除すると、Bean Trader アプリが .NET Core で正常に実行されます。

![.NET Core で実行される Bean Trader](./media/convert-project-from-net-framework/running-on-core.png)

すべてのアプリは異なっているため、ご自身のアプリを .NET Core に移行するために必要な具体的な手順もそれぞれ異なります。 しかし、この Bean Trader サンプルによって、一般的なワークフローと想定される問題の種類が示されることと思います。 また、この記事の長さとは対照的に、.NET Core で動作させるために Bean Trader サンプルに必要な実際の変更は、かなり限定されていました。 多くのアプリは、これと同じ方法で .NET Core に移行します。必要なコード変更は限定的であり、場合によっては一切不要です。
