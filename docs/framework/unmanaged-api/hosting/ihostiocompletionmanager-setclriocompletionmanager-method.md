---
title: IHostIoCompletionManager::SetCLRIoCompletionManager メソッド
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.SetCLRIoCompletionManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::SetCLRIoCompletionManager
helpviewer_keywords:
- IHostIoCompletionManager::SetCLRIoCompletionManager method [.NET Framework hosting]
- SetCLRIoCompletionManager method [.NET Framework hosting]
ms.assetid: 4254bb01-3a14-4f34-a3be-60ff1f5072b5
topic_type:
- apiref
ms.openlocfilehash: a76e807e6b316fc4b904e3f085a17b00d6a11c73
ms.sourcegitcommit: d223616e7e6fe2139079052e6fcbe25413fb9900
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2020
ms.locfileid: "83804694"
---
# <a name="ihostiocompletionmanagersetclriocompletionmanager-method"></a>IHostIoCompletionManager::SetCLRIoCompletionManager メソッド
共通言語ランタイム (CLR) によって実装された[Iclrioの](iclriocompletionmanager-interface.md)インスタンスへのインターフェイスポインターをホストに提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetCLRIoCompletionManager (  
    [in] ICLRIoCompletionManager *pManager  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pManager`  
 から`ICLRIoCompletionManager`CLR によって提供されるインスタンスへのインターフェイスポインター。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetCLRIoCompletionManager`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 CLR が呼び出された後 `SetCLRIoCompletionManager` 、ホストは[Iclriocompleted manager:: oncomplete](iclriocompletionmanager-oncomplete-method.md)を呼び出して、i/o 要求が完了したことを clr に通知する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRIoCompletionManager インターフェイス](iclriocompletionmanager-interface.md)
- [IHostIoCompletionManager インターフェイス](ihostiocompletionmanager-interface.md)
