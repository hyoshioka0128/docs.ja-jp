---
title: ICorProfilerInfo3::GetFunctionTailcall3Info メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo3.GetFunctionTailcall3Info Method
api_location:
- Mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo3::GetFunctionTailcall3Info
helpviewer_keywords:
- ICorProfilerInfo3::GetFunctionTailcall3Info method [.NET Framework profiling]
- GetFunctionTailcall3Info method [.NET Framework profiling]
ms.assetid: afdb5ac9-5bf5-4b91-b7cb-f81db23d7da3
topic_type:
- apiref
ms.openlocfilehash: e4d0d9ed07c707e51e5833483b71079f2c330505
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84496530"
---
# <a name="icorprofilerinfo3getfunctiontailcall3info-method"></a>ICorProfilerInfo3::GetFunctionTailcall3Info メソッド
[FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)関数によってプロファイラーに報告される関数のスタックフレームを提供します。 このメソッドは、`FunctionTailcall3WithInfo` コールバック中にのみ呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunctionTailcall3Info(
            [in]  FunctionID functionId,
            [in]  COR_PRF_ELT_INFO eltInfo,  
            [out] COR_PRF_FRAME_INFO *pFrameInfo);  
```  
  
## <a name="parameters"></a>パラメーター  
 `functionId`  
 からを `FunctionID` 返す関数の。  
  
 `eltInfo`  
 [in] 特定のスタック フレームに関する情報を表す不透明ハンドル。 プロファイラーは、 `eltInfo` 関数によってプロファイラーに与えられたものと同じを提供する必要があり `FunctionTailcall3WithInfo` ます。  
  
 `pFrameInfo`  
 [out] 特定のスタック フレームに関するジェネリック情報を表す不透明ハンドル。 このハンドルは、プロファイラーが `FunctionTailcall3WithInfo` メソッドを呼び出した `GetFunctionTailcall3Info` コールバック内でのみ有効です。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [FunctionEnter3WithInfo](functionenter3withinfo-function.md)
- [FunctionLeave3WithInfo](functionleave3withinfo-function.md)
- [FunctionTailcall3WithInfo](functiontailcall3withinfo-function.md)
- [ICorProfilerInfo3 インターフェイス](icorprofilerinfo3-interface.md)
- [プロファイリングのインターフェイス](profiling-interfaces.md)
- [プロファイル](index.md)
