---
title: アプリケーション管理の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application management [WPF]
ms.assetid: 32b1c054-5aca-423b-b4b5-ed8dc4dc637d
ms.openlocfilehash: dbc5bd9f699415fb47f21c6a45b1c58cfcff0f33
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77124521"
---
# <a name="application-management-overview"></a>アプリケーション管理の概要

すべてのアプリケーションは、アプリケーションの実装と管理に適用される機能を共有することがよくあります。 このトピックでは、アプリケーションの作成と管理のための <xref:System.Windows.Application> クラスの機能の概要について説明します。

## <a name="the-application-class"></a>Application クラス

WPF では、共通のアプリケーション スコープの機能は、<xref:System.Windows.Application> クラスにカプセル化されます。 <xref:System.Windows.Application> クラスには、次の機能が含まれています。

- アプリケーションの有効期間を追跡し、相互作用する。

- コマンド ライン パラメーターを取得し、処理する。

- 未処理の例外を検出し、応答する。

- アプリケーション スコープのプロパティと リソースを共有する。

- スタンドアロン アプリケーションのウィンドウを管理する。

- ナビゲーションを追跡し、管理する。

<a name="The_Application_Class"></a>

## <a name="how-to-perform-common-tasks-using-the-application-class"></a>アプリケーションのクラスを使用して一般的なタスクを実行する方法

<xref:System.Windows.Application> クラスのすべての詳細に興味がない場合は、<xref:System.Windows.Application> の一般的なタスクとそれらを実行する方法を示す次の表を参照してください。 関連する API とトピックを表示することによって、詳細情報とサンプル コードを参照できます。

|タスク|方法|
|----------|--------------|
|現在のアプリケーションを表すオブジェクトを取得する|<xref:System.Windows.Application.Current%2A?displayProperty=nameWithType> プロパティを使用します。|
|起動画面をアプリケーションに追加する|「[スプラッシュ スクリーンを WPF アプリケーションに追加する](how-to-add-a-splash-screen-to-a-wpf-application.md)」を参照してください。|
|アプリケーションを起動する|<xref:System.Windows.Application.Run%2A?displayProperty=nameWithType> メソッドを使用します。|
|アプリケーションを停止する|<xref:System.Windows.Application.Shutdown%2A> オブジェクトの <xref:System.Windows.Application.Current%2A?displayProperty=nameWithType> メソッドを使用します。|
|コマンド ラインから引数を取得する|<xref:System.Windows.Application.Startup?displayProperty=nameWithType> イベントを処理し、<xref:System.Windows.StartupEventArgs.Args%2A?displayProperty=nameWithType> プロパティを使用します。 例については、<xref:System.Windows.Application.Startup?displayProperty=nameWithType> を参照してください。|
|アプリケーションの終了コードを取得し、設定する|<xref:System.Windows.Application.Exit?displayProperty=nameWithType> イベント ハンドラーの <xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A?displayProperty=nameWithType> プロパティを設定するか、<xref:System.Windows.Application.Shutdown%2A> メソッドを呼び出して、整数を渡します。|
|未処理の例外を検出し、応答する|<xref:System.Windows.Application.DispatcherUnhandledException> イベントを処理します。|
|アプリケーション スコープのリソースを取得し、設定する|<xref:System.Windows.Application.Resources%2A?displayProperty=nameWithType> プロパティを使用します。|
|アプリケーション スコープのリソース ディクショナリを使用する|「[アプリケーション スコープのリソース ディクショナリを使用する](how-to-use-an-application-scope-resource-dictionary.md)」を参照してください。|
|アプリケーション スコープのプロパティを取得し、設定する|<xref:System.Windows.Application.Properties%2A?displayProperty=nameWithType> プロパティを使用します。|
|アプリケーションの状態を取得し、保存する|「[アプリケーション セッション全体でアプリケーション スコープのプロパティを永続化および復元する](persist-and-restore-application-scope-properties.md)」を参照してください。|
|リソース ファイル、コンテンツ ファイル、起点ファイルなど、コード以外のデータ ファイルを管理する。|「[WPF アプリケーションのリソース、コンテンツ ファイル、およびデータ ファイル](wpf-application-resource-content-and-data-files.md)」を参照してください。|
|スタンドアロン アプリケーションのウィンドウを管理する|「[WPF ウィンドウの概要](wpf-windows-overview.md)」を参照してください。|
|ナビゲーションを追跡し、管理する|「[ナビゲーションの概要](navigation-overview.md)」を参照してください。|

