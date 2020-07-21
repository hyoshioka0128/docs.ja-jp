---
title: System.ServiceModel.Channels.MsmqMessageRejected
ms.date: 03/30/2017
ms.assetid: 9b7c10a7-2af6-44a2-8b1a-90bba0c7cf26
ms.openlocfilehash: c388a9dc3569e20639de09abc5f4941b73c561ad
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84578052"
---
# <a name="systemservicemodelchannelsmsmqmessagerejected"></a>System.ServiceModel.Channels.MsmqMessageRejected
MSMQ はメッセージを拒否しました。  
  
## <a name="description"></a>説明  
 このトレースは、MSMQ メッセージが拒否されたことを示します。  
  
 MSMQ メッセージは、Windows Communication Foundation (WCF) (NetMsmqBinding または MsmqIntegrationBinding で使用される) が処理できない場合に拒否されることがあります。 このようなメッセージは、有害メッセージと呼ばれます。 有害メッセージは、NetMsmqBinding または MsmqIntegrationBinding の `ReceiveErrorHandling` プロパティが `Reject` に設定されると拒否されます。 拒否されたメッセージは、送信側の[配信不能キュー](https://docs.microsoft.com/dotnet/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures)に配信されます。  
  
 メッセージが有害になった場合の詳細、およびメッセージを適切に処理するようにサービスを構成する方法については、「[有害メッセージの処理](../../feature-details/poison-message-handling.md)」を参照してください。  
  
 MSMQ での拒否されたメッセージの意味の詳細については、「 [MQMarkMessageRejected](https://docs.microsoft.com/previous-versions/windows/desktop/msmq/ms707071(v%3dvs.85))」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
- [有害メッセージの処理](../../feature-details/poison-message-handling.md)
- [MQMarkMessageRejected](https://docs.microsoft.com/previous-versions/windows/desktop/msmq/ms707071(v%3dvs.85))
