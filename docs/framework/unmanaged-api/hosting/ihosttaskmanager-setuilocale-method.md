---
title: IHostTaskManager::SetUILocale メソッド
ms.date: 03/30/2017
api_name:
- IHostTaskManager.SetUILocale
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::SetUILocale
helpviewer_keywords:
- SetUILocale method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::SetUILocale method [.NET Framework hosting]
ms.assetid: d0c87a9c-ea81-4237-a16b-c22b36ec9dc8
topic_type:
- apiref
ms.openlocfilehash: e7e65c3b9bcafdf4c8b1185fcff1fc0740b2ef7c
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83841434"
---
# <a name="ihosttaskmanagersetuilocale-method"></a>IHostTaskManager::SetUILocale メソッド
共通言語ランタイム (CLR) によって、現在実行中のタスクのユーザーインターフェイス (UI) ロケール (カルチャ) が変更されたことをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetUILocale (  
    [in] LCID lcid  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `lcid`  
 から新しく割り当てられた地理的カルチャおよび言語にマップされるロケール識別子の値。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetUILocale`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_NOTIMPL|ホストでは、マネージユーザーコードで UI カルチャを変更することはできません。|  
  
## <a name="remarks"></a>コメント  
 ランタイムは、 `SetUILocale` プロパティの値 <xref:System.Threading.Thread.CurrentUICulture%2A?displayProperty=nameWithType> がマネージコードによって変更されたときにを呼び出します。 この方法を使用すると、ホストはロケールの同期に必要なメカニズムを実行できます。 ホストで UI ロケールをマネージコードから変更できない場合、またはロケールを同期する機構を実装していない場合は、このメソッドから E_NOTIMPL が返されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [SetLocale メソッド](ihosttaskmanager-setlocale-method.md)
