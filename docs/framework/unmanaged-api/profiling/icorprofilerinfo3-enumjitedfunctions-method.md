---
title: ICorProfilerInfo3::EnumJITedFunctions メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.EnumJITedFunctions Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::EnumJITedFunctions
helpviewer_keywords:
- ICorProfilerInfo3::EnumJITedFunctions method [.NET Framework profiling]
- EnumJITedFunctions method [.NET Framework profiling]
ms.assetid: e2847a36-f460-45e2-9b6c-b33b008f40d9
topic_type:
- apiref
ms.openlocfilehash: 3ebf4a7706b3d3495e4a617b4f86a50281115436
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496556"
---
# <a name="icorprofilerinfo3enumjitedfunctions-method"></a>ICorProfilerInfo3::EnumJITedFunctions メソッド
以前に JIT でコンパイルされたすべての関数の列挙子を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力[ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)列挙子へのポインター。  
  
## <a name="remarks"></a>解説  
 このメソッドは `JITCompilation` 、 [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)メソッドなどのコールバックと重複する場合があります。 このメソッドによって返される列挙子には、Ngen.exe で生成されたネイティブイメージから読み込まれた関数は含まれません。  
  
> [!NOTE]
> 返された列挙体には、フィールドの値に対して "0" のみが含まれ `COR_PRF_FUNCTION::reJitId` ます。  有効な値が必要な場合は `COR_PRF_FUNCTION::reJitId` 、 [ICorProfilerInfo4:: EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md)メソッドを使用します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
