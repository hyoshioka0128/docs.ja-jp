---
title: FunctionIDMapper2 関数
ms.date: 03/30/2017
api_name:
- FunctionIDMapper2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionIDMapper2
helpviewer_keywords:
- FunctionIDMapper2 function [.NET Framework profiling]
ms.assetid: 466ad51b-8f0c-41d9-81f7-371aac3374cb
topic_type:
- apiref
ms.openlocfilehash: 65c5d2d4f288d927d79c233374edfec54c0b77ae
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500651"
---
# <a name="functionidmapper2-function"></a>FunctionIDMapper2 関数
指定された関数の識別子が、その関数の[FunctionEnter3](functionenter3-function.md)、 [FunctionLeave3](functionleave3-function.md)、 [FunctionTailcall3](functiontailcall3-function.md)、または[FunctionEnter3WithInfo](functionenter3withinfo-function.md)、 [FunctionLeave3WithInfo](functionleave3withinfo-function.md)、および[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)コールバックで使用される代替 ID に再マップされる可能性があることをプロファイラーに通知します。 また `FunctionIDMapper2` により、プロファイラーはその関数のコールバックを受信するかどうかを示すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
UINT_PTR __stdcall FunctionIDMapper2 (  
    [in]  FunctionID  funcId,  
    [in]  void * clientData,  
    [out] BOOL       *pbHookFunction  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `funcId`

  \[in) 再マップする関数の識別子。

- `clientData`

  \[では、ランタイム間を明確に区別するために使用されるデータへのポインター。

- `pbHookFunction`

  \[out] プロファイラーが、、、、、、、の各コールバックを受信する場合は、に設定する値へのポインター `true` `FunctionEnter3` `FunctionLeave3` `FunctionTailcall3` `FunctionEnter3WithInfo` `FunctionLeave3WithInfo` `FunctionTailcall3WithInfo` 。それ以外の場合は、この値をに設定 `false` します。

## <a name="return-value"></a>戻り値  
 プロファイラーは、実行エンジンが代替関数識別子として使用する値を返します。 `false` で `pbHookFunction` を返さない限り、戻り値を null にすることはできません。 これ以外の状況で戻り値を null にすると、プロセスの中止など、予測できない結果が発生します。  
  
## <a name="remarks"></a>解説  
 このメソッドは、クライアントデータを渡すために使用される追加のパラメーターを使用して[Functionidmapper](functionidmapper-function.md)関数を拡張します。 クライアント データを使用すると、ランタイム間のあいまいさが解消されます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo::SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)
- [ICorProfilerInfo3::SetFunctionIDMapper2](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
