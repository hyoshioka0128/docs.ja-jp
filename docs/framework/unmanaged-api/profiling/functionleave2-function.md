---
title: FunctionLeave2 関数
ms.date: 03/30/2017
api_name:
- FunctionLeave2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave2
helpviewer_keywords:
- FunctionLeave2 function [.NET Framework profiling]
ms.assetid: 8cdac941-8b94-4497-b874-4e571785f3fe
topic_type:
- apiref
ms.openlocfilehash: a2a3d58e0631fceab96c32f9d86fef25973fed84
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500664"
---
# <a name="functionleave2-function"></a>FunctionLeave2 関数
関数が呼び出し元に戻り、スタックフレームおよび関数の戻り値に関する情報を提供することをプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionLeave2 (  
    [in]  FunctionID                        funcId,  
    [in]  UINT_PTR                          clientData,  
    [in]  COR_PRF_FRAME_INFO                func,  
    [in]  COR_PRF_FUNCTION_ARGUMENT_RANGE  *retvalRange  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `funcId`

  \[in] を返す関数の識別子。

- `clientData`

  \[in] プロファイラーが以前に[Functionidmapper](functionidmapper-function.md)関数を使用して指定した、再マップされた関数識別子。

- `func`

  \[in] `COR_PRF_FRAME_INFO` スタックフレームに関する情報を示す値。

  プロファイラーは、これを[ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md)メソッドの実行エンジンに渡すことができる不透明なハンドルとして処理する必要があります。  
  
- `retvalRange`

  \[では、関数の戻り値のメモリ位置を指定する[COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md)構造体へのポインター。

  戻り値の情報にアクセスするには、 `COR_PRF_ENABLE_FUNCTION_RETVAL` フラグを設定する必要があります。 プロファイラーは、 [ICorProfilerInfo:: SetEventMask](icorprofilerinfo-seteventmask-method.md)メソッドを使用してイベントフラグを設定できます。

## <a name="remarks"></a>解説  
 値が変更さ `func` `retvalRange` `FunctionLeave2` れるか、値が破棄される可能性があるため、関数から制御が戻った後に、パラメーターとパラメーターの値が無効になります。  
  
 `FunctionLeave2`関数はコールバックであるため、実装する必要があります。 実装では、 `__declspec` ( `naked` ) ストレージクラス属性を使用する必要があります。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装は、 `FunctionLeave2` ガベージコレクションを遅延させるため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにしてください。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionLeave2` ます。  
  
 また、 `FunctionLeave2` 関数はマネージコードを呼び出さないようにするか、マネージメモリ割り当てを発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter2 関数](functionenter2-function.md)
- [FunctionTailcall2 関数](functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 メソッド](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
