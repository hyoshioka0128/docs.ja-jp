---
title: XAML ブラウザー アプリケーションの概要
description: Windows Presentation Foundation (WPF) で、Web アプリケーションとリッチクライアント アプリケーションの機能が XAML ブラウザー アプリケーションでどのように組み合わされているかについて説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XBAP [WPF], XAML browser application
- WPF XAML browser applications (XBAP)
- XAML browser applications (XBAP)
- browser-hosted applications [WPF]
ms.assetid: 3a7a86a8-75d5-4898-96b9-73da151e5e16
ms.openlocfilehash: 3395445dd5639e25f62aeef09d070e326704ed40
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617913"
---
# <a name="wpf-xaml-browser-applications-overview"></a>WPF XAML ブラウザー アプリケーションの概要
<a name="introduction"></a> XAML ブラウザー アプリケーション (XBAP) は、Web アプリケーションとリッチ クライアント アプリケーションの両方の機能を兼ね備えています。 たとえば、Web アプリケーションと同様、Web サーバーに配置して、Internet Explorer または Firefox から開始できます。 また、リッチ クライアント アプリケーションと同様、WPF の機能を利用することができます。 XBAP の開発方法もリッチ クライアントの開発に似ています。 このトピックでは、XBAP 開発の概要を示し、XBAP 開発が標準的なリッチ クライアント開発と異なる点について説明します。

 このトピックは、次のセクションで構成されています。

