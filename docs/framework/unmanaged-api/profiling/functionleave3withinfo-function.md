---
title: FunctionLeave3WithInfo 関数
ms.date: 03/30/2017
api_name:
- FunctionLeave3WithInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave3WithInfo
helpviewer_keywords:
- FunctionLeave3WithInfo function [.NET Framework profiling]
ms.assetid: 5fa68a67-ced6-41c6-a2c0-467060fd0692
topic_type:
- apiref
ms.openlocfilehash: 235bae64fe5e6a534f2a650050c6c9ad4aa8fe84
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500625"
---
# <a name="functionleave3withinfo-function"></a>FunctionLeave3WithInfo 関数
関数から制御が返されていることをプロファイラーに通知し、スタックフレームと戻り値を取得するために[ICorProfilerInfo3:: GetFunctionLeave3Info メソッド](icorprofilerinfo3-getfunctionleave3info-method.md)に渡すことができるハンドルを提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionLeave3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a>パラメーター

- `functionIDOrClientID`

  \[in] コントロールが返される関数の識別子。

- `eltInfo`

  \[in) 特定のスタックフレームに関する情報を表す不透明なハンドル。 このハンドルは、渡されるコールバック中にのみ有効です。

## <a name="remarks"></a>解説  
 `FunctionLeave3WithInfo`コールバックメソッドは、関数が呼び出されたことをプロファイラーに通知します。また、プロファイラーは[ICorProfilerInfo3:: GetFunctionLeave3Info メソッド](icorprofilerinfo3-getfunctionleave3info-method.md)を使用して、戻り値を調べることができます。 戻り値の情報にアクセスするには、 `COR_PRF_ENABLE_FUNCTION_RETVAL` フラグを設定する必要があります。 プロファイラーは、 [ICorProfilerInfo:: SetEventMask メソッド](icorprofilerinfo-seteventmask-method.md)を使用してイベントフラグを設定し、 [ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3WithInfo メソッド](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)を使用してこの関数の実装を登録できます。  
  
 `FunctionLeave3WithInfo`関数はコールバックであるため、実装する必要があります。 実装では、ストレージクラス属性を使用する必要があり `__declspec(naked)` ます。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装では `FunctionLeave3WithInfo` 、ガベージコレクションが遅延するため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにする必要があります。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionLeave3WithInfo` ます。  
  
 関数は、 `FunctionLeave3WithInfo` マネージコードを呼び出さないようにするか、マネージメモリの割り当てを任意の方法で発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetFunctionLeave3Info](icorprofilerinfo3-getfunctionleave3info-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)
- [SetFunctionIDMapper2](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
