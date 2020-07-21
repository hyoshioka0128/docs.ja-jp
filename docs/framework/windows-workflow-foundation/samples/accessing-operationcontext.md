---
title: OperationContext へのアクセス
ms.date: 03/30/2017
ms.assetid: 4e92efe8-7e79-41f3-b50e-bdc38b9f41f8
ms.openlocfilehash: 5a2731c7918c216221b0adcafd5c804e80f36dfb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182855"
---
# <a name="accessing-operationcontext"></a>OperationContext へのアクセス
このサンプルでは、メッセージング アクティビティ (<xref:System.ServiceModel.Activities.Receive>および<xref:System.ServiceModel.Activities.Send>) をカスタム スコープ アクティビティで使用<xref:System.ServiceModel.OperationContext.Current%2A>して、送信メッセージまたは受信メッセージ内のカスタム メッセージ ヘッダーにアクセスし、添付または取得する方法を示します。  
  
## <a name="demonstrates"></a>対象  
 メッセージング アクティビティ、<xref:System.ServiceModel.Activities.ISendMessageCallback>、<xref:System.ServiceModel.Activities.IReceiveMessageCallback>。  
  
## <a name="discussion"></a>ディスカッション  
 このサンプルでは、メッセージング アクティビティで拡張ポイント (<xref:System.ServiceModel.Activities.ISendMessageCallback> および <xref:System.ServiceModel.Activities.IReceiveMessageCallback>) を使用して <xref:System.ServiceModel.OperationContext.Current%2A> にアクセスする方法を示します。 これらのコールバックは、実行時にメッセージング アクティビティによって取得される <xref:System.Activities.IExecutionProperty> の実装としてワークフロー ランタイム内に登録されます。 その <xref:System.Activities.IExecutionProperty> 実装と同じスコープ内のメッセージング アクティビティはすべて影響を受けます。 具体的には、このサンプルでは、カスタムのスコープ アクティビティを使用してコールバック動作を適用します。 <xref:System.ServiceModel.Activities.ISendMessageCallback> は、ワークフローの <xref:System.Activities.WorkflowApplication.Id%2A> を送信 <xref:System.ServiceModel.Channels.MessageHeader> として含めるためにクライアント ワークフローで使用されます。 このヘッダーはサービスで <xref:System.ServiceModel.Activities.IReceiveMessageCallback> を使用して取得され、ヘッダーの値がコンソールに出力されます。  
  
#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには  
  
1. このサンプルでは、HTTP エンドポイントを使用してワークフロー サービスを公開します。 このサンプルを実行するには、Visual Studio を管理者として実行するか、管理者特権のプロンプトで次のコマンドを実行して適切な ACL を追加する (詳細については[、HTTP および HTTPS](../../wcf/feature-details/configuring-http-and-https.md)の構成を参照) 必要があります。 ドメインとユーザー名は置き換えてください。  
  
    ```console  
    netsh http add urlacl url=http://+:8000/ user=%DOMAIN%\%UserName%  
    ```  
  
2. URL ACL を追加したら、次の手順を実行します。  
  
    1. ソリューションをビルドします。  
  
    2. ソリューションを右クリックし、[スタートアップ プロジェクトの設定] を選択して、複数の**スタートアップ プロジェクトを設定**します。  
  
    3. **サービス**と**クライアント**を複数のスタートアップ プロジェクトとして (この順序で) 追加します。  
  
    4. アプリケーションを実行します。 クライアント コンソールに実行中のワークフローが 2 回示され、[サービス] ウィンドウにこれらのワークフローのインスタンス ID が示されます。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\Services\Accessing Operation Context`
