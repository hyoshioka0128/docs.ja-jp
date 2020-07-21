---
title: FunctionEnter3WithInfo 関数
ms.date: 03/30/2017
api_name:
- FunctionEnter3WithInfo
api_location:
- mscorwks.cll
api_type:
- COM
f1_keywords:
- FunctionEnter3WithInfo
helpviewer_keywords:
- FunctionEnter3WithInfo function [.NET Framework profiling]
ms.assetid: 277c3344-d0cb-431e-beae-eb1eeeba8eea
topic_type:
- apiref
ms.openlocfilehash: ff4b32185e604611eaaead2847c11bc139d405a6
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500690"
---
# <a name="functionenter3withinfo-function"></a>FunctionEnter3WithInfo 関数
コントロールが関数に渡されていることをプロファイラーに通知し、 [ICorProfilerInfo3:: GetFunctionEnter3Info メソッド](icorprofilerinfo3-getfunctionenter3info-method.md)に渡すことができるハンドルを提供して、スタックフレームと関数の引数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionEnter3WithInfo(  
               [in] FunctionIDOrClientID functionIDOrClientID,  
               [in] COR_PRF_ELT_INFO eltInfo);  
```  
  
## <a name="parameters"></a>パラメーター

- `functionIDOrClientID`

  \[in] コントロールが渡される関数の識別子。

- `eltInfo`

  \[in) 特定のスタックフレームに関する情報を表す不透明なハンドル。 このハンドルは、渡されるコールバック中にのみ有効です。

## <a name="remarks"></a>解説  
 `FunctionEnter3WithInfo`コールバックメソッドは、関数が呼び出されたことをプロファイラーに通知し、プロファイラーが[ICorProfilerInfo3:: GetFunctionEnter3Info メソッド](icorprofilerinfo3-getfunctionenter3info-method.md)を使用して引数値を検査できるようにします。 引数情報にアクセスするには、 `COR_PRF_ENABLE_FUNCTION_ARGS` フラグを設定する必要があります。 プロファイラーは、 [ICorProfilerInfo:: SetEventMask メソッド](icorprofilerinfo-seteventmask-method.md)を使用してイベントフラグを設定し、 [ICorProfilerInfo3:: SetEnterLeaveFunctionHooks3WithInfo メソッド](icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)を使用してこの関数の実装を登録できます。  
  
 `FunctionEnter3WithInfo`関数はコールバックであるため、実装する必要があります。 実装では、ストレージクラス属性を使用する必要があり `__declspec(naked)` ます。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装では `FunctionEnter3WithInfo` 、ガベージコレクションが遅延するため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにする必要があります。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionEnter3WithInfo` ます。  
  
 関数は、 `FunctionEnter3WithInfo` マネージコードを呼び出さないようにするか、マネージメモリの割り当てを任意の方法で発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetFunctionEnter3Info](icorprofilerinfo3-getfunctionenter3info-method.md)
- [FunctionEnter3](functionenter3-function.md)
- [FunctionLeave3](functionleave3-function.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
