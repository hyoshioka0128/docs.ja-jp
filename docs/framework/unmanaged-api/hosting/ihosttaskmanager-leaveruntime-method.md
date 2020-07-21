---
title: IHostTaskManager::LeaveRuntime メソッド
ms.date: 03/30/2017
api_name:
- IHostTaskManager.LeaveRuntime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager::LeaveRuntime
helpviewer_keywords:
- IHostTaskManager::LeaveRuntime method [.NET Framework hosting]
- LeaveRuntime method [.NET Framework hosting]
ms.assetid: 43689cc4-e48e-46e5-a22d-bafd768b8759
topic_type:
- apiref
ms.openlocfilehash: deaebbce3b9b8a26bf9668b826a6818dba94dcc3
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501380"
---
# <a name="ihosttaskmanagerleaveruntime-method"></a>IHostTaskManager::LeaveRuntime メソッド
現在実行中のタスクが共通言語ランタイム (CLR) を終了しようとしていることをホストに通知し、アンマネージコードを入力します。  
  
> [!IMPORTANT]
> [IHostTaskManager:: EnterRuntime](ihosttaskmanager-enterruntime-method.md)への対応する呼び出しは、現在実行中のタスクがマネージコードを再要求していることをホストに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LeaveRuntime (  
    [in] SIZE_T target  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `target`  
 から呼び出されるアンマネージ関数の、マップされた移植可能な実行可能ファイル内のアドレス。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`LeaveRuntime`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|CLR がプロセスに読み込まれていないか、CLR がマネージドコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
|E_OUTOFMEMORY|要求された割り当てを完了するために必要なメモリが不足しています。|  
  
## <a name="remarks"></a>解説  
 アンマネージコードとの間の呼び出しシーケンスは入れ子にすることができます。 たとえば、次の一覧は、 `LeaveRuntime` 、 [IHostTaskManager:: ReverseEnterRuntime](ihosttaskmanager-reverseenterruntime-method.md)、 [IHostTaskManager:: ReverseLeaveRuntime](ihosttaskmanager-reverseleaveruntime-method.md)に対する呼び出しのシーケンスによって、 `IHostTaskManager::EnterRuntime` ホストが入れ子になったレイヤーを識別できるようにする仮定の状況を示しています。  
  
|アクション|対応するメソッド呼び出し|  
|------------|-------------------------------|  
|マネージ Visual Basic 実行可能ファイルは、プラットフォーム呼び出しを使用して C で記述されたアンマネージ関数を呼び出します。|`IHostTaskManager::LeaveRuntime`|  
|アンマネージ C 関数は、C# で記述されたマネージ DLL 内のメソッドを呼び出します。|`IHostTaskManager::ReverseEnterRuntime`|  
|マネージ C# 関数は、C で記述された別のアンマネージ関数を呼び出します。これは、プラットフォーム呼び出しを使用することもできます。|`IHostTaskManager::LeaveRuntime`|  
|2番目のアンマネージ関数は、C# 関数に実行を返します。|`IHostTaskManager::EnterRuntime`|  
|C# 関数は、最初のアンマネージ関数に実行を返します。|`IHostTaskManager::ReverseLeaveRuntime`|  
|最初のアンマネージ関数は、実行を Visual Basic プログラムに返します。|`IHostTaskManager::EnterRuntime`|  
  
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
