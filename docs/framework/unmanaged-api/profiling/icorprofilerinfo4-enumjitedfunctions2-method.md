---
title: ICorProfilerInfo4::EnumJITedFunctions2 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.EnumJITedFunctions2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::EnumJITedFunctions2
helpviewer_keywords:
- EnumJITedFunctions2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::EnumJITedFunctions2 method [.NET Framework profiling]
ms.assetid: 40e9a1be-9bd2-4fad-9921-34a84b61c1e3
topic_type:
- apiref
ms.openlocfilehash: 2c4a89d5f96ef572518f25bf58a0005454f8e3f0
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496130"
---
# <a name="icorprofilerinfo4enumjitedfunctions2-method"></a>ICorProfilerInfo4::EnumJITedFunctions2 メソッド
以前に JIT コンパイルおよび JIT 再コンパイルされたすべての関数の列挙子を返します。 このメソッドは、JIT 再コンパイルされた Id を列挙しない[ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md)メソッドを置き換えます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力[ICorProfilerFunctionEnum](icorprofilerfunctionenum-interface.md)列挙子へのポインター。  
  
## <a name="remarks"></a>解説  
 このメソッドは `JITCompilation` 、 [ICorProfilerCallback:: JITCompilationStarted](icorprofilercallback-jitcompilationstarted-method.md)メソッドなどのコールバックと重複する場合があります。 返される列挙体には、フィールドの値が含まれ `COR_PRF_FUNCTION::reJitId` ます。 このメソッドで置き換えられる[ICorProfilerInfo3:: EnumJITedFunctions](icorprofilerinfo3-enumjitedfunctions-method.md)メソッドでは、 `COR_PRF_FUNCTION::reJitId` フィールドが常に0に設定されているため、JIT 再コンパイルされた id は列挙されません。 `ICorProfilerInfo4::EnumJITedFunctions`フィールドが適切に設定されているため、メソッドは JIT 再コンパイルされた id を列挙し `COR_PRF_FUNCTION::reJitId` ます。 [ICorProfilerInfo4:: EnumJITedFunctions2](icorprofilerinfo4-enumjitedfunctions2-method.md)メソッドではガベージコレクションをトリガーできるのに対し、 [ICorProfilerInfo3:: EnumJITedFunctions メソッド](icorprofilerinfo3-enumjitedfunctions-method.md)ではトリガーされないことに注意してください。  詳細については、「 [HRESULT CORPROF_E_UNSUPPORTED_CALL_SEQUENCE](corprof-e-unsupported-call-sequence-hresult.md)」を参照してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [EnumJITedFunctions メソッド](icorprofilerinfo3-enumjitedfunctions-method.md)
- [ICorProfilerInfo4 インターフェイス](icorprofilerinfo4-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
