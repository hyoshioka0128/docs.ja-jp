---
title: ウィンドウの概要
description: Windows Presentation Foundation (WPF) におけるスタンドアロン アプリケーションでのウィンドウの作成と管理の基本について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XAML [WPF], displaying content via
- XAML pages [WPF], displaying
- content [WPF], displaying via XAML
- window objects [WPF]
- hosting [WPF], applications
- managing windows [WPF]
- dialog boxes [WPF]
- Page object [WPF]
- NavigationWindow objects [WPF]
- applications [WPF], hosting
- content [WPF], displaying
- events [WPF]
- content [WPF], displaying via procedural code
- modal windows [WPF]
- procedural code [WPF], displaying content via
- displaying content via procedural code [WPF]
- window management [WPF]
- displaying content [WPF]
- window events [WPF]
- windows [WPF]
- modal dialog boxes [WPF]
- displaying XAML pages [WPF]
ms.assetid: 737d04ec-8861-46c3-8d44-fa11d3528d23
ms.openlocfilehash: e1ad3c118fbaea8f1e23d012721f0cf3c2c50015
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622888"
---
# <a name="wpf-windows-overview"></a>WPF ウィンドウの概要
ユーザーは、ウィンドウを通じて Windows Presentation Foundation (WPF) スタンドアロン アプリケーションと対話します。 ウィンドウの主な目的は、データを視覚化してユーザーがデータと対話できるコンテンツをホストすることです。 スタンドアロンの WPF アプリケーションには、<xref:System.Windows.Window> クラスを使用した独自のウィンドウがあります。 このトピックでは、<xref:System.Windows.Window> について説明してから、スタンドアロン アプリケーションにおけるウィンドウの作成と管理の基本について説明します。  
  
> [!NOTE]
> XAML ブラウザー アプリケーション (XBAP) や Loose [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] のページなど、ブラウザーによってホストされる WPF アプリケーションには、独自のウィンドウはありません。 その代わり、Windows Internet Explorer で提供されるウィンドウでホストされます。 「[WPF XAML ブラウザー アプリケーションの概要](wpf-xaml-browser-applications-overview.md)」を参照してください。  

<a name="TheWindowClass"></a>
## <a name="the-window-class"></a>ウィンドウ クラス  
 次の図は、ウィンドウの構成パーツを示しています。  
  
 ![ウィンドウ要素を示すスクリーンショット。](./media/wpf-windows-overview/window-constituent-elements.png)  
  
 ウィンドウは、非クライアント領域とクライアント領域の 2 つに分かれます。  
  
 ウィンドウの "*非クライアント領域*" は、WPF によって実装され、多くのウィンドウに共通のウィンドウのパーツが含まれます。これらのパーツには次のものがあります。  
  
- 境界線。  
  
- タイトル バー。  
  
- アイコン。  
  
- 最小化ボタン、最大化ボタン、および元に戻すボタン。  
  
- 閉じるボタン。  
  
- ウィンドウを最小化、最大化、元のサイズに戻す、移動、サイズ変更、および閉じるためのメニュー項目を含むシステム メニュー。  
  
 ウィンドウの "*クライアント領域*" は、ウィンドウの非クライアント領域の内側の領域であり、開発者がメニュー バー、ツール バー、コントロールなどのアプリケーション固有のコンテンツを追加するために使用します。  
  
 WPF では、ウィンドウは <xref:System.Windows.Window> クラスでカプセル化され、これを使用して以下の操作を実行できます。  
  
- ウィンドウを表示する。  
  
- ウィンドウのサイズ、位置、および外観を構成する。  
  
- アプリケーション固有のコンテンツをホストする。  
  
- ウィンドウの有効期間を管理する。  
  
