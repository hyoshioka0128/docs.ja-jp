---
title: ICorProfilerCallback::RuntimeSuspendStarted メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.RuntimeSuspendStarted
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::RuntimeSuspendStarted
helpviewer_keywords:
- ICorProfilerCallback::RuntimeSuspendStarted method [.NET Framework profiling]
- RuntimeSuspendStarted method [.NET Framework profiling]
ms.assetid: c8461cac-e31b-4efa-ad2c-26598173eb96
topic_type:
- apiref
ms.openlocfilehash: cc01254d9604ce39c964c7d78059ef4087483c77
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503225"
---
# <a name="icorprofilercallbackruntimesuspendstarted-method"></a>ICorProfilerCallback::RuntimeSuspendStarted メソッド
ランタイムがすべてのランタイムスレッドを中断しようとしていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RuntimeSuspendStarted(  
    [in] COR_PRF_SUSPEND_REASON suspendReason);  
```  
  
## <a name="parameters"></a>パラメーター  
 `suspendReason`  
 から中断の理由を示す[COR_PRF_SUSPEND_REASON](cor-prf-suspend-reason-enumeration.md)列挙体の値。  
  
## <a name="remarks"></a>解説  
 アンマネージコード内のすべてのランタイムスレッドは、ランタイムを再入力しようとするまで実行を継続できます。 その時点で、ランタイムが再開されるまで中断されます。 これは、ランタイムに入る新しいスレッドにも当てはまります。 ランタイム内のすべてのスレッドは、割り込み可能なコードに既に存在する場合は直ちに中断されます。または、割り込み可能なコードになると中断するように求められます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [RuntimeSuspendAborted メソッド](icorprofilercallback-runtimesuspendaborted-method.md)
- [RuntimeSuspendFinished メソッド](icorprofilercallback-runtimesuspendfinished-method.md)
