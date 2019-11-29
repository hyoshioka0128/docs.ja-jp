---
title: FunctionIDMapper 関数
ms.date: 03/30/2017
api_name:
- FunctionIDMapper
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionIDMapper
helpviewer_keywords:
- FunctionIDMapper function [.NET Framework profiling]
ms.assetid: b8205b60-1893-4303-8cff-7ac5a00892aa
topic_type:
- apiref
ms.openlocfilehash: 23c6f0a29160b6e1dc194cf360c07374c565522b
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74440703"
---
# <a name="functionidmapper-function"></a>FunctionIDMapper 関数
関数の特定の識別子が、その関数の[FunctionEnter2](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)、 [FunctionLeave2](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)、および[FunctionTailcall2](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)コールバックで使用される代替 ID に再マップされる可能性があることをプロファイラーに通知します。 また、`FunctionIDMapper` では、その関数のコールバックを受信するかどうかをプロファイラーが示すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper (  
    [in]  FunctionID  funcId,   
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `funcId`  
 [入力] 再割り当てされる関数識別子。  
  
 `pbHookFunction`  
 入出力プロファイラーが `FunctionEnter2`、`FunctionLeave2`、および `FunctionTailcall2` のコールバックを受信する場合に `true` するように設定する値へのポインター。それ以外の場合は、この値を `false`に設定します。  
  
## <a name="return-value"></a>戻り値  
 プロファイラーは、実行エンジンが代替関数識別子として使用する値を返します。 `false` で `pbHookFunction` を返さない限り、戻り値を null にすることはできません。 それ以外の場合、null 値が返されると、処理が停止する可能性があるなど、予測できない結果が生成されます。  
  
## <a name="remarks"></a>コメント  
 `FunctionIDMapper` 関数はコールバックです。 プロファイラーによって実装され、関数 ID を他の識別子にマップし直すことができます。これは、プロファイラーにとって便利です。 `FunctionIDMapper` は、指定された関数に使用される代替 ID を返します。 その後、実行エンジンは、従来の関数 ID に加えて、この代替 ID を渡してプロファイラーの要求を受け入れ、`FunctionEnter2`、`FunctionLeave2`、および `FunctionTailcall2` フックの `clientData` パラメーターのプロファイラーに戻り、フックが呼び出されている関数を識別します。  
  
 [ICorProfilerInfo:: SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)メソッドを使用して、`FunctionIDMapper` 関数の実装を指定できます。 `ICorProfilerInfo::SetFunctionIDMapper` メソッドは1回だけ呼び出すことができ、 [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md)コールバックで呼び出すことをお勧めします。  
  
 既定では、 [ICorProfilerInfo:: SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)を使用して COR_PRF_MONITOR_ENTERLEAVE フラグを設定し、 [ICorProfilerInfo:: SetEnterLeaveFunctionHooks](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md)または[ICorProfilerInfo2:: SetEnterLeaveFunctionHooks2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-setenterleavefunctionhooks2-method.md)を介してフックを設定するプロファイラーは、すべての関数に対して `FunctionEnter2`、`FunctionLeave2`、および `FunctionTailcall2` コールバックを受け取る必要があることを前提としています。 ただし、`pbHookFunction` を `false`に設定することによって、特定の関数に対してこれらのコールバックが受信されないように、`FunctionIDMapper` を実装する場合があります。  
  
 プロファイラーは、プロファイルされたアプリケーションの複数のスレッドが同時に同じメソッドまたは関数を呼び出す場合を許容します。 このような場合、プロファイラーは同じ `FunctionID`に対して複数の `FunctionIDMapper` コールバックを受け取ることがあります。 同じ `FunctionID`で複数回呼び出された場合、このコールバックから同じ値が返されるようにするには、プロファイラーが適切である必要があります。  
  
## <a name="requirements"></a>要件  
 **:** 「[システム要件](../../../../docs/framework/get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [SetFunctionIDMapper メソッド](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)
- [FunctionIDMapper2 関数](../../../../docs/framework/unmanaged-api/profiling/functionidmapper2-function.md)
- [FunctionEnter2 関数](../../../../docs/framework/unmanaged-api/profiling/functionenter2-function.md)
- [FunctionLeave2 関数](../../../../docs/framework/unmanaged-api/profiling/functionleave2-function.md)
- [FunctionTailcall2 関数](../../../../docs/framework/unmanaged-api/profiling/functiontailcall2-function.md)
- [グローバル静的関数のプロファイル](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)
