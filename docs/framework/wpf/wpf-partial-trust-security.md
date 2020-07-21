---
title: 部分信頼セキュリティ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- partial trust security [WPF]
- detecting permissions [WPF]
- security settings for Internet Explorer [WPF]
- partial trust applications [WPF], debugging
- permissions [WPF], managing
- debugging partial trust applications [WPF]
- permissions [WPF], detecting
- feature security requirements [WPF]
- managing permissions [WPF]
ms.assetid: ef2c0810-1dbf-4511-babd-1fab95b523b5
ms.openlocfilehash: 99c7d9cfae2b137053ca77d9e3d7055b4674ce5b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174577"
---
# <a name="wpf-partial-trust-security"></a>WPF 部分信頼セキュリティ
<a name="introduction"></a> 一般的に、インターネット アプリケーションでは、悪意による損害を防ぐため、重要なシステム リソースへの直接アクセスを制限する必要があります。 既定では、HTML およびクライアント側のスクリプト言語では、重要なシステム リソースにアクセスできません。 ブラウザーでホストされる Windows Presentation Foundation (WPF) アプリケーションは、ブラウザーから起動できるため、同様の一連の制限に準拠している必要があります。 これらの制限を適用するため、WPF ではコード アクセス セキュリティ (CAS) と ClickOnce の両方が使用されます (詳細については、「[WPF のセキュリティ方針 - プラットフォーム セキュリティ](wpf-security-strategy-platform-security.md)」を参照してください)。 既定では、ブラウザーでホストされるアプリケーションは、インターネット、ローカル イントラネット、またはローカル コンピューターのどこから起動するかに関係なく、インターネット ゾーンの一連の CAS 権限が要求されます。 アクセス許可がフルセットで付与されていないアプリケーションは、部分信頼で実行されている、と言います。  
  
 WPF には、可能な限り多くの機能を部分信頼で安全にできるようにするさまざまなサポートが用意されています。また、CAS と共に、部分信頼プログラミングのサポートが追加されています。  
  
 このトピックは、次のセクションで構成されています。  
  
