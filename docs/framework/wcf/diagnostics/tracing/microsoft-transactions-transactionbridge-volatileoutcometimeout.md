---
title: Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
ms.date: 03/30/2017
ms.assetid: 2dbe34c5-57c7-4b64-9257-63021911d03c
ms.openlocfilehash: dd2a0b67ec140aa2e6fe1abad8e85c0206abd8ea
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84579022"
---
# <a name="microsofttransactionstransactionbridgevolatileoutcometimeout"></a>Microsoft.Transactions.TransactionBridge.VolatileOutcomeTimeout
不安定な参加要素からの結果メッセージに対する応答を受信するのを待機しているときに WS-AT プロトコル サービスがタイムアウトしました。 受信者が応答した場合、トランザクションの結果が不明である場合があります。  
  
## <a name="description"></a>説明  
 不安定な参加要素がコミットまたは中止を決定したが、一定時間内にコミット要求またはロールバック要求に応答していない場合にトレースされます。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
 不安定な参加要素がすべて一定時間内に応答できることを確認します。 既定の時間は 180 秒です。  この時間が不十分な場合は、WS-AT の `VolatileOutcomeDelay` タイマー ポリシーを増やします。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
