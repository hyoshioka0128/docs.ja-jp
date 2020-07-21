---
title: IHostAutoEvent インターフェイス
ms.date: 03/30/2017
api_name:
- IHostAutoEvent
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostAutoEvent
helpviewer_keywords:
- IHostAutoEvent interface [.NET Framework hosting]
ms.assetid: 6c1d15c1-a80a-4ee9-b1e4-6e859db6575a
topic_type:
- apiref
ms.openlocfilehash: a24939ac0b0808546ef3615fae4909c6c3cf8a2e
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804993"
---
# <a name="ihostautoevent-interface"></a>IHostAutoEvent インターフェイス
自動リセットイベントのホストの実装の表現を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Set メソッド](ihostautoevent-set-method.md)|現在の `IHostAutoEvent` インスタンスをシグナル状態に設定します。|  
|[Wait メソッド](ihostautoevent-wait-method.md)|`IHostAutoEvent`イベントが所有されるか、指定した時間が経過するまで、現在のインスタンスを待機させます。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [IHostManualEvent インターフェイス](ihostmanualevent-interface.md)
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
