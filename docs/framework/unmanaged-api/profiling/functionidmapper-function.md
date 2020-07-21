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
ms.openlocfilehash: afc818dfe625bfc329ceb1660539eb119702a90d
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500677"
---
# <a name="functionidmapper-function"></a>FunctionIDMapper 関数
関数の特定の識別子が、その関数の[FunctionEnter2](functionenter2-function.md)、 [FunctionLeave2](functionleave2-function.md)、および[FunctionTailcall2](functiontailcall2-function.md)コールバックで使用される代替 ID に再マップされる可能性があることをプロファイラーに通知します。 また `FunctionIDMapper` により、プロファイラーはその関数のコールバックを受信するかどうかを示すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper (  
    [in]  FunctionID  funcId,
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `funcId`

  \[in) 再マップする関数の識別子。

- `pbHookFunction`

  \[out] プロファイラーが、、の各コールバックを受信する場合は、に設定する値へのポインター `true` `FunctionEnter2` `FunctionLeave2` `FunctionTailcall2` 。それ以外の場合は、この値をに設定 `false` します。

## <a name="return-value"></a>戻り値  
 プロファイラーは、実行エンジンが代替関数識別子として使用する値を返します。 `false` で `pbHookFunction` を返さない限り、戻り値を null にすることはできません。 それ以外の場合、null 値が返されると、処理が停止する可能性があるなど、予測できない結果が生成されます。  
  
## <a name="remarks"></a>解説  
 `FunctionIDMapper`関数はコールバックです。 プロファイラーによって実装され、関数 ID を他の識別子にマップし直すことができます。これは、プロファイラーにとって便利です。 は、指定された `FunctionIDMapper` 関数に使用される代替 ID を返します。 次に、実行エンジンは、従来の関数 ID に加えて、この代替 ID を `clientData` 、、、およびフックのパラメーターでプロファイラーに渡して `FunctionEnter2` 、 `FunctionLeave2` フックが呼び出されている関数を識別することによって、プロファイラーの要求を受け入れ `FunctionTailcall2` ます。  
  
 [ICorProfilerInfo:: SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)メソッドを使用して、関数の実装を指定でき `FunctionIDMapper` ます。 メソッドを呼び出すことができるのは1回だけです。このメソッドは、 `ICorProfilerInfo::SetFunctionIDMapper` [ICorProfilerCallback:: Initialize](icorprofilercallback-initialize-method.md)コールバックで行うことをお勧めします。  
  
 既定では、 [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)を使用して COR_PRF_MONITOR_ENTERLEAVE フラグを設定し、 [ICorProfilerInfo:: SetEnterLeaveFunctionHooks](icorprofilerinfo-setenterleavefunctionhooks-method.md)または[ICorProfilerInfo2:: SetEnterLeaveFunctionHooks2](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)を介してフックを設定するプロファイラーは `FunctionEnter2` 、 `FunctionLeave2` `FunctionTailcall2` すべての関数に対して、、およびのコールバックを受け取る必要があると想定されています。 ただし、 `FunctionIDMapper` をに設定することにより、特定の関数に対してこれらのコールバックが受信されないように、を実装する場合があり `pbHookFunction` `false` ます。  
  
 プロファイラーは、プロファイルされたアプリケーションの複数のスレッドが同時に同じメソッドまたは関数を呼び出す場合を許容します。 このような場合、プロファイラーは同じに `FunctionIDMapper` 対して複数のコールバックを受け取ることがあり `FunctionID` ます。 プロファイラーは、同じを使用して複数回呼び出された場合に、このコールバックから同じ値を返すようにする必要があり `FunctionID` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [SetFunctionIDMapper メソッド](icorprofilerinfo-setfunctionidmapper-method.md)
- [FunctionIDMapper2 関数](functionidmapper2-function.md)
- [FunctionEnter2 関数](functionenter2-function.md)
- [FunctionLeave2 関数](functionleave2-function.md)
- [FunctionTailcall2 関数](functiontailcall2-function.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
