---
title: System.ServiceModel.ManualFlowThrottleLimitReached
ms.date: 03/30/2017
ms.assetid: 9aba851f-1830-493b-8e3e-60f454eb923e
ms.openlocfilehash: bffa6361df5a50748f45aa3004f7a307ad516d7b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84580490"
---
# <a name="systemservicemodelmanualflowthrottlelimitreached"></a>System.ServiceModel.ManualFlowThrottleLimitReached
System.ServiceModel.ManualFlowThrottleLimitReached  
  
## <a name="description"></a>説明  
 システムは ManualFlowControlLimit スロットルに設定された制限値に達しました。 スロットル値を変更するには、ServiceHost または InstanceContext の ManualFlowControlLimit プロパティを適宜変更します。  
  
 このトレースは、マニュアル フロー制御制限が初めて 0 に減少したときに出力されます。 それ以降は、0 に変更されてもトレースされません。 インスタンス コンテキストに対するフロー制御制限は、コンテキストごとに 1 回トレースされます。  
  
## <a name="see-also"></a>関連項目

- [トレース](index.md)
- [トレースを使用したアプリケーションのトラブルシューティング](using-tracing-to-troubleshoot-your-application.md)
- [管理と診断](../index.md)