<a name="The_Application_Definition"></a>

## <a name="the-application-definition"></a>アプリケーション定義

<xref:System.Windows.Application> クラスの機能を利用するには、アプリケーション定義を実装する必要があります。 WPF アプリケーションの定義は、<xref:System.Windows.Application> から派生したクラスであり、特別な MSBuild の設定で構成されます。

### <a name="implementing-an-application-definition"></a>アプリケーション定義の実装

一般的な WPF アプリケーション定義は、マークアップと分離コードの両方を使用して実装されます。 これにより、マークアップを使用して、アプリケーションのプロパティやリソースを宣言によって設定したり、イベントを登録したりでき、分離コードでイベントを処理し、アプリケーション固有の動作を実装することができます。

次の例では、マークアップと分離コードの両方を使用してアプリケーション定義を実装する方法を示します。

[!code-xaml[ApplicationSnippets#ApplicationXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml#applicationxaml)]

[!code-csharp[ApplicationSnippets#ApplicationCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSnippets/CSharp/App.xaml.cs#applicationcodebehind)]
[!code-vb[ApplicationSnippets#ApplicationCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSnippets/visualbasic/application.xaml.vb#applicationcodebehind)]

マークアップ ファイルと分離コード ファイルを連携させるには、次のようにする必要があります。

- マークアップでは、`Application` 要素に `x:Class` 属性を含める必要があります。 アプリケーションのビルド時にマークアップ ファイルに `x:Class` が含まれていると、MSBuild により、`x:Class` 属性で指定された名前を持つ、<xref:System.Windows.Application> から派生した `partial` クラスが作成されます。 そのためには、XAML スキーマ (`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`) に XML 名前空間宣言を追加する必要があります。

- 分離コードでは、クラスは、マークアップ内の `x:Class` 属性で指定されている名前を持つ `partial` クラスでなければなりません。また、<xref:System.Windows.Application> から派生する必要があります。 これによって、分離コード ファイルと、アプリケーションのビルド時にマークアップ ファイル用に生成される `partial` クラスとが関連付けられます (「[WPF アプリケーションのビルド](building-a-wpf-application-wpf.md)」を参照)。

> [!NOTE]
> Visual Studio を使用して新しい WPF アプリケーション プロジェクトまたは WPF ブラウザー アプリケーション プロジェクトを作成すると、アプリケーション定義が既定で含まれ、マークアップと分離コードの両方を使用して定義されます。

このコードは、アプリケーション定義を実装するために最低限必要です。 ただし、アプリケーションをビルドして実行する前に、アプリケーション定義に対して MSBuild の追加構成を行う必要があります。

### <a name="configuring-the-application-definition-for-msbuild"></a>MSBuild 用のアプリケーション定義の構成

スタンドアロン アプリケーションや XAML ブラウザー アプリケーション (XBAP) を実行できるようにするには、一定レベルのインフラストラクチャの実装が必要です。 このインフラストラクチャの最も重要な部分は、エントリ ポイントです。 ユーザーがアプリケーションを起動するとき、オペレーティング システムはエントリ ポイントを呼び出します。これは、アプリケーションを起動するための、よく知られている機能です。

従来、開発者は、テクノロジに応じて、このコードの一部または全部を自分で記述する必要がありました。 しかし、WPF では、次の MSBuild プロジェクト ファイルに示されているように、アプリケーション定義のマークアップ ファイルが MSBuild の `ApplicationDefinition` 項目として構成されると、このコードが自動生成されます。

```xml
<Project
  DefaultTargets="Build"
                        xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  ...
  <ApplicationDefinition Include="App.xaml" />
  <Compile Include="App.xaml.cs" />
  ...
</Project>
```

分離コード ファイルはコードを含んでいるため、通常どおり、MSBuild の `Compile` 項目としてマークされます。

これらの MSBuild 構成をアプリケーション定義のマークアップ ファイルと分離コード ファイルに適用すると、MSBuild によって次のようなコードが生成されます。

[!code-csharp[auto-generated-code](~/samples/snippets/csharp/VS_Snippets_Wpf/AppDefAugSnippets/CSharp/App.cs)]
[!code-vb[auto-generated-code](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AppDefAugSnippets/VisualBasic/App.vb)]

生成されるコードにより、アプリケーション定義に追加のインフラストラクチャのコードが追加され、そこに `Main` というエントリ ポイント メソッドが含まれます。 <xref:System.STAThreadAttribute> 属性が `Main` メソッドに適用されて、WPF アプリケーションのメイン UI スレッドが、WPF アプリケーションに必須の STA スレッドであることが示されます。 呼び出されると、`Main` では、`App` の新しいインスタンスが作成されてから、`InitializeComponent` メソッドが呼び出されて、イベントが登録され、マークアップで実装されるプロパティが設定されます。 `InitializeComponent` は自動的に生成されるので、<xref:System.Windows.Controls.Page> や <xref:System.Windows.Window> の実装のように、アプリケーション定義から `InitializeComponent` を明示的に呼び出す必要はありません。 最後に、<xref:System.Windows.Application.Run%2A> メソッドが呼び出されて、アプリケーションが起動されます。

<a name="Getting_the_Current_Application"></a>

## <a name="getting-the-current-application"></a>現在のアプリケーションの取得

<xref:System.Windows.Application> クラスの機能はアプリケーション間で共有されるため、<xref:System.Windows.Application> クラスのインスタンスは、<xref:System.AppDomain> ごとに 1 つだけです。 これを強制するため、<xref:System.Windows.Application> クラスはシングルトン クラスとして実装されます (「[C# でのシングルトンの実装](https://docs.microsoft.com/previous-versions/msp-n-p/ff650316(v=pandp.10))」を参照)。つまり、インスタンスが 1 つだけ作成され、`static` <xref:System.Windows.Application.Current%2A> プロパティを使用して、インスタンスへの共有アクセスが提供されます。

次のコードでは、現在の <xref:System.AppDomain> の <xref:System.Windows.Application> オブジェクトへの参照を取得する方法を示します。

[!code-csharp[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getcurrentappcode)]
[!code-vb[ApplicationManagementOverviewSnippets#GetCurrentAppCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getcurrentappcode)]

<xref:System.Windows.Application.Current%2A> では、<xref:System.Windows.Application> クラスのインスタンスへの参照が返されます。 <xref:System.Windows.Application> 派生クラスへの参照が必要な場合は、次の例で示すように、<xref:System.Windows.Application.Current%2A> プロパティの値をキャストする必要があります。

[!code-csharp[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/MainWindow.xaml.cs#getstcurrentappcode)]
[!code-vb[ApplicationManagementOverviewSnippets#GetSTCurrentAppCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/VisualBasic/MainWindow.xaml.vb#getstcurrentappcode)]

<xref:System.Windows.Application.Current%2A> の値は、<xref:System.Windows.Application> オブジェクトの有効期間中はいつでも調べることができます。 ただし、注意が必要です。 <xref:System.Windows.Application> クラスがインスタンス化された後、<xref:System.Windows.Application> オブジェクトの状態の一貫性が失われる期間があります。 この期間中、<xref:System.Windows.Application> では、アプリケーション インフラストラクチャの確立、プロパティの設定、イベントの登録など、コードの実行に必要なさまざまな初期化タスクが実行されます。 この期間中に <xref:System.Windows.Application> オブジェクトを使用しようとすると、コードが予期しない結果になることがあります (特に設定中のさまざまな <xref:System.Windows.Application> プロパティに依存している場合)。

<xref:System.Windows.Application> での初期化作業を完了すると、実質的な有効期間が始まります。

<a name="Application_Lifetime"></a>

## <a name="application-lifetime"></a>アプリケーションの有効期間

WPF アプリケーションの有効期間は、アプリケーションが起動されたこと、アクティブになったこと、非アクティブになったこと、シャットダウンされたことなどを通知するために、<xref:System.Windows.Application> によって発生させられるいくつかのイベントによってマークされます。

<a name="Splash_Screen"></a>

### <a name="splash-screen"></a>スプラッシュ スクリーン

.NET Framework 3.5 SP1 以降では、スタートアップ ウィンドウ ("*スプラッシュ スクリーン*") で使用する画像を指定できます。 <xref:System.Windows.SplashScreen> クラスを使用すると、アプリケーションを読み込んでいるときに、スタートアップ ウィンドウを簡単に表示できます。 <xref:System.Windows.SplashScreen> ウィンドウは、<xref:System.Windows.Application.Run%2A> が呼び出される前に作成されて表示されます。 詳細については、「[アプリケーションの起動時間](../advanced/application-startup-time.md)」および「[スプラッシュ スクリーンを WPF アプリケーションに追加する](how-to-add-a-splash-screen-to-a-wpf-application.md)」を参照してください。

<a name="Starting_an_Application"></a>

### <a name="starting-an-application"></a>アプリケーションの起動

<xref:System.Windows.Application.Run%2A> が呼び出され、アプリケーションが初期化されると、アプリケーションの実行準備が整います。 このタイミングは、<xref:System.Windows.Application.Startup> イベントが発生したときに通知されます。

[!code-csharp[Startup-event](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs?range=3-11,31-33)]
[!code-vb[Startup-event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb?range=5-11,30-32)]

アプリケーションの有効期間中のこの時点で最も一般的に行われるのは、UI の表示です。

<a name="Showing_a_User_Interface"></a>

### <a name="showing-a-user-interface"></a>ユーザー インターフェイスの表示

ほとんどのスタンドアロン Windows アプリケーションでは、実行を開始するとき、<xref:System.Windows.Window> が開かれます。 次のコードに示されているように、<xref:System.Windows.Application.Startup> イベント ハンドラーは、これを行うことができる場所の 1 つです。

[!code-xaml[AppShowWindowHardSnippets#StartupEventMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml#startupeventmarkup)]

[!code-csharp[AppShowWindowHardSnippets#StartupEventCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/AppShowWindowHardSnippets/CSharp/App.xaml.cs#startupeventcodebehind)]
[!code-vb[AppShowWindowHardSnippets#StartupEventCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/AppShowWindowHardSnippets/VisualBasic/Application.xaml.vb#startupeventcodebehind)]

> [!NOTE]
> スタンドアロン アプリケーションではインスタンス化された最初の <xref:System.Windows.Window> が、既定でメイン アプリケーション ウィンドウになります。 この <xref:System.Windows.Window> オブジェクトは、<xref:System.Windows.Application.MainWindow%2A?displayProperty=nameWithType> プロパティによって参照されます。 最初にインスタンス化された <xref:System.Windows.Window> 以外のウィンドウをメイン ウィンドウにする必要がある場合は、<xref:System.Windows.Application.MainWindow%2A> プロパティの値をプログラムで変更できます。

通常、XBAP は起動すると最初に、<xref:System.Windows.Controls.Page> にナビゲートします。 これを次のコードに示します。

[!code-xaml[XBAPAppStartupSnippets#StartupXBAPMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml#startupxbapmarkup)]

[!code-csharp[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/XBAPAppStartupSnippets/CSharp/App.xaml.cs#startupxbapcodebehind)]
[!code-vb[XBAPAppStartupSnippets#StartupXBAPCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XBAPAppStartupSnippets/VisualBasic/Application.xaml.vb#startupxbapcodebehind)]

<xref:System.Windows.Application.Startup> の処理目的が <xref:System.Windows.Window> を開くことか、<xref:System.Windows.Controls.Page> にナビゲートすることのみの場合は、代わりに、マークアップで `StartupUri` 属性を設定できます。

次の例では、スタンドアロン アプリケーションから <xref:System.Windows.Application.StartupUri%2A> を使用して <xref:System.Windows.Window> を開く方法を示します。

[!code-xaml[ApplicationManagementOverviewSnippets#OverviewStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationManagementOverviewSnippets/CSharp/App.xaml#overviewstartupurimarkup)]

次の例では、XBAP から <xref:System.Windows.Application.StartupUri%2A> を使用して <xref:System.Windows.Controls.Page> にナビゲートする方法を示します。

[!code-xaml[PageSnippets#XBAPStartupUriMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/PageSnippets/CSharp/App.xaml#xbapstartupurimarkup)]

このマークアップは、ウィンドウを開くことについて、前のコードと同じ効果があります。

> [!NOTE]
> ナビゲーションの詳細については、「[ナビゲーションの概要](navigation-overview.md)」を参照してください。

パラメーターなしではないコンストラクターを使用してウィンドウをインスタンス化する必要がある場合、またはウィンドウを表示する前にウィンドウのプロパティを設定するか、イベントをサブスクライブする必要がある場合、またはアプリケーションの起動時に指定されたコマンド ライン引数を処理する必要がある場合、<xref:System.Windows.Window> を開くには、<xref:System.Windows.Application.Startup> イベントを処理する必要があります。

<a name="Processing_Command_Line_Arguments"></a>

### <a name="processing-command-line-arguments"></a>コマンド ライン引数の処理

Windows では、スタンドアロン アプリケーションは、コマンド プロンプトまたはデスクトップから起動できます。 どちらの場合も、コマンド ライン引数をアプリケーションに渡すことができます。 次の例は、1 つのコマンド ライン引数 "/StartMinimized" を指定して起動されるアプリケーションを示しています。

`wpfapplication.exe /StartMinimized`

アプリケーションの初期化中に、WPF によってオペレーティング システムからコマンド ライン引数が取得され、<xref:System.Windows.StartupEventArgs> パラメーターの <xref:System.Windows.StartupEventArgs.Args%2A> プロパティを介して <xref:System.Windows.Application.Startup> イベント ハンドラーに渡されます。 次のようなコードを使用して、コマンド ライン引数を取得し、格納することができます。

[!code-xaml[ApplicationStartupSnippets#HandleStartupXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml#handlestartupxaml)]

[!code-csharp[ApplicationStartupSnippets#HandleStartupCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationStartupSnippets/CSharp/App.xaml.cs#handlestartupcodebehind)]
[!code-vb[ApplicationStartupSnippets#HandleStartupCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationStartupSnippets/visualbasic/application.xaml.vb#handlestartupcodebehind)]

このコードでは、<xref:System.Windows.Application.Startup> が処理されて、 **/StartMinimized** コマンド ライン引数が指定されたかどうかが確認されます。指定されている場合は、<xref:System.Windows.WindowState> を <xref:System.Windows.WindowState.Minimized> にしてメイン ウィンドウが開かれます。 <xref:System.Windows.Window.WindowState%2A> プロパティはプログラムで設定する必要があるため、メイン <xref:System.Windows.Window> をコードで明示的に開く必要があることに注意してください。

XBAP は、ClickOnce 配置を使用して起動されるため、コマンド ライン引数を処理できません (「[WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)」を参照)。 ただし、起動に使用される URL のクエリ文字列パラメーターを取得して処理することはできます。

<a name="Application_Activation_and_Deactivation"></a>

### <a name="application-activation-and-deactivation"></a>アプリケーションのアクティブ化と非アクティブ化

Windows では、ユーザーがアプリケーションを切り替えることができます。 最も一般的な方法は、Alt キーを押しながら Tab キーを押す方法です。 アプリケーションを切り替えることができるのは、ユーザーが選択できる可視の <xref:System.Windows.Window> がある場合だけです。 現在選択されている <xref:System.Windows.Window> は、"*アクティブ ウィンドウ*" であり ("*フォアグラウンド ウィンドウ*" とも呼ばれます)、ユーザー入力を受け取る <xref:System.Windows.Window> です。 アクティブ ウィンドウを持つアプリケーションは、"*アクティブ アプリケーション*" (または "*フォア グラウンド アプリケーション*") です。 アプリケーションは、次の状況でアクティブ アプリケーションになります。

- 起動され、<xref:System.Windows.Window> を表示している。

- ユーザーがアプリケーションの <xref:System.Windows.Window> を選択することによって、別のアプリケーションから切り替えた。

アプリケーションがアクティブになったことは、<xref:System.Windows.Application.Activated?displayProperty=nameWithType> イベントを処理することによって検出できます。

同様に、アプリケーションは、次の状況で非アクティブになります。

- ユーザーが現在のアプリケーションから別のアプリケーションに切り替えた。

- アプリケーションがシャットダウンされた。

アプリケーションが非アクティブになったことは、<xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> イベントを処理することによって検出できます。

次のコードでは、<xref:System.Windows.Application.Activated> および <xref:System.Windows.Application.Deactivated> イベントを処理して、アプリケーションがアクティブかどうかを確認する方法を示します。

[!code-xaml[ApplicationActivationSnippets#DetectActivationStateXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml#detectactivationstatexaml)]

[!code-csharp[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationActivationSnippets/CSharp/App.xaml.cs#detectactivationstatecodebehind)]
[!code-vb[ApplicationActivationSnippets#DetectActivationStateCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationActivationSnippets/visualbasic/application.xaml.vb#detectactivationstatecodebehind)]

<xref:System.Windows.Window> もアクティブまたは非アクティブにできます。 詳細については、「<xref:System.Windows.Window.Activated?displayProperty=nameWithType>」および「<xref:System.Windows.Window.Deactivated?displayProperty=nameWithType>」を参照してください。

> [!NOTE]
> <xref:System.Windows.Application.Activated?displayProperty=nameWithType> も <xref:System.Windows.Application.Deactivated?displayProperty=nameWithType> も、XBAP については発生しません。

<a name="Application_Shutdown"></a>

### <a name="application-shutdown"></a>アプリケーションのシャットダウン

アプリケーションの有効期間は、シャット ダウンされると終了します。シャットダウンは、次の理由で発生します。

- ユーザーがすべての <xref:System.Windows.Window> を閉じた。

- ユーザーがメイン <xref:System.Windows.Window> を閉じた。

- ユーザーがログオフまたはシャットダウンして、Windows セッションを終了した。

- アプリケーション固有の条件が満たされた。

アプリケーションのシャット ダウンの管理を支援するために、<xref:System.Windows.Application> には、<xref:System.Windows.Application.Shutdown%2A> メソッド、<xref:System.Windows.Application.ShutdownMode%2A> プロパティ、<xref:System.Windows.Application.SessionEnding> イベント、<xref:System.Windows.Application.Exit> イベントが用意されています。

> [!NOTE]
> <xref:System.Windows.Application.Shutdown%2A> は、<xref:System.Security.Permissions.UIPermission> を持つアプリケーションからのみ呼び出すことができます。 スタンドアロン WPF アプリケーションには、常にこのアクセス許可があります。 一方、インターネット ゾーン部分信頼セキュリティ サンド ボックスで実行される XBAP には、このアクセス許可がありません。

#### <a name="shutdown-mode"></a>シャットダウン モード

ほとんどのアプリケーションは、すべてのウィンドウが閉じられるか、メイン ウィンドウが閉じられたときにシャットダウンします。 ただし、場合によっては、他のアプリケーションに固有の条件によって、アプリケーションがシャット ダウンするタイミングに影響します。 <xref:System.Windows.Application.ShutdownMode%2A> に次のいずれかの <xref:System.Windows.ShutdownMode> 列挙値を設定することによって、アプリケーションがシャットダウンする条件を指定できます。

- <xref:System.Windows.ShutdownMode.OnLastWindowClose>

- <xref:System.Windows.ShutdownMode.OnMainWindowClose>

- <xref:System.Windows.ShutdownMode.OnExplicitShutdown>

<xref:System.Windows.Application.ShutdownMode%2A> の既定値は <xref:System.Windows.ShutdownMode.OnLastWindowClose> であり、アプリケーションの最後のウィンドウがユーザーによって閉じられたときにアプリケーションが自動的にシャットダウンすることを意味します。 一方、メイン ウィンドウが閉じられたときにアプリケーションがシャットダウンするようにする必要がある場合は、<xref:System.Windows.Application.ShutdownMode%2A> を <xref:System.Windows.ShutdownMode.OnMainWindowClose> に設定すると、WPF は自動的にシャットダウンします。 これを次の例に示します。

[!code-xaml[ApplicationShutdownModeSnippets#OnMainWindowCloseMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationShutdownModeSnippets/CS/Page1.xaml#onmainwindowclosemarkup)]

アプリケーション固有のシャットダウン条件があるときは、<xref:System.Windows.Application.ShutdownMode%2A> を <xref:System.Windows.ShutdownMode.OnExplicitShutdown> に設定します。 この場合、明示的に <xref:System.Windows.Application.Shutdown%2A> メソッドを呼び出すことによってアプリケーションをシャット ダウンする必要があります。そうしないと、すべてのウィンドウが閉じられた場合でも、アプリケーションは実効を続けます。 <xref:System.Windows.Application.Shutdown%2A> は、<xref:System.Windows.Application.ShutdownMode%2A> が <xref:System.Windows.ShutdownMode.OnLastWindowClose> または <xref:System.Windows.ShutdownMode.OnMainWindowClose> のときに暗黙的に呼び出されることに注意してください。

> [!NOTE]
> <xref:System.Windows.Application.ShutdownMode%2A> は、XBAP から設定できますが、無視されます。XBAP は、ブラウザーで他にナビゲートされたか、または XBAP をホストするブラウザーが閉じられると、必ずシャットダウンします。 詳細については、「[ナビゲーションの概要](navigation-overview.md)」を参照してください。

#### <a name="session-ending"></a>セッションの終了

<xref:System.Windows.Application.ShutdownMode%2A> プロパティによって記述されるシャットダウン条件は、アプリケーションに固有です。 ただし、場合によっては、アプリケーションは、外部条件の結果としてシャットダウンすることもあります。 最も一般的な外部条件は、ユーザーが次の操作によって Windows セッションを終了した場合です。

- ログオフ

- シャット ダウン

- 再起動

- 休止

Windows セッションの終了を検出するには、次の例に示されているように、<xref:System.Windows.Application.SessionEnding> イベントを処理します。

[!code-xaml[ApplicationSessionEndingSnippets#HandlingSessionEndingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml#handlingsessionendingxaml)]

[!code-csharp[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/CSharp/App.xaml.cs#handlingsessionendingcodebehind)]
[!code-vb[ApplicationSessionEndingSnippets#HandlingSessionEndingCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationSessionEndingSnippets/visualbasic/application.xaml.vb#handlingsessionendingcodebehind)]

この例のコードでは、<xref:System.Windows.SessionEndingCancelEventArgs.ReasonSessionEnding%2A> プロパティを調べて、Windows セッションの終了方法を決定します。 この値を使用して、ユーザーに確認メッセージを表示します。 ユーザーがセッションの終了を意図していない場合、コードでは <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> を `true` に設定して、Windows セッションが終了しないようにします。

> [!NOTE]
> <xref:System.Windows.Application.SessionEnding> は、XBAP に対しては発生しません。

#### <a name="exit"></a>終了

アプリケーションがシャット ダウンするときには、アプリケーション状態の保存など、いくつかの最終処理を実行しなければならない場合があります。 このような状況では、次の例の `App_Exit` イベント ハンドラーで行われているように、<xref:System.Windows.Application.Exit> イベントを処理できます。 これは、*App.xaml* ファイル内でイベント ハンドラーとして定義されています。 その実装は、*App.xaml.cs* ファイルと *Application.xaml.vb* ファイルで強調表示されています。

[!code-xaml[Defining-the-Exit-event-handler](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml?highlight=1-7)]

[!code-csharp[Handling-the-Exit-event](~/samples/snippets/csharp/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/CSharp/App.xaml.cs?highlight=42-55)]
[!code-vb[Handling-the-Exit-event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HOWTOApplicationModelSnippets/visualbasic/application.xaml.vb?highlight=34-45)]

完全な例については、「[アプリケーション セッション全体でアプリケーション スコープのプロパティを永続化および復元する](persist-and-restore-application-scope-properties.md)」を参照してください。

<xref:System.Windows.Application.Exit> は、スタンドアロン アプリケーションと XBAP の両方によって処理できます。 XBAP では、次の状況で <xref:System.Windows.Application.Exit> が発生します。

- XBAP から外部にナビゲートされた。

- Internet Explorer で、XBAP をホストしているタブが閉じられた。

- ブラウザーが閉じられた。

#### <a name="exit-code"></a>終了コード

ほとんどのアプリケーションは、ユーザー要求に応じてオペレーティング システムから起動されます。 ただし、アプリケーションは、特定のタスクを実行するために、別のアプリケーションに起動されることもあります。 起動されたアプリケーションがシャット ダウンするとき、起動元のアプリケーションは、起動されたアプリケーションのシャット ダウン条件を知ならなければならないことがあります。 このような場合、Windows では、アプリケーションは終了時にアプリケーション終了コードを返すことができます。 既定では、WPF アプリケーションは 0 の終了コード値を返します。

> [!NOTE]
> Visual Studio からデバッグする場合、アプリケーション終了コードは、アプリケーションのシャットダウン時に、 **[出力]** ウィンドウに次のようなメッセージで表示されます。
>
> `The program '[5340] AWPFApp.vshost.exe: Managed' has exited with code 0 (0x0).`
>
> **[出力]** ウィンドウを開くには、 **[表示]** メニューの **[出力]** をクリックします。

終了コードを変更するには、<xref:System.Windows.Application.Shutdown%28System.Int32%29> オーバーロードを呼び出します。これは、終了コードとして整数引数を受け入れます。

[!code-csharp[ApplicationExitSnippets#AppExitCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationExitSnippets/CSharp/MainWindow.xaml.cs#appexitcode)]
[!code-vb[ApplicationExitSnippets#AppExitCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationExitSnippets/visualbasic/mainwindow.xaml.vb#appexitcode)]

<xref:System.Windows.Application.Exit> イベントを処理することによって、終了コードの値を検出し、変更できます。 <xref:System.Windows.Application.Exit> イベント ハンドラーに渡される <xref:System.Windows.ExitEventArgs> では、<xref:System.Windows.ExitEventArgs.ApplicationExitCode%2A> プロパティで終了コードへのアクセスが提供されます。 詳細については、「<xref:System.Windows.Application.Exit>」を参照してください。

> [!NOTE]
> 終了コードは、スタンドアロン アプリケーションと XBAP の両方で設定できます。 ただし、XBAP の場合、終了コード値は無視されます。

<a name="Unhandled_Exceptions"></a>

### <a name="unhandled-exceptions"></a>未処理の例外

ときには、アプリケーションは、予期しない例外がスローされたときなど、異常な条件下でシャットダウンすることがあります。 この場合、アプリケーションには、例外を検出して処理するためのコードがありません。 この種類の例外は、未処理の例外と呼ばれます。アプリケーションが閉じられる前に、次の図に示されているような通知が表示されます。

![ハンドルされない例外通知を示すスクリーンショット。](./media/application-management-overview/unhandled-exception-notification.png)

ユーザー エクスペリエンスの観点から、アプリケーションは、次のいずれか、またはすべてを行うことによって、この既定の動作を回避することをお勧めします。

- わかりやすい情報を表示する。

- アプリケーションの続行を試みる。

- 開発者向けの詳細な例外情報を Windows イベント ログに記録する。

このサポートを実装するには、<xref:System.Windows.Application.DispatcherUnhandledException> イベントが発生した未処理の例外を検出できることが前提になります。

[!code-xaml[detecting-unhandled-exceptions](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml#handledispatcherunhandledexceptionxaml)]

[!code-csharp[code-to-detect-unhandled-exceptions](~/samples/snippets/csharp/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/CSharp/App.xaml.cs)]
[!code-vb[code-to-detect-unhandled-exceptions](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ApplicationDispatcherUnhandledExceptionSnippets/visualbasic/application.xaml.vb)]

<xref:System.Windows.Application.DispatcherUnhandledException> イベント ハンドラーには、例外そのもの (<xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Exception%2A?displayProperty=nameWithType>) も含め、未処理の例外に関するコンテキスト情報を含む <xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs> パラメーターが渡されます。 この情報を使用して、例外の処理方法を決定できます。

<xref:System.Windows.Application.DispatcherUnhandledException> を処理するときには、<xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A?displayProperty=nameWithType> プロパティを `true` に設定する必要があります。そうしないと、WPF は例外を未処理のままとみなし、前述の既定の動作に戻ります。 ハンドルされない例外が発生し、<xref:System.Windows.Application.DispatcherUnhandledException> イベントが処理されないか、イベントが処理されても、<xref:System.Windows.Threading.DispatcherUnhandledExceptionEventArgs.Handled%2A> が `false` に設定されていた場合、アプリケーションはただちにシャットダウンします。 さらに、他の <xref:System.Windows.Application> イベントは発生しません。 結果として、アプリケーションに、アプリケーションがシャットダウンする前に実行しなければならないコードがある場合は、<xref:System.Windows.Application.DispatcherUnhandledException> を処理する必要があります。

アプリケーションは、未処理の例外の結果としてシャットダウンすることがありますが、通常は、次のセクションで説明されているように、ユーザーの要求に応じてシャットダウンします。

<a name="Application_Lifetime_Events"></a>

### <a name="application-lifetime-events"></a>アプリケーションの有効期間イベント

スタンドアロン アプリケーションと XBAP の有効期間は、厳密に同じわけではありません。 次の図は、スタンドアロン アプリケーションの有効期間中の主なイベントと発生順を示しています。

![スタンドアロン アプリケーション &#45; アプリケーション オブジェクト イベント](./media/applicationmodeloverview-applicationobjectevents.png "ApplicationModelOverview_ApplicationObjectEvents")

同様に、次の図では、XBAP の有効期間中の主なイベントと発生順を示します。

![XBAP &#45; アプリケーション オブジェクト イベント](./media/applicationmodeloverview-applicationobjectevents-xbap.png "ApplicationModelOverview_ApplicationObjectEvents_xbap")

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Application>
- [WPF ウィンドウの概要](wpf-windows-overview.md)
- [ナビゲーションの概要](navigation-overview.md)
- [WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](wpf-application-resource-content-and-data-files.md)
- [WPF におけるパッケージの URI](pack-uris-in-wpf.md)
- [アプリケーション モデル: 方法のトピック](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms749013(v=vs.100))
- [アプリケーションの開発](index.md)
