---
title: IHostCrst::SetSpinCount メソッド
ms.date: 03/30/2017
api_name:
- IHostCrst.SetSpinCount
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostCrst::SetSpinCount
helpviewer_keywords:
- IHostCrst::SetSpinCount method [.NET Framework hosting]
- SetSpinCount method [.NET Framework hosting]
ms.assetid: 863fc8ce-9b8a-477e-8dd8-75c8544bb43a
topic_type:
- apiref
ms.openlocfilehash: 2436809f35d5c46416f48987cc92feb51d291a6a
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804879"
---
# <a name="ihostcrstsetspincount-method"></a>IHostCrst::SetSpinCount メソッド
現在の[IHostCrst](ihostcrst-interface.md)インスタンスのスピンカウントを設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetSpinCount (  
    [in] DWORD dwSpinCount  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwSpinCount`  
 から現在のインスタンスの新しいスピンカウント `IHostCrst` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetSpinCount`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 マルチプロセッサシステムでは、現在のインスタンスによって表されるクリティカルセクション `IHostCrst` が使用できない場合、呼び出し元のスレッドは、 `dwSpinCount` クリティカルセクションに関連付けられているセマフォで[IHostSemaphore:: Wait](ihostsemaphore-wait-method.md)を呼び出す前に時間をスピンします。 スピン操作中にクリティカルセクションが解放されると、呼び出し元のスレッドは待機操作を回避します。  
  
 の使用方法 `dwSpinCount` は、Win32 関数で同じ名前のパラメーターを使用する場合と同じです `InitializeCriticalSectionAndSpinCount` 。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [IHostCrst インターフェイス](ihostcrst-interface.md)
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
