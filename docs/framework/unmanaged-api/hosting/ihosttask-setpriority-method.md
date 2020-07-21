---
title: IHostTask::SetPriority メソッド
ms.date: 03/30/2017
api_name:
- IHostTask.SetPriority
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTask::SetPriority
helpviewer_keywords:
- IHostTask::SetPriority method [.NET Framework hosting]
- SetPriority method [.NET Framework hosting]
ms.assetid: cd8c379b-c7a0-434f-8e23-899bd26be75d
topic_type:
- apiref
ms.openlocfilehash: ac3a8479cdf05e55885bd55d4e4fb8e6e47686f9
ms.sourcegitcommit: e5772b3ddcc114c80b4c9767ffdb3f6c7fad8f05
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83842401"
---
# <a name="ihosttasksetpriority-method"></a>IHostTask::SetPriority メソッド
現在の[IHostTask](ihosttask-interface.md)インスタンスによって表されるタスクのスレッドの優先度レベルをホストが調整するように要求します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetPriority (  
    [in] int newPriority  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `newPriority`  
 から現在のインスタンスによって表されるタスクについて、要求されたスレッドの優先順位値を表す整数 `IHostTask` 。  
  
## <a name="return-value"></a>戻り値  
  
|HRESULT|説明|  
|-------------|-----------------|  
|S_OK|`SetPriority`正常に返されました。|  
|HOST_E_CLRNOTAVAILABLE|共通言語ランタイム (CLR) がプロセスに読み込まれていないか、CLR がマネージコードを実行できない状態であるか、または呼び出しが正常に処理されていません。|  
|HOST_E_TIMEOUT|呼び出しがタイムアウトしました。|  
|HOST_E_NOT_OWNER|呼び出し元がロックを所有していません。|  
|HOST_E_ABANDONED|ブロックされたスレッドまたはファイバーが待機しているときに、イベントが取り消されました。|  
|E_FAIL|原因不明の致命的なエラーが発生しました。 メソッドが E_FAIL を返すと、そのプロセス内で CLR が使用できなくなります。 後続のホストメソッドの呼び出しでは HOST_E_CLRNOTAVAILABLE が返されます。|  
  
## <a name="remarks"></a>コメント  
 スレッドには、スレッドの優先度レベルに基づいたラウンドロビンシステムを使用した処理時間が与えられます。 `SetPriority`CLR が現在のタスクに対して、そのスレッドの優先度レベルを設定できるようにします。 次の `newPriority` 値がサポートされています。  
  
- THREAD_PRIORITY_ABOVE_NORMAL  
  
- THREAD_PRIORITY_BELOW_NORMAL  
  
- THREAD_PRIORITY_HIGHEST  
  
- THREAD_PRIORITY_IDLE  
  
- THREAD_PRIORITY_LOWEST  
  
- THREAD_PRIORITY_NORMAL  
  
- THREAD_PRIORITY_TIME_CRITICAL  
  
 CLR は `SetPriority` 、の値 <xref:System.Threading.Thread.Priority%2A?displayProperty=nameWithType> がユーザーコードによって変更されたときにを呼び出します。 ホストは、スレッドの優先度割り当てに対して独自のアルゴリズムを定義でき、この要求を無視することができます。  
  
> [!NOTE]
> `SetPriority`では、スレッドの優先度レベルが変更されたかどうかは報告されません。 [IHostTask:: GetPriority](ihosttask-getpriority-method.md)を呼び出して、タスクのスレッド優先度レベルの値を決定します。  
  
 スレッドの優先度レベルの値は、Win32 関数によって定義され `SetThreadPriority` ます。 スレッドの優先順位の詳細については、Windows プラットフォームのドキュメントを参照してください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Threading.Thread>
- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [GetPriority メソッド](ihosttask-getpriority-method.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
