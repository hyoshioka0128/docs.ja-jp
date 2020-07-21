---
title: IHostTaskManager インターフェイス
ms.date: 03/30/2017
api_name:
- IHostTaskManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostTaskManager
helpviewer_keywords:
- IHostTaskManager interface [.NET Framework hosting]
ms.assetid: 4a0b05b9-3ef1-4607-b7c8-bd4dd43647a0
topic_type:
- apiref
ms.openlocfilehash: 190908c675b96b8ea2d81fb0203aa16a80d6a8b4
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501402"
---
# <a name="ihosttaskmanager-interface"></a>IHostTaskManager インターフェイス
標準のオペレーティングシステムのスレッド処理やファイバー関数を使用する代わりに、共通言語ランタイム (CLR) がホストを通じてタスクを操作できるようにするメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[BeginDelayAbort メソッド](ihosttaskmanager-begindelayabort-method.md)|マネージコードが、現在のタスクを中止できない期間を入力していることをホストに通知します。|  
|[BeginThreadAffinity メソッド](ihosttaskmanager-beginthreadaffinity-method.md)|マネージコードが、現在のタスクを別のオペレーティングシステムのスレッドに移動できない期間を入力していることをホストに通知します。|  
|[CallNeedsHostHook メソッド](ihosttaskmanager-callneedshosthook-method.md)|共通言語ランタイムがアンマネージ関数に対して指定された呼び出しをインライン展開できるかどうかを指定できるようにします。|  
|[CreateTask メソッド](ihosttaskmanager-createtask-method.md)|ホストが新しいタスクを作成することを要求します。|  
|[EndDelayAbort メソッド](ihosttaskmanager-enddelayabort-method.md)|を以前に呼び出した後に、マネージコードが現在のタスクを中止できない期間を終了することをホストに通知し `BeginDelayAbort` ます。|  
|[EndThreadAffinity メソッド](ihosttaskmanager-endthreadaffinity-method.md)|以前にを呼び出した後に、マネージコードが、現在のタスクを別のオペレーティングシステムのスレッドに移動できない期間を終了していることをホストに通知し `BeginThreadAffinity` ます。|  
|[EnterRuntime メソッド](ihosttaskmanager-enterruntime-method.md)|プラットフォーム呼び出しメソッドなどのアンマネージメソッドへの呼び出しが実行制御を CLR に返すことをホストに通知します。|  
|[GetCurrentTask メソッド](ihosttaskmanager-getcurrenttask-method.md)|この呼び出しが行われたオペレーティングシステムスレッドで現在実行されているタスクへのインターフェイスポインターを取得します。|  
|[GetStackGuarantee メソッド](ihosttaskmanager-getstackguarantee-method.md)|スタック操作が完了した後、プロセスが終了する前に使用可能であることが保証されているスタック領域の量を取得します。|  
|[LeaveRuntime メソッド](ihosttaskmanager-leaveruntime-method.md)|マネージコードがアンマネージ関数の呼び出しを実行しようとしていることをホストに通知します。|  
|[ReverseEnterRuntime メソッド](ihosttaskmanager-reverseenterruntime-method.md)|アンマネージコードから共通言語ランタイム (CLR) への呼び出しが行われていることをホストに通知します。|  
|[ReverseLeaveRuntime メソッド](ihosttaskmanager-reverseleaveruntime-method.md)|コントロールが CLR から出ていること、およびマネージコードから呼び出されたアンマネージ関数を入力したことをホストに通知します。|  
|[SetCLRTaskManager メソッド](ihosttaskmanager-setclrtaskmanager-method.md)|CLR によって実装された[ICLRTaskManager](iclrtaskmanager-interface.md)インスタンスへのインターフェイスポインターをホストに提供します。|  
|[SetLocale メソッド](ihosttaskmanager-setlocale-method.md)|CLR によって現在のタスクのロケールが変更されたことをホストに通知します。|  
|[SetStackGuarantee メソッド](ihosttaskmanager-setstackguarantee-method.md)|内部使用専用に予約されています。|  
|[SetUILocale メソッド](ihosttaskmanager-setuilocale-method.md)|現在のタスクでユーザーインターフェイスのロケールが変更されたことをホストに通知します。|  
|[Sleep メソッド](ihosttaskmanager-sleep-method.md)|現在のタスクがスリープ状態になることをホストに通知します。|  
|[SwitchToTask メソッド](ihosttaskmanager-switchtotask-method.md)|現在のタスクを切り替える必要があることをホストに通知します。|  
  
## <a name="remarks"></a>解説  
 `IHostTaskManager`CLR がタスクを作成および管理できるようにします。また、コントロールからアンマネージコードへの転送を制御するときにホストがアクションを実行できるようにしたり、コードの実行中にホストが実行できない特定のアクションを指定したりできるようにします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTask インターフェイス](iclrtask-interface.md)
- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
