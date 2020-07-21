---
title: IHostTaskManager::ReverseEnterRuntime メソッド
ms.date: 03/30/2017
api_name:
- IHostTaskManager.ReverseEnterRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::ReverseEnterRuntime
helpviewer_keywords:
- IHostTaskManager::ReverseEnterRuntime method [.NET Framework hosting]
- ReverseEnterRuntime method [.NET Framework hosting]
ms.assetid: b1e26bff-d3ea-436e-9867-29720df999f4
topic_type:
- apiref
ms.openlocfilehash: 1981fdf25440a296801bdbd06c41ebcb4b87e870
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501397"
---
# <a name="ihosttaskmanagerreverseenterruntime-method"></a>IHostTaskManager::ReverseEnterRuntime メソッド
アンマネージコードから共通言語ランタイム (CLR) への呼び出しが行われていることをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ReverseEnterRuntime ();  
```  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`ReverseEnterRuntime`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたリソース割り当てを完了するために必要なメモリが不足しています。|  
  
## <a name="remarks"></a>解説  
 マネージコードで開始されたシーケンスから CLR への呼び出しが行われる場合、への各呼び出しは、 `ReverseEnterRuntime` [ReverseLeaveRuntime](ihosttaskmanager-reverseleaveruntime-method.md)の呼び出しに対応します。  
  
> [!NOTE]
> 呼び出しは、入れ子になっていなくてもアンマネージコードから発生することがあります。 この場合、 [Enterruntime](ihosttaskmanager-enterruntime-method.md)、all [veruntime](ihosttaskmanager-leaveruntime-method.md)、またはが呼び出され `ReverseLeaveRuntime` ておらず、への呼び出しの回数がの `ReverseEnterRuntime` 呼び出しの数と等しくありません `ReverseLeaveRuntime` 。  
  
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
