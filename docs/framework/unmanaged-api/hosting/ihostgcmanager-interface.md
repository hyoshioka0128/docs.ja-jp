---
title: IHostGCManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostGCManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostGCManager
helpviewer_keywords:
- IHostGCManager interface [.NET Framework hosting]
ms.assetid: 820330a4-244c-4f67-ab5e-f24b0b3c2080
topic_type:
- apiref
ms.openlocfilehash: 428e4cf8997713b08e40d9376c34ae5eee8cfa32
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804854"
---
# <a name="ihostgcmanager-interface"></a>IHostGCManager インターフェイス
共通言語ランタイム (CLR) によって実装されるガベージコレクション機構でイベントのホストに通知するメソッドを提供します。  
  
## <a name="members"></a>メンバー  
  
|メンバー|説明|  
|------------|-----------------|  
|[SuspensionEnding メソッド](ihostgcmanager-suspensionending-method.md)|CLR がガベージコレクションのために中断されたスレッドでタスクの実行を再開していることをホストに通知します。|  
|[SuspensionStarting メソッド](ihostgcmanager-suspensionstarting-method.md)|ガベージコレクションを実行するために、CLR がタスクの実行を中断していることをホストに通知します。|  
|[ThreadIsBlockingForSuspension メソッド](ihostgcmanager-threadisblockingforsuspension-method.md)|メソッド呼び出しが行われたスレッドがガベージコレクションに対してブロックされようとしていることをホストに通知します。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
