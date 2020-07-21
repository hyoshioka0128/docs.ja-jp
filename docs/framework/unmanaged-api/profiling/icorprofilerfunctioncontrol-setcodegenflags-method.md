---
title: ICorProfilerFunctionControl::SetCodegenFlags メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetCodegenFlags
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetCodegenFlags
helpviewer_keywords:
- ICorProfilerFunctionControl::SetCodegenFlags method [.NET Framework profiling]
- SetCodegenFlags method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: a2d5daa5-b990-4ae5-bf2a-c0862fe58bd7
topic_type:
- apiref
ms.openlocfilehash: a3d5527fc34ad7292974c005179e9d9cad210c94
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503121"
---
# <a name="icorprofilerfunctioncontrolsetcodegenflags-method"></a>ICorProfilerFunctionControl::SetCodegenFlags メソッド
[COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md)列挙型の1つ以上のフラグを設定して、JUST-IN-TIME (JIT) 再コンパイル関数のコード生成を制御します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetCodegenFlags(  
    [in] DWORD flags);  
```  
  
## <a name="parameters"></a>パラメーター  
 `flags`  
 から[COR_PRF_CODEGEN_FLAGS](cor-prf-codegen-flags-enumeration.md)列挙体の1つ以上のフラグ。  
  
## <a name="remarks"></a>解説  
 プロファイラーは、 [ICorProfilerCallback4:: GetReJITParameters](icorprofilercallback4-getrejitparameters-method.md)コールバックを使用して、このインターフェイスのインスタンスを取得します。 `SetCodegenFlags`プロファイラーが再コンパイルされた関数のコード生成を制御できるようにします。 他のすべての JIT 再コンパイルパラメーターと同様に、コード生成フラグは関数のすべてのインスタンスに適用されます。  
  
 JIT コンパイラは、関数をコンパイルするときに、これらのコンパイルフラグを他のソースによって指定された他のフラグと共に考慮します。  その他のソースには、デバッガー、 [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)メソッド (値と) を使用した起動時のプロファイラーによって設定されたグローバルフラグ、 `COR_PRF_DISABLE_INLINING` `COR_PRF_DISABLE_OPTIMIZATIONS` およびプロファイラーの[ICorProfilerCallback:: JITInlining](icorprofilercallback-jitinlining-method.md)コールバックが含まれます。  JIT コンパイラは、最小限の最適化を要求するソースに優先順位を付けます。  たとえば、プロファイラーが起動時にを指定し、 `COR_PRF_DISABLE_INLINING` `COR_PRF_CODEGEN_DISABLE_INLINING` [ICorProfilerFunctionControl:: SetCodegenFlags](icorprofilerfunctioncontrol-setcodegenflags-method.md)コールバックでを指定していない場合でも、インライン展開は無効になります。  同様に、プロファイラーででを指定せず、 `COR_PRF_CODEGEN_DISABLE_INLINING` `SetCodegenFlags` [ICorProfilerCallback:: JITInlining](icorprofilercallback-jitinlining-method.md)コールバックを使用してインライン展開を無効にした場合は、インライン展開が無効になります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerFunctionControl インターフェイス](icorprofilerfunctioncontrol-interface.md)
