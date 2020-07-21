---
title: WCF Visual Studio テンプレート
ms.date: 03/30/2017
ms.assetid: 6a608575-3535-4190-89da-911e24c8374f
ms.openlocfilehash: 13183ad5f05350c34eebd025eca3faa7d97644f8
ms.sourcegitcommit: d9470d8b2278b33108332c05224d86049cb9484b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81608024"
---
# <a name="wcf-visual-studio-templates"></a>WCF Visual Studio テンプレート
Windows 通信基礎 (WCF) Visual Studio テンプレートは、定義済みのプロジェクトと項目のテンプレートで、WCF サービスと周辺アプリケーションをすばやく構築するために Visual Studio で使用できます。  
  
## <a name="using-the-wcf-templates"></a>WCF テンプレートの使用  
 WCF Visual Studio テンプレートは、サービス開発のための基本的なクラス構造を提供します。 これには、サービス コントラクト、データ コントラクト、サービス実装、および構成の基本的な定義が含まれます。 これらのテンプレートを使用すると、最小限のコードを使用した単純なサービスや、より高度なサービスのビルド ブロックを作成できます。  
  
### <a name="wcf-service-library-project-template"></a>WCF サービス ライブラリ プロジェクト テンプレート  
 WCF サービス ライブラリ プロジェクト テンプレートは、新しいプロジェクト ダイアログ ボックスの **[Visual C#\WCF]** および **[Visual Basic\WCF]** の下で使用できます。  
  
 **WCF サービス**テンプレートを使用して新しいプロジェクトを作成すると、新しいプロジェクトには、次の 3 つのファイルが自動的に含まれます。  
  
- サービス コントラクト ファイル (IService1.cs または IService1.vb)。 サービス コントラクト ファイルは、WCF サービス属性が適用されたインターフェイスです。 このファイルには、サービスの定義方法を示す単純なサービスの定義が含まれています。その他に、パラメーター ベースの操作や、単純なデータ コントラクトのサンプルも含まれています。 これは、WCF サービス プロジェクトを作成した後にコード エディターに表示される既定のファイルです。  
  
- サービス実装ファイル (Service1.cs または Service1.vb)。 サービス実装ファイルは、サービス コントラクト ファイルに定義されているコントラクトを実装します。  
  
- アプリケーション構成ファイル (App.config)。 構成ファイルは、セキュリティで保護された HTTP バインディングを使用して、WCF サービス モデルの基本要素を提供します。 サービスのエンドポイントも含まれており、メタデータの交換も可能です。  
  
> [!NOTE]
> 既定の構成である[WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)を使用して実行される場合、プロジェクトの構成ファイルとして App.config ファイルを認識するように構成されています。 サービス ライブラリを実行可能ファイルでホストする場合は、DLL の構成ファイルは無効になるため、その実行可能ファイルの構成ファイルに構成コードを移動する必要があります。  
  
### <a name="wcf-service-application-template"></a>WCF サービス アプリケーション テンプレート  
 WCF サービス アプリケーション テンプレートは、[新しいプロジェクト] ダイアログ ボックスの **[Visual C#\WCF]** および **[Visual Basic\WCF]** の下にあります。  
  
 **WCF Web アプリケーション サービス**テンプレートを使用して新しいプロジェクトを作成すると、プロジェクトには次の 4 つのファイルが含まれます。  
  
- サービス ホスト ファイル (service1.svc)。  
  
- サービス コントラクト ファイル (IService1.cs または IService1.vb)。  
  
- サービス実装ファイル (Service1.svc.cs または Service1.svc.vb)。  
  
- Web 構成ファイル (Web.config)。  
  
 このテンプレートでは、自動的に Web サイトが作成されて (仮想ディレクトリに配置されます)、サービスがホストされます。  
  
### <a name="wcf-web-site-template"></a>WCF Web サイト テンプレート  
 WCF Web サイト テンプレートは、[新しいプロジェクト] ダイアログ ボックスの **[Visual C#\Web サイト\WCF サービス**] および **[Visual Basic\Web サイト\WCF サービス**] の下にあります。 これによって、WCF サービス アプリケーションのテンプレートと同じファイルが作成されますが、ASP.NET Web サイトであるかのように編成されます。 App_Code フォルダーと App_Data フォルダーが作成されます。  
  
### <a name="wcf-service-item-template"></a>WCF サービス項目テンプレート  
 WCF サービス項目テンプレートは、既存の Visual Studio プロジェクトに WCF サービスを追加する簡単な方法を提供するカスタム テンプレートです。  
  
 このテンプレートを使用するには、[ソリューション**エクスプローラー** ] ウィンドウに移動し、プロジェクト名を右クリックして **[追加**] をポイントし、[**新しい項目**] をクリックして **[新しい項目の追加**] ダイアログ ボックスを開きます。  
  
 サービス インターフェイス ファイルとサービス実装ファイルがルート プロジェクト フォルダーに配置されます。  
  
 このテンプレートでは、新しいサービスの構成セクションが既存の構成ファイルと互換性がある場合にそれらがマージされます。  
  
 既存のプロジェクトが Web プロジェクトの場合は、サービス ホスト ファイル (service1.svc) も作成されます。  
  
### <a name="wcf-wf-service-project-and-item-template"></a>WCF WF サービス プロジェクト/項目テンプレート  
 これらのテンプレートは、Web サービスのようにアクセスできるワークフローであるワークフロー サービスをホストする WCF サービスを作成します。 この他に、XAML プログラミング モデルや命令型プログラミング モデルのテンプレートも用意されています。 これらのテンプレートを使用すると、シーケンシャル ワークフローやステート マシン ワークフローを作成できます。 これらのワークフローの詳細については[、「[方法] ワークフローを作成する](../windows-workflow-foundation/how-to-create-a-workflow.md)」を参照してください。 ワークフロー プロジェクトの作成の詳細については、「[従来のワークフロー プロジェクトの作成](/visualstudio/workflow-designer/developing-applications-with-the-workflow-designer)」を参照してください。  
  
 コード ベースのワークフローではなく XOML 型ワークフローを使用する場合、Visual Studio デザイナーの方が応答性が高くなります。 XOML ワークフローは、既定で作成されるワークフロー型です。  
  
### <a name="wcf-syndication-service-library-template"></a>WCF 配信サービス ライブラリ テンプレート  
 このテンプレートを使用すると、フィードを RSS または ATOM 形式で WCF サービスとして公開できます。 詳細については、「 [WCF 配信](./feature-details/wcf-syndication.md)」を参照してください。  
  
#### <a name="changing-the-address-of-the-feed"></a>フィードのアドレスの変更  
 配信テンプレートは、実行中に Internet Explorer を使用します。 Visual Studio の**ソリューション エクスプローラー**でプロジェクトを右クリックし、[**プロパティ ]** を選択し、[**デバッグ**] タブを選択すると、テンプレートの既定のアドレスを確認できます。 Internet Explorer は、このアドレスにあるフィードを開きます。  
  
 フィードのアドレスを変更する場合は、[**デバッグ**] タブでもアドレスを変更する必要があります。これを行わない場合、Internet Explorer は既定のアドレスでフィードを開こうとし、失敗します。  
  
### <a name="ajax-enabled-wcf-service-item-template"></a>AJAX 対応 WCF サービス項目テンプレート  
 このテンプレートは、WCF サービスとして AJAX コントロールを公開します。 AJAX コントロールの詳細については、 [AJAX コントロールのドキュメントを参照してください](/aspnet/ajax/)。  
  
### <a name="silverlight-enabled-wcf-service-item-template"></a>Silverlight 対応 WCF サービス項目テンプレート  
 このテンプレートは、Silverlight クライアントまたはフロントエンドにデータを提供する Web サービスを作成します。 テンプレートを Web サイトまたは Web アプリケーション プロジェクトに追加して、サービス コードと Silverlight クライアントとの通信をサポートする構成を含む WCF サービスを作成できます。 その後、[**サービス参照の追加]** を使用して、サービスのクライアント プロキシをクライアントに追加し、Silverlight クライアントと Silverlight 対応 WCF サービス間でデータを交換できます。  
  
 このテンプレートにアクセスするには、**ソリューション エクスプローラ**で Web サイトまたは Web アプリケーション プロジェクトを右クリックし、[**新しい項目の追加**]**をクリックします**。  
  
> [!NOTE]
> Silverlight 対応 WCF サービスは、セキュリティ設定を一切有効にせずに `basicHttpBinding` エンドポイントを公開します。 したがって、サービスに接続しているすべてのクライアントが、このサービスに関する情報を取得できることになります。 また、サービスとクライアント間で交換されるメッセージの署名と暗号化も行われません。 エンドポイントを正しくセキュリティで保護するには、ASP.NET 認証や HTTPS などのメカニズムを使用する必要があります。  
  
## <a name="see-also"></a>関連項目

- [WCF サービス ホスト (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [WCF のテスト用クライアント (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
