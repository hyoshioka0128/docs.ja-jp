---
title: 順番を無視したメッセージの処理
ms.date: 03/30/2017
ms.assetid: 33fc62a5-5d59-461c-a37a-0e1b51ac763d
ms.openlocfilehash: 7930f26cf5957158a16d65085267cf1bab2e4504
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598724"
---
# <a name="out-of-order-message-processing"></a>順番を無視したメッセージの処理
ワークフロー サービスは、特定の順序で送信されるメッセージに依存する場合があります。 ワークフロー サービスには 1 つ以上の <xref:System.ServiceModel.Activities.Receive> アクティビティが含まれ、それぞれの <xref:System.ServiceModel.Activities.Receive> アクティビティは特定のメッセージに対応しています。 特定のトランスポート配信保証がないと、クライアントから送信されるメッセージに遅延が生じ、それによって、ワークフロー サービスが予期しない順序でメッセージが配信されることがあります。 特定の順序でメッセージが送信されることを必要としないワークフローは、通常、Parallel アクティビティを使用して実装されます。 アプリケーション プロトコルがより複雑な場合は、ワークフローがすぐに複雑になります。  Windows Communication Foundation (WCF) の順序を指定しないメッセージ処理機能を使用すると、入れ子になった並列アクティビティがすべて複雑になることなく、このようなワークフローを作成できます。 順序を区別しないメッセージ処理は、WCF MSMQ バインドなどをサポートするチャネルでのみサポートされてい <xref:System.ServiceModel.Channels.ReceiveContext> ます。  
  
## <a name="enabling-out-of-order-message-processing"></a>順番を無視したメッセージ処理の有効化  
 順番を無視したメッセージ処理は、ワークフロー サービスで <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> プロパティを `true` に設定することで有効化できます。 次の例は、コードで <xref:System.ServiceModel.Activities.WorkflowService.AllowBufferedReceive%2A> プロパティを設定する方法を示しています。  
  
```csharp  
// Code: Opt-in to Buffered Receive processing...  
WorkflowService service = new WorkflowService  
{  
    Name="MyService",  
    Body = workflow,  
    AllowBufferedReceive = true  
};  
```  
  
 また、次の例に示すように、XAML で `AllowBufferedReceive` 属性をワークフロー サービスに適用することもできます。  
  
```xaml  
// Xaml: Opt-in to Buffered Receive processing...  
<WorkflowService AllowBufferedReceive="True">  
   <!--the actual children activities -->  
</Sequence>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.ServiceModel.Channels.ReceiveContext>
- [ワークフロー サービス](workflow-services.md)
- [キューと信頼できるセッション](queues-and-reliable-sessions.md)
