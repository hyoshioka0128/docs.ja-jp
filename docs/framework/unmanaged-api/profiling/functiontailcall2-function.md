---
title: FunctionTailcall2 関数
ms.date: 03/30/2017
api_name:
- FunctionTailcall2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionTailcall2
helpviewer_keywords:
- FunctionTailcall2 function [.NET Framework profiling]
ms.assetid: 249f9892-b5a9-41e1-b329-28a925904df6
topic_type:
- apiref
ms.openlocfilehash: cb7e21e0c6aad5ebb328ae5d1a993716f96e8d47
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500573"
---
# <a name="functiontailcall2-function"></a>FunctionTailcall2 関数
現在実行中の関数が別の関数の末尾呼び出しを実行しようとしていることをプロファイラーに通知し、スタックフレームに関する情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp
void __stdcall FunctionTailcall2 (  
    [in] FunctionID         funcId,
    [in] UINT_PTR           clientData,
    [in] COR_PRF_FRAME_INFO func  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `funcId`

  \[in] 末尾呼び出しを実行しようとしている現在実行中の関数の識別子。

- `clientData`

  \[では、現在実行中の関数の末尾呼び出しを実行しようとしているときに、プロファイラーが以前に[Functionidmapper](functionidmapper-function.md)を使用して指定したリマップ関数識別子。
  
- `func`

  \[in] `COR_PRF_FRAME_INFO` スタックフレームに関する情報を示す値。

  プロファイラーは、これを[ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md)メソッドの実行エンジンに渡すことができる不透明なハンドルとして処理する必要があります。

## <a name="remarks"></a>解説  
 Tail 呼び出しの対象となる関数は、現在のスタックフレームを使用し、末尾呼び出しを行った関数の呼び出し元に直接戻ります。 つまり、 [FunctionLeave2](functionleave2-function.md)コールバックは、末尾呼び出しのターゲットである関数に対しては発行されません。  
  
 `func` `FunctionTailcall2` 値が変更または破棄される可能性があるため、関数がを返すと、パラメーターの値が無効になります。  
  
 `FunctionTailcall2`関数はコールバックであるため、実装する必要があります。 実装では、 `__declspec` ( `naked` ) ストレージクラス属性を使用する必要があります。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装は、 `FunctionTailcall2` ガベージコレクションを遅延させるため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにしてください。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionTailcall2` ます。  
  
 また、 `FunctionTailcall2` 関数はマネージコードを呼び出さないようにするか、マネージメモリ割り当てを発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter2 関数](functionenter2-function.md)
- [FunctionLeave2 関数](functionleave2-function.md)
- [SetEnterLeaveFunctionHooks2 メソッド](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
