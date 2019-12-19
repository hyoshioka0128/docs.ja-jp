---
title: LINQ メッセージ クエリの関連付け
ms.date: 03/30/2017
ms.assetid: b746872e-57b1-4514-b337-53398a0e0deb
ms.openlocfilehash: a4b0ed058cfe8d3d487342c9feefdf1b1efe07c8
ms.sourcegitcommit: 5fb5b6520b06d7f5e6131ec2ad854da302a28f2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74715595"
---
# <a name="linq-message-query-correlation"></a>LINQ メッセージ クエリの関連付け
このサンプルでは、システム標準の <xref:System.ServiceModel.Dispatcher.MessageQuery> ではなく、カスタムの <xref:System.ServiceModel.XPathMessageQuery> 実装を使用して、コンテンツ ベースの関連付けを実行する方法を示します。  
  
## <a name="demonstrates"></a>例  
 カスタムの <xref:System.ServiceModel.Dispatcher.MessageQuery>、コンテンツ ベースの相関関係。  
  
## <a name="discussion"></a>ディスカッション  
 このサンプルでは、関連付けのために <xref:System.ServiceModel.Dispatcher.MessageQuery> 基本クラスから拡張する方法を示します。 カスタム実装の `LinqMessageQuery` を使用すると、XLinq を使用してメッセージ内で検索する XName を指定できます。 クエリによって取得されたデータを使用して、メッセージを適切なワークフロー インスタンスにディスパッチするための相関関係キーを作成します。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. このサンプルでは、HTTP エンドポイントを使用してワークフロー サービスを公開します。 このサンプルを実行するには、適切な URL Acl を追加する必要があります (詳細については、「 [HTTP および HTTPS の構成](https://go.microsoft.com/fwlink/?LinkId=70353)」を参照してください)。管理者として Visual Studio を実行するか、管理者特権のプロンプトで次のコマンドを実行して適切な acl を追加します。 ドメインとユーザー名は置き換えてください。  
  
    ```console  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. URL ACL を追加したら、次の手順を実行します。  
  
    1. ソリューションをビルドします。  
  
    2. 複数のスタートアッププロジェクトを設定するには、ソリューションを右クリックし、 **[スタートアッププロジェクトの設定]** を選択します。 **サービス**と**クライアント**を (この順序で) 複数のスタートアッププロジェクトとして追加します。  
  
    3. アプリケーションを実行します。 クライアント コンソールには、注文を送信し、発注書 ID を受信した後に、注文を確認するワークフローが示されます。 Service のウィンドウには、処理されている要求が示されます。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>   
> `<InstallDrive>:\WF_WCF_Samples`  
>   
> このディレクトリが存在しない場合は、 [Windows Communication Foundation (wcf) および Windows Workflow Foundation (WF) のサンプルの .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459)にアクセスして、すべての WINDOWS COMMUNICATION FOUNDATION (wcf) と [!INCLUDE[wf1](../../../../includes/wf1-md.md)] サンプルをダウンロードしてください。 このサンプルは、次のディレクトリに格納されます。  
>   
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\LinqMessageQueryCorrelation`
