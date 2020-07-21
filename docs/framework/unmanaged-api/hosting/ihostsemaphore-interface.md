---
title: IHostSemaphore インターフェイス
ms.date: 03/30/2017
api_name:
- IHostSemaphore
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSemaphore
helpviewer_keywords:
- IHostSemaphore interface [.NET Framework hosting]
ms.assetid: c0765321-656c-441e-bab5-58176292be1e
topic_type:
- apiref
ms.openlocfilehash: 8345d85502087568cb05dd262cccf181e3ca07ac
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83803702"
---
# <a name="ihostsemaphore-interface"></a>IHostSemaphore インターフェイス
スレッド処理のためのセマフォのホストの実装を表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ReleaseSemaphore メソッド](ihostsemaphore-releasesemaphore-method.md)|現在のインスタンスの数を `IHostSemaphore` 指定された量だけ増やします。|  
|[Wait メソッド](ihostsemaphore-wait-method.md)|現在の `IHostSemaphore` インスタンスが所有されるか、指定された時間が経過するまで待機するようにします。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [IHostAutoEvent インターフェイス](ihostautoevent-interface.md)
- [IHostManualEvent インターフェイス](ihostmanualevent-interface.md)
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
