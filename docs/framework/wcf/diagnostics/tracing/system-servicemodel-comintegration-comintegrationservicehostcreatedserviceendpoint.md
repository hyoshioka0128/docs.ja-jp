---
title: System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed
ms.date: 03/30/2017
ms.assetid: d75d39da-7502-4a6a-91b9-eaa05b8e24d5
ms.openlocfilehash: 8b81cdcaf74aca044260495867b2c4f1de517682
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84593751"
---
# <a name="systemservicemodelchannelsmsmqmoveordeleteattemptfailed"></a>System.ServiceModel.Channels.MsmqMoveOrDeleteAttemptFailed
メッセージを移動または削除できません。  
  
## <a name="description"></a>説明  
 このトレースは、MSMQ メッセージの移動、削除、または拒否の試行中にエラーが発生したことを示しています。  
  
 MSMQ メッセージは Windows Communication Foundation (WCF) によって採用されています (NetMsmqBinding または MsmqIntegrationBinding のいずれかと共に使用する場合)。このトレースは `ReceiveErrorHandling` 、NetMsmqBinding または MsmqIntegrationBinding で選択されたプロパティの値に関連しています。  
  
 このトレースはシステム全体についてのエラーを示すものではありません。 ただし、選択した有害メッセージの処置に失敗したことを示しています。 メッセージが有害になった場合の詳細、およびメッセージを適切に処理するようにサービスを構成する方法については、「[有害メッセージの処理](../../feature-details/poison-message-handling.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
