---
title: SOAP エンドポイントおよび HTTP エンドポイント
ms.date: 03/30/2017
ms.assetid: e3c8be75-9dda-4afa-89b6-a82cb3b73cf8
ms.openlocfilehash: fee1df86026716941f65dccca15d437ae917770b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84600946"
---
# <a name="soap-and-http-endpoints"></a>SOAP エンドポイントおよび HTTP エンドポイント
このサンプルでは、WCF Web プログラミングモデルを使用して、RPC ベースのサービスを実装し、SOAP 形式および "Plain Old XML" (POX) 形式で公開する方法を示します。 サービスの HTTP バインディングの詳細については、「[基本的な Http サービス](basic-http-service.md)のサンプル」を参照してください。 このサンプルでは、さまざまなバインドを使用して SOAP および HTTP で RPC ベースのサービスを公開する方法について詳しく示します。  
  
## <a name="demonstrates"></a>対象  
 WCF を使用して SOAP および HTTP 経由で RPC サービスを公開する。  
  
## <a name="discussion"></a>ディスカッション  
 このサンプルは2つのコンポーネントで構成されています。 WCF サービスを含む Web アプリケーションプロジェクト (サービス) と、SOAP および HTTP バインディングを使用してサービス操作を呼び出すコンソールアプリケーション (クライアント) です。  
  
 WCF サービスは、 `GetData` `PutData` 入力として渡された文字列をエコーする2つの操作 (と) を公開します。 サービス操作には、<xref:System.ServiceModel.Web.WebGetAttribute> および <xref:System.ServiceModel.Web.WebInvokeAttribute> を使用して注釈が付けられます。 これらの属性は、これらの操作の HTTP 投影を制御します。 また、サービス操作には、<xref:System.ServiceModel.OperationContractAttribute> を使用して注釈が付けられます。この属性では、サービス操作を SOAP バインディングで公開できます。 サービスの `PutData` メソッドは <xref:System.ServiceModel.Web.WebFaultException> をスローします。この例外は、HTTP では HTTP ステータス コードを使用して返送され、SOAP では SOAP エラーとして返送されます。  
  
 Web.config ファイルは、3つのエンドポイントを使用して WCF サービスを構成します。  
  
- SOAP ベースのクライアントからアクセスするためのサービス メタデータを公開する ~/service.svc/mex エンドポイント  
  
- クライアントが HTTP バインディングを使用してサービスにアクセスできる ~/service.svc/http エンドポイント  
  
- クライアントが HTTP バインディングで SOAP を使用してサービスにアクセスできる ~/service.svc/soap endpoint エンドポイント  
  
 HTTP エンドポイントは、<> 標準エンドポイントで構成され、がに設定されてい `webHttp` `helpEnabled` `true` ます。 その結果、サービスは、HTTP ベースのクライアントがサービスにアクセスするために使用できる、XHTML ベースのヘルプ ページ (~/service.svc/http/help) を公開します。  
  
 クライアントプロジェクトは、(**サービス参照の追加**によって生成された) SOAP プロキシを使用してサービスにアクセスし、を使用してサービスにアクセスする方法を示して <xref:System.Net.WebClient> います。  
  
 サンプルは、1 つの Web ホスト サービスと 1 つのコンソール アプリケーションで構成されています。 コンソール アプリケーションが実行されると、クライアントはサービスに要求を発行し、応答からの適切な情報をコンソール ウィンドウに書き込みます。  
  
#### <a name="to-run-the-sample"></a>サンプルを実行するには  
  
1. SOAP および HTTP エンドポイント サンプルのソリューションを開きます。  
  
2. Ctrl + Shift + B キーを押して、ソリューションをビルドします。  
  
3. まだ開いていない場合は、CTRL + W、S キーを押して、[**ソリューションエクスプローラー** ] ウィンドウを開きます。  
  
4. [**ソリューションエクスプローラー** ] ウィンドウで**サービス**プロジェクトを右クリックし、[**デバッグ**] コンテキストメニューオプションの上にカーソルを置き、[**新しいインスタンスを開始**] コンテキストメニューが表示されるようにします。 [**新しいインスタンスを開始**] をクリックします。 これで、サービスをホストする ASP.NET 開発サーバーが起動します。  
  
5. ソリューションエクスプローラーウィンドウで、クライアントプロジェクトを右クリックし、[**デバッグ**] コンテキストメニューオプションの上にカーソルを置き、[**新しいインスタンスを開始**] コンテキストメニューが表示されるようにします。 [**新しいインスタンスを開始**] をクリックします。  
  
6. クライアント コンソール ウィンドウが表示されて、実行中のサービスの URI および実行中のサービスの HTML ヘルプ ページの URI が示されます。 ブラウザーでヘルプ ページの URI を入力することで、いつでも HTML ヘルプ ページを表示することができます。  
  
7. サンプルが実行されると、クライアントは現在のアクティビティのステータスを書き込みます。  
  
8. クライアント コンソール アプリケーションを終了するには、任意のキーを押します。  
  
9. サービスのデバッグを停止するには、Shift キーを押しながら F5 キーを押します。  
  
10. Windows 通知領域で、ASP.NET development サーバーアイコンを右クリックし、コンテキストメニューの [**停止**] をクリックします。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) とサンプルをダウンロードして [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ください。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Web\SoapAndHttpEndpoints`
