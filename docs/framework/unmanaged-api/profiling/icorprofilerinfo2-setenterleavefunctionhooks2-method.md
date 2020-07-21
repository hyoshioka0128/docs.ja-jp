---
title: ICorProfilerInfo2::SetEnterLeaveFunctionHooks2 メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.SetEnterLeaveFunctionHooks2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::SetEnterLeaveFunctionHooks2
helpviewer_keywords:
- ICorProfilerInfo2::SetEnterLeaveFunctionHooks2 method [.NET Framework profiling]
- SetEnterLeaveFunctionHooks2 method [.NET Framework profiling]
ms.assetid: 3c26b3e7-f72b-48a5-bf8c-edc122523a4b
topic_type:
- apiref
ms.openlocfilehash: 78489aae840ff17e68b10bd7593fb7be4dae1af7
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496738"
---
# <a name="icorprofilerinfo2setenterleavefunctionhooks2-method"></a>ICorProfilerInfo2::SetEnterLeaveFunctionHooks2 メソッド
マネージ関数の "enter"、"leave"、および "tailcall" の各フックの更新バージョンで呼び出されるプロファイラー実装関数を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetEnterLeaveFunctionHooks2(  
    [in] FunctionEnter2    *pFuncEnter,  
    [in] FunctionLeave2    *pFuncLeave,  
    [in] FunctionTailcall2 *pFuncTailcall);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFuncEnter`  
 から[FunctionEnter2](functionenter2-function.md)コールバックとして使用される実装へのポインター。  
  
 `pFuncLeave`  
 から[FunctionLeave2](functionleave2-function.md)コールバックとして使用される実装へのポインター。  
  
 `pFuncTailcall`  
 から[FunctionTailcall2](functiontailcall2-function.md)コールバックとして使用される実装へのポインター。  
  
## <a name="remarks"></a>解説  
 `SetEnterLeaveFunctionHooks2`メソッドは、 [ICorProfilerInfo:: SetEnterLeaveFunctionHooks](icorprofilerinfo-setenterleavefunctionhooks-method.md)メソッドに似ています。 前者を使用して、enter/leave/tailcall コールバックの新しいバージョンとして使用する関数を指定します。後者の場合は、以前のバージョンの enter/leave/tailcall コールバックとして使用する関数を指定します。  
  
 コールバックのセットは一度に1つしかアクティブにできません。 したがって、プロファイラーがとの両方を呼び出す `ICorProfilerInfo::SetEnterLeaveFunctionHooks` と `SetEnterLeaveFunctionHooks2` 、 `SetEnterLeaveFunctionHooks2` が使用されます。  
  
 メソッドは、 `SetEnterLeaveFunctionHooks2` プロファイラーの[ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md)コールバックからのみ呼び出すことができます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
