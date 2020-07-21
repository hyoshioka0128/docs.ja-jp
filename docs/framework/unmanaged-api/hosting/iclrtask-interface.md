---
title: ICLRTask インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRTask
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRTask
helpviewer_keywords:
- ICLRTask interface [.NET Framework hosting]
ms.assetid: b3a44df3-578a-4451-b55e-70c8e7695f5e
topic_type:
- apiref
ms.openlocfilehash: b1327e13006ca4b3f9074c1348b1817c9a1b3728
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503953"
---
# <a name="iclrtask-interface"></a>ICLRTask インターフェイス
ホストが共通言語ランタイム (CLR) の要求を行うことができるようにするメソッド、または関連付けられたタスクについて CLR に通知を提供するためのメソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Abort メソッド](iclrtask-abort-method.md)|現在のインスタンスが表すタスクを CLR が中止することを要求 `ICLRTask` します。|  
|[ExitTask メソッド](iclrtask-exittask-method.md)|現在のインスタンスに関連付けられているタスクが終了したことを CLR に通知 `ICLRTask` し、タスクを正常にシャットダウンしようとします。|  
|[GetMemStats メソッド](iclrtask-getmemstats-method.md)|現在のインスタンスによって表されるタスクによるメモリリソースの使用に関する統計情報を取得し `ICLRTask` ます。|  
|[LocksHeld メソッド](iclrtask-locksheld-method.md)|タスクに現在保持されているロックの数を取得します。|  
|[NeedsPriorityScheduling メソッド](iclrtask-needspriorityscheduling-method.md)|現在のインスタンスによって表されるタスクを再スケジュールするために、優先順位の高いホストを割り当てる必要があるかどうかを示す値を取得し `ICLRTask` ます。|  
|[Reset メソッド](iclrtask-reset-method.md)|ホストがタスクを完了したことを CLR に通知し、CLR が現在のインスタンスを再利用して別のタスクを表すことができるようにし `ICLRTask` ます。|  
|[RudeAbort メソッド](iclrtask-rudeabort-method.md)|CLR が、 `ICLRTask` ファイナライザーが実行されることを保証せずに、現在のインスタンスによって表されるタスクをすぐに中止します。|  
|[SetTaskIdentifier メソッド](iclrtask-settaskidentifier-method.md)|デバッグに使用するために、現在のインスタンスによって表されるタスクの一意の識別子を設定し `ICLRTask` ます。|  
|[SwitchIn メソッド](iclrtask-switchin-method.md)|現在のインスタンスによって表されるタスクが操作可能な状態であることを CLR に通知し `ICLRTask` ます。|  
|[SwitchOut メソッド](iclrtask-switchout-method.md)|現在のインスタンスによって表されるタスクが操作可能 `ICLRTask` な状態ではなくなったことを CLR に通知します。|  
|[YieldTask メソッド](iclrtask-yieldtask-method.md)|CLR がプロセッサ時間を他のタスクで使用できるようにすることを要求します。 CLR では、処理時間を生成できる状態にタスクが配置されるという保証はありません。|  
  
## <a name="remarks"></a>解説  
 `ICLRTask`は、CLR のタスクの表現です。 コードの実行中はいつでも、実行中または実行の待機中のいずれかのタスクを記述できます。 ホストは、メソッドを呼び出して、 `ICLRTask::SwitchIn` 現在のインスタンスが表すタスクが操作可能 `ICLRTask` な状態になったことを CLR に通知します。 を呼び出した後、 `ICLRTask::SwitchIn` ホストは任意のオペレーティングシステムスレッドでタスクをスケジュールできます。ただし、 [IHostTaskManager:: beginthreadaffinity](ihosttaskmanager-beginthreadaffinity-method.md)メソッドと[IHostTaskManager:: endthreadaffinity](ihosttaskmanager-endthreadaffinity-method.md)メソッドの呼び出しで指定されているように、ランタイムにスレッドアフィニティが必要な場合を除きます。 しばらくすると、オペレーティングシステムは、スレッドからタスクを削除して、実行されていない状態にする可能性があります。 たとえば、タスクが同期プリミティブでブロックされた場合や、i/o 操作が完了するまで待機している場合に発生することがあります。 ホストは[Switchout](iclrtask-switchout-method.md)を呼び出して、現在のインスタンスによって表されるタスクが操作可能 `ICLRTask` な状態ではなくなったことを CLR に通知します。  
  
 タスクは通常、コード実行の終了時に終了します。 その時点で、ホストは `ICLRTask::ExitTask` を呼び出して、関連付けられているを破棄し `ICLRTask` ます。 ただし、の呼び出しを使用してタスクをリサイクルすることもでき `ICLRTask::Reset` ます。これにより、 `ICLRTask` インスタンスを再度使用できます。 この方法では、インスタンスを繰り返し作成および破棄するオーバーヘッドを回避できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICLRTaskManager インターフェイス](iclrtaskmanager-interface.md)
- [IHostTask インターフェイス](ihosttask-interface.md)
- [IHostTaskManager インターフェイス](ihosttaskmanager-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [ICLRTask2 インターフェイス](iclrtask2-interface.md)
