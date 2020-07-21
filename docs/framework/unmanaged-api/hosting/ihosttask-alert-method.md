---
title: IHostTask::Alert メソッド
ms.date: 03/30/2017
api_name:
- IHostTask.Alert
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::Alert
helpviewer_keywords:
- IHostTask::Alert method [.NET Framework hosting]
- Alert method, IHostTask interface [.NET Framework hosting]
ms.assetid: 5245d4b5-b6c3-48df-9cb9-8caf059f43fb
topic_type:
- apiref
ms.openlocfilehash: c95b787101d4d0302ce4d2a5cd3bdc7e11f9cd63
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501431"
---
# <a name="ihosttaskalert-method"></a>IHostTask::Alert メソッド
現在の[IHostTask](ihosttask-interface.md)インスタンスによって表されるタスクをホストがスリープ解除するように要求します。これにより、タスクを中止できます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Alert ();  
```  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 `Alert` <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> がユーザーコードから呼び出された場合、または <xref:System.AppDomain> 現在のに関連付けられているがシャットダウンした場合、CLR はメソッドを呼び出し <xref:System.Threading.Thread> ます。 呼び出しは非同期的に行われるため、ホストはすぐに制御を返す必要があります。 ホストがすぐにタスクを警告できない場合は、次にアラートが通知される状態になったときに起動する必要があります。  
  
> [!NOTE]
> `Alert`は、ランタイムが[Join](ihosttask-join-method.md)などのメソッドに WAIT_ALERTABLE の[WAIT_OPTION](wait-option-enumeration.md)値を渡したタスクにのみ影響します。  
  
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
