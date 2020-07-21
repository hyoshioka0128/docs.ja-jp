---
title: ICLRDebugManager::SetConnectionTasks メソッド
ms.date: 03/30/2017
api_name:
- ICLRDebugManager.SetConnectionTasks
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRDebugManager::SetConnectionTasks
helpviewer_keywords:
- SetConnectionTasks method [.NET Framework hosting]
- ICLRDebugManager::SetConnectionTasks method [.NET Framework hosting]
ms.assetid: b38bbc9a-872c-41a9-b8c3-ca011d25456a
topic_type:
- apiref
ms.openlocfilehash: f63b761497b3e9a19a9b939b45acf60d5a7d37b0
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504239"
---
# <a name="iclrdebugmanagersetconnectiontasks-method"></a>ICLRDebugManager::SetConnectionTasks メソッド
[ICLRTask](iclrtask-interface.md)インスタンスのリストを識別子とフレンドリ名に関連付けます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetConnectionTasks (  
    [in] CONNID id,  
    [in] DWORD dwCount,  
    [in, size_is(dwCount)] ICLRTask **ppCLRTask  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `id`  
 から配列を関連付ける接続のホスト固有の識別子 `ppCLRTask` 。  
  
 `dwCount`  
 からのメンバーの数 `ppCLRTask` 。 この値は0より大きくなければなりません。  
  
 `ppCLRTask`  
 から`ICLRTask`によって識別される接続に関連付けるポインターの配列 `id` 。 この配列には、少なくとも1つのメンバーが含まれている必要があります。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetConnectionTasks`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_INVALIDARG|[Beginconnection](iclrdebugmanager-beginconnection-method.md)がこの値を使用して呼び出されていないか、 `id` `dwCount` またはが0であるか、または `id` の要素の1つが `ppCLRTask` null です。|  
  
## <a name="remarks"></a>解説  
 [ICLRDebugManager](iclrdebugmanager-interface.md)では、、、および endconnection という3つのメソッドを使用し `BeginConnection` `SetConnectionTasks` て、タスクリストを識別子とフレンドリ名に関連付けることができます。 [EndConnection](iclrdebugmanager-endconnection-method.md)  
  
> [!IMPORTANT]
> これら3つのメソッドは、一連のタスクごとに特定の順序で呼び出す必要があります。 `BeginConnection`は、新しい接続を確立するために最初に呼び出されます。 `SetConnectionTasks`は、その接続に関連する一連のタスクを提供するために、次に呼び出されます。 `EndConnection`は、タスク一覧と識別子とフレンドリ名の間の関連付けを削除するために最後に呼び出されます。ただし、異なる接続の呼び出しは入れ子にすることができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICLRDebugManager インターフェイス](iclrdebugmanager-interface.md)
- [BeginConnection メソッド](iclrdebugmanager-beginconnection-method.md)
- [EndConnection メソッド](iclrdebugmanager-endconnection-method.md)
- [IHostControl インターフェイス](ihostcontrol-interface.md)
