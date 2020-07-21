---
title: IHostSyncManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostSyncManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSyncManager
helpviewer_keywords:
- IHostSyncManager interface [.NET Framework hosting]
ms.assetid: 2e081a37-6a28-4c93-b7ab-1c96a464637c
topic_type:
- apiref
ms.openlocfilehash: fd3c941d89fbd93f30fc1af235f6310b23758973
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501457"
---
# <a name="ihostsyncmanager-interface"></a>IHostSyncManager インターフェイス
Win32 同期関数を使用する代わりに、共通言語ランタイム (CLR) がホストを呼び出して同期プリミティブを作成できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CreateAutoEvent メソッド](ihostsyncmanager-createautoevent-method.md)|自動リセットイベントオブジェクトを作成します。|  
|[CreateCrst メソッド](ihostsyncmanager-createcrst-method.md)|同期のための重要なセクションオブジェクトを作成します。|  
|[CreateCrstWithSpinCount メソッド](ihostsyncmanager-createcrstwithspincount-method.md)|同期のためにスピンカウントを持つクリティカルセクションオブジェクトを作成します。|  
|[CreateManualEvent メソッド](ihostsyncmanager-createmanualevent-method.md)|手動リセットイベントオブジェクトを作成します。|  
|[CreateMonitorEvent メソッド](ihostsyncmanager-createmonitorevent-method.md)|監視対象の自動リセットイベントオブジェクトを作成します。|  
|[CreateRWLockReaderEvent メソッド](ihostsyncmanager-createrwlockreaderevent-method.md)|リーダーロックの実装のための手動リセットイベントオブジェクトを作成します。|  
|[CreateRWLockWriterEvent メソッド](ihostsyncmanager-createrwlockwriterevent-method.md)|ライターロックの実装用の自動リセットイベントオブジェクトを作成します。|  
|[CreateSemaphore メソッド](ihostsyncmanager-createsemaphore-method.md)|CLR が待機イベントのセマフォとして使用する[IHostSemaphore](ihostsemaphore-interface.md)オブジェクトを作成します。|  
|[SetCLRSyncManager メソッド](ihostsyncmanager-setclrsyncmanager-method.md)|現在のインスタンスに関連付ける[ICLRSyncManager](iclrsyncmanager-interface.md)インスタンスを設定 `IHostSyncManager` します。|  
  
## <a name="remarks"></a>解説  
 CLR は、 `IHostSyncManager` IID_IHostSyncManager のを使用して[IHostControl:: GetHostManager](ihostcontrol-gethostmanager-method.md)メソッドを呼び出すことで、ホストのの実装を検出し `IID` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
