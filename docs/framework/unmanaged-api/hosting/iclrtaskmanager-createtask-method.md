---
title: ICLRTaskManager::CreateTask メソッド
ms.date: 03/30/2017
api_name:
- ICLRTaskManager.CreateTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTaskManager::CreateTask
helpviewer_keywords:
- ICLRTaskManager::CreateTask method [.NET Framework hosting]
- CreateTask method, ICLRTaskManager interface [.NET Framework hosting]
ms.assetid: eea570d9-2e53-4320-9ea0-eb777bf9dcf3
topic_type:
- apiref
ms.openlocfilehash: 9829f57da911b43626516284e4858adc4139a3ca
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762878"
---
# <a name="iclrtaskmanagercreatetask-method"></a>ICLRTaskManager::CreateTask メソッド
共通言語ランタイム (CLR) によって新しいタスクが作成されることを明示的に要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateTask (  
    [out] ICLRTask **pTask  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pTask`  
 入出力新しく作成された[ICLRTask](iclrtask-interface.md)のアドレスへのポインター、またはタスクを作成できなかった場合は null。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|メソッドから正常に値が返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求されたリソースを割り当てるのに十分なメモリがありません。|  
  
## <a name="remarks"></a>解説  
 CLR は、初期化時、ユーザーコードが名前空間の型を使用してスレッドを作成するとき、 <xref:System.Threading> またはスレッドプールのサイズが増加したときに、新しいタスクを自動的に作成します。 また、アンマネージコードがマネージ関数を呼び出す場合にも、タスクが作成されます。  
  
 `CreateTask`CLR によって新しいタスクが作成されることをホストが明示的に要求できるようにします。 たとえば、ホストはこのメソッドを呼び出して、データ構造を事前に初期化できます。  
  
> [!IMPORTANT]
> 新しいタスクは中断状態で返され、ホストが明示的に[IHostTask:: Start](ihosttask-start-method.md)を呼び出すまで中断されたままになります。  
  
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
