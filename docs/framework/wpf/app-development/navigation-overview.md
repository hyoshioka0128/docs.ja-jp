---
title: ナビゲーションの概要
description: Windows Presentation Foundation (WPF) のスタンドアロン アプリケーションと XAML ブラウザー アプリケーションで使用されるブラウザー スタイルのナビゲーションに対するサポートについて説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- loose XAML files [WPF]
- windows [WPF]
- Start page [WPF]
- HTML files [WPF]
- structured navigation [WPF]
- fragment navigation [WPF]
- URIs (Uniform Resource Identifiers)
- custom objects [WPF]
- Uniform Resource Identifiers (URIs)
- pages [WPF]
- frames [WPF]
- navigation hosts [WPF]
- journals [WPF]
- lifetimes [WPF]
- retaining content state [WPF]
- content state [WPF]
- programmatic navigation [WPF]
- hyperlinks [WPF]
ms.assetid: 86ad2143-606a-4e34-bf7e-51a2594248b8
ms.openlocfilehash: 2aac1b3a38b6240bfba1b90983fd9cbd18b31b6f
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621705"
---
# <a name="navigation-overview"></a>ナビゲーションの概要

Windows Presentation Foundation (WPF) では、2 種類のアプリケーション (スタンドアロン アプリケーションと XAML ブラウザー アプリケーション (XBAP)) で使用できるブラウザー スタイルのナビゲーションがサポートされています。 ナビゲーション用にコンテンツをパッケージ化するため、WPF では <xref:System.Windows.Controls.Page> クラスが提供されています。 <xref:System.Windows.Controls.Page> 間は、<xref:System.Windows.Documents.Hyperlink> を使用して宣言により、または <xref:System.Windows.Navigation.NavigationService> を使用してプログラムにより、ナビゲートできます。 WPF では、ナビゲート元のページを記憶し、それらのページに戻るために、履歴が使用されます。

<xref:System.Windows.Controls.Page>、<xref:System.Windows.Documents.Hyperlink>、<xref:System.Windows.Navigation.NavigationService>、および履歴は、WPF によって提供されるナビゲーション サポートの中核を形成しています。 この概要では、これらの機能を詳しく説明してから、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ファイル、HTML ファイル、およびオブジェクトへのナビゲーションなど、高度なナビゲーション サポートについて説明します。

> [!NOTE]
> このトピックでは、"ブラウザー" という用語は、WPF アプリケーションをホストできるブラウザーのみを指し、現時点では、Microsoft Internet Explorer と Firefox が含まれます。 特定の WPF 機能が特定のブラウザーによってのみサポートされる場合は、ブラウザーのバージョンを示します。

## <a name="navigation-in-wpf-applications"></a>WPF アプリケーションでのナビゲーション

このトピックでは、WPF における主なナビゲーション機能の概要を説明します。 これらの機能は、スタンドアロン アプリケーションと XBAP の両方で使用できますが、このトピックでは XBAP のコンテキストで説明します。

> [!NOTE]
> このトピックは、XBAP のビルドと配置の方法については説明しません。 XBAP の詳細については、「[WPF XAML ブラウザー アプリケーションの概要](wpf-xaml-browser-applications-overview.md)」を参照してください。

このセクションでは、ナビゲーションの次の側面について説明し、例を示します。

