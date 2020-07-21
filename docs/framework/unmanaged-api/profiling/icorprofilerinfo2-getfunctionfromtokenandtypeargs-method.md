---
title: ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetFunctionFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs
helpviewer_keywords:
- ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
- GetFunctionFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: ce8f6aa6-4ebf-4a86-b429-4bbc8af41a8f
topic_type:
- apiref
ms.openlocfilehash: 7f1276e1adeece086ca7b6791eb6e870faf4d010
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502874"
---
# <a name="icorprofilerinfo2getfunctionfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetFunctionFromTokenAndTypeArgs メソッド
`FunctionID`指定されたメタデータトークン、クラス、および `ClassID` 任意の型引数の値を使用して、関数のを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunctionFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdMethodDef funcDef,  
    [in] ClassID classId,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] FunctionID* pFunctionID);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleID`  
 から関数が存在するモジュールの ID。  
  
 `funcDef`  
 から`mdMethodDef`関数を参照するメタデータトークン。  
  
 `classId`  
 からクラスを含んでいる関数の ID。  
  
 `cTypeArgs`  
 から指定された関数の型パラメーターの数。 非ジェネリック関数の場合、この値は0である必要があります。  
  
 `typeArgs`  
 から値の配列 `ClassID` 。それぞれが関数の引数です。 が0に設定されている場合、の値は `typeArgs` NULL `cTypeArgs` になります。  
  
 `pFunctionID`  
 入出力`FunctionID`指定した関数のへのポインター。  
  
## <a name="remarks"></a>解説  
 メタデータ `GetFunctionFromTokenAndTypeArgs` トークンではなくメタデータを使用してメソッドを呼び出すと、 `mdMethodRef` `mdMethodDef` 予期しない結果が発生する可能性があります。 呼び出し元は、 `mdMethodRef` を渡すときにをに解決する必要があり `mdMethodDef` ます。  
  
 関数がまだ読み込まれていない場合、を呼び出すと `GetFunctionFromTokenAndTypeArgs` 読み込みが発生します。これは、多くのコンテキストでは危険な操作です。 たとえば、モジュールまたは型の読み込み中にこのメソッドを呼び出すと、ランタイムが循環読み込みを試みたときに無限ループが発生する可能性があります。  
  
 一般に、の使用 `GetFunctionFromTokenAndTypeArgs` は推奨されていません。 プロファイラーが特定の関数のイベントに関心を持っている場合は、 `ModuleID` その関数のとを格納し、 `mdMethodDef` [ICorProfilerInfo2:: GetFunctionInfo2](icorprofilerinfo2-getfunctioninfo2-method.md)を使用して、 `FunctionID` 目的の関数のが指定されているかどうかを確認します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
