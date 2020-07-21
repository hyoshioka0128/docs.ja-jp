---
title: ICorProfilerCallback8::D ynamicMethodJITCompilationStarted メソッド
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8.DynamicMethodJITCompilationStarted
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
ms.openlocfilehash: a4c434c5d458602db8a4d582b239d6e57def6ace
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84499000"
---
# <a name="icorprofilercallback8dynamicmethodjitcompilationstarted-method"></a>ICorProfilerCallback8::D ynamicMethodJITCompilationStarted メソッド
[.NET Framework 4.7 以降のバージョンでサポートされています]  
  
動的メソッドの JIT コンパイルが開始されるたびにプロファイラーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DynamicMethodJITCompilationStarted(  
     [in]  FunctionID  functionId,
     [in]  BOOL        fIsSafeToBlock,
     [in]  LPCBYTE     pILHeader,
     [in]  LONG        cbILHeader
);  
```  
  
## <a name="parameters"></a>パラメーター  
[入力] `functionId`  
JIT コンパイルが開始されるメモリ内関数の識別子。

[入力] `fIsSafeToBlock` 
 `true`ブロックが原因で、ランタイムが呼び出し元のスレッドがこのコールバックから戻るのを待機する場合があることを示します。`false`ブロックがランタイムの動作に影響を与えないことを示す場合。  

[入力] `pILHeader`メソッドの IL ヘッダーの最初のバイトへのポインター。

[入力] `cbILHeader`IL ヘッダー内のバイト数。

## <a name="remarks"></a>解説  

このコールバックは、動的メソッドが JIT コンパイルされるたびにトリガーされます。 これには、さまざまな IL スタブおよび LCG メソッドが含まれます。 その目的は、コンパイルされたメソッドをユーザーに識別するのに十分な情報をプロファイラーライターに提供することです。

> [!NOTE]
> `functionId`動的メソッドにはメタデータがないため、値を使用してメタデータトークンを解決することはできません。

`pILHeader`ポインターは、コールバック中にのみ有効です。

## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  
  
## <a name="see-also"></a>関連項目

- [DynamicMethodJITCompilationFinished メソッド](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
- [ICorProfilerCallback8 インターフェイス](icorprofilercallback8-interface.md)
