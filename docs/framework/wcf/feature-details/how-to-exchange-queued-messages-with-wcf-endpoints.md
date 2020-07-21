---
title: '方法: WCF エンドポイントを使用してキューに置かれたメッセージを交換する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 938e7825-f63a-4c3d-b603-63772fabfdb3
ms.openlocfilehash: 7da7ba1b680bae2b29eeff8fe669e097ea8eda32
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84595376"
---
# <a name="how-to-exchange-queued-messages-with-wcf-endpoints"></a>方法: WCF エンドポイントを使用してキューに置かれたメッセージを交換する
キューを使用すると、通信時にサービスを利用できない場合でも、クライアントと Windows Communication Foundation (WCF) サービスの間で信頼できるメッセージングを行うことができます。 次の手順では、WCF サービスを実装するときに、標準のキューに登録されたバインディングを使用して、クライアントとサービス間の永続的な通信を確保する方法を示します。  
  
 このセクションでは、 <xref:System.ServiceModel.NetMsmqBinding> wcf クライアントと wcf サービスの間のキュー通信にを使用する方法について説明します。  
  
### <a name="to-use-queuing-in-a-wcf-service"></a>WCF サービスでキューを使用するには  
  
1. <xref:System.ServiceModel.ServiceContractAttribute> でマークされたインターフェイスを使用して、サービス コントラクトを定義します。 サービス コントラクトの一部であるインターフェイスの動作を <xref:System.ServiceModel.OperationContractAttribute> でマークし、メソッドに対して応答が返されないため、一方向と指定します。 サービス コントラクトおよびその操作の定義の例を次のコードに示します。  
  
     [!code-csharp[S_Msmq_Transacted#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#1)]
     [!code-vb[S_Msmq_Transacted#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#1)]  
  
2. サービス コントラクトがユーザー定義型を渡す場合は、その型のデータ コントラクトを定義する必要があります。 次のコードは、2 つのデータ コントラクト (`PurchaseOrder` および `PurchaseOrderLineItem`) を示します。 これらの 2 つの型は、サービスに送信されるデータを定義します  (このデータ コントラクトを定義するクラスによって多数のメソッドが定義されることに注意してください)。 これらのメソッドは、データ コントラクトの一部とは見なされません。 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性で宣言されているメンバーだけがデータ コントラクトに含まれます。  
  
     [!code-csharp[S_Msmq_Transacted#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#2)]
     [!code-vb[S_Msmq_Transacted#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#2)]  
  
3. インターフェイスで定義したサービス コントラクトのメソッドをクラスに実装します。  
  
     [!code-csharp[S_Msmq_Transacted#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#3)]
     [!code-vb[S_Msmq_Transacted#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#3)]  
  
     <xref:System.ServiceModel.OperationBehaviorAttribute> メソッド上の `SubmitPurchaseOrder` に注意してください。 これは、トランザクション内でこの操作を呼び出す必要があること、およびメソッドが完了したときにトランザクションが自動的に完了することを指定します。  
  
4. <xref:System.Messaging> を使用してトランザクション キューを作成します。 代わりに、MSMQ (Microsoft Message Queuing) Microsoft 管理コンソール (MMC: Microsoft Management Console) を使用してキューを作成することもできます。 その場合は、トランザクション キューを作成してください。  
  
     [!code-csharp[S_Msmq_Transacted#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#4)]
     [!code-vb[S_Msmq_Transacted#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#4)]  
  
5. サービス アドレスを指定し、標準の <xref:System.ServiceModel.Description.ServiceEndpoint> バインディングを使用する <xref:System.ServiceModel.NetMsmqBinding> を構成で定義します。 WCF 構成の使用方法の詳細については、「 [wcf サービスの構成](../configuring-services.md)」を参照してください。  

6. `OrderProcessing` を使用して、キューからメッセージを読み取って処理する <xref:System.ServiceModel.ServiceHost> サービスのホストを作成します。 サービス ホストを開いてサービスを使用できるようにします。 任意のキーを押してサービスを終了するようユーザーに伝えるメッセージを表示します。 `ReadLine` を呼び出して、キーが押されるまで待機してサービスを終了します。  
  
     [!code-csharp[S_Msmq_Transacted#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#6)]
     [!code-vb[S_Msmq_Transacted#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#6)]  
  
### <a name="to-create-a-client-for-the-queued-service"></a>キューに置かれたサービスのクライアントを作成するには  
  
1. 次の例は、ホストアプリケーションを実行し、Svcutil.exe ツールを使用して WCF クライアントを作成する方法を示しています。  
  
    ```console
    svcutil http://localhost:8000/ServiceModelSamples/service  
    ```  
  
2. 次の例に示すように、アドレスを指定し、標準の <xref:System.ServiceModel.Description.ServiceEndpoint> バインディングを使用する <xref:System.ServiceModel.NetMsmqBinding> を構成で定義します。  

3. トランザクションキューに書き込むトランザクションスコープを作成し、操作を呼び出して、 `SubmitPurchaseOrder` WCF クライアントを閉じます。次に例を示します。  
  
     [!code-csharp[S_Msmq_Transacted#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#8)]
     [!code-vb[S_Msmq_Transacted#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#8)]  
  
## <a name="example"></a>例  
 次の例は、この例に含まれるサービス コード、ホスト アプリケーション、App.config ファイル、およびクライアント コードを示します。  
  
 [!code-csharp[S_Msmq_Transacted#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#9)]
 [!code-vb[S_Msmq_Transacted#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#9)]  
  
 [!code-csharp[S_Msmq_Transacted#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#10)]
 [!code-vb[S_Msmq_Transacted#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#10)]  

 [!code-csharp[S_Msmq_Transacted#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#12)]
 [!code-vb[S_Msmq_Transacted#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#12)]  

## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.NetMsmqBinding>
- [トランザクション MSMQ バインディング](../samples/transacted-msmq-binding.md)
- [WCF でのキュー](queuing-in-wcf.md)
- [方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する](how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)
- [Windows Communication Foundation でのメッセージ キュー](../samples/wcf-to-message-queuing.md)
- [メッセージ キュー (MSMQ) のインストール](../samples/installing-message-queuing-msmq.md)
- [Windows Communication Foundation へのメッセージ キュー](../samples/message-queuing-to-wcf.md)
- [メッセージ キューを介したメッセージ セキュリティ](../samples/message-security-over-message-queuing.md)
