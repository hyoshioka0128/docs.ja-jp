---
title: IHostTaskManager::CreateTask メソッド
ms.date: 03/30/2017
api_name:
- IHostTaskManager.CreateTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::CreateTask
helpviewer_keywords:
- CreateTask method, IHostTaskManager interface [.NET Framework hosting]
- IHostTaskManager::CreateTask method [.NET Framework hosting]
ms.assetid: a6f8ad36-61e1-42b0-9db2-add575646d18
topic_type:
- apiref
ms.openlocfilehash: 4037ffe63d8ebfca67cbd0b3293d36be7481b1bd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501418"
---
# <a name="ihosttaskmanagercreatetask-method"></a>IHostTaskManager::CreateTask メソッド
ホストが新しいタスクを作成することを要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateTask (  
    [in]  DWORD stacksize,
    [in]  LPTHREAD_START_ROUTINE pStartAddress,  
    [in]  PVOID pParameter,  
    [out] IHostTask **ppTask  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `stacksize`  
 から要求されたスタックの要求されたサイズ (バイト単位)、または既定のサイズの 0 (ゼロ)。  
  
 `pStartAddress`  
 からタスクが実行する関数へのポインター。  
  
 `pParameter`  
 から関数に渡されるユーザーデータへのポインター。関数がパラメーターを受け取らない場合は null。  
  
 `ppTask`  
 入出力ホストによって作成された[IHostTask](ihosttask-interface.md)インスタンスのアドレスへのポインター。タスクを作成できない場合は null。 このタスクは、 [IHostTask:: Start](ihosttask-start-method.md)の呼び出しによって明示的に開始されるまで、中断状態のままになります。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`CreateTask`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたタスクを作成するのに十分なメモリがありませんでした。|  
  
## <a name="remarks"></a>解説  
 CLR はを呼び出して、 `CreateTask` ホストが新しいタスクを作成することを要求します。 ホストは、インスタンスへのインターフェイスポインターを返し `IHostTask` ます。 を呼び出すことによって明示的に開始されるまで、返されたタスクは中断されたままである必要があり `IHostTask::Start` ます。  
  
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
