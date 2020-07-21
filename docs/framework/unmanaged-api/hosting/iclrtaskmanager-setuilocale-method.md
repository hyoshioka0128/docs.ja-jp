---
title: ICLRTaskManager::SetUILocale メソッド
ms.date: 03/30/2017
api_name:
- ICLRTaskManager.SetUILocale
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTaskManager::SetUILocale
helpviewer_keywords:
- ICLRTaskManager::SetUILocale method [.NET Framework hosting]
- SetUILocale method, ICLRTaskManager interface [.NET Framework hosting]
ms.assetid: 03adaa9a-2beb-49b3-b2c4-6b4fc3f10715
topic_type:
- apiref
ms.openlocfilehash: e6ab7c7af1cf9f30f6708c4e970db619ca071343
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762774"
---
# <a name="iclrtaskmanagersetuilocale-method"></a>ICLRTaskManager::SetUILocale メソッド
現在実行中のタスクのユーザーインターフェイス (UI) ロケール (カルチャ) がホストによって変更されたことを、共通言語ランタイム (CLR) に通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetUILocale (  
    [in] LCID lcid  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `lcid`  
 から新しく割り当てられた地理的カルチャとユーザーインターフェイスの言語にマップされるロケール識別子の値。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetUILocale`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `SetUILocale`ロケールの同期に必要なメカニズムをホストが実行する機会を提供します。  
  
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
