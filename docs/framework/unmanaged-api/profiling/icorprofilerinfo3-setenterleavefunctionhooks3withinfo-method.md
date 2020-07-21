---
title: ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.SetEnterLeaveFunctionHooks3WithInfo Method
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo
helpviewer_keywords:
- SetEnterLeaveFunctionHooks3WithInfo method [.NET Framework profiling]
- ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo method [.NET Framework profiling]
ms.assetid: ca8ea534-e441-47b8-be85-466410988c0a
topic_type:
- apiref
ms.openlocfilehash: d40cb424306535cc502d930dd61e6a1e254667da
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496179"
---
# <a name="icorprofilerinfo3setenterleavefunctionhooks3withinfo-method"></a>ICorProfilerInfo3::SetEnterLeaveFunctionHooks3WithInfo メソッド
マネージ関数の[FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)フックで呼び出されるプロファイラー実装関数を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetEnterLeaveFunctionHooks3WithInfo(  
            [in] FunctionEnter3WithInfo    *pFuncEnter3,  
            [in] FunctionLeave3withInfo    *pFuncLeave3,  
            [in] FunctionTailcall3WithInfo *pFuncTailcall3);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFuncEnter3`  
 からコールバックとして使用される実装へのポインター `FunctionEnter3WithInfo` 。  
  
 `pFuncLeave3`  
 からコールバックとして使用される実装へのポインター `FunctionLeave3WithInfo` 。  
  
 `pFuncTailcall3`  
 からコールバックとして使用される実装へのポインター `FunctionTailcall3WithInfo` 。  
  
## <a name="remarks"></a>解説  
 [FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)の各フックは、スタックフレームと引数の検査を提供します。 この情報にアクセスするには、 `COR_PRF_ENABLE_FUNCTION_ARGS` 、 `COR_PRF_ENABLE_FUNCTION_RETVAL` 、および/または `COR_PRF_ENABLE_FRAME_INFO` フラグを設定する必要があります。 プロファイラーは、 [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)メソッドを使用してイベントフラグを設定し、メソッドを使用し `SetEnterLeaveFunctionHooks3WithInfo` てこの関数の実装を登録できます。  
  
 コールバックのセットは一度に1つしかアクティブにできません。また、最新バージョンが優先されます。 したがって、プロファイラーが[SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)との両方を呼び出すと `SetEnterLeaveFunctionHooks3WithInfo` 、 `SetEnterLeaveFunctionHooks3WithInfo` が使用されます。  
  
 メソッドは、 `SetEnterLeaveFunctionHooks3WithInfo` プロファイラーの[ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md)コールバックからのみ呼び出すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
