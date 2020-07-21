---
title: System.ServiceModel.Channels.MsmqPoisonMessageRejected
ms.date: 03/30/2017
ms.assetid: 0e64b9bd-1f12-43df-a189-d7be3c2bace1
ms.openlocfilehash: f0e49fcfa13bb9932a88a4e79d617343c080bb3c
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598373"
---
# <a name="systemservicemodelchannelsmsmqpoisonmessagerejected"></a>System.ServiceModel.Channels.MsmqPoisonMessageRejected
有害メッセージは拒否されました。  
  
## <a name="description"></a>説明  

 このトレースは、有害メッセージが検出され、続いて拒否されたことを示します。 これは、NetMsmqBinding または MsmqIntegrationBinding の `ReceiveErrorHandling` プロパティが `Reject` に設定されると発生します。 拒否されたメッセージは、送信側の[配信不能キュー](../../feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)に配信されます。  
  
 メッセージが有害になった場合の詳細、およびメッセージを適切に処理するようにサービスを構成する方法については、「[有害メッセージの処理](../../feature-details/poison-message-handling.md)」を参照してください。 MSMQ での拒否されたメッセージの意味の詳細については、「 [MQMarkMessageRejected](https://docs.microsoft.com/previous-versions/windows/desktop/msmq/ms707071(v%3dvs.85))」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
- [有害メッセージの処理](../../feature-details/poison-message-handling.md)
- [MQMarkMessageRejected](https://docs.microsoft.com/previous-versions/windows/desktop/msmq/ms707071(v%3dvs.85))
