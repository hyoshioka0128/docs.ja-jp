---
title: セキュリティ
ms.date: 03/30/2017
helpviewer_keywords:
- XAML files [WPF], sandbox behavior
- browser-hosted application security [WPF]
- application security [WPF]
- navigation security [WPF]
- loose XAML files [WPF], sandbox behavior
- WPF security [WPF]
- WebBrowser control [WPF], security
- feature controls [WPF], security
- XBAP security [WPF]
- Internet Explorer security settings [WPF]
ms.assetid: ee1baea0-3611-4e36-9ad6-fcd5205376fb
ms.openlocfilehash: e0a56dcbf8d151fcb0d4f6271ecba15c0ff955a4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174616"
---
# <a name="security-wpf"></a>セキュリティ (WPF)
<a name="introduction"></a>Windows Presentation Foundation (WPF) スタンドアロン アプリケーションとブラウザーでホストされるアプリケーションを開発する際に、セキュリティ モデルを検討する必要があります。 WPF スタンドアロン アプリケーションは、Windows インストーラー (.msi)、XCopy、または ClickOnce のどれを使用して配置する場合でも、無制限のアクセス許可 (CAS**FullTrust** アクセス許可セット) で実行されます。 部分的に信頼されたスタンドアロンの WPF アプリケーションを ClickOnce で展開することはサポートされていません。 ただし、完全に信頼されたホスト アプリケーションでは、.NET Framework アドイン モデルを使用して、部分的に信頼された <xref:System.AppDomain> を作成することができます。 詳細については、「[WPF アドインの概要](./app-development/wpf-add-ins-overview.md)」を参照してください。  
  
 ブラウザーでホストされる WPF アプリケーションは Windows Internet Explorer または Firefox によってホストされ、XAML ブラウザー アプリケーション (XBAP) または Loose [!INCLUDE[TLA#tla_xaml](../../../includes/tlasharptla-xaml-md.md)] ドキュメントにすることができます。詳細については、「[WPF XAML ブラウザー アプリケーションの概要](./app-development/wpf-xaml-browser-applications-overview.md)」を参照してください。  
  
 ブラウザーでホストされる WPF アプリケーションは部分信頼セキュリティ サンドボックス内で実行され、既定では、既定の CAS**Internet** ゾーン アクセス許可セットに限定されています。 これは、一般的な Web アプリケーションの分離と同じ方法で、ブラウザーでホストされる WPF アプリケーションをクライアント コンピューターから効果的に分離できます。 XBAP は、デプロイメント URL およびクライアントのセキュリティ構成のセキュリティ ゾーンに基づいて、完全な信頼まで特権を昇格することができます。 詳細については、「[WPF 部分信頼セキュリティ](wpf-partial-trust-security.md)」を参照してください。  
  
 このトピックでは、Windows Presentation Foundation (WPF) のスタンドアロン アプリケーションとブラウザーでホストされるアプリケーションのセキュリティ モデルについて説明します。  
  
 このトピックは、次のセクションで構成されています。  
  
- [安全なナビゲーション](#SafeTopLevelNavigation)  
  
- [Web ブラウザーのセキュリティ設定](#InternetExplorerSecuritySettings)  
  
- [WebBrowser コントロールと機能コントロール](#webbrowser_control_and_feature_controls)  
  
- [部分信頼クライアント アプリケーションに対する APTCA の無効化](#APTCA)  
  
- [Loose XAML ファイルに対するサンドボックスの動作](#LooseContentSandboxing)  
  
- [セキュリティを向上する WPF アプリケーションを開発するためのリソース](#BestPractices)  
  
<a name="SafeTopLevelNavigation"></a>
## <a name="safe-navigation"></a>安全なナビゲーション  
 XBAP では、WPF はアプリケーションとブラウザーという 2 種類のナビゲーションを区別します。  
  
 *アプリケーション ナビゲーション*は、ブラウザーによってホストされるアプリケーション内のコンテンツ項目間のナビゲーションです。 *ブラウザー ナビゲーション*は、ブラウザー自体のコンテンツとロケーション URL を変更するナビゲーションです。 アプリケーション ナビゲーション (通常は XAML) とブラウザー ナビゲーション (通常は HTML) の関係を次の図に示します。
  
 ![アプリケーション ナビゲーションとブラウザー ナビゲーションの関係。](./media/security-wpf/application-browser-navigation-relationship.png)  
  
 XBAP の移動先として安全と見なされるコンテンツの種類は、主に、アプリケーション ナビゲーションとブラウザーのナビゲーションのどちらが使用されているかで決まります。  
  
<a name="Application_Navigation_Security"></a>
### <a name="application-navigation-security"></a>アプリケーション ナビゲーションのセキュリティ  
 アプリケーション ナビゲーションが安全と見なされるのは、以下の 4 種類のコンテンツをサポートするパック URI で識別できる場合です。  
  
|コンテンツ タイプ|説明|URI の例|  
|------------------|-----------------|-----------------|  
|リソース|ビルドの種類が **Resource** のプロジェクトに追加されるファイル。|`pack://application:,,,/MyResourceFile.xaml`|  
|Content|ビルドの種類が **Content** のプロジェクトに追加されるファイル。|`pack://application:,,,/MyContentFile.xaml`|  
|起点サイト|ビルドの種類が **None** のプロジェクトに追加されるファイル。|`pack://siteoforigin:,,,/MySiteOfOriginFile.xaml`|  
|アプリケーション コード|コンパイルされたコード分離を含む XAML リソース。<br /><br /> \- または -<br /><br /> ビルドの種類が **Page** のプロジェクトに追加される XAML ファイル。|`pack://application:,,,/MyResourceFile` `.xaml`|  
  
> [!NOTE]
> アプリケーション データ ファイルとパック URI の詳細については、「[WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](./app-development/wpf-application-resource-content-and-data-files.md)」を参照してください。  
  
 これらのコンテンツ タイプのファイルは、ユーザーまたはプログラムを使用して移動できます。  
  
- **ユーザー ナビゲーション**。 ユーザーは <xref:System.Windows.Documents.Hyperlink> 要素をクリックして移動します。  
  
- **プログラム ナビゲーション**。 アプリケーションは、たとえば <xref:System.Windows.Navigation.NavigationWindow.Source%2A?displayProperty=nameWithType> プロパティを設定するなどして、ユーザーの関与なしで移動します。  
  
<a name="Browser_Navigation_Security"></a>
### <a name="browser-navigation-security"></a>ブラウザー ナビゲーションのセキュリティ  
 ブラウザー ナビゲーションは、次の条件の下でのみ安全と見なされます。  
  
- **ユーザー ナビゲーション**。 ユーザーは、入れ子になった <xref:System.Windows.Controls.Frame> ではなく、メインの <xref:System.Windows.Navigation.NavigationWindow> 内にある <xref:System.Windows.Documents.Hyperlink> 要素をクリックして移動します。  
  
- **ゾーン**。 移動先のコンテンツが、インターネットまたはローカル イントラネット上に存在する。  
  
- **プロトコル**。 使用されるプロトコルは、**http**、**https**、**file**、または **mailto** です。  
  
 これらの条件に適合しない方法で XBAP がコンテンツに移動しようとすると、<xref:System.Security.SecurityException> がスローされます。  
  
<a name="InternetExplorerSecuritySettings"></a>
## <a name="web-browsing-software-security-settings"></a>Web ブラウザーのセキュリティ設定  
 コンピューターのセキュリティ設定によって、Web ブラウザーに付与されるアクセス権が決まります。 Web ブラウザーには、Internet Explorer や PresentationHost.exe など、[WinINet](/windows/win32/wininet/portal) API または [UrlMon](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa767916(v=vs.85)) API を使用するアプリケーションやコンポーネントがあります。  
  
 Internet Explorer には、Internet Explorer での実行が可能な、下記のような機能を構成できる仕組みを提供しています。  
  
- .NET Framework 依存コンポーネント  
  
- ActiveX コントロールおよびプラグイン  
  
- ダウンロード  
  
- [スクリプティング]  
  
- ユーザー認証  
  
 このような方法でセキュリティ保護できる機能のコレクションは、**インターネット**、**イントラネット**、**信頼済みサイト**、および**制限付きサイト**の各ゾーンでは、ゾーン単位で構成されます。 次の手順では、セキュリティ設定の構成方法について説明します。  
  
1. **[コントロール パネル]** を開きます。  
  
2. **[ネットワークとインターネット]** をクリックし、 **[インターネット オプション]** をクリックします。  
  
     [インターネット オプション] ダイアログ ボックスが表示されます。  
  
3. **[セキュリティ]** タブで、セキュリティ設定を構成するゾーンを選択します。  
  
4. **[レベルのカスタマイズ]** ボタンをクリックします。  
  
     **[セキュリティ設定]** ダイアログ ボックスが表示されるので、選択したゾーンのセキュリティ設定を構成します。  
  
     ![[セキュリティの設定] ダイアログ ボックスを示すスクリーンショット。](./media/security-wpf/windows-presentation-foundation-security-settings.png)  
  
> [!NOTE]
> [インターネット オプション] ダイアログ ボックスは、Internet Explorer から開くこともできます。 **[ツール]** をクリックし、 **[インターネット オプション]** をクリックします。  
  
 Windows Internet Explorer 7 以降では、.NET Framework に特化した次のセキュリティ設定が含まれています。  
  
- **Loose XAML**。 Internet Explorer が Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルに移動できるかどうかを制御します。 ([有効]、[無効]、および [ダイアログを表示する] オプション)。  
  
- **XAML ブラウザー アプリケーション**。 Internet Explorer が XBAP に移動してこれを実行できるかどうかを制御します。 ([有効]、[無効]、および [ダイアログを表示する] オプション)。  
  
 既定では、これらの設定は **インターネット**、**ローカル イントラネット**、および**信頼済みサイト**の各ゾーンではすべて有効になり、**制限付きサイト** ゾーンでは無効になります。  
  
<a name="Security_Settings_for_IE6_and_Below"></a>
### <a name="security-related-wpf-registry-settings"></a>セキュリティ関連の WPF レジストリの設定  
 [インターネット オプション] から使用できるセキュリティ設定以外に、セキュリティ上重要なさまざまな WPF 機能を選択的にブロックするために次のレジストリ値を使用できます。 値は次のキーで定義されます。  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\Windows Presentation Foundation\Features`  
  
 設定可能な値を次の表に示します。  
  
|値名|値型|値のデータ|  
|----------------|----------------|----------------|  
|XBAPDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|LooseXamlDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|WebBrowserDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|MediaAudioDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|MediaImageDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|MediaVideoDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
|ScriptInteropDisallow|REG_DWORD|許可しない場合は 1、許可する場合は 0。|  
  
<a name="webbrowser_control_and_feature_controls"></a>
## <a name="webbrowser-control-and-feature-controls"></a>WebBrowser コントロールと機能コントロール  
 WPF <xref:System.Windows.Controls.WebBrowser> コントロールを使用して、Web コンテンツをホストできます。 WPF <xref:System.Windows.Controls.WebBrowser> コントロールは、基になる WebBrowser ActiveX コントロールをラップします。 WPF では、WPF <xref:System.Windows.Controls.WebBrowser> コントロールを使用して信頼されていない Web コンテンツをホストするときに、アプリケーションの保護を一部サポートします。 ただし、一部のセキュリティ機能は、<xref:System.Windows.Controls.WebBrowser> コントロールを使用してアプリケーションによって直接適用する必要があります。 WebBrowser ActiveX コントロールの詳細については、[WebBrowser コントロールの概要とチュートリアル](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa752041(v=vs.85))に関する記事を参照してください。  
  
> [!NOTE]
> このセクションは、<xref:System.Windows.Controls.WebBrowser> を使用して HTML コンテンツに移動するため、<xref:System.Windows.Controls.Frame> コントロールにも適用されます。  
  
 WPF <xref:System.Windows.Controls.WebBrowser> コントロールを使用して信頼されていない Web コンテンツをホストする場合、アプリケーションでは、部分信頼 <xref:System.AppDomain> を使用して、悪意のある HTML スクリプト コードからアプリケーション コードを分離する必要があります。 これは、アプリケーションが <xref:System.Windows.Controls.WebBrowser.InvokeScript%2A> メソッドと <xref:System.Windows.Controls.WebBrowser.ObjectForScripting%2A> プロパティを使用して、ホストされているスクリプトを操作する場合に特に当てはまります。 詳細については、「[WPF アドインの概要](./app-development/wpf-add-ins-overview.md)」を参照してください。  
  
 アプリケーションで WPF <xref:System.Windows.Controls.WebBrowser> コントロールを使用する場合、セキュリティを強化して攻撃を軽減するもう 1 つの方法は、Internet Explorer 機能コントロールを有効にすることです。 機能コントロールは Internet Explorer の追加機能で、これにより、管理者および開発者は、WPF <xref:System.Windows.Controls.WebBrowser> コントロールよってラップされる WebBrowser ActiveX コントロールをホストする、Internet Explorer およびアプリケーションの機能を構成できます。 機能コントロールを構成するには、[CoInternetSetFeatureEnabled](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537168(v=vs.85)) 関数を使用するか、レジストリの値を変更します。 機能コントロールの詳細については、[機能コントロールの概要](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537184(v=vs.85))に関する記事と[インターネット機能コントロール](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/general-info/ee330720(v=vs.85))に関する記事を参照してください。  
  
 WPF <xref:System.Windows.Controls.WebBrowser> コントロールを使用するスタンドアロン WPF アプリケーションを開発している場合は、アプリケーションに対して次の機能コントロールが自動的に有効になります。  
  
|機能コントロール|  
|---------------------|  
|FEATURE_MIME_HANDLING|  
|FEATURE_MIME_SNIFFING|  
|FEATURE_OBJECT_CACHING|  
|FEATURE_SAFE_BINDTOOBJECT|  
|FEATURE_WINDOW_RESTRICTIONS|  
|FEATURE_ZONE_ELEVATION|  
|FEATURE_RESTRICT_FILEDOWNLOAD|  
|FEATURE_RESTRICT_ACTIVEXINSTALL|  
|FEATURE_ADDON_MANAGEMENT|  
|FEATURE_HTTP_USERNAME_PASSWORD_DISABLE|  
|FEATURE_SECURITYBAND|  
|FEATURE_UNC_SAVEDFILECHECK|  
|FEATURE_VALIDATE_NAVIGATE_URL|  
|FEATURE_DISABLE_TELNET_PROTOCOL|  
|FEATURE_WEBOC_POPUPMANAGEMENT|  
|FEATURE_DISABLE_LEGACY_COMPRESSION|  
|FEATURE_SSLUX|  
  
 これらの機能コントロールは無条件で有効になるため、完全信頼アプリケーションに悪影響が及ぶ場合があります。 この場合、特定のアプリケーションとそのアプリケーションがホストしているコンテンツにセキュリティ上のリスクがなければ、対応する機能コントロールを無効にできます。  
  
 機能コントロールは、WebBrowser ActiveX オブジェクトをインスタンス化するプロセスによって適用されます。 そのため、信頼されていないコンテンツに移動できるスタンドアロン アプリケーションを作成する場合は、その他の機能コントロールを有効にすることを検討すべきです。  
  
> [!NOTE]
> この推奨事項は、MSHTML および SHDOCVW ホスト セキュリティの一般的な推奨事項に基づいています。 詳細については、[MSHTML ホスト セキュリティ FAQ: パート 1](https://msrc-blog.microsoft.com/2009/04/02/the-mshtml-host-security-faq-part-i-of-ii/) に関する記事、および [MSHTML ホスト セキュリティ FAQ: パート 2](https://msrc-blog.microsoft.com/2009/04/03/the-mshtml-host-security-faq-part-ii-of-ii/) に関する記事を参照してください。  
  
 実行可能ファイルでは、レジストリ値を 1 に設定して以下の機能コントロールを有効にすることを検討してください。  
  
|機能コントロール|  
|---------------------|  
|FEATURE_ACTIVEX_REPURPOSEDETECTION|  
|FEATURE_BLOCK_LMZ_IMG|  
|FEATURE_BLOCK_LMZ_OBJECT|  
|FEATURE_BLOCK_LMZ_SCRIPT|  
|FEATURE_RESTRICT_RES_TO_LMZ|  
|FEATURE_RESTRICT_ABOUT_PROTOCOL_IE7|  
|FEATURE_SHOW_APP_PROTOCOL_WARN_DIALOG|  
|FEATURE_LOCALMACHINE_LOCKDOWN|  
|FEATURE_FORCE_ADDR_AND_STATUS|  
|FEATURE_RESTRICTED_ZONE_WHEN_FILE_NOT_FOUND|  
  
 実行可能ファイルでは、レジストリ値を 0 に設定して以下の機能コントロールを無効にすることを検討してください。  
  
|機能コントロール|  
|---------------------|  
|FEATURE_ENABLE_SCRIPT_PASTE_URLACTION_IF_PROMPT|  
  
 WPF <xref:System.Windows.Controls.WebBrowser> コントロールを含む部分信頼 XAML を Windows Internet Explorer で実行する場合、WPF は Internet Explorer プロセスのアドレス空間で WebBrowser ActiveX コントロールをホストします。 WebBrowser ActiveX コントロールは Internet Explorer プロセスでホストされるため、Internet Explorer のすべての機能コントロールは、WebBrowser ActiveX コントロールに対しても有効になります。  
  
 Internet Explorer で実行されている XBAP にも、標準のスタンドアロン アプリケーションよりも高いレベルのセキュリティが適用されます。 このセキュリティの強化の理由は、Windows Vista および Windows 7 では既定で、Internet Explorer (および WebBrowser ActiveX コントロール) が保護モードで実行されるためです。 保護モードの詳細については、「[保護モードの Internet Explorer の理解と機能](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/)」を参照してください。  
  
> [!NOTE]
> インターネット ゾーン内で、WPF <xref:System.Windows.Controls.WebBrowser> コントロールが含まれる XBAP を Firefox で実行しようとすると、<xref:System.Security.SecurityException> がスローされます。 これは、WPF セキュリティ ポリシーが原因です。  
  
<a name="APTCA"></a>
## <a name="disabling-aptca-assemblies-for-partially-trusted-client-applications"></a>部分信頼クライアント アプリケーションに対する APTCA の無効化  
 マネージド アセンブリをグローバル アセンブリ キャッシュ (GAC) にインストールした場合、ユーザーはインストールのために明示的なアクセス許可を提供する必要があるので、これらは完全信頼になります。 完全に信頼されているため、これらを使用できるのは完全信頼マネージド クライアント アプリケーションのみです。 部分的に信頼されたアプリケーションでそれらを使用できるようにするには、<xref:System.Security.AllowPartiallyTrustedCallersAttribute> (APTCA) でマークする必要があります。 この属性は、部分信頼で実行しても安全であるとテストで確認されたアセンブリだけに設定します。  
  
 ただし、APTCA アセンブリは、GAC にインストールされた後にセキュリティの欠陥を発生させる可能性があります。 セキュリティ上の欠陥が検出されたら、アセンブリの発行者は、既存のインストールでの問題を解決し、問題発見後に発生する可能性があるインストールに備えるため、セキュリティ更新プログラムを作成できます。 更新プログラムの 1 つのオプションとして、アセンブリのアンインストールが考えられますが、その場合はこのアセンブリを使用する他の完全信頼クライアント アプリケーションを破損するおそれがあります。  
  
 WPF には、APTCA アセンブリをアンインストールせずに、部分信頼 XBAP に対して APTCA アセンブリを無効にできる仕組みが備わっています。  
  
 APTCA アセンブリを無効にするには、特殊なレジストリ キーを作成する必要があります。  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\policy\APTCA\<AssemblyFullName>, FileVersion=<AssemblyFileVersion>`  
  
 次のコードは一例を示しています。  
  
 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\policy\APTCA\aptcagac, Version=1.0.0.0, Culture=neutral, PublicKeyToken=215e3ac809a0fea7, FileVersion=1.0.0.0`  
  
 このキーにより、APTCA アセンブリのエントリが設定されます。 また、アセンブリを有効または無効にする値をこのキーに作成する必要があります。 値の詳細を次に示します。  
  
- 値の名前: **APTCA_FLAG**。  
  
- 値の型:**REG_DWORD**。  
  
- 値のデータ:無効にする場合は **1**、有効にする場合は **0**。  
  
 部分信頼クライアント アプリケーションに対してアセンブリを無効にする必要がある場合は、レジストリ キーおよび値を作成する更新プログラムを作成します。  
  
> [!NOTE]
> コア .NET Framework アセンブリは、マネージド アプリケーションを実行するために必要であるため、この方法で無効にしても影響を受けません。 APTCA アセンブリの無効化のサポートは、主にサードパーティ アプリケーションを対象にしたものです。  
  
<a name="LooseContentSandboxing"></a>
## <a name="sandbox-behavior-for-loose-xaml-files"></a>Loose XAML ファイルに対するサンドボックスの動作  
 Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルは、コードビハインド、イベント ハンドラー、またはアプリケーション固有のアセンブリに依存しない、マークアップのみの XAML ファイルです。 ブラウザーから直接 Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルに移動するときは、既定のインターネット ゾーン アクセス許可セットに基づいてセキュリティ サンドボックスに読み込まれます。  
  
 ただし、このセキュリティ動作は、loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルが <xref:System.Windows.Navigation.NavigationWindow> またはスタンドアロン アプリケーションの <xref:System.Windows.Controls.Frame> から移動した場合は異なります。  
  
 どちらの場合も、移動先の Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルは、ホスト アプリケーションのアクセス許可を継承します。 ただし、この動作はセキュリティの観点からは望ましくない場合があります。特に、Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルが信頼されていないエンティティまたは不明エンティティによって生成された場合には問題です。 このタイプのコンテンツは*外部コンテンツ*と呼ばれ、<xref:System.Windows.Controls.Frame> と <xref:System.Windows.Navigation.NavigationWindow> の両方を構成して、移動してきたときに分離するようにできます。 分離するには、次に示す例 <xref:System.Windows.Controls.Frame> と <xref:System.Windows.Navigation.NavigationWindow> の例のように、**SandboxExternalContent** プロパティを true に設定します。  
  
 [!code-xaml[SecurityOverviewSnippets#FrameMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/SecurityOverviewSnippets/CS/Window2.xaml#framemarkup)]  
  
 [!code-xaml[SecurityOverviewSnippets#NavigationWindowMARKUP](~/samples/snippets/csharp/VS_Snippets_Wpf/SecurityOverviewSnippets/CS/Window1.xaml#navigationwindowmarkup)]  
  
 このように設定すると、外部コンテンツは、アプリケーションをホストするプロセスとは異なるプロセスに読み込まれます。 このプロセスは既定のインターネット ゾーン アクセス許可セットに限定されており、ホスト アプリケーションとクライアント コンピューターから外部コンテンツを効果的に分離します。  
  
> [!NOTE]
> スタンドアロン アプリケーションでの <xref:System.Windows.Navigation.NavigationWindow> または <xref:System.Windows.Controls.Frame> からの Loose [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ファイルへの移動を、PresentationHost プロセスを含む WPF ブラウザーのホスト処理インフラストラクチャに基づいて実装しても、Windows Vista および Windows 7 上の Internet Explorer でコンテンツを直接読み込む場合 (やはり PresentationHost を使用) に比べると、セキュリティ レベルは若干低くなります。 これは、Web ブラウザーを使用しているスタンドアロン WPF アプリケーションに、Internet Explorer の保護モード セキュリティ機能が追加されていないためです。  
  
<a name="BestPractices"></a>
## <a name="resources-for-developing-wpf-applications-that-promote-security"></a>セキュリティを向上する WPF アプリケーションを開発するためのリソース  
 セキュリティを向上する WPF アプリケーションの開発に役立つその他のリソースを次に示します。  
  
|区分|リソース|  
|----------|--------------|  
|マネージド コード|[patterns & practices アプリケーション セキュリティ ガイダンス インデックス](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))|  
|CAS|[コード アクセス セキュリティ](../misc/code-access-security.md)|  
|ClickOnce|[ClickOnce のセキュリティと配置](/visualstudio/deployment/clickonce-security-and-deployment)|  
|WPF|[WPF 部分信頼セキュリティ](wpf-partial-trust-security.md)|  
  
## <a name="see-also"></a>関連項目

- [WPF 部分信頼セキュリティ](wpf-partial-trust-security.md)
- [WPF のセキュリティ方針 - プラットフォーム セキュリティ](wpf-security-strategy-platform-security.md)
- [WPF のセキュリティ方針 - セキュリティ エンジニアリング](wpf-security-strategy-security-engineering.md)
- [patterns & practices アプリケーション セキュリティ ガイダンス インデックス](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))
- [コード アクセス セキュリティ](../misc/code-access-security.md)
- [ClickOnce のセキュリティと配置](/visualstudio/deployment/clickonce-security-and-deployment)
- [XAML の概要 (WPF)](../../desktop-wpf/fundamentals/xaml.md)
