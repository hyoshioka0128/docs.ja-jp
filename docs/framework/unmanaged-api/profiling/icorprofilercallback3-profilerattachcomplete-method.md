---
title: ICorProfilerCallback3::ProfilerAttachComplete メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback3.ProfilerAttachComplete Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback3::ProfilerAttachComplete
helpviewer_keywords:
- ProfilerAttachComplete method [.NET Framework profiling]
- ICorProfilerCallback3::ProfilerAttachComplete method [.NET Framework profiling]
ms.assetid: 257d6076-06e0-4d93-bb33-651fbb2b92d7
topic_type:
- apiref
ms.openlocfilehash: bcc938ff9322fca4f45366fdc695e0c3901484b5
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499663"
---
# <a name="icorprofilercallback3profilerattachcomplete-method"></a>ICorProfilerCallback3::ProfilerAttachComplete メソッド
プロファイラーが[ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md)および[ICorProfilerInfo3:: enummodules](icorprofilerinfo3-enummodules-method.md)のキャッチアップメソッドを呼び出せるようになったことを示すために、共通言語ランタイム (CLR) によって呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ProfilerAttachComplete ();  
```  
  
## <a name="remarks"></a>解説  
 `ProfilerAttachComplete`コールバックは、 [ICorProfilerCallback3:: InitializeForAttach](icorprofilercallback3-initializeforattach-method.md)メソッドが呼び出された後に発行されます。 これは、次のことを示します。  
  
- `InitializeForAttach` でプロファイラーによって要求されたコールバックがアクティブ化されました。  
  
- プロファイラーは、通知されないことを心配せずに、関連付けられた ID でキャッチアップを実行できます。  
  
 CLR はこのコールバックからの戻り値を無視します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerCallback インターフェイス](icorprofilercallback-interface.md)
- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
