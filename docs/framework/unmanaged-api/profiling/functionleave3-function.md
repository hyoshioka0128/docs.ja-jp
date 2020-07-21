---
title: FunctionLeave3 関数
ms.date: 03/30/2017
api_name:
- FunctionLeave3
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave3
helpviewer_keywords:
- FunctionLeave3 function [.NET Framework profiling]
ms.assetid: 5d798088-7992-48a0-ae55-d2a7ee31913f
topic_type:
- apiref
ms.openlocfilehash: 456d9a0e8236948ac69ed069495b1999ebf7e80a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500612"
---
# <a name="functionleave3-function"></a>FunctionLeave3 関数
関数から制御が返されていることをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionLeave3(FunctionOrRemappedID functionOrRemappedID);  
```  
  
## <a name="parameters"></a>パラメーター  

- `functionOrRemappedID`

  \[in] コントロールが返される関数の識別子。
  
## <a name="remarks"></a>解説  
 `FunctionLeave3`コールバック関数は、関数が呼び出されていることをプロファイラーに通知しますが、戻り値の検査はサポートしていません。 [ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3 メソッド](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)を使用して、この関数の実装を登録します。  
  
 `FunctionLeave3`関数はコールバックであるため、実装する必要があります。 実装では、ストレージクラス属性を使用する必要があり `__declspec(naked)` ます。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装では `FunctionLeave3` 、ガベージコレクションが遅延するため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにする必要があります。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionLeave3` ます。  
  
 関数は、 `FunctionLeave3` マネージコードを呼び出さないようにするか、マネージメモリの割り当てを任意の方法で発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter3](functionenter3-function.md)
- [FunctionTailcall3](functiontailcall3-function.md)
- [FunctionEnter3WithInfo](functiontailcall3-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [SetEnterLeaveFunctionHooks3](icorprofilerinfo3-setenterleavefunctionhooks3-method.md)
- [SetEnterLeaveFunctionHooks3WithInfo](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)
- [SetFunctionIDMapper](icorprofilerinfo-setfunctionidmapper-method.md)
- [SetFunctionIDMapper2](icorprofilerinfo3-setfunctionidmapper2-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
