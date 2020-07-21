---
title: System.ServiceModel.Channels.MsmqMessageDropped
ms.date: 03/30/2017
ms.assetid: 8b6e644d-fa68-4be7-abe9-3659671a37c1
ms.openlocfilehash: 4b016f53a75d9527a5cd1bbadacacd650b7f35b0
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601913"
---
# <a name="systemservicemodelchannelsmsmqmessagedropped"></a>System.ServiceModel.Channels.MsmqMessageDropped
MSMQ はメッセージを破棄しました。  
  
## <a name="description"></a>説明  
 このトレースは、MSMQ メッセージが破棄されたことを示します。 MSMQ メッセージは Windows Communication Foundation (WCF) (NetMsmqBinding または MsmqIntegrationBinding で使用) が処理できない場合に削除できます。 このようなメッセージは、有害メッセージと呼ばれます。  
  
 有害メッセージは、NetMsmqBinding または MsmqIntegrationBinding の `ReceiveErrorHandling` プロパティが `Drop` に設定されていると破棄されます。 破棄されたメッセージはキューから削除され、元に戻すことはできません。  
  
 メッセージが有害になった場合の詳細、およびメッセージを適切に処理するようにサービスを構成する方法については、「[有害メッセージの処理](../../feature-details/poison-message-handling.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
- [有害メッセージの処理](../../feature-details/poison-message-handling.md)
