---
title: ICLRTask::Reset メソッド
ms.date: 03/30/2017
api_name:
- ICLRTask.Reset
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask::Reset
helpviewer_keywords:
- ICLRTask::Reset method [.NET Framework hosting]
- Reset method, ICLRTask interface [.NET Framework hosting]
ms.assetid: 1bfb5d3a-0ffd-4bb4-9bf6-aec00cb675b7
topic_type:
- apiref
ms.openlocfilehash: 15004238ee296e44ae77cd8739b7f62ea2a7a100
ms.sourcegitcommit: c76c8b2c39ed2f0eee422b61a2ab4c05ca7771fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83762969"
---
# <a name="iclrtaskreset-method"></a>ICLRTask::Reset メソッド
ホストがタスクを完了したことを共通言語ランタイム (CLR) に通知し、CLR が現在の[ICLRTask](iclrtask-interface.md)インスタンスを再利用して別のタスクを表すことができるようにします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Reset (  
    [in] BOOL fFull  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fFull`  
 [in] `true` 。ランタイムが、現在のインスタンスに関連するセキュリティおよびロケール情報に加えて、スレッドに関連するすべての静的な値をリセットする必要がある場合は `ICLRTask` 。それ以外の場合は `false` 。  
  
 値がの場合 `true` 、ランタイムはまたはを使用して格納されたデータをリセットし <xref:System.Threading.Thread.AllocateDataSlot%2A> <xref:System.Threading.Thread.AllocateNamedDataSlot%2A> ます。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`Reset`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しを処理できません。 なく|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>解説  
 CLR では、 `ICLRTask` 新しいタスクが必要になるたびに新しいインスタンスを繰り返し作成するオーバーヘッドを回避するために、以前に作成されたインスタンスをリサイクルできます。 ホストは、 `ICLRTask::Reset` タスクを完了したときに、 [ICLRTask:: exittask](iclrtask-exittask-method.md)ではなくを呼び出すことにより、この機能を有効にします。 インスタンスの通常のライフサイクルの概要を次に示し `ICLRTask` ます。  
  
1. ランタイムは、新しいインスタンスを作成し `ICLRTask` ます。  
  
2. ランタイムは、 [IHostTaskManager:: GetCurrentTask](ihosttaskmanager-getcurrenttask-method.md)を呼び出して、現在のホストタスクへの参照を取得します。  
  
3. ランタイムは、新しいインスタンスをホストタスクに関連付けるために、 [IHostTask:: SetCLRTask](ihosttask-setclrtask-method.md)を呼び出します。  
  
4. タスクが実行され、完了します。  
  
5. ホストは、を呼び出すことによってタスクを破棄し `ICLRTask::ExitTask` ます。  
  
 `Reset`では、このシナリオを次の2つの方法で変更します。 上記の手順5では、ホストがを呼び出して `Reset` タスクをクリーンな状態にリセットし、その `ICLRTask` インスタンスを関連する[IHostTask](ihosttask-interface.md)インスタンスから切り離します。 必要に応じて、ホストはインスタンスをキャッシュして再利用することもでき `IHostTask` ます。 上記の手順 1. では、ランタイムは、 `ICLRTask` 新しいインスタンスを作成する代わりに、キャッシュからリサイクルしたを取得します。  
  
 この方法は、ホストに再利用可能なワーカータスクのプールがある場合に適しています。 ホストがそのインスタンスの1つを破棄すると、を `IHostTask` `ICLRTask` 呼び出すことによって、対応するを破棄し `ExitTask` ます。  
  
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
