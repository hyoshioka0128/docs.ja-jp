---
title: FunctionLeave 関数
ms.date: 03/30/2017
api_name:
- FunctionLeave
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- FunctionLeave
helpviewer_keywords:
- FunctionLeave function [.NET Framework profiling]
ms.assetid: 18e89f45-e068-426a-be16-9f53a4346860
topic_type:
- apiref
ms.openlocfilehash: 836e4843ead940bc9f76ff6bdd0433e21e400afd
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84500638"
---
# <a name="functionleave-function"></a>FunctionLeave 関数
関数が呼び出し元に戻りようとしていることをプロファイラーに通知します。  
  
> [!NOTE]
> `FunctionLeave`関数は、.NET Framework 2.0 では非推奨とされます。 これは引き続き機能しますが、パフォーマンスが低下します。 代わりに、 [FunctionLeave2](functionleave2-function.md)関数を使用してください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void __stdcall FunctionLeave (  
    [in] FunctionID funcID  
);  
```  
  
## <a name="parameters"></a>パラメーター

- `funcID`

  \[in] を返す関数の識別子。

## <a name="remarks"></a>解説  
 `FunctionLeave`関数はコールバックであるため、実装する必要があります。 実装では、 `__declspec` ( `naked` ) ストレージクラス属性を使用する必要があります。  
  
 この関数を呼び出す前に、実行エンジンはレジスタを保存しません。  
  
- 入力時には、浮動小数点単位 (FPU) に含まれるすべてのレジスタを含め、使用するすべてのレジスタを保存する必要があります。  
  
- 終了時に、呼び出し元によってプッシュされたすべてのパラメーターをポップして、スタックを復元する必要があります。  
  
 の実装は、 `FunctionLeave` ガベージコレクションを遅延させるため、ブロックしないでください。 スタックがガベージコレクションに対応していない可能性があるため、この実装ではガベージコレクションを実行しないようにしてください。 ガベージコレクションが試行された場合、ランタイムはが返されるまでブロックし `FunctionLeave` ます。  
  
 また、 `FunctionLeave` 関数はマネージコードを呼び出さないようにするか、マネージメモリ割り当てを発生させることはできません。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Corprof.idl  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 1.1、1.0  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter2 関数](functionenter2-function.md)
- [FunctionLeave2 関数](functionleave2-function.md)
- [FunctionTailcall2 関数](functiontailcall2-function.md)
- [SetEnterLeaveFunctionHooks2 メソッド](icorprofilerinfo2-setenterleavefunctionhooks2-method.md)
- [グローバル静的関数のプロファイル](profiling-global-static-functions.md)
