---
title: ICorProfilerInfo2::GetClassFromTokenAndTypeArgs メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo2.GetClassFromTokenAndTypeArgs
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo2::GetClassFromTokenAndTypeArgs
helpviewer_keywords:
- GetClassFromTokenAndTypeArgs method [.NET Framework profiling]
- ICorProfilerInfo2::GetClassFromTokenAndTypeArgs method [.NET Framework profiling]
ms.assetid: b25c88f0-71b9-443b-8eea-1c94db0a44b9
topic_type:
- apiref
ms.openlocfilehash: 702c5f9f2bc08c824bdc0607741a6afd65a3e89b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84497258"
---
# <a name="icorprofilerinfo2getclassfromtokenandtypeargs-method"></a>ICorProfilerInfo2::GetClassFromTokenAndTypeArgs メソッド
`ClassID`指定されたメタデータトークンと `ClassID` 任意の型引数の値を使用して、型のを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetClassFromTokenAndTypeArgs(  
    [in] ModuleID moduleID,  
    [in] mdTypeDef typeDef,  
    [in] ULONG32 cTypeArgs,  
    [in, size_is(cTypeArgs)] ClassID typeArgs[],  
    [out] ClassID* pClassID);  
```  
  
## <a name="parameters"></a>パラメーター  
 `moduleID`  
 から型が存在するモジュールの ID。  
  
 `typeDef`  
 から`mdTypeDef`型を参照するメタデータトークン。  
  
 `cTypeArgs`  
 から指定された型の型パラメーターの数。 非ジェネリック型の場合、この値は0である必要があります。  
  
 `typeArgs`  
 から値の配列 `ClassID` 。それぞれが型の引数になります。 が0に設定されている場合、の値は `typeArgs` NULL `cTypeArgs` になります。  
  
 `pClassID`  
 入出力`ClassID`指定した型のへのポインター。  
  
## <a name="remarks"></a>解説  
 メタデータトークンの代わりにを指定してメソッドを呼び出すと、 `GetClassFromTokenAndTypeArgs` `mdTypeRef` `mdTypeDef` 予期しない結果が発生する可能性があります。呼び出し元は、 `mdTypeRef` を `mdTypeDef` 渡すときにを解決する必要があります。  
  
 型がまだ読み込まれていない場合、を呼び出す `GetClassFromTokenAndTypeArgs` と読み込みがトリガーされます。これは、多くのコンテキストでは危険な操作です。 たとえば、モジュールまたはその他の型の読み込み中にこのメソッドを呼び出すと、ランタイムが循環読み込みを試みたときに無限ループが発生する可能性があります。  
  
 一般に、の使用 `GetClassFromTokenAndTypeArgs` は推奨されていません。 プロファイラーが特定の型のイベントに関心を持っている場合は、その型のとを格納し、ICorProfilerInfo2:: GetClassIDInfo2 を使用して、特定の `ModuleID` `mdTypeDef` [ICorProfilerInfo2::GetClassIDInfo2](icorprofilerinfo2-getclassidinfo2-method.md) `ClassID` が目的の型であるかどうかを確認する必要があります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerInfo インターフェイス](icorprofilerinfo-interface.md)
- [ICorProfilerInfo2 インターフェイス](icorprofilerinfo2-interface.md)
