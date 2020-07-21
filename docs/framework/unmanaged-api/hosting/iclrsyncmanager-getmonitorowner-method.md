---
title: ICLRSyncManager::GetMonitorOwner メソッド
ms.date: 03/30/2017
api_name:
- ICLRSyncManager.GetMonitorOwner
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRSyncManager::GetMonitorOwner
helpviewer_keywords:
- ICLRSyncManager::GetMonitorOwner method [.NET Framework hosting]
- GetMonitorOwner method [.NET Framework hosting]
ms.assetid: 840983a4-396d-47b4-86a0-d35f9b437cdb
topic_type:
- apiref
ms.openlocfilehash: 77debe047f5b379237022f44ef8f9d96718b227d
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762501"
---
# <a name="iclrsyncmanagergetmonitorowner-method"></a>ICLRSyncManager::GetMonitorOwner メソッド
指定したクッキーによって識別されるモニターを所有する[IHostTask](ihosttask-interface.md)インスタンスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetMonitorOwner (  
    [in]  SIZE_T     cookie,  
    [out] IHostTask *ppOwnerHostTask  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cookie`  
 からモニターに関連付けられているクッキー。  
  
 `ppOwnerHostTask`  
 入出力`IHostTask`現在モニターを所有しているへのポインター。タスクに所有権がない場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`GetMonitorOwner`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 ホストは通常、 `GetMonitorOwner` デッドロック検出メカニズムの一部としてを呼び出します。 クッキーは、 [IHostSyncManager:: CreateMonitorEvent](ihostsyncmanager-createmonitorevent-method.md)の呼び出しを使用して作成されるときに、モニターに関連付けられます。  
  
> [!NOTE]
> モニターの基になるイベントを解放する呼び出しはブロックされる可能性がありますが、このメソッドの呼び出しが、そのモニターに関連付けられているクッキーで現在有効である場合、デッドロックは発生しません。 他のタスクも、このモニタを取得しようとするとブロックされることがあります。  
  
 `GetMonitorOwner`は常にを直ちに返します。を呼び出した後、いつでも呼び出すことができ `CreateMonitorEvent` ます。 ホストは、タスクがイベントを待機するまで待機する必要はありません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRSyncManager インターフェイス](iclrsyncmanager-interface.md)
- [IHostSyncManager インターフェイス](ihostsyncmanager-interface.md)
