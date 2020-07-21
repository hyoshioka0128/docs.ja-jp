---
title: '方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 62210fd8-a372-4d55-ab9b-c99827d1885e
ms.openlocfilehash: 0775de90903aed27a8d0006614a4b6f2d857eee3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597099"
---
# <a name="how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications"></a>方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する
Msmq 統合バインディングを使用して、既存のメッセージキュー (MSMQ) アプリケーションを Windows Communication Foundation (WCF) アプリケーションと統合し、msmq メッセージを WCF メッセージとの間で変換することができます。 これにより、WCF クライアントから MSMQ 受信アプリケーションを呼び出したり、MSMQ 送信者アプリケーションから WCF サービスを呼び出すことができます。  
  
 このセクションでは、 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> (1) WCF クライアントと、(2) msmq アプリケーションクライアントと WCF サービスを使用して記述された msmq アプリケーションサービスの間で、キューに置かれた通信を使用する方法について説明します。  
  
 WCF クライアントから MSMQ 受信アプリケーションを呼び出す方法を示す完全なサンプルについては、「 [Windows Communication Foundation To Message Queuing](../samples/wcf-to-message-queuing.md) sample」を参照してください。  
  
 MSMQ クライアントから WCF サービスを呼び出す方法を示す完全なサンプルについては、「 [Windows Communication Foundation サンプルのメッセージキュー](../samples/message-queuing-to-wcf.md) 」を参照してください。  
  
### <a name="to-create-a-wcf-service-that-receives-messages-from-a-msmq-client"></a>MSMQ クライアントからのメッセージを受信する WCF サービスを作成するには  
  
1. 次のコード例に示すように、MSMQ 送信者アプリケーションからキューに置かれたメッセージを受信する WCF サービスのサービスコントラクトを定義するインターフェイスを定義します。  
  
     [!code-csharp[S_MsmqToWcf#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmqtowcf/cs/service.cs#1)]
     [!code-vb[S_MsmqToWcf#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmqtowcf/vb/service.vb#1)]  
  
2. 次のコード例に示すように、定義したインターフェイスを実装し、<xref:System.ServiceModel.ServiceBehaviorAttribute> 属性をクラスに適用します。  
  
     [!code-csharp[S_MsmqToWcf#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmqtowcf/cs/service.cs#2)]
     [!code-vb[S_MsmqToWcf#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmqtowcf/vb/service.vb#2)]  
  
3. <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> を指定する構成ファイルを作成します。  

4. 構成されたバインディングを使用する <xref:System.ServiceModel.ServiceHost> オブジェクトをインスタンス化します。  

### <a name="to-create-a-wcf-client-that-sends-messages-to-a-msmq-receiver-application"></a>MSMQ の受信側アプリケーションにメッセージを送信する WCF クライアントを作成するには  
  
1. 次のコード例に示すように、キューに置かれたメッセージを MSMQ 受信者に送信する WCF クライアントのサービスコントラクトを定義するインターフェイスを定義します。  
  
     [!code-csharp[S_WcfToMsmq#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/proxy.cs#6)]
     [!code-vb[S_WcfToMsmq#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/proxy.vb#6)]  
  
2. WCF クライアントが MSMQ 受信者を呼び出すために使用するクライアントクラスを定義します。  
  
     [!code-csharp[S_WcfToMsmq#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/snippets.cs#2)]
     [!code-vb[S_WcfToMsmq#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/snippets.vb#2)]  
  
3. MsmqIntegrationBinding バインディングの使用を指定する構成を作成します。  
  
     [!code-csharp[S_WcfToMsmq#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/snippets.cs#3)]
     [!code-vb[S_WcfToMsmq#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_wcftomsmq/vb/snippets.vb#3)]  
  
4. クライアント クラスのインスタンスを作成し、メッセージ受信サービスによって定義されたメソッドを呼び出します。  
  
     [!code-csharp[S_WcfToMsmq#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_wcftomsmq/cs/client.cs#4)]  
  
## <a name="see-also"></a>関連項目

- [キューの概要](queues-overview.md)
- [方法: WCF エンドポイントを使用してキューに置かれたメッセージを交換する](how-to-exchange-queued-messages-with-wcf-endpoints.md)
- [Windows Communication Foundation でのメッセージ キュー](../samples/wcf-to-message-queuing.md)
- [メッセージ キュー (MSMQ) のインストール](../samples/installing-message-queuing-msmq.md)
- [Windows Communication Foundation へのメッセージ キュー](../samples/message-queuing-to-wcf.md)
- [メッセージ キューを介したメッセージ セキュリティ](../samples/message-security-over-message-queuing.md)
