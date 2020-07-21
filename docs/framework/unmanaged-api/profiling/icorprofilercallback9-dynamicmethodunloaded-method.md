---
title: ICorProfilerCallback9::D ynamicMethodUnloaded メソッド
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback9.DynamicMethodUnloaded
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: 2391ad854b17ec117940a3d3568c40d6cf7f4725
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84498974"
---
# <a name="icorprofilercallback9dynamicmethodunloaded-method"></a>ICorProfilerCallback9::D ynamicMethodUnloaded メソッド
[.NET Framework 4.7.2 以降のバージョンでサポートされています]  
  
動的メソッドがガベージコレクションされ、その後アンロードされるたびに、プロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DynamicMethodUnloaded(  
     [in]  FunctionID  functionId
);  
```  
  
## <a name="parameters"></a>パラメーター  
[入力] `functionId`  
ガベージコレクションおよびアンロードされたメモリ内の関数の識別子。

## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback8 DynamicMethodJITCompilationStarted メソッド](icorprofilercallback8-dynamicmethodjitcompilationstarted-method.md)
- [ICorProfilerCallback8 DynamicMethodJITCompilationFinished メソッド](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
- [ICorProfilerCallback9 インターフェイス](icorprofilercallback9-interface.md)
- [COR_PRF_HIGH_MONITOR_DYNAMIC_FUNCTION_UNLOADS](cor-prf-high-monitor-enumeration.md)