<a name="DefiningAWindow"></a>
## <a name="implementing-a-window"></a>ウィンドウの実装  
 一般的なウィンドウの実装は、外観と動作で構成されます。"*外観*" では、ユーザーに対するウィンドウの表示方法を定義します。"*動作*" では、ユーザーがウィンドウと対話するときのウィンドウの動作を定義します。 WPF では、コードまたは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップを使用して、ウィンドウの外観と動作を実装できます。  
  
 ただし、通常は、次の例に示すように、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップを使用してウィンドウの外観を実装して、分離コードを使用してウィンドウの動作を実装します。  
  
 [!code-xaml[WindowsOverviewSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップ ファイルと分離コード ファイルを連携させるには、次のことが必要です。  
  
- マークアップの `Window` 要素に `x:Class` 属性を含める必要があります。 アプリケーションのビルド時にマークアップ ファイルに `x:Class` が含まれていると、Microsoft Build Engine (MSBuild) により、`x:Class` 属性で指定された名前を持つ、<xref:System.Windows.Window> から派生した `partial` クラスが作成されます。 そのためには、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] スキーマ (`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`) に XML 名前空間宣言を追加する必要があります。 生成された `partial` クラスでは `InitializeComponent` メソッドが実装されます。このメソッドを呼び出すとイベントが登録され、マークアップで実装されるプロパティが設定されます。  
  
- 分離コードでは、クラスは、マークアップ内の `x:Class` 属性で指定されている名前を持つ `partial` クラスでなければなりません。また、<xref:System.Windows.Window> から派生する必要があります。 これによって、分離コード ファイルと、アプリケーションのビルド時にマークアップ ファイル用に生成される `partial` クラスとが関連付けられます (「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照)。  
  
- 分離コードでは、<xref:System.Windows.Window> クラスによって実装されるコンストラクターで `InitializeComponent` メソッドが呼び出される必要があります。 `InitializeComponent` は、マークアップ ファイル用に生成された `partial` クラスによって実装されるもので、イベントの登録と、マークアップで定義されたプロパティの設定を実行します。  
  
> [!NOTE]
> Visual Studio を使用してプロジェクトに新しい <xref:System.Windows.Window> を追加すると、ここで説明したように、マークアップと分離コードの両方を使用して <xref:System.Windows.Window> が実装され、マークアップ ファイルと分離コード ファイル間の関連付けの作成に必要な構成が組み込まれます。  
  
 この構成が組み込まれると、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップ内でウィンドウの外観を定義し、分離コード内でウィンドウの動作を実装することに集中できます。 ボタンを含むウィンドウを [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップで実装し、そのボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントのイベント ハンドラーを分離コードで実装する例を、次に示します。  
  
 [!code-xaml[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml#markupandcodebehindwindowmarkup)]  
  
 [!code-csharp[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/CSharp/MarkupAndCodeBehindWindow.xaml.cs#markupandcodebehindwindowcodebehind)]
 [!code-vb[WindowsOverviewWindowWithButtonSnippets#MarkupAndCodeBehindWindowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewWindowWithButtonSnippets/VisualBasic/MarkupAndCodeBehindWindow.xaml.vb#markupandcodebehindwindowcodebehind)]  
  
<a name="ConfiguringWindowForMSBuild"></a>
## <a name="configuring-a-window-definition-for-msbuild"></a>MSBuild 用のウィンドウ定義の構成  
 ウィンドウを実装する方法によって、MSBuild を構成する方法が決定されます。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップと分離コードの両方を使用して定義したウィンドウの場合:  
  
- XAML マークアップ ファイルは、MSBuild `Page` 項目として構成する必要があります。  
  
- 分離コード ファイルは、MSBuild `Compile` 項目として構成されます。  
  
 これを次の MSBuild プロジェクト ファイルに示します。  
  
```xml  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003" ... >  
    ...  
    <Page Include="MarkupAndCodeBehindWindow.xaml" />  
    <Compile Include=" MarkupAndCodeBehindWindow.xaml.cs" />  
    ...  
</Project>  
```  
  
 WPF アプリケーションのビルドの詳細については、「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照してください。  
  
<a name="WindowLifetime"></a>
## <a name="window-lifetime"></a>ウィンドウの有効期間  
 クラスと同様に、ウィンドウにも有効期間があります。有効期間は、ウィンドウが開いて最初にインスタンス化されたときに開始し、アクティブ化と非アクティブ化を経て、最後に閉じられるまで継続します。  

<a name="Opening_a_Window"></a>
### <a name="opening-a-window"></a>ウィンドウを開く  
 ウィンドウを開くには、次の例に示すように最初にインスタンスを作成します。  
  
 [!code-xaml[WindowsOverviewStartupEventSnippets#AppMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml#appmarkup)]  
  
 [!code-csharp[WindowsOverviewStartupEventSnippets#AppCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewStartupEventSnippets/CSharp/App.xaml.cs#appcodebehind)]  
  
 この例では、<xref:System.Windows.Application.Startup> イベントが発生してアプリケーションが開始するときに `MarkupAndCodeBehindWindow` がインスタンス化されます。  
  
 ウィンドウがインスタンス化されると、<xref:System.Windows.Application> オブジェクトによって管理されるウィンドウのリストにそのウィンドウへの参照が自動的に追加されます (「<xref:System.Windows.Application.Windows%2A?displayProperty=nameWithType>」を参照)。 さらに、インスタンス化される最初のウィンドウは、既定で <xref:System.Windows.Application> によってメイン アプリケーション ウィンドウとして設定されます (「<xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType>」を参照)。  
  
 最後に <xref:System.Windows.Window.Show%2A> メソッドを呼び出すことによってウィンドウが開き、次の図に示すような結果になります。  
  
 ![Window.Show の呼び出しによって開いたウィンドウ](./media/wpf-windows-overview//window-opened-show-method.png)  
  
 <xref:System.Windows.Window.Show%2A> を呼び出すことによって開いたウィンドウは、モードレス ウィンドウです。これは、ユーザーが同じアプリケーションで他のウィンドウをアクティブ化できるモードでアプリケーションが動作することを意味します。  
  
> [!NOTE]
> <xref:System.Windows.Window.ShowDialog%2A> は、ダイアログ ボックスなどのウィンドウをモーダルで開くために呼び出されます。 詳細については、「[ダイアログ ボックスの概要](dialog-boxes-overview.md)」を参照してください。  
  
 <xref:System.Windows.Window.Show%2A> を呼び出すと、ウィンドウでは表示される前に初期化処理が実行され、ユーザーの入力を受け取ることのできるインフラストラクチャが確立されます。 ウィンドウが初期化されると、<xref:System.Windows.Window.SourceInitialized> イベントが発生し、ウィンドウが表示されます。  
  
 簡単な方法として、<xref:System.Windows.Application.StartupUri%2A> を設定し、アプリケーションの開始時に自動的に開く最初のウィンドウを指定できます。  
  
 [!code-xaml[WindowsOverviewSnippets#ApplicationStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/App.xaml#applicationstartupurimarkup)]  
  
 アプリケーションが開始したら、<xref:System.Windows.Application.StartupUri%2A> の値で指定されたウィンドウがモードレスで開きます。内部的には、ウィンドウはその <xref:System.Windows.Window.Show%2A> メソッドを呼び出すことによって開かれます。  
  
<a name="Ownership"></a>
#### <a name="window-ownership"></a>ウィンドウの所有権  
 <xref:System.Windows.Window.Show%2A> メソッドを使用して開いたウィンドウと、そのウィンドウを作成したウィンドウには、暗黙的な関係はありません。ユーザーは、どちらのウィンドウとも、もう一方のウィンドウに関係なく対話できます。つまり、どちらのウィンドウでも次の作業ができます。  
  
- もう一方の上に表示する (いずれかのウィンドウの <xref:System.Windows.Window.Topmost%2A> プロパティが `true` に設定されている場合を除く)。  
  
- もう一方のウィンドウに影響を与えずに、最小化/最大化し、元のサイズに戻す。  
  
 一部のウィンドウには、そのウィンドウを開いたウィンドウとの関係が必要です。 たとえば、統合開発環境 (IDE) アプリケーションでは、プロパティ ウィンドウやツール ウィンドウのように、一般的に作成元のウィンドウの上に表示されるウィンドウが開く場合があります。 また、そのようなウィンドウは、必ず作成元のウィンドウと一緒に閉じ、最小化/最大化し、元のサイズに戻す必要があります。 このような関係を確立するには、あるウィンドウが別のウィンドウを "*所有*" するようにします。そのためには、"*所有されているウィンドウ*" の <xref:System.Windows.Window.Owner%2A> プロパティに、"*オーナー ウィンドウ*" への参照を設定します。 これを次の例に示します。  
  
 [!code-csharp[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/CSharp/MainWindow.xaml.cs#setwindowownercode)]
 [!code-vb[WindowOwnerOwnedWindowsSnippets#SetWindowOwnerCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowOwnerOwnedWindowsSnippets/visualbasic/mainwindow.xaml.vb#setwindowownercode)]  
  
 所有権が確立されると、次のようになります。  
  
- 所有されているウィンドウでは、<xref:System.Windows.Window.Owner%2A> プロパティの値を検査することによってオーナー ウィンドウを参照できます。  
  
- オーナー ウィンドウでは、<xref:System.Windows.Window.OwnedWindows%2A> プロパティの値を検査することによって、所有するすべてのウィンドウを検出できます。  
  
<a name="Preventing"></a>
#### <a name="preventing-window-activation"></a>ウィンドウのアクティブ化の防止  
 表示されてもアクティブにしないことが適切なウィンドウもあります。インターネット メッセンジャーのようなアプリケーションの対話ウィンドウや、電子メール アプリケーションの通知ウィンドウなどです。  
  
 表示されるときにアクティブにしないウィンドウがアプリケーションにある場合は、<xref:System.Windows.Window.Show%2A> メソッドの初回呼び出し前に、<xref:System.Windows.Window.ShowActivated%2A> プロパティを `false` に設定します。 結果は次のようになります。  
  
- ウィンドウはアクティブになりません。  
  
- ウィンドウの <xref:System.Windows.Window.Activated> イベントは発生しません。  
  
- 現在アクティブなウィンドウは、アクティブのままです。  
  
 ただし、ユーザーがクライアント領域または非クライアント領域をクリックすると、ウィンドウは直ちにアクティブになります。 この場合、次のようになります。  
  
- ウィンドウはアクティブになります。  
  
- ウィンドウの <xref:System.Windows.Window.Activated> イベントが発生します。  
  
- 直前にアクティブだったウィンドウは非アクティブになります。  
  
- その後、ウィンドウの <xref:System.Windows.Window.Deactivated> イベントと <xref:System.Windows.Window.Activated> イベントが、ユーザーの操作への応答として想定どおりに発生します。  
  
<a name="Window_Activation"></a>
### <a name="window-activation"></a>ウィンドウのアクティブ化  
 ウィンドウを最初に開いたときは、そのウィンドウがアクティブ ウィンドウになります (<xref:System.Windows.Window.ShowActivated%2A> が `false` に設定されている場合を除く)。 "*アクティブ ウィンドウ*" は、キー ストロークやマウス クリックなどのユーザー入力を現在キャプチャしているウィンドウです。 ウィンドウがアクティブになると、<xref:System.Windows.Window.Activated> イベントが発生します。  
  
> [!NOTE]
> ウィンドウが最初に開かれるとき、<xref:System.Windows.FrameworkElement.Loaded> イベントと <xref:System.Windows.Window.ContentRendered> イベントは、<xref:System.Windows.Window.Activated> イベントが発生した後にのみ発生します。 そのため、事実上、ウィンドウは <xref:System.Windows.Window.ContentRendered> が発生した場合にのみ開いたと見なすことができます。  
  
 ウィンドウがアクティブになった後で、ユーザーは同じアプリケーションの別のウィンドウをアクティブ化したり、別のアプリケーションをアクティブ化したりできます。 このとき、現在アクティブなウィンドウが非アクティブ化され、<xref:System.Windows.Window.Deactivated> イベントが発生します。 同様に、ユーザーが現在非アクティブなウィンドウを選択すると、ウィンドウは再びアクティブになり、<xref:System.Windows.Window.Activated> が発生します。  
  
 一般に、<xref:System.Windows.Window.Activated> と <xref:System.Windows.Window.Deactivated> を処理するのは、ウィンドウがアクティブなときにのみ実行できる機能を有効または無効にするためです。 たとえば、ゲームやビデオ プレーヤーなど、ユーザーの一定の入力や介入が必要な対話型コンテンツが表示されるウィンドウがあります。 この動作を実装するために <xref:System.Windows.Window.Activated> と <xref:System.Windows.Window.Deactivated> を処理する方法を、次の簡単なビデオ プレーヤーの例で示します。  
  
 [!code-xaml[WindowsOverviewSnippets#ActivationDeactivationMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml#activationdeactivationmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/CustomMediaPlayerWindow.xaml.cs#activationdeactivationcodebehind)]
 [!code-vb[WindowsOverviewSnippets#ActivationDeactivationCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/CustomMediaPlayerWindow.xaml.vb#activationdeactivationcodebehind)]  
  
 ウィンドウが非アクティブでも、バックグラウンドでコードを実行できる種類のアプリケーションもあります。 たとえば、メール クライアントは、ユーザーが他のアプリケーションを使用している間もメール サーバーへのポーリングを続けています。 このようなアプリケーションは、メイン ウィンドウが非アクティブのときにも、別の動作や追加の動作を頻繁に実行します。 メール プログラムでは、新しいメール アイテムを受信トレイに追加し、通知アイコンをシステム トレイに追加することがあります。 通知アイコンは、メール ウィンドウがアクティブでないときにのみ表示する必要があります。メール ウィンドウがアクティブかどうかは、<xref:System.Windows.Window.IsActive%2A> プロパティを検査することで確認できます。  
  
 バックグラウンド タスクの完了時に、ユーザーに緊急に通知する必要がある場合は、<xref:System.Windows.Window.Activate%2A> メソッドを呼び出します。 <xref:System.Windows.Window.Activate%2A> を呼び出したときに、ユーザーが別のアクティブなアプリケーションと対話している場合は、ウィンドウのタスク バー ボタンが点滅します。 ユーザーが現在のアプリケーションと対話している場合は、<xref:System.Windows.Window.Activate%2A> を呼び出すと、ウィンドウが前面に表示されます。  
  
> [!NOTE]
> <xref:System.Windows.Application.Activated?displayProperty=nameWithType> イベントと <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> イベントを使用して、アプリケーションスコープのアクティベーションを処理できます。  
  
<a name="Closing_a_Window"></a>
### <a name="closing-a-window"></a>ウィンドウを閉じる  
 ウィンドウの有効期間は、表示されたときに開始し、ユーザーが閉じたときに終了します。 ウィンドウを閉じるには、非クライアント領域の要素を使用します。これには、次のものが含まれます。  
  
- **[システム]** メニューの **[閉じる]** 項目。  
  
- Alt キーを押しながら F4 キーを押す。  
  
- **[閉じる]** ボタンを押す。  
  
 クライアント領域にさらに機構を追加してウィンドウを閉じることもできます。その一般的な例を、次に示します。  
  
- 一般にメイン アプリケーション ウィンドウにある、 **[ファイル]** メニューの **[終了]** 項目。  
  
- 一般にアプリケーションの 2 次ウィンドウにある、 **[ファイル]** メニューの **[閉じる]** 項目。  
  
- 一般にモーダル ダイアログ ボックスにある **[キャンセル]** ボタン。  
  
- 一般にモードレス ダイアログ ボックスにある **[閉じる]** ボタン。  
  
 これらのカスタム機構のいずれかに対応してウィンドウを閉じるには、<xref:System.Windows.Window.Close%2A> メソッドを呼び出す必要があります。 **[ファイル]** メニューの **[終了]** をクリックすることでウィンドウを閉じる機能を実装する方法を、次の例に示します。  
  
 [!code-xaml[WindowsOverviewSnippets#WindowWithFileExitMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml#windowwithfileexitmarkup)]  
  
 [!code-csharp[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowWithFileExit.xaml.cs#windowwithfileexitcodebehind)]
 [!code-vb[WindowsOverviewSnippets#WindowWithFileExitCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowsOverviewSnippets/VisualBasic/WindowWithFileExit.xaml.vb#windowwithfileexitcodebehind)]  
  
 ウィンドウが閉じるとき、<xref:System.Windows.Window.Closing> と <xref:System.Windows.Window.Closed> の 2 つのイベントが発生します。  
  
 <xref:System.Windows.Window.Closing> はウィンドウが閉じる前に発生し、ウィンドウが閉じるのを防ぐことができる機構を提供します。 ウィンドウが閉じるのを防ぐのは、一般的に、ウィンドウ コンテンツに変更したデータが含まれている場合です。 この場合、<xref:System.Windows.Window.Closing> イベントを処理して、データが変更されているかどうかを確認できます。変更されている場合は、ユーザーにデータを保存しないでこのままウィンドウを閉じるか、またはウィンドウを閉じる操作を取り消すかを確認できます。 <xref:System.Windows.Window.Closing> を処理するときの要点を、次の例に示します。  
  
 [!code-csharp[WindowClosingSnippets](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowClosingSnippets/CSharp/DataWindow.xaml.cs)]
 [!code-vb[WindowClosingSnippets](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WindowClosingSnippets/visualbasic/datawindow.xaml.vb)]  

 <xref:System.Windows.Window.Closing> イベント ハンドラーに <xref:System.ComponentModel.CancelEventArgs> が渡されます。これにより、ウィンドウが閉じるのを防ぐために `true` に設定する `Boolean`<xref:System.ComponentModel.CancelEventArgs.Cancel%2A> プロパティが実装されます。  
  
 <xref:System.Windows.Window.Closing> が処理されない場合、または処理されたがキャンセルされていない場合、ウィンドウは閉じられます。 ウィンドウが実際に閉じられる直前に、<xref:System.Windows.Window.Closed> が発生します。 この時点で、ウィンドウが閉じるのを防ぐことはできません。  
  
> [!NOTE]
> メイン アプリケーション ウィンドウを閉じるか、最後のウィンドウを閉じるときに、アプリケーションが自動的にシャットダウンされるように構成することができます (「<xref:System.Windows.Application.MainWindow%2A>」を参照)。 詳細については、「<xref:System.Windows.Application.ShutdownMode%2A>」を参照してください。  
  
 非クライアント領域およびクライアント領域に提供される機構によって、ウィンドウを明示的に閉じることができます。また、次のような場合に、アプリケーションまたは Windows の他の部分の動作の結果として、ウィンドウを暗黙的に閉じることもできます。  
  
- ユーザーが Windows からログオフしたか、Windows をシャットダウンした場合。  
  
- ウィンドウのオーナーが閉じた場合 (「<xref:System.Windows.Window.Owner%2A>」を参照)。  
  
- メイン アプリケーション ウィンドウが閉じられ、<xref:System.Windows.Application.ShutdownMode%2A> が <xref:System.Windows.ShutdownMode.OnMainWindowClose> である場合。  
  
- <xref:System.Windows.Application.Shutdown%2A> が呼ばれたとき。  
  
> [!NOTE]
> ウィンドウを閉じると、再度開くことはできません。  
  
<a name="Window_Lifetime_Events"></a>
### <a name="window-lifetime-events"></a>ウィンドウの有効期間イベント  
 次の図は、ウィンドウの有効期間内における主要なイベントのシーケンスを示しています。  
  
 ![ウィンドウの有効期間内のイベントを示す図。](./media/wpf-windows-overview/window-lifetime-events.png)  
  
 次の図は、アクティブ化しないで表示されるウィンドウの有効期間内における主要なイベントのシーケンスを示しています (ウィンドウが表示される前に <xref:System.Windows.Window.ShowActivated%2A> は `false` に設定されています)。  
  
 ![アクティブ化なしでのウィンドウの有効期間内のイベントを示す図。](./media/wpf-windows-overview/window-lifetime-no-activation.png)  
  
<a name="WindowLocation"></a>
## <a name="window-location"></a>ウィンドウの位置  
 ウィンドウが開いているとき、ウィンドウはデスクトップに対して相対的な x ディメンションと y ディメンションの位置にあります。 この位置は、<xref:System.Windows.Window.Left%2A> プロパティと <xref:System.Windows.Window.Top%2A> プロパティをそれぞれ検査することで確認できます。 これらのプロパティを設定して、ウィンドウの位置を変更できます。  
  
 <xref:System.Windows.Window.WindowStartupLocation%2A> プロパティを次の <xref:System.Windows.WindowStartupLocation> 列挙値のいずれかに設定して、<xref:System.Windows.Window> が最初に表示されるときの初期位置を指定することもできます。  
  
- <xref:System.Windows.WindowStartupLocation.CenterOwner> (既定値)  
  
- <xref:System.Windows.WindowStartupLocation.CenterScreen>  
  
- <xref:System.Windows.WindowStartupLocation.Manual>  
  
 開始位置が <xref:System.Windows.WindowStartupLocation.Manual> と指定され、<xref:System.Windows.Window.Left%2A> プロパティと <xref:System.Windows.Window.Top%2A> プロパティが設定されていない場合、<xref:System.Windows.Window> では、ウィンドウに表示位置が問い合わされます。  
  
<a name="Topmost_Windows_and_Z_Order"></a>
### <a name="topmost-windows-and-z-order"></a>最上位ウィンドウと Z オーダー  
 ウィンドウには、x 位置と y 位置に加えて、他のウィンドウを基準にして垂直位置を決定する z ディメンションの位置もあります。 これはウィンドウの z オーダーともいい、標準 z オーダーと最上位 z オーダーの 2 種類があります。 "*標準 z オーダー*" にあるウィンドウの位置は、そのウィンドウが現在アクティブかどうかによって決まります。 既定では、ウィンドウは標準 z オーダーにあります。 "*最上位 z オーダー*" にあるウィンドウの位置も、そのウィンドウが現在アクティブかどうかによって決まります。 また、最上位 z オーダーにあるウィンドウは、常に、標準 z オーダーにあるウィンドウの上に位置します。 ウィンドウを最上位 z オーダーに配置するには、ウィンドウの <xref:System.Windows.Window.Topmost%2A> プロパティを `true` に設定します。  
  
 [!code-xaml[WindowsOverviewSnippets#TopmostWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TopmostWindow.xaml#topmostwindowmarkup1)]  
  
 各 z オーダー内では、現在アクティブなウィンドウは、同じ z オーダーにある他のすべてのウィンドウの上に表示されます。  
  
<a name="WindowSize"></a>
## <a name="window-size"></a>ウィンドウ サイズ  
 ウィンドウには、デスクトップの位置に加えて、さまざまな幅と高さのプロパティや <xref:System.Windows.Window.SizeToContent%2A> など、複数のプロパティによって決定されるサイズがあります。  
  
 <xref:System.Windows.FrameworkElement.MinWidth%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、および <xref:System.Windows.FrameworkElement.MaxWidth%2A> を使用して、有効期間中にウィンドウに指定できる幅の範囲を管理します。これは、次の例に示すように構成します。  
  
 [!code-xaml[WindowsOverviewSnippets#WidthWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WidthWindow.xaml#widthwindowmarkup1)]  
  
 ウィンドウの高さは、<xref:System.Windows.FrameworkElement.MinHeight%2A>、<xref:System.Windows.FrameworkElement.Height%2A>、および <xref:System.Windows.FrameworkElement.MaxHeight%2A> によって管理します。これは、次の例に示すように構成します。  
  
 [!code-xaml[WindowsOverviewSnippets#HeightWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/HeightWindow.xaml#heightwindowmarkup1)]  
  
 さまざまな幅の値と高さの値はそれぞれ範囲を指定しているため、サイズを変更できるウィンドウの幅と高さは、それぞれの寸法に指定された範囲内のいずれかの値を取ります。 現在の幅と高さを検出するには、それぞれ <xref:System.Windows.FrameworkElement.ActualWidth%2A> と <xref:System.Windows.FrameworkElement.ActualHeight%2A> を検査します。  
  
 ウィンドウの幅と高さを、ウィンドウのコンテンツのサイズに合わせたサイズにする場合は、<xref:System.Windows.Window.SizeToContent%2A> プロパティを使用できます。これは、次の値を取ります。  
  
- <xref:System.Windows.SizeToContent.Manual>。 効果 (既定値)。  
  
- <xref:System.Windows.SizeToContent.Width>。 コンテンツの幅に合わせます。これは、<xref:System.Windows.FrameworkElement.MinWidth%2A> と <xref:System.Windows.FrameworkElement.MaxWidth%2A> の両方をコンテンツの幅に設定するのと同じ効果があります。  
  
- <xref:System.Windows.SizeToContent.Height>。 コンテンツの高さに合わせます。これは、<xref:System.Windows.FrameworkElement.MinHeight%2A> と <xref:System.Windows.FrameworkElement.MaxHeight%2A> の両方をコンテンツの高さに設定するのと同じ効果があります。  
  
- <xref:System.Windows.SizeToContent.WidthAndHeight>。 コンテンツの幅と高さに合わせます。これは、<xref:System.Windows.FrameworkElement.MinHeight%2A> と <xref:System.Windows.FrameworkElement.MaxHeight%2A> の両方をコンテンツの高さに設定し、<xref:System.Windows.FrameworkElement.MinWidth%2A> と <xref:System.Windows.FrameworkElement.MaxWidth%2A> の両方をコンテンツの幅に設定するのと同じ効果があります。  
  
 次の例では、ウィンドウを最初に表示するときに、そのコンテンツに合わせて垂直方向と水平方向の両方のサイズを自動的に変更するウィンドウを示しています。  
  
 [!code-xaml[WindowsOverviewSnippets#SizeToContentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/SizeToContentWindow.xaml#sizetocontentwindowmarkup1)]  
  
 次の例では、ウィンドウをそのコンテンツに合わせてサイズ変更する方法を指定するために、コード内に <xref:System.Windows.Window.SizeToContent%2A> プロパティを設定する方法を示します。
  
 [!code-csharp[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/CSharp/MainWindow.xaml.cs#setwindowsizetocontentpropertycode)]
 [!code-vb[HOWTOWindowManagementSnippets#SetWindowSizeToContentPropertyCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOWindowManagementSnippets/visualbasic/mainwindow.xaml.vb#setwindowsizetocontentpropertycode)]  
  
<a name="OrderOfPrecedence"></a>
## <a name="order-of-precedence-for-sizing-properties"></a>サイズ変更プロパティの優先順位  
 基本的に、ウィンドウのさまざまなサイズのプロパティを組み合わせて、サイズを変更できるウィンドウの幅と高さの範囲を定義します。 有効な範囲が維持されていることを確認するために、<xref:System.Windows.Window> では次の優先順位でサイズ プロパティの値が評価されます。  
  
 **高さのプロパティ:**  
  
1. <xref:System.Windows.FrameworkElement.MinHeight%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxHeight%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Height?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Height%2A?displayProperty=nameWithType>  
  
 **幅のプロパティ:**  
  
1. <xref:System.Windows.FrameworkElement.MinWidth%2A?displayProperty=nameWithType>
  
2. <xref:System.Windows.FrameworkElement.MaxWidth%2A?displayProperty=nameWithType>
  
3. <xref:System.Windows.SizeToContent.Width?displayProperty=nameWithType>/<xref:System.Windows.SizeToContent.WidthAndHeight?displayProperty=nameWithType>
  
4. <xref:System.Windows.FrameworkElement.Width%2A?displayProperty=nameWithType>  
  
 優先順位では、ウィンドウが最大化されたときのサイズも決定されます。これは、<xref:System.Windows.Window.WindowState%2A> プロパティで管理します。  
  
<a name="WindowState"></a>
## <a name="window-state"></a>ウィンドウの状態  
 サイズを変更できるウィンドウには、有効期間中、通常、最小化、最大化の 3 つの状態があります。 "*通常*" の状態のウィンドウは、ウィンドウの既定の状態です。 この状態のウィンドウは、サイズ変更グリップ、またはサイズ変更可能な場合は境界線を使用して、ユーザーが移動したりサイズ変更したりできます。  
  
 "*最小化*" された状態のウィンドウは、<xref:System.Windows.Window.ShowInTaskbar%2A> が `true` に設定されている場合は、折りたたまれてタスク バー ボタンになります。それ以外の場合は、折りたたまれて、可能な最小のサイズになり、デスクトップの左下隅に自動的に再配置されます。 最小化されたウィンドウはいずれの種類も、境界線またはサイズ変更グリップを使用してサイズ変更できません。ただし、タスク バーに表示されていない最小化されたウィンドウはデスクトップの任意の場所にドラッグできます。  
  
 "*最大化*" された状態のウィンドウは、拡大されて、可能な最大のサイズになります。これは、<xref:System.Windows.FrameworkElement.MaxWidth%2A> プロパティ、<xref:System.Windows.FrameworkElement.MaxHeight%2A> プロパティ、および <xref:System.Windows.Window.SizeToContent%2A> プロパティが指定するのと同じサイズです。 最小化されたウィンドウと同様、最大化されたウィンドウは、サイズ変更グリップを使用したり、境界線をドラッグしたりすることによってサイズ変更できません。  
  
> [!NOTE]
> ウィンドウが現在最大化または最小化されている場合でも、ウィンドウの <xref:System.Windows.Window.Top%2A>、<xref:System.Windows.Window.Left%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、および <xref:System.Windows.FrameworkElement.Height%2A> の各プロパティの値は、通常の状態の値を常に表します。  
  
 ウィンドウの状態は、<xref:System.Windows.Window.WindowState%2A> プロパティを設定することによって構成できます。これは、次の <xref:System.Windows.WindowState> 列挙値のいずれかを取ります。  
  
- <xref:System.Windows.WindowState.Normal> (既定値)  
  
- <xref:System.Windows.WindowState.Maximized>  
  
- <xref:System.Windows.WindowState.Minimized>  
  
 開くときに最大化されて表示されるウィンドウを作成する方法を、次の例に示します。  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStateWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStateWindow.xaml#windowstatewindowmarkup1)]  
  
 通常は、<xref:System.Windows.Window.WindowState%2A> を設定してウィンドウの初期状態を構成する必要があります。 サイズ変更可能なウィンドウが表示されると、ユーザーはウィンドウのタイトル バーにある最小化ボタン、最大化ボタン、および元に戻すボタンを使用して、ウィンドウの状態を変更できます。  
  
<a name="WindowAppearance"></a>
## <a name="window-appearance"></a>ウィンドウの外観  
 ウィンドウのクライアント領域の外観を変更するために、ボタン、ラベル、テキスト ボックスなど、ウィンドウ固有のコンテンツを追加します。 非クライアント領域を構成するために、<xref:System.Windows.Window> には、ウィンドウのアイコンを設定する <xref:System.Windows.Window.Icon%2A>、タイトルを設定する <xref:System.Windows.Window.Title%2A> など、いくつかのプロパティが用意されています。  
  
 また、ウィンドウのサイズ変更モード、ウィンドウ スタイル、デスクトップのタスク バーにボタンとして表示するかどうかを構成して、非クライアント領域の境界線の外観と動作も変更できます。  

<a name="Resize_Mode"></a>
### <a name="resize-mode"></a>サイズ変更モード  
 <xref:System.Windows.Window.WindowStyle%2A> プロパティに応じて、ユーザーがどのようにウィンドウのサイズを変更するか、またはウィンドウのサイズを変更できるかどうかを制御できます。 ウィンドウ スタイルの選択は、ユーザーがマウスで境界線をドラッグすることによってウィンドウのサイズを変更できるかどうか、 **[最小化]** ボタン、 **[最大化]** ボタン、および **[サイズ変更]** ボタンが非クライアント領域に表示されるかどうか、表示される場合にボタンが有効かどうかに影響を与えます。  
  
 ウィンドウのサイズ変更方法は、<xref:System.Windows.Window.ResizeMode%2A> プロパティを設定することによって構成できます。これは、次の <xref:System.Windows.ResizeMode> 列挙値のいずれかを取ります。  
  
- <xref:System.Windows.ResizeMode.NoResize>  
  
- <xref:System.Windows.ResizeMode.CanMinimize>  
  
- <xref:System.Windows.ResizeMode.CanResize> (既定値)  
  
- <xref:System.Windows.ResizeMode.CanResizeWithGrip>  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] と同様に、ウィンドウのサイズ変更モードは、有効期間中に変更される可能性はほとんどありません。したがって、多くの場合は <xref:System.Windows.Window.WindowStyle%2A> マークアップから設定します。  
  
 [!code-xaml[WindowsOverviewSnippets#ResizeModeWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ResizeModeWindow.xaml#resizemodewindowmarkup1)]  
  
 <xref:System.Windows.Window.WindowState%2A> プロパティを検査することによって、ウィンドウが最大化されているか、最小化されているか、元のサイズに戻されているかを検出できることに注意してください。  
  
<a name="Window_Style"></a>
### <a name="window-style"></a>ウィンドウ スタイル  
 ウィンドウの非クライアント領域から公開される境界線は、多くのアプリケーションに適しています。 ただし、ウィンドウの種類によって、異なる種類の境界線が必要な状況や、境界線がまったく必要ない状況があります。  
  
 ウィンドウの境界線の種類を制御するには、<xref:System.Windows.Window.WindowStyle%2A> プロパティを次の <xref:System.Windows.WindowStyle> 列挙値のいずれかに設定します。  
  
- <xref:System.Windows.WindowStyle.None>  
  
- <xref:System.Windows.WindowStyle.SingleBorderWindow> (既定値)  
  
- <xref:System.Windows.WindowStyle.ThreeDBorderWindow>  
  
- <xref:System.Windows.WindowStyle.ToolWindow>  
  
 これらのウィンドウ スタイルの効果については、次の図で説明します。  
  
 ![ウィンドウの境界線スタイルの図。](./media/wpf-windows-overview/window-border-styles.png)  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップまたはコードのいずれかを使用して <xref:System.Windows.Window.WindowStyle%2A> を設定できます。ウィンドウの有効期間中に変更される可能性はほとんどないため、多くの場合は [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップを使用して構成します。  
  
 [!code-xaml[WindowsOverviewSnippets#WindowStyleWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/WindowStyleWindow.xaml#windowstylewindowmarkup1)]  
  
#### <a name="non-rectangular-window-style"></a>四角形以外のウィンドウ スタイル  
 <xref:System.Windows.Window.WindowStyle%2A> で使用できる境界線のスタイルでは十分ではない状況もあります。 たとえば、Microsoft Windows Media Player で使用されるような、四角形以外の境界線を持つアプリケーションを作成する場合があります。  
  
 たとえば、次の図に示す吹き出しウィンドウを想定します。  
  
 !["ここをドラッグしてください" という吹き出しウィンドウ。](./media/wpf-windows-overview/non-rectangular-window-figure.png)  
  
 この種類のウィンドウは、<xref:System.Windows.Window.WindowStyle%2A> プロパティを <xref:System.Windows.WindowStyle.None> に設定し、<xref:System.Windows.Window> が透明度に対して持つ特殊なサポートを使用することによって作成できます。  
  
 [!code-xaml[WindowsOverviewSnippets#TransparentWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/TransparentWindow.xaml#transparentwindowmarkup1)]  
  
 値をこの組み合わせで使用し、ウィンドウが完全に透明にレンダリングされるように設定します。 この状態では、ウィンドウの非クライアント領域の表示要素 (閉じるメニュー、最小化ボタン、最大化ボタン、元に戻すボタンなど) は使用できません。 したがって、独自の表示要素を用意する必要があります。  
  
<a name="Task_Bar_Presence"></a>
### <a name="task-bar-presence"></a>タスク バーのプレゼンス  

ウィンドウの既定の外観には、次の図に示すような、タスク バー ボタンも含まれます。

 ![タスク バー ボタンのあるウィンドウを示すスクリーンショット。](./media/wpf-windows-overview/window-taskbar-button.png)  
  
 メッセージ ボックスやダイアログ ボックスなど、ウィンドウの種類によっては、タスク バー ボタンがありません (「[ダイアログ ボックスの概要](dialog-boxes-overview.md)」を参照)。 ウィンドウのタスク バー ボタンを表示するかどうかは、<xref:System.Windows.Window.ShowInTaskbar%2A> プロパティを設定することによって制御できます (既定値は `true`)。  
  
 [!code-xaml[WindowsOverviewSnippets#ShowInTaskbarWindowMARKUP1](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsOverviewSnippets/CSharp/ShowInTaskbarWindow.xaml#showintaskbarwindowmarkup1)]  
  
<a name="SecurityConsiderations"></a>
## <a name="security-considerations"></a>セキュリティの考慮事項  
 <xref:System.Windows.Window> をインスタンス化するには、`UnmanagedCode` セキュリティ アクセス許可が必要です。 ローカル コンピューターにインストールされ、ローカル コンピューターから起動されるアプリケーションの場合は、アプリケーションに付与されるアクセス許可セットの範囲内になります。  
  
 ただし、これは、ClickOnce を使用して、インターネット ゾーンまたはローカル イントラネット ゾーンから起動されるアプリケーションに付与されるアクセス許可セットの範囲外になります。 そのため、ユーザーは ClickOnce セキュリティ警告を受け取り、アプリケーションのアクセス許可セットを完全信頼に昇格させる必要があります。  
  
 さらに、XBAP では、既定でウィンドウまたはダイアログ ボックスを表示できません。 スタンドアロン アプリケーションのセキュリティに関する考慮事項については、「[WPF のセキュリティ方針 - プラットフォーム セキュリティ](../wpf-security-strategy-platform-security.md)」を参照してください。  
  
<a name="Other_Types_of_Windows"></a>
## <a name="other-types-of-windows"></a>その他の種類のウィンドウ  
 <xref:System.Windows.Navigation.NavigationWindow> は、ナビゲーション可能なコンテンツをホストするように設計されたウィンドウです。 詳しくは、「[ナビゲーションの概要](navigation-overview.md)」をご覧ください。  
  
 ダイアログ ボックスは、ユーザーから情報を収集して機能を完了するためによく使用されるウィンドウです。 たとえば、ユーザーがファイルを開く場合は、通常、ユーザーからファイル名を取得するために、アプリケーションによって **[ファイルを開く]** ダイアログ ボックスが表示されます。 詳細については、「[ダイアログ ボックスの概要](dialog-boxes-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Window>
- <xref:System.Windows.MessageBox>
- <xref:System.Windows.Navigation.NavigationWindow>
- <xref:System.Windows.Application>
- [ダイアログ ボックスの概要](dialog-boxes-overview.md)
- [WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)