- [ページの実装](#CreatingAXAMLPage)

- [スタート ページの構成](#Configuring_a_Start_Page)

- [ホスト ウィンドウのタイトル、幅、および高さの構成](#ConfiguringAXAMLPage)

- [ハイパーリンクのナビゲーション](#NavigatingBetweenXAMLPages)

- [フラグメント ナビゲーション](#FragmentNavigation)

- [ナビゲーション サービス](#NavigationService)

- [ナビゲーション サービスによるプログラム ナビゲーション](#Programmatic_Navigation_with_the_Navigation_Service)

- [ナビゲーションの有効期間](#Navigation_Lifetime)

- [履歴によるナビゲーションの記憶](#NavigationHistory)

- [ページの有効期間と履歴](#PageLifetime)

- [ナビゲーション履歴によるコンテンツの状態の保持](#RetainingContentStateWithNavigationHistory)

- [Cookie](#Cookies)

- [構造化ナビゲーション](#Structured_Navigation)

<a name="CreatingAXAMLPage"></a>

### <a name="implementing-a-page"></a>ページの実装

WPF では、.NET Framework オブジェクト、カスタム オブジェクト、列挙値、ユーザー コントロール、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル、HTML ファイルなど、いくつかのコンテンツ タイプにナビゲートできます。 ただし、コンテンツをパッケージ化する最も一般的で便利な方法は、<xref:System.Windows.Controls.Page> を使用することです。 さらに、<xref:System.Windows.Controls.Page> では、ナビゲーション固有の機能が実装されており、それらの外観が強化され、開発が単純化されます。

<xref:System.Windows.Controls.Page> を使用すると、次のようなマークアップを使用して、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のコンテンツのナビゲート可能なページを宣言によって実装できます。

[!code-xaml[NavigationOverviewSnippets#Page1XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/Page1.xaml#page1xaml)]

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップで実装される <xref:System.Windows.Controls.Page> には、ルート要素として `Page` があり、WPF XML 名前空間の宣言が必要です。 `Page` 要素には、ナビゲートして表示するコンテンツが格納されます。 コンテンツは、次のマークアップに示されているように、`Page.Content` プロパティ要素を設定することによって追加します。

[!code-xaml[NavigationOverviewSnippets#Page2XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/Page2.xaml#page2xaml)]

`Page.Content` には、1 つの子要素のみを含めることができます。前の例では、コンテンツは単一の文字列「Hello, Page!」です。 実際には、通常、レイアウト コントロールを子要素として使用して (「[レイアウト](../advanced/layout.md)」を参照)、コンテンツを格納し、構成します。

`Page` 要素の子要素は、<xref:System.Windows.Controls.Page> のコンテンツとみなされるため、明示的な `Page.Content` 宣言を使用する必要はありません。 次のマークアップは、前のサンプルの宣言と同等です。

[!code-xaml[NavigationOverviewSnippets#Page3XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/Page3.xaml#page3xaml)]

この場合、`Page.Content` は、`Page` 要素の子要素を使用して自動的に設定されます。 詳細については、「[WPF のコンテンツ モデル](../controls/wpf-content-model.md)」を参照してください。

マークアップのみの <xref:System.Windows.Controls.Page> は、コンテンツの表示に役立ちます。 ただし、<xref:System.Windows.Controls.Page> では、ユーザーがページと対話するためのコントロールも表示でき、イベントを処理し、アプリケーション ロジックを呼び出すことによって、ユーザーの操作に応答できます。 対話形式の <xref:System.Windows.Controls.Page> は、次の例に示されているように、マークアップと分離コードの組み合わせを使用して実装されます。

[!code-xaml[XBAPAppDefSnippets#HomePageMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppDefSnippets/CSharp/HomePage.xaml#homepagemarkup)]

[!code-csharp[XBAPAppDefSnippets#HomePageCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppDefSnippets/CSharp/HomePage.xaml.cs#homepagecodebehind)]
[!code-vb[XBAPAppDefSnippets#HomePageCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XBAPAppDefSnippets/VisualBasic/HomePage.xaml.vb#homepagecodebehind)]

マークアップ ファイルと分離コード ファイルを連携させるには、次の構成が必要です。

- マークアップでは、`Page` 要素に `x:Class` 属性を含める必要があります。 アプリケーションのビルド時にマークアップ ファイルに `x:Class` が含まれていると、Microsoft Build Engine (MSBuild) により、`x:Class` 属性で指定された名前を持つ、<xref:System.Windows.Controls.Page> から派生した `partial` クラスが作成されます。 そのためには、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] スキーマ (`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`) に XML 名前空間宣言を追加する必要があります。 生成された `partial` クラスでは、`InitializeComponent` メソッドが実装されています。このメソッドを呼び出すと、イベントが登録され、マークアップで実装されるプロパティが設定されます。

- 分離コードでは、クラスは、マークアップ内の `x:Class` 属性で指定されている名前を持つ `partial` クラスでなければなりません。また、<xref:System.Windows.Controls.Page> から派生する必要があります。 これによって、分離コード ファイルと、アプリケーションのビルド時にマークアップ ファイル用に生成される `partial` クラスとが関連付けられます (「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照)。

- 分離コードでは、<xref:System.Windows.Controls.Page> クラスによって実装されるコンストラクターで `InitializeComponent` メソッドが呼び出される必要があります。 `InitializeComponent` は、マークアップ ファイル用に生成された `partial` クラスによって実装されるもので、マークアップで定義されているイベントの登録と、プロパティの設定を行います。

> [!NOTE]
> Visual Studio を使用してプロジェクトに新しい <xref:System.Windows.Controls.Page> を追加すると、ここで説明したように、マークアップと分離コードの両方を使用して <xref:System.Windows.Controls.Page> が実装され、マークアップ ファイルと分離コード ファイル間の関連付けの作成に必要な構成が組み込まれます。

<xref:System.Windows.Controls.Page> を作成したら、そこにナビゲートできます。 アプリケーションが最初にナビゲートする <xref:System.Windows.Controls.Page> を指定するには、スタート <xref:System.Windows.Controls.Page> を構成する必要があります。

<a name="Configuring_a_Start_Page"></a>

### <a name="configuring-a-start-page"></a>スタート ページの構成

XBAP では、一定の量のアプリケーション インフラストラクチャをブラウザーでホストする必要があります。 WPF では、<xref:System.Windows.Application> クラスは、必要なアプリケーション インフラストラクチャを確立するアプリケーション定義の一部です (「[アプリケーション管理の概要](application-management-overview.md)」を参照)。

アプリケーション定義は、通常、MSBuild の `ApplicationDefinition` 項目として構成されたマークアップ ファイルで、マークアップとコードビハインドの両方を使用して実装されます。 XBAP のアプリケーション定義を次に示します。

[!code-xaml[XBAPAppDefSnippets#XBAPApplicationDefinitionMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppDefSnippets/CSharp/App.xaml#xbapapplicationdefinitionmarkup)]

[!code-csharp[XBAPAppDefSnippets#XBAPApplicationDefinitionCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppDefSnippets/CSharp/App.xaml.cs#xbapapplicationdefinitioncodebehind)]
[!code-vb[XBAPAppDefSnippets#XBAPApplicationDefinitionCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XBAPAppDefSnippets/VisualBasic/Application.xaml.vb#xbapapplicationdefinitioncodebehind)]

XBAP では、アプリケーション定義を使用して、スタート <xref:System.Windows.Controls.Page> を指定でき、これは、XBAP が起動されたときに自動的に呼び出される <xref:System.Windows.Controls.Page> です。 このためには、目的の <xref:System.Windows.Controls.Page> の Uniform Resource Identifier (URI) を <xref:System.Windows.Application.StartupUri%2A> プロパティに設定します。

> [!NOTE]
> ほとんどの場合、<xref:System.Windows.Controls.Page> は、アプリケーションにコンパイルされるか、アプリケーションと共に配置されます。 このような場合、<xref:System.Windows.Controls.Page> を識別する URI はパック URI であり、これは、"*パック*" スキームに準拠した URI です。 パック URI については、「[WPF におけるパック URI](pack-uris-in-wpf.md)」で詳しく説明します。 以下で説明する http スキームを使用してコンテンツにナビゲートすることもできます。

次の例に示されているように、マークアップで宣言することによって、<xref:System.Windows.Application.StartupUri%2A> を設定することができます。

[!code-xaml[NavigationOverviewSnippets#XBAPApplicationDefinitionMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/App.xaml#xbapapplicationdefinitionmarkup)]

この例では、`StartupUri` 属性は、HomePage.xaml を識別する相対パック URI で設定されます。 XBAP が起動されると、HomePage.xaml に自動的にナビゲートして、それが表示されます。 これを次の図に示します。これは、Web サーバーから起動された XBAP を示しています。

![XBAP ページ](./media/navigation-overview/xbap-launched-from-a-web-server.png "これは、Web サーバーから起動された XBAP を示してす。")

> [!NOTE]
> XBAP の開発および配置の詳細については、「[WPF XAML ブラウザー アプリケーションの概要](wpf-xaml-browser-applications-overview.md)」および「[WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)」を参照してください。

<a name="ConfiguringAXAMLPage"></a>

### <a name="configuring-the-host-windows-title-width-and-height"></a>ホスト ウィンドウのタイトル、幅、および高さの構成

前の図を見て気付くことは、ブラウザーとタブのパネルのタイトルがどちらも XBAP の URI になっていることです。 このタイトルは、長いだけでなく、見た目が良いわけでも、有益な情報になっているわけでもありません。 このため、<xref:System.Windows.Controls.Page> には、<xref:System.Windows.Controls.Page.WindowTitle%2A> プロパティを設定することによってタイトルを変更する方法が用意されています。 さらに、<xref:System.Windows.Controls.Page.WindowWidth%2A> と <xref:System.Windows.Controls.Page.WindowHeight%2A> を設定することによって、ブラウザー ウィンドウの幅と高さをそれぞれ構成することができます。

<xref:System.Windows.Controls.Page.WindowTitle%2A>、<xref:System.Windows.Controls.Page.WindowWidth%2A>、および <xref:System.Windows.Controls.Page.WindowHeight%2A> は、次の例に示されているように、マークアップで宣言して設定できます。

[!code-xaml[NavigationOverviewSnippets#HomePageMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/HomePage.xaml#homepagemarkup)]

結果を次の例に示します。

![ウィンドウのタイトル、高さ、幅](./media/navigation-overview/window-title-width-height.png "これは、構成できるウィンドウのタイトル、高さ、幅を示します。")

<a name="NavigatingBetweenXAMLPages"></a>

### <a name="hyperlink-navigation"></a>ハイパーリンクのナビゲーション

一般的な XBAP は、複数のページで構成されます。 あるページから別のページにナビゲートする最も簡単な方法は、<xref:System.Windows.Documents.Hyperlink> を使用することです。 次のマークアップに示されているように、`Hyperlink` 要素を使用することによって、<xref:System.Windows.Documents.Hyperlink> を <xref:System.Windows.Controls.Page> に宣言によって追加できます。

[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml1)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml2)]
[!code-xaml[NavigationOverviewSnippets#HyperlinkXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithHyperlink.xaml#hyperlinkxaml3)]

`Hyperlink` 要素には、次のものが必要です。

- `NavigateUri` 属性によって使用される、ナビゲート先の <xref:System.Windows.Controls.Page> のパック URI。

- テキストやイメージなど、ユーザーがナビゲーションを開始するためにクリックできるコンテンツ (`Hyperlink` 要素に格納できるコンテンツについては、<xref:System.Windows.Documents.Hyperlink> を参照)。

次の図では、<xref:System.Windows.Documents.Hyperlink> がある <xref:System.Windows.Controls.Page> を持つ XBAP を示します。

![ハイパーリンクを含むページ](./media/navigation-overview/xbap-with-a-page-with-a-hyperlink.png "これは、ハイパーリンクのあるページが含まれる XBAP を示します。")

想定されるとおり、<xref:System.Windows.Documents.Hyperlink> をクリックすると、XBAP は `NavigateUri` 属性によって識別される <xref:System.Windows.Controls.Page> にナビゲートします。 さらに、XBAP により、前の <xref:System.Windows.Controls.Page> のエントリが、Internet Explorer の [最近表示したページ] の一覧に追加されます。 これを次の図に示します。

![[戻る] ボタンと [次に進む] ボタン](./media/navigation-overview/back-and-forward-navigation.png "[戻る] ボタンと [進む] ボタンでナビゲートします。")

<xref:System.Windows.Controls.Page> 間のナビゲーションのサポートだけでなく、<xref:System.Windows.Documents.Hyperlink> ではフラグメント ナビゲーションもサポートされます。

<a name="FragmentNavigation"></a>

### <a name="fragment-navigation"></a>フラグメント ナビゲーション

"*フラグメント ナビゲーション*" は、現在の <xref:System.Windows.Controls.Page> または別の <xref:System.Windows.Controls.Page> にあるコンテンツ フラグメントへのナビゲーションです。 WPF では、コンテンツ フラグメントは、名前付き要素に格納されるコンテンツです。 名前付き要素とは、`Name` 属性が設定されている要素です。 次のマークアップは、コンテンツ フラグメントを含む名前付き `TextBlock` 要素を示しています。

[!code-xaml[NavigationOverviewSnippets#PageWithContentFragmentsMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithFragments.xaml#pagewithcontentfragmentsmarkup1)]
[!code-xaml[NavigationOverviewSnippets#PageWithContentFragmentsMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithFragments.xaml#pagewithcontentfragmentsmarkup2)]
[!code-xaml[NavigationOverviewSnippets#PageWithContentFragmentsMARKUP3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithFragments.xaml#pagewithcontentfragmentsmarkup3)]

コンテンツ フラグメントにナビゲートする <xref:System.Windows.Documents.Hyperlink> の場合、`NavigateUri` 属性に次のものを含める必要があります。

- ナビゲート先のコンテンツ フラグメントがある <xref:System.Windows.Controls.Page> の URI。

- 「#」文字。

- コンテンツ フラグメントがある <xref:System.Windows.Controls.Page> 上の要素の名前。

フラグメント URI の形式は、次のとおりです。

*PageURI* `#` *ElementName*

コンテンツ フラグメントにナビゲートするように構成された `Hyperlink` の例を次に示します。

[!code-xaml[NavigationOverviewSnippets#PageThatNavigatesXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageThatNavigatesToFragment.xaml#pagethatnavigatesxaml1)]
[!code-xaml[NavigationOverviewSnippets#PageThatNavigatesXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageThatNavigatesToFragment.xaml#pagethatnavigatesxaml2)]
[!code-xaml[NavigationOverviewSnippets#PageThatNavigatesXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageThatNavigatesToFragment.xaml#pagethatnavigatesxaml3)]

> [!NOTE]
> このセクションでは、WPF での既定のフラグメント ナビゲーション実装について説明します。 WPF では、部分的に <xref:System.Windows.Navigation.NavigationService.FragmentNavigation?displayProperty=nameWithType> イベントの処理が必要な、独自のフラグメント ナビゲーション スキームを実装することもできます。

> [!IMPORTANT]
> Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページ (ルート要素として `Page` を持つマークアップのみの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル) 内のフラグメントにナビゲートできるのは、HTTP でページを参照できる場合に限られます。
>
> ただし、Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページは、自身のフラグメントにナビゲートできます。

<a name="NavigationService"></a>

### <a name="navigation-service"></a>ナビゲーション サービス

<xref:System.Windows.Documents.Hyperlink> を使用すると、ユーザーは特定の <xref:System.Windows.Controls.Page> へのナビゲーションを開始できますが、ページの位置を特定し、ダウンロードする作業は、<xref:System.Windows.Navigation.NavigationService> クラスによって実行されます。 基本的に、<xref:System.Windows.Navigation.NavigationService> では、<xref:System.Windows.Documents.Hyperlink> などのクライアント コードの代わりに、ナビゲーション要求を処理できます。 さらに、<xref:System.Windows.Navigation.NavigationService> では、ナビゲーション要求の追跡と制御のための高レベルのサポートが実装されています。

<xref:System.Windows.Documents.Hyperlink> がクリックされると、WPF で <xref:System.Windows.Navigation.NavigationService.Navigate%2A?displayProperty=nameWithType> が呼び出され、指定されたパック URI にある <xref:System.Windows.Controls.Page> が特定されて、ダウンロードされます。 ダウンロードされた <xref:System.Windows.Controls.Page> は、ルート オブジェクトが、ダウンロードされた <xref:System.Windows.Controls.Page> のインスタンスであるオブジェクト ツリーに変換されます。 ルート <xref:System.Windows.Controls.Page> オブジェクトへの参照は、<xref:System.Windows.Navigation.NavigationService.Content%2A?displayProperty=nameWithType> プロパティに格納されます。 ナビゲート先のコンテンツのパック URI は、<xref:System.Windows.Navigation.NavigationService.Source%2A?displayProperty=nameWithType> プロパティに格納されますが、<xref:System.Windows.Navigation.NavigationService.CurrentSource%2A?displayProperty=nameWithType> には、ナビゲート先の最後のページのパック URI が格納されます。

> [!NOTE]
> WPF アプリケーションでは、現在アクティブな <xref:System.Windows.Navigation.NavigationService> を複数持つことが可能です。 詳細については、このトピックで後述する「[ナビゲーション ホスト](#Navigation_Hosts)」を参照してください。

<a name="Programmatic_Navigation_with_the_Navigation_Service"></a>

### <a name="programmatic-navigation-with-the-navigation-service"></a>ナビゲーション サービスによるプログラム ナビゲーション

ナビゲーションが <xref:System.Windows.Documents.Hyperlink> を使用してマークアップで宣言として実装される場合、開発者は <xref:System.Windows.Navigation.NavigationService> について知る必要はありません。<xref:System.Windows.Documents.Hyperlink> では <xref:System.Windows.Navigation.NavigationService> が自動的に使用されるためです。 つまり、<xref:System.Windows.Documents.Hyperlink> の直接的または間接的な親がナビゲーション ホストである限り (「[ナビゲーション ホスト](#Navigation_Hosts)」を参照)、<xref:System.Windows.Documents.Hyperlink> では、ナビゲーション ホストのナビゲーション サービスを発見および使用して、ナビゲーション要求を処理できます。

ただし、次のような場合は、<xref:System.Windows.Navigation.NavigationService> を直接使用する必要があります。

- パラメーターなしではないコンストラクターを使用して <xref:System.Windows.Controls.Page> をインスタンス化する必要がある場合。

- ナビゲートする前に、<xref:System.Windows.Controls.Page> のプロパティを設定する必要がある場合。

- どの <xref:System.Windows.Controls.Page> にナビゲートするかが、実行時まで決定できない場合。

このような場合は、<xref:System.Windows.Navigation.NavigationService> オブジェクトの <xref:System.Windows.Navigation.NavigationService.Navigate%2A> メソッドを呼び出すことによって、プログラムでナビゲーションを開始するコードを記述する必要があります。 そのためには、<xref:System.Windows.Navigation.NavigationService> への参照を取得する必要があります。

#### <a name="getting-a-reference-to-the-navigationservice"></a>NavigationService への参照の取得

「[ナビゲーション ホスト](#Navigation_Hosts)」のセクションで説明した理由から、WPF アプリケーションでは複数の <xref:System.Windows.Navigation.NavigationService> を持つことができます。 これは、<xref:System.Windows.Navigation.NavigationService> (通常は、現在の <xref:System.Windows.Controls.Page> にナビゲートした <xref:System.Windows.Navigation.NavigationService>) を検索する手段がコードに必要なことを意味します。 <xref:System.Windows.Navigation.NavigationService> への参照は、`static` <xref:System.Windows.Navigation.NavigationService.GetNavigationService%2A?displayProperty=nameWithType> メソッドを呼び出すことによって取得できます。 特定の <xref:System.Windows.Controls.Page> にナビゲートした <xref:System.Windows.Navigation.NavigationService> を取得するには、<xref:System.Windows.Controls.Page> への参照を <xref:System.Windows.Navigation.NavigationService.GetNavigationService%2A> メソッドの引数として渡します。 次のコードでは、現在の <xref:System.Windows.Controls.Page> に対する <xref:System.Windows.Navigation.NavigationService> を取得する方法を示します。

[!code-csharp[NavigationOverviewSnippets#GetNSCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/GetNSPage.xaml.cs#getnscodebehind1)]
[!code-csharp[NavigationOverviewSnippets#GetNSCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/GetNSPage.xaml.cs#getnscodebehind2)]
[!code-vb[NavigationOverviewSnippets#GetNSCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/GetNSPage.xaml.vb#getnscodebehind2)]

<xref:System.Windows.Controls.Page> に対する <xref:System.Windows.Navigation.NavigationService> を検索するショートカットとして、<xref:System.Windows.Controls.Page> では <xref:System.Windows.Controls.Page.NavigationService%2A> プロパティが実装されています。 これを次の例に示します。

[!code-csharp[NavigationOverviewSnippets#GetNSShortcutCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/GetNSPageShortCut.xaml.cs#getnsshortcutcodebehind1)]
[!code-csharp[NavigationOverviewSnippets#GetNSShortcutCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/GetNSPageShortCut.xaml.cs#getnsshortcutcodebehind2)]
[!code-vb[NavigationOverviewSnippets#GetNSShortcutCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/GetNSPageShortCut.xaml.vb#getnsshortcutcodebehind2)]

> [!NOTE]
> <xref:System.Windows.Controls.Page> で <xref:System.Windows.FrameworkElement.Loaded> イベントが発生したとき、<xref:System.Windows.Controls.Page> ではその <xref:System.Windows.Navigation.NavigationService> に対する参照だけを取得できます。

#### <a name="programmatic-navigation-to-a-page-object"></a>ページ オブジェクトへのプログラム ナビゲーション

次の例では、<xref:System.Windows.Navigation.NavigationService> を使用して、<xref:System.Windows.Controls.Page> にプログラムによってナビゲートする方法を示します。 ナビゲート先の <xref:System.Windows.Controls.Page> は単一のパラメーターなしではないコンストラクターを使用しなければインスタンス化できないため、プログラム ナビゲーションが必要になります。 次のマークアップとコードでは、パラメーターなしではないコンストラクターを持つ <xref:System.Windows.Controls.Page> を示します。

[!code-xaml[NavigationOverviewSnippets#PageWithNonDefaultConstructorXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithNonDefaultConstructor.xaml#pagewithnondefaultconstructorxaml)]

[!code-csharp[NavigationOverviewSnippets#PageWithNonDefaultConstructorCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithNonDefaultConstructor.xaml.cs#pagewithnondefaultconstructorcodebehind)]
[!code-vb[NavigationOverviewSnippets#PageWithNonDefaultConstructorCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/PageWithNonDefaultConstructor.xaml.vb#pagewithnondefaultconstructorcodebehind)]

次のマークアップとコードでは、パラメーターなしではないコンストラクターを持つ <xref:System.Windows.Controls.Page> にナビゲートする <xref:System.Windows.Controls.Page> を示します。

[!code-xaml[NavigationOverviewSnippets#NSNavigationPageXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSNavigationPage.xaml#nsnavigationpagexaml)]

[!code-csharp[NavigationOverviewSnippets#NSNavigationPageCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSNavigationPage.xaml.cs#nsnavigationpagecodebehind)]
[!code-vb[NavigationOverviewSnippets#NSNavigationPageCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/NSNavigationPage.xaml.vb#nsnavigationpagecodebehind)]

この <xref:System.Windows.Controls.Page> 上の <xref:System.Windows.Documents.Hyperlink> がクリックされると、パラメーターなしではないコンストラクターを使用し、<xref:System.Windows.Navigation.NavigationService.Navigate%2A?displayProperty=nameWithType> メソッドを呼び出して、ナビゲート先の <xref:System.Windows.Controls.Page> をインスタンス化することによって、ナビゲーションが開始されます。 <xref:System.Windows.Navigation.NavigationService.Navigate%2A> では、パック URI ではなく、<xref:System.Windows.Navigation.NavigationService> がナビゲートするオブジェクトへの参照が受け入れられます。

#### <a name="programmatic-navigation-with-a-pack-uri"></a>パック URI によるプログラム ナビゲーション

パック URI をプログラムによって構築する必要がある場合 (たとえば、実行時にのみパック URI を決定できる場合など) は、<xref:System.Windows.Navigation.NavigationService.Navigate%2A?displayProperty=nameWithType> メソッドを使用できます。 これを次の例に示します。

[!code-xaml[NavigationOverviewSnippets#NSUriNavigationPageXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSUriNavigationPage.xaml#nsurinavigationpagexaml)]

[!code-csharp[NavigationOverviewSnippets#NSUriNavigationPageCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSUriNavigationPage.xaml.cs#nsurinavigationpagecodebehind)]
[!code-vb[NavigationOverviewSnippets#NSUriNavigationPageCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/NSUriNavigationPage.xaml.vb#nsurinavigationpagecodebehind)]

#### <a name="refreshing-the-current-page"></a>現在のページの更新

<xref:System.Windows.Controls.Page> が <xref:System.Windows.Navigation.NavigationService.Source%2A?displayProperty=nameWithType> プロパティに格納されているパック URI と同じパック URI を持つ場合、このページはダウンロードされません。 WPF で現在のページを強制的に再びダウンロードするには、次の例に示されているように、<xref:System.Windows.Navigation.NavigationService.Refresh%2A?displayProperty=nameWithType> メソッドを呼び出します。

[!code-xaml[NavigationOverviewSnippets#NSRefreshNavigationPageXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSRefreshNavigationPage.xaml#nsrefreshnavigationpagexaml1)]

[!code-csharp[NavigationOverviewSnippets#NSRefreshNavigationPageCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSRefreshNavigationPage.xaml.cs#nsrefreshnavigationpagecodebehind1)]
[!code-vb[NavigationOverviewSnippets#NSRefreshNavigationPageCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/NSRefreshNavigationPage.xaml.vb#nsrefreshnavigationpagecodebehind1)]
[!code-csharp[NavigationOverviewSnippets#NSRefreshNavigationPageCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NSRefreshNavigationPage.xaml.cs#nsrefreshnavigationpagecodebehind2)]
[!code-vb[NavigationOverviewSnippets#NSRefreshNavigationPageCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/NSRefreshNavigationPage.xaml.vb#nsrefreshnavigationpagecodebehind2)]

<a name="Navigation_Lifetime"></a>

### <a name="navigation-lifetime"></a>ナビゲーションの有効期間

これまでに説明したように、ナビゲーションを開始するには多くの方法があります。 ナビゲーションが開始されると、ナビゲーション中に、<xref:System.Windows.Navigation.NavigationService> によって実装される次のイベントを使用して、ナビゲーションを追跡および制御できます。

- <xref:System.Windows.Navigation.NavigationService.Navigating>。 新しいナビゲーションが要求されたときに発生します。 ナビゲーションのキャンセルに使用できます。

- <xref:System.Windows.Navigation.NavigationService.NavigationProgress>。 ナビゲーション進行状況の情報提供を目的として、ダウンロード中に定期的に発生します。

- <xref:System.Windows.Navigation.NavigationService.Navigated>。 ページの位置が特定され、ダウンロードされたときに発生します。

- <xref:System.Windows.Navigation.NavigationService.NavigationStopped>。 ナビゲーションが停止されたとき (<xref:System.Windows.Navigation.NavigationService.StopLoading%2A> を呼び出すことによって)、または現在のナビゲーションの進行中に新しいナビゲーションが要求されたときに発生します。

- <xref:System.Windows.Navigation.NavigationService.NavigationFailed>。 要求されたコンテンツにナビゲートするときにエラーが発生したときに発生します。

- <xref:System.Windows.Navigation.NavigationService.LoadCompleted>。 ナビゲート先のコンテンツが読み込まれ、解析されて、レンダリングが開始されたときに発生します。

- <xref:System.Windows.Navigation.NavigationService.FragmentNavigation>。 コンテンツ フラグメントへのナビゲーションが開始されたときに、次のタイミングで発生します。

  - 目的のフラグメントが現在のコンテンツの場合は、すぐに発生します。

  - 目的のフラグメントが別のコンテンツにある場合は、ソース コンテンツが読み込まれた後で発生します。

ナビゲーション イベントは、次の図に示されている順序で発生します。

![ページ ナビゲーションのフロー チャート](./media/navigation-overview/order-of-navigation-events.png "ページ ナビゲーション イベントのフロー チャート")

一般に、<xref:System.Windows.Controls.Page> は、これらのイベントの影響を受けません。 アプリケーションは、これらのイベントの影響を受ける可能性が高いため、これらのイベントは <xref:System.Windows.Application> クラスによっても発生します。

- <xref:System.Windows.Application.Navigating?displayProperty=nameWithType>

- <xref:System.Windows.Application.NavigationProgress?displayProperty=nameWithType>

- <xref:System.Windows.Application.Navigated?displayProperty=nameWithType>

- <xref:System.Windows.Application.NavigationFailed?displayProperty=nameWithType>

- <xref:System.Windows.Application.NavigationStopped?displayProperty=nameWithType>

- <xref:System.Windows.Application.LoadCompleted?displayProperty=nameWithType>

- <xref:System.Windows.Application.FragmentNavigation?displayProperty=nameWithType>

<xref:System.Windows.Navigation.NavigationService> によってイベントが発生するたびに、<xref:System.Windows.Application> クラスでは対応するイベントが発生します。 <xref:System.Windows.Controls.Frame> と <xref:System.Windows.Navigation.NavigationWindow> では、それぞれのスコープ内でナビゲーションを検出するために、同じイベントが提供されています。

場合によっては、<xref:System.Windows.Controls.Page> がこれらのイベントに関与することがあります。 たとえば、<xref:System.Windows.Controls.Page> では、<xref:System.Windows.Navigation.NavigationService.Navigating?displayProperty=nameWithType> イベントを処理して、そのページ以外へのナビゲーションをキャンセルするかどうかを決定することがあります。 これを次の例に示します。

[!code-xaml[NavigationOverviewSnippets#CancelNavigationPageXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/CancelNavigationPage.xaml#cancelnavigationpagexaml)]

[!code-csharp[NavigationOverviewSnippets#CancelNavigationPageCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/CancelNavigationPage.xaml.cs#cancelnavigationpagecodebehind)]
[!code-vb[NavigationOverviewSnippets#CancelNavigationPageCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/CancelNavigationPage.xaml.vb#cancelnavigationpagecodebehind)]

前の例で行ったように、<xref:System.Windows.Controls.Page> からのナビゲーション イベントにハンドラーを登録した場合は、イベント ハンドラーの登録解除も行う必要があります。 解除しなかった場合、WPF ナビゲーションが履歴を使用して <xref:System.Windows.Controls.Page> ナビゲーションを記憶する方法に関して、副作用が発生する可能性があります。

<a name="NavigationHistory"></a>

### <a name="remembering-navigation-with-the-journal"></a>履歴によるナビゲーションの記憶

WPF では、戻るスタックと進むスタックの 2 つのスタックを使用して、ナビゲート元のページが記憶されます。 現在の <xref:System.Windows.Controls.Page> から新しい <xref:System.Windows.Controls.Page> にナビゲートするか、既存の <xref:System.Windows.Controls.Page> に進むときは、現在の <xref:System.Windows.Controls.Page> が "*戻るスタック*" に追加されます。 現在の <xref:System.Windows.Controls.Page> から前の <xref:System.Windows.Controls.Page> に戻るときは、現在の <xref:System.Windows.Controls.Page> が "*進むスタック*" に追加されます。 戻るスタック、進むスタック、およびそれらを管理する機能を、まとめて履歴と呼びます。 戻るスタックと進むスタックの各項目は、<xref:System.Windows.Navigation.JournalEntry> クラスのインスタンスであり、"*履歴エントリ*" と呼ばれます。

#### <a name="navigating-the-journal-from-internet-explorer"></a>Internet Explorer からの履歴のナビゲート

概念として、履歴は、Internet Explorer の **[戻る]** ボタンと **[進む]** ボタンと同じように機能します。 これを次の図に示します。

![[戻る] ボタンと [次に進む] ボタン](./media/navigation-overview/back-and-forward-navigation.png "[戻る] ボタンと [進む] ボタンでナビゲートします。")

Internet Explorer によってホストされる XBAP の場合、WPF では、履歴が Internet Explorer のナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] に統合されます。 これにより、ユーザーは、Internet Explorer の **[戻る]** 、 **[進む]** 、 **[最近表示したページ]** ボタンを使用して、XBAP のページ間をナビゲートできます。

> [!IMPORTANT]
> Internet Explorer では、ユーザーが XBAP との間でナビゲートすると、キープ アライブされなかったページの履歴項目のみが履歴に保持されます。 ページのキープ アライブについては、このトピックで後述する「[ページの有効期間と履歴](#PageLifetime)」を参照してください。

既定では、Internet Explorer の **[最近表示したページ]** の一覧に表示される各 <xref:System.Windows.Controls.Page> のテキストは、<xref:System.Windows.Controls.Page> の URI です。 多くの場合、これは、ユーザーにとって特に意味がありません。 幸い、次のオプションのいずれかを使用して、テキストを変更できます。

1. 添付 `JournalEntry.Name` 属性値。

2. `Page.Title` 属性値。

3. `Page.WindowTitle` 属性値と現在の <xref:System.Windows.Controls.Page> の URI。

4. 現在の <xref:System.Windows.Controls.Page> の URI。 (既定)

これらのオプションの順序は、テキスト検索の優先順位と一致します。 たとえば、`JournalEntry.Name` が設定された場合、他の値は無視されます。

次の例では、`Page.Title` 属性を使用して、履歴エントリに表示されるテキストを変更します。

[!code-xaml[NavigationOverviewSnippets#PageTitleMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithTitle.xaml#pagetitlemarkup1)]
[!code-xaml[NavigationOverviewSnippets#PageTitleMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithTitle.xaml#pagetitlemarkup2)]

[!code-csharp[NavigationOverviewSnippets#PageTitleCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithTitle.xaml.cs#pagetitlecodebehind1)]
[!code-vb[NavigationOverviewSnippets#PageTitleCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/PageWithTitle.xaml.vb#pagetitlecodebehind1)]
[!code-csharp[NavigationOverviewSnippets#PageTitleCODEBEHIND2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/PageWithTitle.xaml.cs#pagetitlecodebehind2)]
[!code-vb[NavigationOverviewSnippets#PageTitleCODEBEHIND2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigationOverviewSnippets/VisualBasic/PageWithTitle.xaml.vb#pagetitlecodebehind2)]

#### <a name="navigating-the-journal-using-wpf"></a>WPF を使用する履歴のナビゲート

ユーザーは Internet Explorer の **[戻る]** 、 **[進む]** 、 **[最近表示したページ]** を使用して履歴をナビゲートできますが、WPF によって提供される宣言およびプログラム メカニズムを使用して履歴をナビゲートすることもできます。 これを行う理由の 1 つは、カスタム ナビゲーション UI をページに表示するためです。

<xref:System.Windows.Input.NavigationCommands> によって公開されるナビゲーション コマンドを使用して、宣言によって履歴ナビゲーション サポートを追加できます。 次の例では、`BrowseBack` ナビゲーション コマンドの使用方法を示します。

[!code-xaml[NavigationOverviewSnippets#NavigationCommandsPageXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NavigationCommandsPage.xaml#navigationcommandspagexaml1)]
[!code-xaml[NavigationOverviewSnippets#NavigationCommandsPageXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NavigationCommandsPage.xaml#navigationcommandspagexaml2)]
[!code-xaml[NavigationOverviewSnippets#NavigationCommandsPageXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NavigationCommandsPage.xaml#navigationcommandspagexaml3)]
[!code-xaml[NavigationOverviewSnippets#NavigationCommandsPageXAML4](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/NavigationCommandsPage.xaml#navigationcommandspagexaml4)]

<xref:System.Windows.Navigation.NavigationService> クラスの次のメンバーのいずれかを使用して、プログラムによって履歴をナビゲートできます。

- <xref:System.Windows.Navigation.NavigationService.GoBack%2A>

- <xref:System.Windows.Navigation.NavigationService.GoForward%2A>

- <xref:System.Windows.Navigation.NavigationService.CanGoBack%2A>

- <xref:System.Windows.Navigation.NavigationService.CanGoForward%2A>

このトピックの「[ナビゲーション履歴によるコンテンツ状態の保持](#RetainingContentStateWithNavigationHistory)」で説明するように、プログラムによって履歴を操作することも可能です。

<a name="PageLifetime"></a>

### <a name="page-lifetime-and-the-journal"></a>ページの有効期間と履歴

グラフィックス、アニメーション、メディアなどのリッチ コンテンツを含む複数のページがある XBAP を考えてみます。 このようなページのメモリ使用量は、特にビデオやオーディオ メディアが使用されている場合、非常に大きくなることがあります。 履歴がナビゲート先のページを "記憶" することを考えると、このような XBAP はすぐに大量のメモリを消費する可能性があります。

このため、履歴の既定の動作では、<xref:System.Windows.Controls.Page> オブジェクトへの参照ではなく、<xref:System.Windows.Controls.Page> メタデータが各履歴エントリに格納されます。 履歴エントリにナビゲートすると、その <xref:System.Windows.Controls.Page> メタデータを使用して、指定された <xref:System.Windows.Controls.Page> の新しいインスタンスが作成されます。 その結果、ナビゲートされた各 <xref:System.Windows.Controls.Page> の有効期間は、次の図のようになります。

![ページの有効期間](./media/navigation-overview/navigated-page-lifetime.png "これは、ページがナビゲートされるときの有効期間を示します。")

既定の履歴動作を使用すると、メモリ消費量を節約できますが、特にコンテンツが多い場合は、ページごとのレンダリングのパフォーマンスが低下し、<xref:System.Windows.Controls.Page> の再インスタンス化に時間がかかることがあります。 <xref:System.Windows.Controls.Page> インスタンスを履歴に保持する必要がある場合、2 つの方法があります。 1 つ目の方法は、<xref:System.Windows.Navigation.NavigationService.Navigate%2A?displayProperty=nameWithType> メソッドを呼び出すことによって、<xref:System.Windows.Controls.Page> オブジェクトにプログラムでナビゲートできます。

2 つ目の方法は、<xref:System.Windows.Controls.Page.KeepAlive%2A> プロパティを `true` (既定値は `false`) に設定することによって、WPF で <xref:System.Windows.Controls.Page> のインスタンスを保持するように指定することができます。 次の例に示されているように、マークアップで宣言することによって、<xref:System.Windows.Controls.Page.KeepAlive%2A> を設定することができます。

[!code-xaml[NavigationOverviewSnippets#KeepAlivePageXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/KeepAlivePage.xaml#keepalivepagexaml)]

キープ アライブされる <xref:System.Windows.Controls.Page> の有効期間とキープ アライブされないページの有効期間は、わずかに異なります。 キープ アライブされる <xref:System.Windows.Controls.Page> に最初にナビゲートするときには、キープ アライブされない <xref:System.Windows.Controls.Page> と同様にインスタンス化されます。 ただし、<xref:System.Windows.Controls.Page> のインスタンスは履歴に保持されているため、履歴に保持されている限り、再びインスタンス化されることはありません。 その結果、<xref:System.Windows.Controls.Page> へのナビゲートが行われるたびに呼び出す必要がある初期化ロジックが <xref:System.Windows.Controls.Page> にある場合、それをコンストラクターから <xref:System.Windows.FrameworkElement.Loaded> イベントのハンドラーに移動する必要があります。 このようにしても、次の図に示されているように、<xref:System.Windows.Controls.Page> がナビゲート先およびナビゲート元になるたびに、それぞれ <xref:System.Windows.FrameworkElement.Loaded> イベントと <xref:System.Windows.FrameworkElement.Unloaded> イベントが発生します。

![Loaded イベントと Unloaded イベントが発生した場合](./media/navigation-overview/loaded-and-unloaded-events.png "ページがナビゲートされると、読み込みイベントとアンロード イベントが発生します。")

<xref:System.Windows.Controls.Page> がキープ ア ライブされないときは、次のいずれの操作も行わないでください。

- ページへの参照、またはその一部への参照を格納する。

- ページによって実装されていないイベントのイベント ハンドラーを登録する。

このいずれかの操作を行うと、<xref:System.Windows.Controls.Page> が履歴から削除された後も、強制的にメモリに保持される参照が作成されます。

一般に、<xref:System.Windows.Controls.Page> をキープ アライブしない <xref:System.Windows.Controls.Page> の既定の動作を優先する必要があります。 ただし、これには、次のセクションで説明されている状態も関係します。

<a name="RetainingContentStateWithNavigationHistory"></a>

### <a name="retaining-content-state-with-navigation-history"></a>ナビゲーション履歴によるコンテンツの状態の保持

<xref:System.Windows.Controls.Page> がキープ アライブされず、ユーザーからデータを収集するコントロールを持っている場合、ユーザーが <xref:System.Windows.Controls.Page> からナビゲートしたり、そこに戻ったりすると、データに何が起きるでしょうか。 ユーザー エクスペリエンスの観点から見ると、ユーザーは以前に入力したデータが表示されることを期待します。 残念ながら、ナビゲーションごとに <xref:System.Windows.Controls.Page> の新しいインスタンスが作成されるため、データを収集したコントロールが再インスタンス化されて、データは失われます。

幸いにも、履歴では <xref:System.Windows.Controls.Page> ナビゲーション間をまたいでデータ (コントロール データなど) を記憶するサポートが提供されています。 具体的には、各 <xref:System.Windows.Controls.Page> の履歴エントリは、関連付けられた <xref:System.Windows.Controls.Page> の状態の一時的なコンテナーとして機能します。 次の手順では、<xref:System.Windows.Controls.Page> からナビゲートするときに、このサポートがどのように使用されるかを示しています。

1. 現在の <xref:System.Windows.Controls.Page> のエントリが履歴に追加されます。

2. <xref:System.Windows.Controls.Page> の状態が、そのページの履歴エントリに格納され、戻るスタックに追加されます。

3. 新しい <xref:System.Windows.Controls.Page> にナビゲートします。

履歴を使用して、<xref:System.Windows.Controls.Page> に戻るときには、次の手順が実行されます。

1. <xref:System.Windows.Controls.Page> (戻るスタックの先頭の履歴エントリ) がインスタンス化されます。

2. <xref:System.Windows.Controls.Page> の履歴エントリに格納された状態で、<xref:System.Windows.Controls.Page> が更新されます。

3. <xref:System.Windows.Controls.Page> に戻ります。

<xref:System.Windows.Controls.Page> で次のようなコントロールが使用されるとき、WPF では、このサポートが自動的に使用されます。

- <xref:System.Windows.Controls.CheckBox>

- <xref:System.Windows.Controls.ComboBox>

- <xref:System.Windows.Controls.Expander>

- <xref:System.Windows.Controls.Frame>

- <xref:System.Windows.Controls.ListBox>

- <xref:System.Windows.Controls.ListBoxItem>

- <xref:System.Windows.Controls.MenuItem>

- <xref:System.Windows.Controls.ProgressBar>

- <xref:System.Windows.Controls.RadioButton>

- <xref:System.Windows.Controls.Slider>

- <xref:System.Windows.Controls.TabControl>

- <xref:System.Windows.Controls.TabItem>

- <xref:System.Windows.Controls.TextBox>

次の図の **[Favorite Color]** <xref:System.Windows.Controls.ListBox> で示されているように、<xref:System.Windows.Controls.Page> でこれらのコントロールが使用される場合、これらに入力されたデータは、<xref:System.Windows.Controls.Page> ナビゲーション間をまたいで記憶されます。

![状態を記憶するコントロールを含むページ](./media/navigation-overview/data-remembered-across-page-navigations.png "入力されたデータは、ページ ナビゲーション間で記憶されます。")

前述の一覧にないコントロールが <xref:System.Windows.Controls.Page> に含まれている場合や、状態情報がカスタム オブジェクトに格納される場合、<xref:System.Windows.Controls.Page> ナビゲーション間をまたいで履歴に状態を記憶するコードを記述する必要があります。

<xref:System.Windows.Controls.Page> ナビゲーション間をまたいで少量の状態情報を記憶する必要がある場合、<xref:System.Windows.FrameworkPropertyMetadata.Journal%2A?displayProperty=nameWithType> メタデータ フラグを使用して構成される依存関係プロパティ (<xref:System.Windows.DependencyProperty> を参照) を使用できます。

ナビゲーション間をまたいで状態を記憶する必要がある <xref:System.Windows.Controls.Page> が複数のデータで構成される場合、状態情報を 1 つのクラスにカプセル化して、<xref:System.Windows.Navigation.IProvideCustomContentState> インターフェイスを実装すると、コードが簡単になることがあります。

<xref:System.Windows.Controls.Page> 自体からはナビゲートせずに、1 つの <xref:System.Windows.Controls.Page> のさまざまな状態をナビゲートする必要がある場合には、<xref:System.Windows.Navigation.IProvideCustomContentState> と <xref:System.Windows.Navigation.NavigationService.AddBackEntry%2A?displayProperty=nameWithType> を使用できます。

<a name="Cookies"></a>

### <a name="cookies"></a>クッキー

WPF アプリケーションでデータを格納するもう 1 つの方法は、クッキーを使用することです。Cookie は、<xref:System.Windows.Application.SetCookie%2A> メソッドと <xref:System.Windows.Application.GetCookie%2A> メソッドを使用して、作成、更新、および削除されます。 WPF で作成できる Cookie は、他の種類の Web アプリケーションが使用する Cookie と同じです。クッキーは、アプリケーション セッション中またはアプリケーション セッションにまたがって、クライアント コンピューター上にアプリケーションによって格納される任意のデータです。 クッキー データは、通常、次の形式の名前と値のペアです。

<*名前*> `=` <*値*>

データが、Cookie を設定する位置の <xref:System.Uri> と共に <xref:System.Windows.Application.SetCookie%2A> に渡されると、メモリ内に Cookie が作成され、現在のアプリケーション セッションの期間中のみ使用可能です。 この種類の Cookie は、"*セッション Cookie*" と呼ばれます。

複数のアプリケーション セッションにまたがってクッキーを格納するには、次の形式を使用して、有効期限をクッキーに追加する必要があります。

<*名前*> `=` <*値*> `; expires=DAY, DD-MMM-YYYY HH:MM:SS GMT`

有効期限を持つ Cookie は、Cookie の有効期限が切れるまで、現在の Windows インストールのインターネット一時ファイル フォルダーに格納されます。 このような Cookie は、アプリケーション セッションをまたいで存続するため、"*永続的な Cookie*" と呼ばれます。

セッション Cookie と永続的な Cookie の両方を取得するには、<xref:System.Windows.Application.GetCookie%2A> メソッドを呼び出し、<xref:System.Windows.Application.SetCookie%2A> メソッドで Cookie が設定された位置の <xref:System.Uri> を渡します。

WPF で Cookie がどのようにサポートされるかを次に示します。

- WPF スタンドアロン アプリケーションと XBAP では、Cookie の作成と管理の両方を行うことができます。

- XBAP によって作成された Cookie には、ブラウザーからアクセスできます。

- 同じドメインの XBAP は、Cookie を作成して共有できます。

- 同じドメインの XBAP ページと HTML ページでは、Cookie を作成して共有できます。

- XBAP ページと Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページで Web 要求が行われると、Cookie がディスパッチされます。

- 最上位の XBAP と IFRAMES でホストされる XBAP のどちらでも、Cookie にアクセスできます。

- WPF での Cookie のサポートは、サポートされているすべてのブラウザーで同じです。

- Internet Explorer では、WPF は、Cookie に関する P3P ポリシー (特に開発元とサードパーティの XBAP に関して) に従います。

<a name="Structured_Navigation"></a>

### <a name="structured-navigation"></a>構造化ナビゲーション

<xref:System.Windows.Controls.Page> 間でデータを渡す必要がある場合、<xref:System.Windows.Controls.Page> のパラメーターなしではないコンストラクターにデータを引数として渡すことができます。 この方法を使用する場合は、<xref:System.Windows.Controls.Page> をキープ アライブ必要があることに注意してください。そうしなかった場合、次回、<xref:System.Windows.Controls.Page> にナビゲートすると、WPF ではパラメーターなしのコンストラクターを使用して <xref:System.Windows.Controls.Page> が再インスタンス化されます。

または、<xref:System.Windows.Controls.Page> で、渡す必要のあるデータが設定されるプロパティを実装することができます。 ただし、<xref:System.Windows.Controls.Page> でナビゲート元の <xref:System.Windows.Controls.Page> にデータを渡す必要があるときは、少し手間がかかります。 問題は、ナビゲーションでは、ナビゲート後に <xref:System.Windows.Controls.Page> に戻ることを保証するメカニズムがネイティブではサポートされていないことにあります。 基本的に、ナビゲーションは、"呼び出す/戻る" というセマンティクスをサポートしていません。 この問題を解決するため、WPF では、予測可能な構造化された方法で <xref:System.Windows.Controls.Page> に戻ることを可能にする <xref:System.Windows.Navigation.PageFunction%601> クラスが提供されています。 詳細については、「[構造化ナビゲーションの概要](structured-navigation-overview.md)」を参照してください。

<a name="The_NavigationWindow_Class"></a>

## <a name="the-navigationwindow-class"></a>NavigationWindow クラス

ここまでで、ナビゲート可能なコンテンツを含むアプリケーションをビルドするために使用する可能性が最も高いナビゲーション サービスの全容を説明しました。 これらのサービスについては、XBAP のコンテキストで説明しましたが、XBAP に限定されるわけではありません。 最新のオペレーティング システムと Windows アプリケーションでは、最近のユーザーがブラウザーの使用経験を持つことを考慮して、スタンドアロン アプリケーションにブラウザー スタイルのナビゲーションが組み込まれています。 一般的な例は、次のとおりです。

- **Word の類義語辞典**: 単語の選択をナビゲートします。

- **エクスプローラー**: ファイルとフォルダーをナビゲートします。

- **ウィザード**: 複雑なタスクを複数のページに分割し、ページ間をナビゲートできます。 たとえば、Windows の機能の追加と削除を行う Windows コンポーネント ウィザードなどがあります。

ブラウザー スタイルのナビゲーションをスタンドアロン アプリケーションに組み込むには、<xref:System.Windows.Navigation.NavigationWindow> クラスを使用します。 <xref:System.Windows.Navigation.NavigationWindow> は、<xref:System.Windows.Window> から派生し、XBAP で提供されるのと同様のナビゲーション サポートによってウィンドウを拡張します。 <xref:System.Windows.Navigation.NavigationWindow> は、スタンドアロン アプリケーションのメイン ウィンドウとして、またはダイアログ ボックスなどの 2 次ウィンドウとして使用できます。

<xref:System.Windows.Navigation.NavigationWindow> を実装するには、WPF の最上位クラス (<xref:System.Windows.Window>、<xref:System.Windows.Controls.Page> など) と同様に、マークアップとコードビハインドの組み合わせを使用します。 これを次の例に示します。

[!code-xaml[IntroToNavNavigationWindowSnippets#NavigationWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/MainWindow.xaml#navigationwindowmarkup)]

[!code-csharp[IntroToNavNavigationWindowSnippets#NavigationWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/MainWindow.xaml.cs#navigationwindowcodebehind)]
[!code-vb[IntroToNavNavigationWindowSnippets#NavigationWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/VisualBasic/MainWindow.xaml.vb#navigationwindowcodebehind)]

このコードでは、<xref:System.Windows.Navigation.NavigationWindow> が開かれたときに自動的に <xref:System.Windows.Controls.Page> (HomePage.xaml) にナビゲートする <xref:System.Windows.Navigation.NavigationWindow> を作成します。 <xref:System.Windows.Navigation.NavigationWindow> がアプリケーションのメイン ウィンドウの場合、`StartupUri` 属性を使用して起動できます。 これを次のマークアップに示します。

[!code-xaml[IntroToNavNavigationWindowSnippets#AppLaunchNavWindow](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/App.xaml#applaunchnavwindow)]

次の図では、スタンドアロン アプリケーションのメイン ウィンドウとしての <xref:System.Windows.Navigation.NavigationWindow> を示します。

![メイン ウィンドウ](./media/navigation-overview/navigation-window-as-main-window.png "メイン ウィンドウとしてのナビゲーション ウィンドウ")

この図では、前の例の <xref:System.Windows.Navigation.NavigationWindow> 実装コードでは設定されなかったにもかかわらず、<xref:System.Windows.Navigation.NavigationWindow> にタイトルが表示されています。 代わりに、タイトルは、次のコードに示されている <xref:System.Windows.Controls.Page.WindowTitle%2A> プロパティを使用して設定されます。

[!code-xaml[IntroToNavNavigationWindowSnippets#HomePageMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/HomePage.xaml#homepagemarkup1)]
[!code-xaml[IntroToNavNavigationWindowSnippets#HomePageMARKUP2](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/HomePage.xaml#homepagemarkup2)]

<xref:System.Windows.Controls.Page.WindowWidth%2A> プロパティと <xref:System.Windows.Controls.Page.WindowHeight%2A> プロパティの設定は、<xref:System.Windows.Navigation.NavigationWindow> にも影響します。

通常、動作や外観をカスタマイズする必要があるときには、独自の <xref:System.Windows.Navigation.NavigationWindow> を実装します。 どちらも行わない場合は、ショートカットを使用できます。 スタンドアロン アプリケーションで、<xref:System.Windows.Controls.Page> のパック URI を <xref:System.Windows.Application.StartupUri%2A> として指定した場合、<xref:System.Windows.Application> では、<xref:System.Windows.Controls.Page> をホストするための <xref:System.Windows.Navigation.NavigationWindow> が自動的に作成されます。 次のマークアップは、この方法を示しています。

[!code-xaml[IntroToNavNavigationWindowSnippets#AppLaunchPage](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/AnotherApp.xaml#applaunchpage)]

ダイアログ ボックスなど、アプリケーションの 2 次ウィンドウを <xref:System.Windows.Navigation.NavigationWindow> にする場合は、次の例のコードを使用して開くことができます。

[!code-csharp[IntroToNavNavigationWindowSnippets#CreateNWDialogBox](~/samples/snippets/csharp/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/CSharp/DialogOwnerWindow.xaml.cs#createnwdialogbox)]
[!code-vb[IntroToNavNavigationWindowSnippets#CreateNWDialogBox](~/samples/snippets/visualbasic/VS_Snippets_Wpf/IntroToNavNavigationWindowSnippets/VisualBasic/DialogOwnerWindow.xaml.vb#createnwdialogbox)]

次の図に、結果を示します。

![ダイアログ ボックス](./media/navigation-overview/navigation-window-as-dialog-box.png "ダイアログ ボックスとしてのナビゲーション ウィンドウ")

この図では、<xref:System.Windows.Navigation.NavigationWindow> に Internet Explorer スタイルの **[戻る]** ボタンと **[進む]** ボタンが表示され、ユーザーは履歴をナビゲートできます。 これらのボタンは、次の図に示されているように、同じユーザー エクスペリエンスを提供します。

![NavigationWindow 内の [戻る] ボタンと [次に進む] ボタン](./media/navigation-overview/back-and-forward-buttons-in-navigation-window.png "ナビゲーション ウィンドウの [戻る] ボタンと [進む] ボタン")

ページで独自の履歴ナビゲーション サポートと UI を提供する場合は、<xref:System.Windows.Navigation.NavigationWindow.ShowsNavigationUI%2A> プロパティの値を `false` に設定することにより、<xref:System.Windows.Navigation.NavigationWindow> によって表示される **[戻る]** ボタンと **[進む]** ボタンを非表示にできます。

または、WPF のカスタマイズ サポートを使用して、<xref:System.Windows.Navigation.NavigationWindow> 自体の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を置き換えることもできます。

<a name="Frame_in_Standalone_Applications"></a>

## <a name="the-frame-class"></a>Frame クラス

ブラウザーと <xref:System.Windows.Navigation.NavigationWindow> は両方とも、ナビゲート可能なコンテンツをホストするウィンドウです。 場合によっては、アプリケーションには、ウィンドウ全体でホストする必要のないコンテンツがあることもあります。 このようなコンテンツは、代わりに、他のコンテンツ内でホストされます。 <xref:System.Windows.Controls.Frame> クラスを使用すると、ナビゲート可能なコンテンツを他のコンテンツに挿入することができます。 <xref:System.Windows.Controls.Frame> では、<xref:System.Windows.Navigation.NavigationWindow> および XBAP と同じサポートが提供されます。

次の例では、`Frame` 要素を使用して <xref:System.Windows.Controls.Frame> を <xref:System.Windows.Controls.Page> に宣言によって追加する方法を示します。

[!code-xaml[NavigationOverviewSnippets#FrameHostPageXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPage.xaml#framehostpagexaml1)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPage.xaml#framehostpagexaml2)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPage.xaml#framehostpagexaml3)]

このマークアップでは、`Frame` 要素の `Source` 属性に、<xref:System.Windows.Controls.Frame> が最初にナビゲートする必要がある <xref:System.Windows.Controls.Page> のパック URI を設定します。 次の図では、複数のページをナビゲートした <xref:System.Windows.Controls.Frame> のある <xref:System.Windows.Controls.Page> が含まれる XBAP を示します。

![複数のページ間を移動したフレーム](./media/navigation-overview/frame-navigation-between-multiple-pages.png "これは、複数のページ間のフレーム ナビゲーションを示します。")

<xref:System.Windows.Controls.Page> のコンテンツの内部にある <xref:System.Windows.Controls.Frame> のみを使用する必要はありません。 <xref:System.Windows.Window> のコンテンツの内部で <xref:System.Windows.Controls.Frame> をホストするのも一般的です。

既定の <xref:System.Windows.Controls.Frame> では、別の履歴がない場合に限り、独自の履歴が使用されます。 <xref:System.Windows.Controls.Frame> が <xref:System.Windows.Navigation.NavigationWindow> または XBAP の内部でホストされるコンテンツの一部である場合、<xref:System.Windows.Controls.Frame> では、<xref:System.Windows.Navigation.NavigationWindow> または XBAP に属する履歴が使用されます。 ただし、場合によっては、<xref:System.Windows.Controls.Frame> では独自の履歴を使用しなければならないことがあります。 その理由の 1 つは、<xref:System.Windows.Controls.Frame> によってホストされるページ内で履歴ナビゲーションを可能にすることです。 これを次の図に示します。

![フレームとページのダイアグラム](./media/navigation-overview/journal-navigation-within-pages-hosted-by-a-frame.png "これは、フレームによってホストされるページ内の履歴ナビゲーションを示します。")

この場合、<xref:System.Windows.Controls.Frame> の <xref:System.Windows.Controls.Frame.JournalOwnership%2A> プロパティを <xref:System.Windows.Navigation.JournalOwnership.OwnsJournal> に設定することによって、<xref:System.Windows.Controls.Frame> が独自の履歴を使用するように構成できます。 これを次のマークアップに示します。

[!code-xaml[NavigationOverviewSnippets#FrameHostPageOwnJournalXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnJournal.xaml#framehostpageownjournalxaml1)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageOwnJournalXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnJournal.xaml#framehostpageownjournalxaml2)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageOwnJournalXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnJournal.xaml#framehostpageownjournalxaml3)]

次の図は、独自の履歴を使用する <xref:System.Windows.Controls.Frame> 内でのナビゲートの結果を示しています。

![独自の履歴を使用するフレーム](./media/navigation-overview/frame-uses-its-own-journal.png "これは、独自の履歴を使用するフレーム内でナビゲートした場合の効果を示します。")

履歴エントリは、Internet Explorer ではなく、<xref:System.Windows.Controls.Frame> 内のナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] によって表示されることに注意してください。

> [!NOTE]
> <xref:System.Windows.Controls.Frame> が <xref:System.Windows.Window> でホストされるコンテンツの一部である場合、<xref:System.Windows.Controls.Frame> では独自の履歴を使用するため、独自のナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] が表示されます。

<xref:System.Windows.Controls.Frame> でナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を表示せずに、独自の履歴を表示することがユーザー エクスペリエンスで必要な場合、<xref:System.Windows.Controls.Frame.NavigationUIVisibility%2A> を <xref:System.Windows.Visibility.Hidden> に設定することによって、ナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を非表示にできます。 これを次のマークアップに示します。

[!code-xaml[NavigationOverviewSnippets#FrameHostPageHidesUIXAML1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnHiddenJournal.xaml#framehostpagehidesuixaml1)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageHidesUIXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnHiddenJournal.xaml#framehostpagehidesuixaml2)]
[!code-xaml[NavigationOverviewSnippets#FrameHostPageHidesUIXAML3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHostPageOwnHiddenJournal.xaml#framehostpagehidesuixaml3)]

<a name="Navigation_Hosts"></a>

## <a name="navigation-hosts"></a>ナビゲーション ホスト

<xref:System.Windows.Controls.Frame> と <xref:System.Windows.Navigation.NavigationWindow> は、ナビゲーション ホストと呼ばれるクラスです。 "*ナビゲーション ホスト*" は、コンテンツにナビゲートして表示できるクラスです。 これを実現するため、各ナビゲーション ホストでは、独自の <xref:System.Windows.Navigation.NavigationService> と履歴が使用されます。 ナビゲーション ホストの基本的な構造を次の図に示します。

![ナビゲーターのダイアグラム](./media/navigation-overview/navigation-host-construction.png "ナビゲーション ホストの基本的な構築")

これにより、<xref:System.Windows.Navigation.NavigationWindow> と <xref:System.Windows.Controls.Frame> では、基本的に、XBAP がブラウザーでホストされるときに提供するのと同じナビゲーション サポートを提供できます。

<xref:System.Windows.Navigation.NavigationService> と履歴を使用するだけでなく、ナビゲーション ホストでは、<xref:System.Windows.Navigation.NavigationService> で実装されるのと同じメンバーが実装されます。 これを次の図に示します。

![フレームおよび NavigationWindow 内の履歴](./media/navigation-overview/navigation-window-and-frame.png "ナビゲーション ウィンドウとフレーム")

これにより、これらのメンバーに対して直接、ナビゲーション サポートをプログラミングできます。 <xref:System.Windows.Window> でホストされる <xref:System.Windows.Controls.Frame> のカスタム ナビゲーション [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を提供する必要がある場合は、この方法を検討してみてください。 さらに、どちらのタイプも、この他に、`BackStack` (<xref:System.Windows.Navigation.NavigationWindow.BackStack%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Frame.BackStack%2A?displayProperty=nameWithType>) や `ForwardStack` (<xref:System.Windows.Navigation.NavigationWindow.ForwardStack%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Frame.ForwardStack%2A?displayProperty=nameWithType>) など、ナビゲーション関連のメンバーを実装し、これらによって、それぞれ戻るスタックと進むスタックの履歴エントリを列挙できます。

前に述べたように、アプリケーション内に複数の履歴が存在することがあります。 次の図は、この例を示しています。

![1 つのアプリケーション内の複数の履歴](./media/navigation-overview/multiple-journals-in-one-application.png "これは、アプリケーション内の複数の履歴の例です。")

<a name="Navigating_to_Content_Other_than_Pages"></a>

## <a name="navigating-to-content-other-than-xaml-pages"></a>XAML ページ以外のコンテンツへのナビゲート

このトピック全体を通じて、<xref:System.Windows.Controls.Page> とパック XBAP を使用して、WPF のさまざまなナビゲーション機能を説明してきました。 ただし、アプリケーションにコンパイルされる <xref:System.Windows.Controls.Page> がナビゲート可能な唯一の種類のコンテンツではなく、パック XBAP がコンテンツを識別する唯一の方法ではありません。

このセクションで示すように、Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル、HTML ファイル、およびオブジェクトにもナビゲートできます。

<a name="Navigating_to_Loose_XAML_Files"></a>

### <a name="navigating-to-loose-xaml-files"></a>Loose XAML ファイルへのナビゲート

Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルは、次の特性を持つファイルです。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のみを含む (つまり、コードがない)。

- 適切な名前空間宣言がある。

- .xaml ファイル名拡張子を持つ。

たとえば、Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル Person.xaml ファイルとして格納されている次のようなコンテンツを考えてみます。

[!code-xaml[NavigationOverviewSnippets#LooseXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/Person.xaml#loosexaml)]

ファイルをダブルクリックすると、ブラウザーが開き、コンテンツにナビゲートして、コンテンツを表示します。 これを次の図に示します。

![Person.XAML ファイルの内容の表示](./media/navigation-overview/contents-of-person-xaml-file.png "Person.XAML ファイルの内容を示します。")

Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルは、次の場所から表示できます。

- ローカル コンピューター、イントラネット、またはインターネット上の Web サイト。

- 汎用名前付け規則 (UNC) ファイル共有。

- ローカル ディスク。

Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルは、ブラウザーのお気に入りに追加したり、ブラウザーのホーム ページにしたりできます。

> [!NOTE]
> Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページの公開と起動の詳細については、「[WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)」を参照してください。

Loose [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] に関する 1 つの制限は、部分信頼で実行しても安全なコンテンツしかホストできないことです。 たとえば、`Window` は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイルのルート要素にはできません。 詳細については、「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」を参照してください。

<a name="Navigating_to_HTML_Files_Using_Frame"></a>

### <a name="navigating-to-html-files-by-using-frame"></a>フレームを使用した HTML ファイルへのナビゲート

ご想像のとおり、HTML にもナビゲートできます。 http スキームを使用する URI を入力するだけです。 たとえば、次の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、HTML ページにナビゲートする <xref:System.Windows.Controls.Frame> が示されています。

[!code-xaml[NavigationOverviewSnippets#FrameHtmlNavMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationOverviewSnippets/CSharp/FrameHTMLNavPage.xaml#framehtmlnavmarkup)]

HTML にナビゲートするには、特殊なアクセス許可が必要です。 たとえば、インターネット ゾーンの部分信頼セキュリティ サンドボックスで実行している XBAP からはナビゲートできません。 詳細については、「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」を参照してください。

<a name="Navigating_to_HTML_Files_Using_WebBrowser"></a>

### <a name="navigating-to-html-files-by-using-the-webbrowser-control"></a>WebBrowser コントロールを使用した HTML ファイルへのナビゲート

<xref:System.Windows.Controls.WebBrowser> コントロールでは、HTML ドキュメントのホスティング、ナビゲーション、およびスクリプトやマネージド コードの相互運用性がサポートされます。 <xref:System.Windows.Controls.WebBrowser> コントロールの詳細については、「<xref:System.Windows.Controls.WebBrowser>」を参照してください。

<xref:System.Windows.Controls.Frame> と同様に、<xref:System.Windows.Controls.WebBrowser> を使用して HTML にナビゲートするには、特殊なアクセス許可が必要です。 たとえば、部分信頼アプリケーションからは、起点サイトにある HTML にのみナビゲートできます。 詳細については、「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」を参照してください。

<a name="Navigating_to_Objects"></a>

### <a name="navigating-to-custom-objects"></a>カスタム オブジェクトへのナビゲート

カスタム オブジェクトとして格納されているデータがある場合、そのデータを表示する方法の 1 つは、それらのオブジェクトにバインドされたコンテンツを使用して <xref:System.Windows.Controls.Page> を作成することです (「[データ バインドの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照)。 オブジェクトを表示するためだけにページ全体を作成するオーバーヘッドが必要ない場合には、代わりに、オブジェクトに直接ナビゲートすることもできます。

次のコードで実装される `Person` クラスを考えてみます。

[!code-csharp[NavigateToObjectSnippets#PersonClassCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/Person.cs#personclasscode)]
[!code-vb[NavigateToObjectSnippets#PersonClassCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigateToObjectSnippets/VisualBasic/Person.vb#personclasscode)]

それにナビゲートするには、次のコードに示されているように、<xref:System.Windows.Navigation.NavigationWindow.Navigate%2A?displayProperty=nameWithType> メソッドを呼び出します。

[!code-xaml[NavigateToObjectSnippets#PageThatNavsToObject1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/HomePage.xaml#pagethatnavstoobject1)]
[!code-xaml[NavigateToObjectSnippets#PageThatNavsToObject2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/HomePage.xaml#pagethatnavstoobject2)]
[!code-xaml[NavigateToObjectSnippets#PageThatNavsToObject3](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/HomePage.xaml#pagethatnavstoobject3)]

[!code-csharp[NavigateToObjectSnippets#PageThatNavsToObjectCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/HomePage.xaml.cs#pagethatnavstoobjectcodebehind)]
[!code-vb[NavigateToObjectSnippets#PageThatNavsToObjectCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/NavigateToObjectSnippets/VisualBasic/HomePage.xaml.vb#pagethatnavstoobjectcodebehind)]

次の図に、結果を示します。

![クラスに移動するページ](./media/navigation-overview/page-navigates-to-an-object.png "これは、オブジェクトにナビゲートするページの例です。")

この図には、役立つものが何も表示されていません。 実際、表示される値は、**Person** オブジェクトの `ToString` メソッドの戻り値です。既定では、これは WPF でオブジェクトの表示に使用できる唯一の値です。 `ToString` メソッドをオーバーライドすると、より意味のある情報を返すことができますが、それでも文字列値でしかありません。 WPF の表示機能を利用する 1 つの方法は、データ テンプレートを使用することです。 WPF で特定の種類のオブジェクトと関連付けることができる、データ テンプレートを実装できます。 次のコードでは、`Person` オブジェクトのデータ テンプレートを示します。

[!code-xaml[NavigateToObjectSnippets#DataTemplateMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigateToObjectSnippets/CSharp/App.xaml#datatemplatemarkup)]

ここでは、データ テンプレートは、`DataType` 属性で `x:Type` マークアップ拡張機能を使用することによって、`Person` 型と関連付けられます。 次に、データ テンプレートでは、`TextBlock` 要素 (<xref:System.Windows.Controls.TextBlock> を参照) が `Person` クラスのプロパティにバインドされます。 次の図は、`Person` オブジェクトの更新された外観を示しています。

![データ テンプレートを持つクラスへの移動](./media/navigation-overview/navigating-to-a-class.png "データ テンプレートを持つクラスへの移動")

この方法の利点は、データ テンプレートを再利用して、アプリケーションの任意の場所で オブジェクトを一貫して表示できることによって得られる一貫性です。

データ テンプレートの詳細については「[データ テンプレートの概要](../data/data-templating-overview.md)」を参照してください。

<a name="Security"></a>

## <a name="security"></a>セキュリティ

WPF ナビゲーション サポートによって、XBAP をインターネットを介してナビゲートでき、アプリケーションでサード パーティの コンテンツをホストできます。 アプリケーションとユーザーの両方を有害な動作から保護するために、WPF では、さまざまなセキュリティ機能が提供されています。これらの機能の詳細は、「[セキュリティ](../security-wpf.md)」と「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」で説明されています。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Application.SetCookie%2A>
- <xref:System.Windows.Application.GetCookie%2A>
- [アプリケーション管理の概要](application-management-overview.md)
- [WPF におけるパッケージの URI](pack-uris-in-wpf.md)
- [構造化ナビゲーションの概要](structured-navigation-overview.md)
- [ナビゲーション トポロジの概要](navigation-topologies-overview.md)
- [方法トピック](navigation-how-to-topics.md)
- [WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)
