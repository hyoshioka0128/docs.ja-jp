---
title: Windows Communication Foundation のキュー
ms.date: 03/30/2017
helpviewer_keywords:
- queues [WCF]
ms.assetid: 43008409-1bb4-4bd4-85d7-862c8f10ae20
ms.openlocfilehash: d1fee4fdde18563ec6ccce4f0675d8581184be08
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84596735"
---
# <a name="queues-in-windows-communication-foundation"></a>Windows Communication Foundation のキュー
このセクションのトピックでは、キューの Windows Communication Foundation (WCF) のサポートについて説明します。 WCF では、Microsoft Message Queuing (旧称 MSMQ) をトランスポートとして利用してキューをサポートし、次のシナリオを実現します。  
  
- 疎結合アプリケーション。 送信元アプリケーションは、受信側アプリケーションでメッセージ処理の用意ができているかどうかを確認せずにキューにメッセージを送信できます。 キューにより処理の独立性が提供されるため、送信元アプリケーションは、受信側アプリケーションのメッセージ処理速度とは関係なく、キューにメッセージを送信できます。 キューに対するメッセージの送信がメッセージ処理と密接に結び付けられていない場合は、システムの全体的な可用性が向上します。  
  
- エラーの分離。 キューにメッセージを送受信するアプリケーションは、互いに影響を与えずにエラーを発生させることができます。 たとえば、受信側のアプリケーションでエラーが発生しても、送信側のアプリケーションではメッセージをキューに送信し続けることができます。 受信側は、エラーからの復帰後、キューにあるメッセージを処理できます。 エラーの分離により、システムの全体的な信頼性と可用性が向上します。  
  
- 負荷の平準化。 送信元アプリケーションから送信するメッセージが多すぎるために、受信側アプリケーションの処理が間に合わなくなることがあります。 キューによってこの送信側と受信側のメッセージの不均衡が調整されるため、受信側の処理が間に合わなくなることはありません。  
  
- 操作の切断。 モバイル デバイスのように遅延の大きなネットワーク、または可用性に制限のあるネットワークを介して通信を行う場合に、送信、受信、および処理の各操作を切断できます。 エンドポイントが切断された場合も、キューによってこれらの操作を続行できます。 接続が再度確立されると、メッセージはキューから受信側アプリケーションに転送されます。  
  
 WCF アプリケーションでキュー機能を使用するには、標準バインディングのいずれかを使用するか、標準バインディングのいずれかが要件を満たさない場合はカスタムバインディングを作成できます。 関連する標準バインディングとその選択方法の詳細については、「[方法: WCF エンドポイントとメッセージキューアプリケーションを使用](how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)してメッセージを交換する」を参照してください。 カスタム バインドを作成する方法の詳細については、「[カスタム バインディング](../extending/custom-bindings.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [キューの概要](queues-overview.md)  
 メッセージ キュー概念について概要を示します。  
  
 [WCF でのキュー](queuing-in-wcf.md)  
 WCF キューのサポートの概要について説明します。  
  
 [方法: WCF エンドポイントを使用してキューに置かれたメッセージを交換する](how-to-exchange-queued-messages-with-wcf-endpoints.md)  
 クラスを使用して、 <xref:System.ServiceModel.NetMsmqBinding> wcf クライアントと wcf サービスの間の通信を行う方法について説明します。  
  
 [方法: WCF エンドポイントとメッセージ キュー アプリケーションを使用してメッセージを交換する](how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)  
 を使用して、 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding> WCF アプリケーションとメッセージキューアプリケーション間の通信を行う方法について説明します。  
  
 [セッションでキューに置かれたメッセージのグループ化](grouping-queued-messages-in-a-session.md)  
 単一の受信側アプリケーションが関連メッセージを迅速に処理できるように、キューでメッセージをグループ化する方法を説明します。  
  
 [トランザクションに含まれるメッセージのバッチ処理](batching-messages-in-a-transaction.md)  
 トランザクションでメッセージをバッチ処理する方法について説明します。  
  
 [配信不能キューを使用したメッセージ転送エラー処理](using-dead-letter-queues-to-handle-message-transfer-failures.md)  
 配信不能キューを使用してメッセージの転送エラーと配信エラーを処理する方法、および配信不能キューのメッセージを処理する方法を説明します。  
  
 [有害メッセージ処理](poison-message-handling.md)  
 有害メッセージ (受信側アプリケーションへの配信試行の回数が最大値を超えたメッセージ) の処理方法を説明します。  
  
 [Windows Vista、Windows Server 2003、および Windows XP におけるキュー機能の相違点](diff-in-queue-in-vista-server-2003-windows-xp.md)  
 Windows Vista、Windows Server 2003、および Windows XP の WCF キュー機能の違いについて概要を説明します。  
  
 [トランスポート セキュリティを使用したメッセージのセキュリティ保護](securing-messages-using-transport-security.md)  
 トランスポート セキュリティを使用して、キューに置かれたメッセージを保護する方法を説明します。  
  
 [メッセージ セキュリティを使用したメッセージのセキュリティ保護](securing-messages-using-message-security.md)  
 メッセージ セキュリティを使用して、キューに置かれたメッセージを保護する方法を説明します。  
  
 [キューに置かれたメッセージングのトラブルシューティング](troubleshooting-queued-messaging.md)  
 一般的なキューの問題をトラブルシューティングする方法について説明します。  
  
 [キューに置かれた通信のベスト プラクティス](best-practices-for-queued-communication.md)  
 WCF キュー通信を使用するためのベストプラクティスについて説明します。  