- [新しい XAML ブラウザー アプリケーション (XBAP) の作成](#creating_a_new_xaml_browser_application_xbap)

- [XBAP の配置](#deploying_a_xbap)

- [ホスト Web ページとの通信](#communicating_with_the_host_web_page)

- [XBAP セキュリティの考慮事項](#xbap_security_considerations)

- [XBAP 起動時のパフォーマンスに関する考慮事項](#xbap_start_time_performance_considerations)

<a name="creating_a_new_xaml_browser_application_xbap"></a>
## <a name="creating-a-new-xaml-browser-application-xbap"></a>新しい XAML ブラウザー アプリケーション (XBAP) の作成
 新しい XBAP プロジェクトを作成する最も簡単な方法は、Visual Studio を使用することです。 新しいプロジェクトを作成するときに、テンプレートの一覧で **[WPF ブラウザー アプリケーション]** を選択します。 詳細については、「[方法:新しい WPF ブラウザー アプリケーション プロジェクトを作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb628663(v=vs.100))」を参照してください。

 XBAP プロジェクトを実行すると、そのプロジェクトは、スタンドアロン ウィンドウではなくブラウザー ウィンドウで開きます。 XBAP を Visual Studio でデバッグするとき、アプリケーションはインターネット ゾーン アクセス許可に基づいて実行されます。したがって、そのアクセス許可を超えると、セキュリティ例外がスローされます。 詳細については、[セキュリティ](../security-wpf.md)に関するページと、「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」を参照してください。

> [!NOTE]
> Visual Studio を使用して開発していない場合やプロジェクト ファイルについて詳しい情報が必要な場合は、「[WPF アプリケーション (WPF) のビルド](building-a-wpf-application-wpf.md)」を参照してください。

<a name="deploying_a_xbap"></a>
## <a name="deploying-an-xbap"></a>XBAP の配置
 XBAP をビルドすると、次の 3 つのファイルが生成されます。

|ファイル|説明|
|----------|-----------------|
|実行可能ファイル (.exe)|コンパイル済みのコードが含まれます。拡張子は .exe です。|
|アプリケーション マニフェスト (.manifest)|アプリケーションに関連付けられたメタデータが含まれます。拡張子は .manifest です。|
|配置マニフェスト (.xbap)|ClickOnce がアプリケーションの配置に使用する情報が含まれます。拡張子は .xbap です。|

 XBAP は Web サーバーに配置します (Microsoft インターネット インフォメーション サービス (IIS) 5.0 以降のバージョンなど)。 .NET Framework を Web サーバーにインストールする必要はありませんが、WPF Multipurpose Internet Mail Extensions (MIME) の種類とファイル名拡張子を登録する必要はあります。 詳細については、[WPF アプリケーションを配置するための IIS 5.0 および IIS 6.0 の構成](how-to-configure-iis-5-0-and-iis-6-0-to-deploy-wpf-applications.md)に関するページをご覧ください。

 XBAP を配置用に準備するには、.exe および関連付けられたマニフェストを Web サーバーにコピーします。 配置マニフェスト (拡張子が .xbap のファイル) を開くために、ハイパーリンクを含む HTML ページを作成します。 ユーザーが .xbap ファイルへのリンクをクリックすると、ClickOnce によって、アプリケーションのダウンロードと開始が自動的に処理されます。 次のコード例は、XBAP を指定するハイパーリンクを含む HTML ページを示しています。

```html
<html>
    <head></head>
    <body>
        <a href="XbapEx.xbap">Click this link to launch the application</a>
    </body>
</html>
```

 Web ページのフレームで XBAP をホストすることもできます。 1 つ以上のフレームを含む Web ページを作成し、 配置マニフェスト ファイルに対するフレームのソース プロパティを設定します。 組み込みのメカニズムを使用して、ホスティング Web ページと XBAP との間で通信を行う場合は、フレームでアプリケーションをホストする必要があります。 次のコード例は、2 つのフレームが含まれる HTML ページを示しています。ここでは、2 つ目のフレームのソースが XBAP に設定されています。

```html
<html>
    <head>
        <title>A page with frames</title>
    </head>
    <frameset cols="50%,50%">
        <frame src="introduction.htm">
        <frame src="XbapEx.xbap">
    </frameset>
</html>
```

### <a name="clearing-cached-xbaps"></a>キャッシュされた XBAP のクリア
 XBAP をリビルドして開始した後に、旧バージョンの XBAP が開くことがあります。 たとえば、この動作は、XBAP アセンブリのバージョン番号が静的である場合に、XBAP をコマンド ラインから開始すると発生することがあります。 この場合、キャッシュされているバージョン (それまで開始されていたバージョン) と新しいバージョンのバージョン番号が同じであるため、XBAP の新しいバージョンはダウンロードされません。 代わりに、キャッシュされたバージョンが読み込まれます。

 このような場合、キャッシュされているバージョンを削除するには、コマンド プロンプトで (Visual Studio または Windows SDK でインストールされる) **Mage** コマンドを使用します。 次のコマンドにより、アプリケーション キャッシュがクリアされます。

 ```console
 Mage.exe -cc
 ```

 このコマンドを実行すると、必ず最新バージョンの XBAP が開始されます。 アプリケーションを Visual Studio でデバッグするときは、XBAP の最新バージョンを開始する必要があります。 一般的に、配置バージョン番号は、ビルドするたびに更新することをお勧めします。 Mage の詳細については、「[Mage.exe (マニフェストの生成および編集ツール)](../../tools/mage-exe-manifest-generation-and-editing-tool.md)」を参照してください。

<a name="communicating_with_the_host_web_page"></a>
## <a name="communicating-with-the-host-web-page"></a>ホスト Web ページとの通信
 アプリケーションが HTML フレーム内でホストされている場合は、XBAP を含む Web ページと通信できます。 それには、<xref:System.Windows.Interop.BrowserInteropHelper> の <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> プロパティを取得します。 このプロパティは、HTML ウィンドウを表すスクリプト オブジェクトを返します。 [window オブジェクト](https://developer.mozilla.org/en-US/docs/Web/API/Window)上のプロパティ、メソッド、およびイベントにアクセスするには、標準のドット構文を使用します。 スクリプト メソッドおよびグローバル変数にアクセスすることもできます。 次の例は、スクリプト オブジェクトを取得して、ブラウザーを閉じる方法を示しています。

 [!code-csharp[XbapBrowserInterop#10](~/samples/snippets/csharp/VS_Snippets_Wpf/xbapbrowserinterop/cs/page1.xaml.cs#10)]
 [!code-vb[XbapBrowserInterop#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/xbapbrowserinterop/vb/page1.xaml.vb#10)]

### <a name="debugging-xbaps-that-use-hostscript"></a>HostScript を使用する XBAP のデバッグ
 XBAP で <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> オブジェクトを使用して HTML ウィンドウと通信する場合、Visual Studio でアプリケーションを実行およびデバッグするには、2 つの設定を指定する必要があります。 そのアプリケーションは元のサイトにアクセスできる必要がありますが、そのアプリケーションを開始するときは、XBAP を含む HTML ページを使用しなければなりません。 この 2 つの設定を確認する手順を次に示します。

1. Visual Studio でプロジェクトのプロパティを開きます。

2. **[セキュリティ]** タブの **[詳細設定]** をクリックします。

     [セキュリティの詳細設定] ダイアログ ボックスが表示されます。

3. **[アプリケーション アクセスをその元のサイトに与える]** チェック ボックスがオンになっていることを確認し、 **[OK]** をクリックします。

4. **[デバッグ]** タブで、 **[ブラウザーを開始時に使用する URL]** をクリックし、XBAP を含む HTML ページの URL を指定します。

5. Internet Explorer で、 **[ツール]** をクリックし、 **[インターネット オプション]** をクリックします。

     [インターネット オプション] ダイアログ ボックスが表示されます。

6. **[詳細設定]** タブをクリックします。

7. **[セキュリティ]** の下にある **[設定]** ボックスで、 **[マイ コンピューターのファイルでのアクティブ コンテンツの実行を許可する]** チェック ボックスをオンにします。

8. **[OK]** をクリックします。

     変更は、Internet Explorer を再起動すると有効になります。

> [!CAUTION]
> Internet Explorer でアクティブ コンテンツを有効にすると、コンピューターが危険にさらされるおそれがあります。 Internet Explorer のセキュリティ設定を変更したくない場合は、HTML ページをサーバーから起動して、Visual Studio デバッガーをプロセスにアタッチできます。

<a name="xbap_security_considerations"></a>
## <a name="xbap-security-considerations"></a>XBAP セキュリティの考慮事項
 XBAP は、通常、インターネット ゾーン アクセス許可セットに制限された部分信頼セキュリティ サンドボックスで実行する必要があります。 したがって、実装ではインターネット ゾーン内でサポートされている WPF 要素のサブセットをサポートするか、アプリケーションのアクセス許可を昇格させる必要があります。 詳細については、[セキュリティ](../security-wpf.md)に関するページをご覧ください。

 <xref:System.Windows.Controls.WebBrowser> コントロールをアプリケーションで使用する場合、内部的には WPF によってネイティブ WebBrowser ActiveX コントロールがインスタンス化されます。 アプリケーションが Internet Explorer で実行されている部分信頼 XBAP である場合、ActiveX コントロールは Internet Explorer プロセスの専用スレッドで実行されます。 このため、次の制限が適用されます。

- <xref:System.Windows.Controls.WebBrowser> コントロールでは、セキュリティ上の制限など、ホスト ブラウザーに似た動作を提供する必要があります。 このようなセキュリティ上の制限の中には、Internet Explorer のセキュリティ設定を使用して制御できるものがあります。 詳細については、[セキュリティ](../security-wpf.md)に関するページをご覧ください。

- XBAP が HTML ページでドメインをまたいでロードされると、例外がスローされます。

- 入力が WPF <xref:System.Windows.Controls.WebBrowser> とは別のスレッドで行われるため、キーボード入力をインターセプトできず、IME の状態が共有されません。

- ナビゲーションのタイミングまたは順序は、ActiveX コントロールが他のスレッド上で実行されるため異なることがあります。 たとえば、ページへの移動が、必ずしも別のナビゲーション要求の開始によって取り消されるとは限りません。

- WPF アプリケーションが独立したスレッドで実行されるため、カスタムの ActiveX コントロールに通信の問題が発生することがあります。

- <xref:System.Windows.Interop.HwndHost> が他のスレッドまたはプロセスで、実行中のウィンドウをサブクラス化できないため、<xref:System.Windows.Interop.HwndHost.MessageHook> は発生しません。

### <a name="creating-a-full-trust-xbap"></a>完全な信頼の XBAP の作成
 XBAP で完全な信頼が必要な場合、プロジェクトを変更してこのアクセス許可を有効にできます。 完全な信頼を有効にする手順を次に示します。

1. Visual Studio でプロジェクトのプロパティを開きます。

2. **[セキュリティ]** タブで、 **[これは完全に信頼するアプリケーションです]** をクリックします。

 この設定により、次の変更が実行されます。

- プロジェクト ファイル内の `<TargetZone>` 要素の値が `Custom` に変更される。

- アプリケーション マニフェスト (app.manifest) の `Unrestricted="true"` 属性が <xref:System.Security.PermissionSet> 要素に追加される。

    ```xml
    <PermissionSet class="System.Security.PermissionSet"
                   version="1"
                   ID="Custom"
                   SameSite="site"
                   Unrestricted="true" />
    ```

### <a name="deploying-a-full-trust-xbap"></a>完全な信頼の XBAP の配置
 ClickOnce 信頼済み配置モデルに従っていない完全な信頼の XBAP を配置する場合、ユーザーがアプリケーションを実行するときの動作は、セキュリティ ゾーンによって異なります。 ユーザーがアプリケーションをインストールしようとすると警告が表示されることもあります。 ユーザーは、インストールを続行するか取り消すかを選択できます。 次の表は、各セキュリティ ゾーンのアプリケーション動作と、完全な信頼を受け取るアプリケーションで行う必要のある操作を示しています。

|セキュリティ ゾーン|動作|完全信頼を受け取るための操作|
|-------------------|--------------|------------------------|
|ローカル コンピューター|完全な信頼を自動的に受け取る|アクションは必要ありません。|
|イントラネットおよび信頼済みサイト|完全な信頼のプロンプトを表示する|プロンプトにソースが表示されるように、証明書を使用して XBAP に署名します。|
|インターネット|"信頼されていません" というメッセージが表示され、失敗する|証明書を使用して XBAP に署名します。|

> [!NOTE]
> 前の表で説明した動作は、ClickOnce 信頼済み配置モデルに従っていない完全な信頼の XBAP の動作です。

 完全な信頼の XBAP を配置する場合は、ClickOnce 信頼済み配置モデルを使用することをお勧めします。 このモデルにより、セキュリティ ゾーンに関係なく、完全な信頼を XBAP に自動的に付与できるため、ユーザーにプロンプトが表示されることはありません。 このモデルの一部として、信頼された発行元からの証明書を使用して、アプリケーションに署名する必要があります。 細については、「[信頼されたアプリケーションの配置の概要](/visualstudio/deployment/trusted-application-deployment-overview)」および「[Introduction to Code Signing (コード署名の概要)](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537361(v=vs.85))」を参照してください。

<a name="xbap_start_time_performance_considerations"></a>
## <a name="xbap-start-time-performance-considerations"></a>XBAP 起動時のパフォーマンスに関する考慮事項
 XBAP のパフォーマンスにとって重要なのは、その起動時にあります。 最初に読み込む WPF アプリケーションが XBAP である場合は、"*コールド スタート*" に 10 秒以上かかることがあります。 これは、進行状況ページは WPF によってレンダリングされますが、アプリケーションを表示するには CLR と WPF の両方をコールド スタートする必要があるためです。

 .NET Framework 3.5 SP1 以降、XBAP のコールド スタート時間は、アンマネージ進行状況ページを配置サイクルの初期に表示することで短縮されています。 進行状況ページは、ネイティブ ホスティング コードによって表示され、HTML でレンダリングされます。このため、ほぼアプリケーションの起動直後に表示されます。

 さらに、ClickOnce のダウンロード シーケンスのコンカレンシーの改良によって、開始時間は最大 10% 短縮されます。 ClickOnce でマニフェストがダウンロードされて評価された後、アプリケーションのダウンロードが始まり、進行状況バーの更新が開始されます。

## <a name="see-also"></a>関連項目

- [Visual Studio を構成して Web サービスを呼び出す XAML ブラウザー アプリケーションをデバッグする](configure-vs-to-debug-a-xaml-browser-to-call-a-web-service.md)
- [WPF アプリケーションの配置](deploying-a-wpf-application-wpf.md)
