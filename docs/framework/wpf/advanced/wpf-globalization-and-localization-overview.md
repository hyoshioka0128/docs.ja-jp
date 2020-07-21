---
title: グローバリゼーションおよびローカリゼーションの概要
ms.date: 03/30/2017
helpviewer_keywords:
- globalization [WPF], about globalization
- localization [WPF], about localization
ms.assetid: 56e5a5c8-6c96-4d19-b8e1-a5be1dc564af
ms.openlocfilehash: ba49b3ec0f6edebff6278f4e90ae22baba9f1edf
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452670"
---
# <a name="wpf-globalization-and-localization-overview"></a>WPF のグローバリゼーションおよびローカリゼーションの概要

製品を 1 つの言語だけで提供するということは、潜在的な顧客ベースを、75 億人という世界人口のほんの一部だけに限定してしまうことを意味します。 アプリケーションを世界中のユーザーに提供したいのであれば、製品をコスト効率よくローカライズすることが、より多くの顧客にリーチするための最良かつ経済的な方法の 1 つだと言えます。

この概要では、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でのグローバリゼーションとローカライズについて説明します。 グローバリゼーションとは、複数の場所で効果的に使用できるアプリケーションを設計、開発することです。 たとえば、グローバリゼーションでは、異なるカルチャのユーザーに対して、ローカライズされたユーザー インターフェイスや地域データを提供します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、自動レイアウト、サテライト アセンブリ、ローカライズされた属性、コメントなど、グローバリゼーションに対応したデザイン機能を提供しています。

