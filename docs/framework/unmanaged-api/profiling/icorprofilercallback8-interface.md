---
title: ICorProfilerCallback8 インターフェイス
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: 617b27923e96d9abc62ccbf158b076c6e45b20a8
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79175097"
---
# <a name="icorprofilercallback8-interface"></a>ICorProfilerCallback8 インターフェイス
[.NET Framework 4.7 以降のバージョンでサポートされています]  

 動的メソッドの JIT コンパイルが開始および終了したことをプロファイラーに通知するために共通言語ランタイムによって使用されるコールバック メソッドを提供する[ICorProfilerCallback7](icorprofilercallback7-interface.md)のサブクラス。
  
## <a name="methods"></a>メソッド  
  
|Method|説明|  
|------------|-----------------|  
|[DynamicMethodJITCompilationStarted メソッド](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)|動的メソッドの JIT コンパイルが開始されたことをプロファイラーに通知します。|  
|[DynamicMethodJITCompilationFinished メソッド](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)|動的メソッドの JIT コンパイルが完了したことをプロファイラーに通知します。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
**.NET Framework のバージョン:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  

## <a name="see-also"></a>関連項目

- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [ICorProfilerCallback9 インターフェイス](icorprofilercallback9-interface.md)