- [WPF 機能の部分信頼のサポート](#WPF_Feature_Partial_Trust_Support)  
  
- [部分信頼プログラミング](#Partial_Trust_Programming)  
  
- [アクセス許可の管理](#Managing_Permissions)  
  
<a name="WPF_Feature_Partial_Trust_Support"></a>
## <a name="wpf-feature-partial-trust-support"></a>WPF 機能の部分信頼のサポート  
 次の表は、インターネット ゾーンのアクセス許可セットの制限内で安全に使用できる Windows Presentation Foundation (WPF) の高度な機能を示しています。  
  
 表 1:部分信頼で安全な WPF 機能  
  
|機能分野|機能|  
|------------------|-------------|  
|全般|ブラウザー ウィンドウ<br /><br /> 起点サイト アクセス<br /><br /> IsolatedStorage (512KB 制限)<br /><br /> UIAutomation プロバイダー<br /><br /> コマンド実行<br /><br /> 入力方式エディター (IME)<br /><br /> タブレットのスタイラスとインク<br /><br /> マウス キャプチャおよび移動イベントを使用した、シミュレートされたドラッグ アンド ドロップ<br /><br /> OpenFileDialog<br /><br /> XAML 逆シリアル化 (XamlReader.Load 経由)|  
|Web 統合|ブラウザーのダウンロード ダイアログ<br /><br /> ユーザーが開始したトップ レベルのナビゲーション<br /><br /> mailto: リンク<br /><br /> Uniform Resource Identifier パラメーター<br /><br /> HTTPWebRequest<br /><br /> IFRAME でホストされている WPF コンテンツ<br /><br /> Frame を使用した同一サイトの HTML ページのホスト<br /><br /> WebBrowser を使用した同一サイトの HTML ページのホスト<br /><br /> Web サービス (ASMX)<br /><br /> Web サービス (Windows Communication Foundation を使用)<br /><br /> [スクリプティング]<br /><br /> ドキュメント オブジェクト モデル|  
|ビジュアル|2D と 3D<br /><br /> アニメーション<br /><br /> メディア (起点サイトとクロス ドメイン)<br /><br /> イメージング/オーディオ/動画|  
|読み取り|FlowDocument<br /><br /> XPS ドキュメント<br /><br /> 埋め込みフォントとシステム フォント<br /><br /> CFF フォントと TrueType フォント|  
|編集|スペル チェック<br /><br /> RichTextBox<br /><br /> プレーン テキストとインク クリップボードのサポート<br /><br /> ユーザーが開始した貼り付け<br /><br /> 選択したコンテンツのコピー|  
|コントロール|一般的なコントロール|  
  
 この表では、大まかな WPF 機能について説明します。 より詳細な情報については、Windows SDK ドキュメントに記載されている、WPF の各メンバーで必要なアクセス許可を参照してください。 また、次の機能には、特別な考慮事項など、部分的な信頼の実行に関する詳細情報が含まれています。  
  
- [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] ([XAML の概要 (WPF)](../../desktop-wpf/fundamentals/xaml.md) を参照)  
  
- ポップアップ (<xref:System.Windows.Controls.Primitives.Popup?displayProperty=nameWithType> を参照)  
  
- ドラッグ アンド ドロップ (「[ドラッグ アンド ドロップの概要](./advanced/drag-and-drop-overview.md)」を参照)  
  
- クリップボード (<xref:System.Windows.Clipboard?displayProperty=nameWithType> を参照)  
  
- イメージング (<xref:System.Windows.Controls.Image?displayProperty=nameWithType>を参照)  
  
- シリアル化 (<xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType> および <xref:System.Windows.Markup.XamlWriter.Save%2A?displayProperty=nameWithType> を参照)  
  
- [ファイルを開く] ダイアログ ボックス (<xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType> を参照)  
  
 次の表は、インターネット ゾーンのアクセス許可セットの制限内で実行するのが安全ではない WPF 機能の概要を示しています。  
  
 表 2:部分信頼では安全でない WPF 機能  
  
|機能分野|機能|  
|------------------|-------------|  
|全般|ウィンドウ (アプリケーション定義のウィンドウおよびダイアログ ボックス)<br /><br /> SaveFileDialog<br /><br /> ファイル システム<br /><br /> レジストリへのアクセス<br /><br /> ドラッグ アンド ドロップ<br /><br /> XAML シリアル化 (XamlWriter.Save 経由)<br /><br /> UIAutomation クライアント<br /><br /> ソース ウィンドウへのアクセス (HwndHost)<br /><br /> 完全な音声サポート<br /><br /> Windows フォームの相互運用性|  
|ビジュアル|ビットマップ効果<br /><br /> 画像のエンコード|  
|編集|リッチ テキスト形式のクリップボード<br /><br /> 完全な XAML サポート|  
  
<a name="Partial_Trust_Programming"></a>
## <a name="partial-trust-programming"></a>部分信頼プログラミング  
 XBAP アプリケーションの場合、既定のアクセス許可セットを超えるコードの動作は、セキュリティ ゾーンによって異なります。 ユーザーがアプリケーションをインストールしようとすると警告が表示されることもあります。 ユーザーは、インストールを続行するか取り消すかを選択できます。 次の表は、各セキュリティ ゾーンのアプリケーション動作と、完全な信頼を受け取るアプリケーションで行う必要のある操作を示しています。  
  
|セキュリティ ゾーン|動作|完全信頼を受け取るための操作|  
|-------------------|--------------|------------------------|  
|ローカル コンピューター|完全な信頼を自動的に受け取る|アクションは必要ありません。|  
|イントラネットおよび信頼済みサイト|完全な信頼のプロンプトを表示する|プロンプトにソースが表示されるように、証明書を使用して XBAP に署名します。|  
|インターネット|"信頼されていません" というメッセージが表示され、失敗する|証明書を使用して XBAP に署名します。|  
  
> [!NOTE]
> 前の表で説明した動作は、ClickOnce 信頼済み配置モデルに従わない完全な信頼の XBAP の動作です。  
  
 一般に、許可されているアクセス許可を超える可能性のあるコードは、おそらく、スタンドアロン アプリケーション間、およびブラウザーでホストされるアプリケーション間の両方で共有される共通コードです。 CAS と WPF は、このシナリオを管理するためのいくつかの手法を提供します。  
  
<a name="Detecting_Permissions_using_CAS"></a>
### <a name="detecting-permissions-using-cas"></a>CAS を使用してアクセス許可を検出する  
 場合によっては、ライブラリ アセンブリの共有コードをスタンドアロン アプリケーションと XBAP の両方で使用できます。 このような場合、コードによって、アプリケーションに付与されているアクセス許可セットよりも多くのアクセス許可を必要とする機能が実行される可能性があります。 アプリケーションでは、Microsoft .NET Framework セキュリティを使用して特定のアクセス許可があるかどうかを検出できます。 具体的には、必要なアクセス許可のインスタンスで <xref:System.Security.CodeAccessPermission.Demand%2A> メソッドを呼び出すことによって、特定のアクセス許可があるかどうかをテストできます。 これを次の例に示します。この例には、ファイルをローカル ディスクに保存できるアクセス許可があるかどうかをクエリするコードが含まれています。  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandling.cs#detectpermscode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandling.vb#detectpermscode2)]  
  
 アプリケーションに必要なアクセス許可がない場合、<xref:System.Security.CodeAccessPermission.Demand%2A> を呼び出すと、セキュリティ例外がスローされます。 それ以外の場合は、アクセス許可が付与されています。 `IsPermissionGranted` はこの動作をカプセル化し、必要に応じて `true` または `false` を返します。  
  
<a name="Graceful_Degradation_of_Functionality"></a>
### <a name="graceful-degradation-of-functionality"></a>機能の適切な低下  
 コードに必要な操作を実行するためのアクセス許可があるかどうかを検出することは、異なるゾーンから実行できるコードにおいては重要です。 ゾーンを検出することもできますが、可能であれば、ユーザーに代替手段を提供することをお勧めします。 たとえば、完全信頼アプリケーションでは、通常、ユーザーは任意の場所にファイルを作成できますが、一方で部分信頼アプリケーションでは、分離ストレージにのみファイルを作成できます。 ファイルを作成するコードが、完全信頼 (スタンドアロン) アプリケーションと部分信頼 (ブラウザーでホストされる) アプリケーションの両方で共有されるアセンブリに存在し、両方のアプリケーションでユーザーがファイルを作成できるようにする場合は、適切な場所にファイルを作成する前に、共有コードが部分信頼または完全な信頼のどちらで実行されているかどうかを検出する必要があります。 次のコードは、これら両方を示しています。  
  
 [!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode1)]
 [!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode1)]  
[!code-csharp[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/csharp/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/CSharp/FileHandlingGraceful.cs#detectpermsgracefulcode2)]
[!code-vb[PartialTrustSecurityOverviewSnippets#DetectPermsGracefulCODE2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PartialTrustSecurityOverviewSnippets/VisualBasic/FileHandlingGraceful.vb#detectpermsgracefulcode2)]  
  
 多くの場合、部分信頼の代替を見つけることができるはずです。  
  
 イントラネットなどの制御された環境では、カスタム マネージド フレームワークをクライアント ベース全体でグローバル アセンブリ キャッシュ (GAC) にインストールできます。 これらのライブラリでは、完全な信頼を必要とするコードを実行できます。また、<xref:System.Security.AllowPartiallyTrustedCallersAttribute> を使用して、部分信頼のみ許可されているアプリケーションから参照できます (詳細については、[セキュリティ](security-wpf.md)に関する記事と、「[WPF のセキュリティ方針 - プラットフォーム セキュリティ](wpf-security-strategy-platform-security.md)」を参照してください)。  
  
<a name="Browser_Host_Detection"></a>
### <a name="browser-host-detection"></a>ブラウザー ホストの検出  
 アクセス許可ごとに確認する必要がある場合は、CAS を使用してアクセス許可を確認することが適切な方法です。 ただし、この手法では通常の処理の一部として例外をキャッチすることに依存していますが、これは一般的には推奨されず、パフォーマンスの問題が発生する可能性があります。 代わりに、XAML ブラウザー アプリケーション (XBAP) がインターネット ゾーンのサンドボックス内でのみ実行されている場合は、<xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A?displayProperty=nameWithType> プロパティを使用できます。このプロパティは、XAML ブラウザー アプリケーション (XBAP) に対して true を返します。  
  
> [!NOTE]
> <xref:System.Windows.Interop.BrowserInteropHelper.IsBrowserHosted%2A> は、アプリケーションがブラウザーで実行されているかどうかを識別するだけで、アプリケーションで実行されている一連のアクセス許可は識別されません。  
  
<a name="Managing_Permissions"></a>
## <a name="managing-permissions"></a>アクセス許可の管理  
 既定では、XBAP は部分信頼 (既定のインターネット ゾーン アクセス許可セット) を使用して実行されます。 ただし、アプリケーションの要件によっては、一連のアクセス許可を既定値から変更することができます。 たとえば、XBAP をローカル イントラネットから起動した場合、次の表に示すように、引き上げられたアクセス許可セットを利用できます。  
  
 表 3:LocalIntranet とインターネットのアクセス許可  
  
|アクセス許可|属性|LocalIntranet|インターネット|  
|----------------|---------------|-------------------|--------------|  
|DNS|DNS サーバーへのアクセス|はい|いいえ|  
|環境変数|読み取り|はい|いいえ|  
|ファイル ダイアログ|開く|はい|はい|  
|ファイル ダイアログ|無制限|はい|いいえ|  
|分離ストレージ|ユーザーによるアセンブリの分離|はい|いいえ|  
|分離ストレージ|不明な分離|はい|はい|  
|分離ストレージ|無制限のユーザー クォータ|はい|いいえ|  
|Media|安全なオーディオ、動画、および画像|はい|はい|  
|印刷|既定の印刷|はい|いいえ|  
|印刷|安全な印刷|はい|はい|  
|リフレクション|出力|はい|いいえ|  
|セキュリティ|マネージド コードの実行|はい|はい|  
|セキュリティ|付与されたアクセス許可のアサート|はい|いいえ|  
|ユーザー インターフェイス|無制限|はい|いいえ|  
|ユーザー インターフェイス|安全なトップ レベルのウィンドウ|はい|はい|  
|ユーザー インターフェイス|独自のクリップボード|はい|はい|  
|Web ブラウザー|HTML への安全なフレーム ナビゲーション|はい|はい|  
  
> [!NOTE]
> 切り取りと貼り付けは、ユーザーが開始したときに部分信頼でのみ許可されます。  
  
 アクセス許可を引き上げる必要がある場合は、プロジェクトの設定と ClickOnce アプリケーション マニフェストを変更する必要があります。 詳細については、「[WPF XAML ブラウザー アプリケーションの概要](./app-development/wpf-xaml-browser-applications-overview.md)」をご覧ください。 次のドキュメントも参照してください。  
  
- [Mage.exe (マニフェスト生成および編集ツール)](../tools/mage-exe-manifest-generation-and-editing-tool.md)。  
  
- [MageUI.exe (マニフェスト生成および編集ツール、グラフィカル クライアント)](../tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client.md)。  
  
- [ClickOnce アプリケーションのセキュリティ保護](/visualstudio/deployment/securing-clickonce-applications)。  
  
 XBAP で完全な信頼が求められる場合は、同じツールを使用して、要求されたアクセス許可を引き上げることができます。 ただし、XBAP で完全な信頼が許可されるのは、ローカル コンピューター、イントラネット、またはブラウザーの信頼済みサイトまたは許可されたサイトに記載されている URL からこれがインストールされて起動している場合にのみです。 アプリケーションがイントラネットまたは信頼済みサイトからインストールされている場合、ユーザー向けに、アクセス許可が昇格された旨を通知する標準の ClickOnce プロンプトが表示されます。 ユーザーは、インストールを続行するか取り消すかを選択できます。  
  
 または、ClickOnce 信頼済みのデプロイ モデルを使用して、任意のセキュリティ ゾーンから完全に信頼された配置を行うことができます。 詳細については、「[信頼されたアプリケーションの配置の概要](/visualstudio/deployment/trusted-application-deployment-overview)」および[セキュリティ](security-wpf.md)に関する記事を参照してください。  
  
## <a name="see-also"></a>関連項目

- [セキュリティ](security-wpf.md)
- [WPF のセキュリティ方針 - プラットフォーム セキュリティ](wpf-security-strategy-platform-security.md)
- [WPF のセキュリティ方針 - セキュリティ エンジニアリング](wpf-security-strategy-security-engineering.md)
