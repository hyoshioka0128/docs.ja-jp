---
title: IHostTaskManager::CallNeedsHostHook メソッド
ms.date: 03/30/2017
api_name:
- IHostTaskManager.CallNeedsHostHook
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::CallNeedsHostHook
helpviewer_keywords:
- CallNeedsHostHook method [.NET Framework hosting]
- IHostTaskManager::CallNeedsHostHook method [.NET Framework hosting]
ms.assetid: b60f1f59-9825-4b57-961f-d2979518e6a7
topic_type:
- apiref
ms.openlocfilehash: 8cbac3b4ad25ba7dc01413f0c1b44541c43b3999
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503875"
---
# <a name="ihosttaskmanagercallneedshosthook-method"></a>IHostTaskManager::CallNeedsHostHook メソッド
共通言語ランタイム (CLR) が、指定された呼び出しをアンマネージ関数にインライン化できるかどうかをホストが指定できるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CallNeedsHostHook (  
    [in]  SIZE_T target,
    [out] BOOL   *pbCallNeedsHostHook  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `target`  
 から呼び出されるアンマネージ関数の、マップされたポータブル実行可能 (PE) ファイル内のアドレス。  
  
 `pbCallNeedsHostHook`  
 入出力ホストがフックの呼び出しを必要とするかどうかを示すブール値へのポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`CallNeedsHostHook`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 コードの実行を最適化するために、CLR はコンパイル中に各プラットフォーム呼び出しの分析を実行し、呼び出しをインライン化できるかどうかを判断します。 `CallNeedsHostHook`アンマネージ関数の呼び出しをフックするように要求することによって、ホストがその決定をオーバーライドできるようにします。 ホストにフックが必要な場合、ランタイムは呼び出しをインライン化しません。  
  
 通常、このホストでは、浮動小数点の状態を調整する必要があるフックが必要になります。または、呼び出しによって実行されるメモリまたはロックのランタイム要求を追跡できない状態になるという通知を受信します。 ホストが呼び出しをフックする必要がある場合、ランタイムは、 [Enterruntime](ihosttaskmanager-enterruntime-method.md)、all [veruntime](ihosttaskmanager-leaveruntime-method.md)、 [ReverseEnterRuntime](ihosttaskmanager-reverseenterruntime-method.md)、および[ReverseLeaveRuntime](ihosttaskmanager-reverseleaveruntime-method.md)の呼び出しを使用して、マネージコードとの間の遷移をホストに通知します。  
  
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