ローカリゼーションとは、アプリケーションのリソースを翻訳し、そのアプリケーションがサポートする特定のカルチャに対応したローカライズ バージョンを作ることです。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でローカライズを行う場合は、<xref:System.Windows.Markup.Localizer> 名前空間の API を使用します。 これらの API によって、[LocBaml ツール サンプル](https://github.com/microsoft/WPF-Samples/tree/master/Tools/LocBaml)のコマンドライン ツールを効果的に活用できます。 LocBaml の使用方法について詳しくは、「[アプリケーションをローカライズする](how-to-localize-an-application.md)」を参照してください。

## <a name="best-practices-for-globalization-and-localization-in-wpf"></a>WPF でのグローバリゼーションとローカライズに関するベスト プラクティス

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に組み込まれているグローバリゼーションやローカリゼーションの機能を最大限に活用するには、このセクションで説明する UI デザインやローカリゼーション関連のヒントに従うのが効果的です。

### <a name="best-practices-for-wpf-ui-design"></a>WPF UI デザインのベスト プラクティス

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を設計する場合は、次のベスト プラクティスを実施することを検討してください。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を作成しましょう。[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] をコードで作成することは避けましょう。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を作成すれば、組み込みのローカライズ API を通じてコードを公開することができます。

- コンテンツのレイアウトに絶対位置や固定サイズを使用することは避けましょう。代わりに、相対サイズや自動サイズ設定を使用するようにしましょう。

  - <xref:System.Windows.Window.SizeToContent%2A> を使用し、幅と高さの設定を `Auto` のままにしましょう。

  - <xref:System.Windows.Controls.Canvas> を使って [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] をレイアウトすることは避けましょう。

  - <xref:System.Windows.Controls.Grid> とそのサイズ共有機能を使用しましょう。

- テキストをローカライズすると、より多くの領域が必要になることが多いので、余白のスペースを十分に用意しましょう。 十分なスペースをとることで、文字がはみ出すのを防ぐことができます。

- クリッピングを防ぐために、<xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.TextWrapping%2A> を有効にしましょう。

- `xml:lang` 属性を設定します。 この属性は、特定の要素とその子要素のカルチャを表します。 このプロパティの値によって、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のいくつかの機能の動作が変わります。 たとえば、ハイフネーション、スペル チェック、数字の置換、複雑なスクリプトの整形、およびフォント フォールバックの動作が変更されます。 [XAML における xml:lang の処理](../../../desktop-wpf/xaml-services/xml-language-handling.md)の設定方法について詳しくは、「[WPF のグローバリゼーション](globalization-for-wpf.md)」を参照してください。

- さまざまな言語で使用されるフォントをより適切に制御できるように、カスタマイズされた複合フォントを作成しましょう。 既定では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では Windows\Fonts ディレクトリ内の GlobalUserInterface フォントが使用されます。

- 作成しようとしているナビゲーション アプリケーションが、テキストを右から左に記述するカルチャでローカライズされる可能性がある場合は、すべてのページの <xref:System.Windows.FlowDirection> を明示的に設定して、<xref:System.Windows.Navigation.NavigationWindow> から <xref:System.Windows.FlowDirection> が継承されないようにしましょう。

- ブラウザーの外部でホストされるスタンドアロン ナビゲーション アプリケーションを作成する場合は、最初のアプリケーションの <xref:System.Windows.Application.StartupUri%2A> を、ページではなく <xref:System.Windows.Navigation.NavigationWindow> に設定しましょう (例: `<Application StartupUri="NavigationWindow.xaml">`)。 このデザインにより、ウィンドウとナビゲーション バーの <xref:System.Windows.FlowDirection> を変えることができます。 詳細と例については、[グローバリゼーション ホームページのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)に関する記事を参照してください。

### <a name="best-practices-for-wpf-localization"></a>WPF のローカライズに関するベスト プラクティス

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションをローカライズする場合は、次のベスト プラクティスを実施することを検討してください。

- ローカライズ コメントを使用して、ローカライザーに追加のコンテキストを提供しましょう。

- 要素の <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを選択的に省略するのではなく、ローカリゼーション属性を使用してローカリゼーションを制御しましょう。 詳細については、「[ローカリゼーション属性とコメント](localization-attributes-and-comments.md)」を参照してください。

- `msbuild -t:updateuid` と `-t:checkuid` を使用して、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを追加および確認しましょう。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティは、開発とローカリゼーションの間の変更を追跡するために使用します。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティは、開発上の新しい変更をローカライズするのに役立ちます。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを手動で [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] に追加すると、通常、タスクが面倒で不正確になります。

  - ローカライズを開始した後で <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティの編集や変更を行うことは避けましょう。

  - <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを重複して使用することは避けましょう (コピーと貼り付けのコマンドを使用する際には、この点に注意してください)。

  - AssemblyInfo.\* で `UltimateResourceFallback` の場所を設定して、フォールバック用の適切な言語を指定しましょう (`[assembly: NeutralResourcesLanguage("en-US",   UltimateResourceFallbackLocation.Satellite)]` など)。

    プロジェクト ファイルの `<UICulture>` タグを省略して、メイン アセンブリにソース言語を含める場合は、`UltimateResourceFallback` の場所をサテライトではなくメイン アセンブリとして設定しましょう (たとえば、`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.MainAssembly)]`)。

## <a name="localize-a-wpf-application"></a>WPF アプリケーションのローカライズ

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションをローカライズする際には、いくつかのオプションがあります。 たとえば、アプリケーション内のローカライズ可能なリソースを XML ファイルにバインドしたり、ローカライズ可能なテキストを resx テーブルに格納したり、ローカライザーに [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ファイルを使用させたりすることができます。 このセクションでは、BAML 形式の XAML を使用するローカライズ ワークフローについて説明します。これには、いくつかの利点があります。

- ビルドの後にローカライズを行うことができます。

- BAML 形式の XAML を、旧バージョンのローカリゼーションによって新バージョンへと更新することで、開発時にローカライズも同時進行することができます。

- BAML 形式の XAML は [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のコンパイル済みの形式なので、元のソース要素とセマンティクスをコンパイル時に検証することができます。

### <a name="localization-build-process"></a>ローカリゼーション ビルド プロセス

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションを開発する場合、ローカリゼーションのビルド プロセスは次のようになります。

- 開発者が [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションを作成し、グローバライズします。 開発者は、プロジェクト ファイルで `<UICulture>en-US</UICulture>` を設定し、アプリケーションのコンパイル時に、言語に依存しないメイン アセンブリが生成されるようにします。 このアセンブリには、ローカライズ可能なすべてのリソースを含んだサテライト .resources.dll ファイルがあります。 ローカリゼーション API ではメイン アセンブリからの抽出がサポートされているので、必要であれば、ソース言語をメイン アセンブリ内に保持することもできます。

- ファイルがコンパイルされてビルドになると、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] は BAML 形式の XAML へと変換されます。 英語圏の顧客には、カルチャに依存しない `MyDialog.exe` と、カルチャに依存する (英語版の) `MyDialog.resources.dll` ファイルがリリースされます。

### <a name="localization-workflow"></a>ローカリゼーション ワークフロー

ローカリゼーション プロセスは、ローカライズされていない `MyDialog.resources.dll` ファイルがビルドされた後に開始されます。 元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素とプロパティは、<xref:System.Windows.Markup.Localizer> にある API を使用して BAML 形式の XAML から抽出され、キーと値のペアに変換されます。 ローカライザーは、キーと値のペアを使用してアプリケーションをローカライズします。 ローカライズが完了したら、新しい値から新しい. resource.dll を生成することができます。

キーと値のペアのキーは、開発者によって元の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]に配置される `x:Uid` 値です。 これらの `x:Uid` 値を使用すると、ローカリゼーション中に開発者とローカライザーの間で発生した変更を、API で追跡およびマージできます。 たとえば、ローカライザーがローカライズを開始した後に開発者が [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を変更した場合、その変更を既にローカライズされている内容とマージすれば、翻訳結果が失われるのを最小限に減らすことができます。

次の図は、BAML 形式の XAML に基づく一般的なローカリゼーション ワークフローを示したものです。 この図では、開発者がアプリケーションを英語で記述していることを前提としています。 開発者は、WPF アプリケーションを作成し、グローバライズします。 開発者は、プロジェクト ファイルで `<UICulture>en-US</UICulture>` を設定することで、言語に依存しないメイン アセンブリと、ローカライズ可能なすべてのリソースを含んだサテライトがビルド時に生成されるようにします。 WPF のローカリゼーション API ではメイン アセンブリからの抽出がサポートされているので、必要であれば、ソース言語をメイン アセンブリ内に保持することもできます。 ビルド プロセスの後、XAML は BAML へとコンパイルされます。 英語圏の顧客には、カルチャに依存しない MyDialog.exe.resources.dll が提供されます。

![ローカリゼーション ワークフローを示した図。](./media/wpf-globalization-and-localization-overview/localization-workflow.png)

![ローカライズしないワークフローを示した図。](./media/wpf-globalization-and-localization-overview/unlocalized-workflow.png)

## <a name="examples-of-wpf-localization"></a>WPF のローカライズの例

このセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションをビルドしてローカライズする方法を理解するのに役立つ、ローカライズされたアプリケーションの例を紹介します。

### <a name="run-dialog-box-example"></a>[ファイル名を指定して実行] ダイアログ ボックスの例

次の図は、 **[ファイル名を指定して実行]** ダイアログ ボックスの出力サンプルです。

**英語:**

![英語版の [ファイル名を指定して実行] ダイアログ ボックスのスクリーンショット。](./media/wpf-globalization-and-localization-overview/run-dialog-box-english.png)

**ドイツ語:**

![ドイツ語版の [ファイル名を指定して実行] ダイアログ ボックスのスクリーンショット。](./media/wpf-globalization-and-localization-overview/run-dialog-box-german.png)

**[ファイル名を指定して実行] ダイアログ ボックスをグローバル対応でデザインする**

この例では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して **[ファイル名を指定して実行]** ダイアログ ボックスを生成します。 このダイアロ グボックスは、Microsoft Windows の [スタート] メニューから使用できる **[ファイル名を指定して実行]** ダイアログ ボックスと同じものです。

グローバル ダイアログ ボックスを作成する際の重要なポイントを以下にいくつか示します。

**自動レイアウト**

*Window1.xaml:*

`<Window SizeToContent="WidthAndHeight">`

上記の Window プロパティでは、コンテンツのサイズに応じてウィンドウのサイズを自動的に変更するよう指定しています。 このプロパティにより、ローカライズ後にコンテンツのサイズが大きくなった場合でも、それがウィンドウからはみ出るのを防ぐことができます。また、ローカライズ後にコンテンツのサイズが小さくなった場合にも、不要な領域が表示されるのを回避できます。

`<Grid x:Uid="Grid_1">`

<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ローカリゼーション API を正しく機能させるために必要です。

これらのプロパティは、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] の開発とローカリゼーションの間で起こる変更を追跡するために、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ローカリゼーション API によって使用されます。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを使用すると、新しいバージョンの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を、その [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の古いローカリゼーションとマージすることができます。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを追加するには、コマンド シェルで `msbuild -t:updateuid RunDialog.csproj` を実行します。 これが、<xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティを追加するための推奨の方法となります。通常、プロパティを手動で追加すると時間がかかり、正確さも低下します。 <xref:System.Windows.Markup.Localizer.BamlLocalizableResourceKey.Uid%2A> プロパティが正しく設定されていることを確認するには、`msbuild -t:checkuid RunDialog.csproj` を実行します。

[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] は <xref:System.Windows.Controls.Grid> コントロールを使用して構築されます。これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で自動レイアウトを活用するために役立つコントロールです。 なお、このダイアログ ボックスは、3 つの行と 5 つの列に分割されることに注意してください。 行と列のいずれも、固定サイズでは定義されていません。そのため、各セルに配置されている [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素は、ローカリゼーション時に起こるサイズの増減に合わせて調整できます。

[!code-xaml[GlobalizationRunDialog#GridColumnDef](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef)]

最初の 2 つの列には、**Open:** というラベルと <xref:System.Windows.Controls.ComboBox> が配置されていますが、これらの列では、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 全体の幅の 10% が使用されます。

[!code-xaml[GlobalizationRunDialog#GridColumnDef2](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationRunDialog/CS/Window1.xaml#gridcolumndef2)]

この例では、<xref:System.Windows.Controls.Grid> の共有サイズ設定機能を使用していることに注意してください。 残りの 3 つの列については、同じ <xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> に配置して、この機能を利用します。 これは、プロパティ名からもわかるように、複数の列で同じサイズを共有できるようにする機能です。 つまり、"Browse..." がローカライズされて "Durchsuchen..." となり、文字列がより長くなった場合、小さい "OK" ボタンに対して不釣り合いな "Durchsuchen..." が表示されるのではなく、すべてのボタンの幅が大きくなります。

**xml:lang**

`xml:lang="en-US"`

[XAML での xml:lang の処理](../../../desktop-wpf/xaml-services/xml-language-handling.md)が [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のルート要素に配置されていることに注意してください。 このプロパティは、指定された要素とその子要素のカルチャを表します。 この値は [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のいくつかの機能で使用されるので、ローカライズ時に適切に変更する必要があります。 ハイフネーションや単語のスペルチェックに使用される言語辞書は、この値によって変わります。 また、この値は、桁の表示方法や、フォント フォールバック システムでの使用フォントの選択方法にも影響します。 さらに、このプロパティは、数値の表示方法や、複雑なスクリプトでのテキストの整形方法にも影響します。 既定値は "en-US" です。

**サテライト リソース アセンブリのビルド**

*.csproj:*

`.csproj` ファイルを編集し、無条件の `<PropertyGroup>` に次のタグを追加します。

`<UICulture>en-US</UICulture>`

`UICulture` の値が追加されていることに注目してください。 これが en-US などの有効な <xref:System.Globalization.CultureInfo> 値に設定されている場合、プロジェクトをビルドすると、ローカライズ可能なすべてのリソースを含んだサテライト アセンブリが生成されます。

`<Resource Include="RunIcon.JPG">`

`<Localizable>False</Localizable>`

`</Resource>`

`RunIcon.JPG` は、すべてのカルチャで同様に表示されるので、ローカライズする必要はありません。 `Localizable` は `false` に設定されているので、サテライト アセンブリではなく、言語に依存しないメイン アセンブリに保持されます。 コンパイルされていないすべてのリソースの既定値では、`true` が `Localizable` に設定されます。

**[ファイル名を指定して実行] ダイアログのローカライズ**

**Parse**

アプリケーションをビルドしたら、それをローカライズするための最初の手順として、サテライト アセンブリのローカライズ可能なリソースを解析します。 このトピックでは、[LocBaml ツール サンプル](https://github.com/microsoft/WPF-Samples/tree/master/Tools/LocBaml)の記事に記載されている、サンプルの LocBaml ツールを使用します。 LocBaml はあくまでも、ローカライズ プロセスに適したローカリゼーション ツールの構築の開始に役立つ、サンプル ツールであることに注意してください。 LocBaml を使用して、**LocBaml /parse RunDialog.resources.dll /out:** を解析し、"RunDialog.resources.dll.CSV" ファイルを生成します。

**Localize**

お好みの CSV エディター (Unicode をサポートしているもの) を使用して、このファイルを編集します。 ローカライズ カテゴリが "None" であるすべてのエントリを除外してください。 次のエントリが表示されます。

|リソース キー|ローカリゼーション カテゴリ|[値]|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|Button|OK|
|Button_2:System.Windows.Controls.Button.$Content|Button|キャンセル|
|Button_3:System.Windows.Controls.Button.$Content|Button|参照...|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|テキスト|実行するプログラム名、または開くフォルダーやドキュメント名、インターネット リソース名を入力してください。|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|テキスト|[オープン]\:|
|Window_1:System.Windows.Window.Title|Title|実行|

アプリケーションをドイツ語にローカライズするには、次のように変換する必要があります。

|リソース キー|ローカリゼーション カテゴリ|[値]|
|-|-|-|
|Button_1:System.Windows.Controls.Button.$Content|Button|OK|
|Button_2:System.Windows.Controls.Button.$Content|Button|Abbrechen|
|Button_3:System.Windows.Controls.Button.$Content|Button|Durchsuchen…|
|ComboBox_1:System.Windows.Controls.ComboBox.$Content|ComboBox||
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|テキスト|Geben Sie den Namen eines Programms, Ordners, Dokuments oder einer Internetresource an.|
|TextBlock_2:System.Windows.Controls.TextBlock.$Content|テキスト|Öffnen:|
|Window_1:System.Windows.Window.Title|Title|実行|

**Generate**

ローカリゼーションの最後の手順として、新たにローカライズされたサテライト アセンブリを作成します。 これを行うには、次の LocBaml コマンドを使用します。

**LocBaml.exe /generate RunDialog.resources.dll /trans:RunDialog.resources.dll.CSV /out: . /cul:de-DE**

ドイツ語版の Windows では、メイン アセンブリの隣の de-DE フォルダーにこの resources.dll が配置されている場合、en-US フォルダーにあるリソースではなく、このリソースが自動的に読み込まれます。 ドイツ語版の Windows がインストールされていない場合、これをテストするには、使用している Windows でカルチャを任意のカルチャ (`en-US` など) に設定し、元のリソース DLL を置き換えてください。

**サテライト リソースの読み込み**

|MyDialog.exe|en-US\MyDialog.resources.dll|de-DE\MyDialog.resources.dll|
|------------------|------------------------------------|------------------------------------|
|コード|元の英語の BAML|ローカライズされた BAML|
|カルチャに依存しないリソース|その他の英語のリソース|ドイツ語にローカライズされたその他のリソース|

.NET では、アプリケーションの <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=nameWithType> に基づいて、読み込むサテライト リソース アセンブリが自動的に選択されます。 これは、既定では Windows OS のカルチャになります。 ドイツ語版の Windows を使用している場合は、*de-DE\MyDialog.resources.dll* ファイルが読み込まれます。 英語版の Windows を使用している場合は、*en-US\MyDialog.resources.dll* ファイルが読み込まれます。 アプリケーションの最終的なフォールバック リソースは、プロジェクトの *AssemblyInfo* ファイルで `NeutralResourcesLanguage` 属性を指定することによって設定できます。 たとえば、次のように指定します。

`[assembly: NeutralResourcesLanguage("en-US", UltimateResourceFallbackLocation.Satellite)]`

このように指定すると、次のいずれのファイルも使用できない場合に、*en-US\MyDialog.resources.dll* ファイルがドイツ語版の Windows で使用されます: *de-DE\MyDialog.resources.dll* または *de\MyDialog.resources.dll*。

### <a name="microsoft-saudi-arabia-homepage"></a>Microsoft サウジ アラビアのホームページ

次の図は、英語とアラビア語のホームページを示したものです。 これらのグラフィックスを生成する完全なサンプルについては、[グローバリゼーション ホームページのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)を参照してください。

**英語:**

![英語版のホーム ページのスクリーンショット。](./media/wpf-globalization-and-localization-overview/english-home-page-sample.jpg)

**アラビア語:**

![アラビア語版のホーム ページのスクリーンショット。](./media/wpf-globalization-and-localization-overview/arabic-home-page-sample.jpg)

### <a name="designing-a-global-microsoft-home-page"></a>グローバル対応の Microsoft ホームページのデザイン

Microsoft サウジアラビアの Web サイトを表したこのモック アップは、RightToLeft 言語用に提供されているグローバリゼーション機能を説明するためのものです。 ヘブライ語やアラビア語などの言語では、読み取りの方向が右から左なので、多くの場合、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のレイアウトは、左から右に記述する英語などの言語とはまったく異なるレイアウトになります。 左から右に記述する言語を右から左の言語へとローカライズしたり、その逆のローカライズを行ったりする場合には、作業が非常に困難になる場合があります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、このようなローカライズを大幅に簡素化できるように設計されています。

**FlowDirection**

*Homepage.xaml:*

[!code-xaml[GlobalizationHomepage#Homepage](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#homepage)]

<xref:System.Windows.Controls.Page> の <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティに注目してください。 このプロパティを <xref:System.Windows.FlowDirection.RightToLeft> に変更すると、<xref:System.Windows.Controls.Page> とその子要素の <xref:System.Windows.FrameworkElement.FlowDirection%2A> が変更されるため、この [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のレイアウトが右から左へと反転され、アラビア語のユーザー向けの表示になります。 継承動作は、任意の要素に対して明示的な <xref:System.Windows.FrameworkElement.FlowDirection%2A> を指定することでオーバーライドできます。 <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティは、<xref:System.Windows.FrameworkElement> またはドキュメント関連の要素で使用でき、暗黙的な値は <xref:System.Windows.FlowDirection.LeftToRight> となります。

ルートの <xref:System.Windows.FrameworkElement.FlowDirection%2A> が変更されたことで、背景のグラデーション ブラシまでもが正しく反転されていることに注目してください。

**FlowDirection="LeftToRight"**

![左から右のグラデーション フローを示すスクリーンショット。](./media/wpf-globalization-and-localization-overview/gradient-flow-left-right.png)

**FlowDirection="RightToLeft"**

![右から左のグラデーション フローを示すスクリーンショット。](./media/wpf-globalization-and-localization-overview/gradient-flow-right-left.png)

**パネルとコントロールに固定ディメンションを使用しない**

Homepage.xaml を見ると、上部の <xref:System.Windows.Controls.DockPanel> の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 全体に対して固定の幅と高さが指定されているのを除いては、固定のディメンションはありません。 ローカライズ後のテキストがソース テキストよりも長くなる可能性がある場合は、テキストがクリップされるのを防ぐため、固定ディメンションを使用しないようにしましょう。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のパネルとコントロールは、配置先のコンテンツに基づいて自動的にサイズ変更されます。 ほとんどのコントロールには、最小値と最大値もあるので、より詳細な制御を設定できます (たとえば、MinWidth = "20")。 また、<xref:System.Windows.Controls.Grid> を使用する場合は、'\*' を使って相対的な幅と高さを設定したり (たとえば、`Width="0.25*"`)、セル サイズの共有機能を使用したりすることもできます。

**ローカリゼーション コメント**

場合によっては、コンテンツがあいまいで、翻訳が困難なケースもあります。 ローカライズ コメントを使用すれば、開発者やデザイナーがローカライザーに追加のコンテキストやコメントを提供できます。 たとえば、次の例では、'&#124;' という文字の用途をローカリゼーション コメントによって明示しています。

[!code-xaml[GlobalizationHomepage#LocalizationComment](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcomment)]

このコメントは TextBlock_1 のコンテンツに関連付けられます。LocBaml ツールの場合 (「[アプリケーションのローカライズ](how-to-localize-an-application.md)」を参照)、出力される .csv ファイルの TextBlock_1 の行の 6 番目の列に表示されます。

|リソース キー|カテゴリ|読み取り可能|変更可能|コメント|[値]|
|-|-|-|-|-|-|
|TextBlock_1:System.Windows.Controls.TextBlock.$Content|テキスト|true|true|この文字は、装飾規則として使用されます。|&#124;|

コメントは、次の構文を使用して、任意の要素のコンテンツやプロパティに配置できます。

[!code-xaml[GlobalizationHomepage#LocalizationCommentsProp](~/samples/snippets/csharp/VS_Snippets_Wpf/GlobalizationHomepage/CS/Homepage.xaml#localizationcommentsprop)]

**ローカリゼーション属性**

多くの場合、開発者やローカリゼーション マネージャーは、ローカライザーがどのような読み取り操作や変更操作を実行できるかを制御する必要があります。 たとえば、会社の名前や法律上の表記をローカライザーに翻訳させたくない場合もあるでしょう。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、要素のコンテンツやプロパティの可読性、変更可能性、およびカテゴリを設定するための属性が使用できます。これらの属性は、ローカリゼーション ツールで要素をロックしたり、非表示にしたり、並べ替えたりするために使用できます。 詳細については、「<xref:System.Windows.Localization.Attributes%2A>」を参照してください。 このサンプルでは、LocBaml ツールによってこれらの属性の値のみを出力しています。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のすべてのコントロールには、これらの属性の既定値がありますが、これらの属性はオーバーライドすることもできます。 たとえば、次の例では、`TextBlock_1` の既定のローカリゼーション属性をオーバーライドし、コンテンツを読み取り可能に設定しています。ただし、ローカライザーはこれを変更できないように設定しています。

[!code-xaml[LocalizationComAtt#LocalizationAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributes)]

可読性と変更可能性の属性に加えて、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では一般的な UI カテゴリ (<xref:System.Windows.LocalizationCategory>) の列挙型も用意されています。これを使用することで、ローカライザーにより多くのコンテキストを提供することができます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で提供されているプラットフォーム コントロールの既定のカテゴリ は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でオーバーライドすることもできます。

[!code-xaml[LocalizationComAtt#LocalizationAttributesOverridden](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationComAtt/CSharp/Attributes.xaml#localizationattributesoverridden)]

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で提供されている既定のローカリゼーション属性は、コードを使用してオーバーライドすることもできます。これにより、カスタム コントロールに適切な既定値を正しく設定することができます。 次に例を示します。

```csharp
[Localizability(Readability = Readability.Readable, Modifiability=Modifiability.Unmodifiable, LocalizationCategory.None)]
public class CorporateLogo : TextBlock
{
    // ...
}
```

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で設定されたインスタンスごとの属性は、カスタム コントロールのコードで設定した値よりも優先されます。 属性とコメントの詳細については、「[ローカリゼーション属性とコメント](localization-attributes-and-comments.md)」を参照してください。

**フォント フォールバックと複合フォント**

特定のコードポイント範囲をサポートしていないフォントを指定した場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、Windows\Fonts ディレクトリにあるグローバル ユーザーの Interface.compositefont を使用して、その範囲をサポートしているフォントへと自動的にフォールバックされます。 複合フォントは他のフォントと同様に動作し、要素の `FontFamily` を設定することによって明示的に使用できます (たとえば、`FontFamily="Global User Interface"`)。 特定のコードポイント範囲と言語に使用するフォントを指定し、独自のフォント フォールバック設定を指定することで、独自の複合フォントを作成することもできます。

複合フォントの詳細については、「<xref:System.Windows.Media.FontFamily>」を参照してください。

**Microsoft ホームページのローカライズ**

このアプリケーションは、[ファイル名を指定して実行] ダイアログの例と同じ手順に従ってローカライズできます。 アラビア語用にローカライズされた .csv ファイルは、[グローバリゼーション ホームページのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Globalization%20and%20Localization/GlobalizationHomepage)から入手できます。
