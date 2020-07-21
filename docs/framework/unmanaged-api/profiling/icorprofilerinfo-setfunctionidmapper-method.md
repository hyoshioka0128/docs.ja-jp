---
title: ICorProfilerInfo::SetFunctionIDMapper メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.SetFunctionIDMapper
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::SetFunctionIDMapper
helpviewer_keywords:
- ICorProfilerInfo::SetFunctionIDMapper method [.NET Framework profiling]
- SetFunctionIDMapper method [.NET Framework profiling]
ms.assetid: 1a6e5dae-d366-4497-9c02-7b5b1f43f9ec
topic_type:
- apiref
ms.openlocfilehash: 5272c5bf256f6e21a83470db094ab79317932018
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497479"
---
# <a name="icorprofilerinfosetfunctionidmapper-method"></a>ICorProfilerInfo::SetFunctionIDMapper メソッド
`FunctionID` 値を代替値に対応付けるために呼び出すプロファイラー実装関数を指定します。代替値は、プロファイラーの関数の開始フックと終了フックに渡されます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetFunctionIDMapper (  
    [in] FunctionIDMapper *pFunc);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pFunc`  
 から値を代替値にマップするために呼び出される[Functionidmapper](functionidmapper-function.md)実装へのポインター `FunctionID` 。  
  
## <a name="remarks"></a>解説  
 値の代替手段は、 `FunctionID` [ICorProfilerInfo2:: SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)メソッドによって指定されたプロファイラーの関数の開始/終了フック ([FunctionEnter2](functionenter2-function.md)、 [FunctionLeave2](functionleave2-function.md)、および[FunctionTailcall2](functiontailcall2-function.md)) に渡されます。  
  
 は `FunctionIDMapper` 一度だけ設定でき、 [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md)コールバックで設定することをお勧めします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
