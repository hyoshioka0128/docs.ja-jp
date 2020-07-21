---
title: ICorProfilerCallback::RuntimeThreadSuspended メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeThreadSuspended
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeThreadSuspended
helpviewer_keywords:
- RuntimeThreadSuspended method [.NET Framework profiling]
- ICorProfilerCallback::RuntimeThreadSuspended method [.NET Framework profiling]
ms.assetid: de830a8b-6ee1-4900-ace3-4237108f6b12
topic_type:
- apiref
ms.openlocfilehash: 54f7dae511c8bf25dc96451e6477acf26655430a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503199"
---
# <a name="icorprofilercallbackruntimethreadsuspended-method"></a>ICorProfilerCallback::RuntimeThreadSuspended メソッド
指定されたスレッドが中断されたか、中断されようとしていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RuntimeThreadSuspended(  
    [in] ThreadID threadId);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadId`  
 から中断されたスレッドの ID。  
  
## <a name="remarks"></a>解説  
 通知は、 `RuntimeThreadSuspended` [ICorProfilerCallback:: RuntimeSuspendStarted](icorprofilercallback-runtimesuspendstarted-method.md)と、関連付けられている[ICorProfilerCallback:: RuntimeResumeStarted](icorprofilercallback-runtimeresumestarted-method.md)コールバックの間でいつでも発生する可能性があります。 [ICorProfilerCallback:: RuntimeSuspendFinished](icorprofilercallback-runtimesuspendfinished-method.md)との間で発生する通知 `RuntimeResumeStarted` は、アンマネージコードで実行されていて、ランタイムへの入力時に中断されたスレッド用です。  
  
 通常、このコールバックは、スレッドが中断された直後に発生します。 ただし、現在実行中のスレッド (このコールバックを呼び出したスレッド) が中断されているスレッドである場合、このコールバックはスレッドが中断される直前に発生します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [RuntimeThreadResumed メソッド](icorprofilercallback-runtimethreadresumed-method.md)
