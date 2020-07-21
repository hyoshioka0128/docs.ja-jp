---
title: ICorProfilerObjectEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorProfilerObjectEnum.Next
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerObjectEnum::Next
helpviewer_keywords:
- Next method, ICorProfilerObjectEnum interface [.NET Framework profiling]
- ICorProfilerObjectEnum::Next method [.NET Framework profiling]
ms.assetid: b420433c-5ebe-4986-bba1-97902e6db819
topic_type:
- apiref
ms.openlocfilehash: 850f05520e4146b5016bb574f02aa800dfcaaf32
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84494580"
---
# <a name="icorprofilerobjectenumnext-method"></a>ICorProfilerObjectEnum::Next メソッド
シーケンス内の列挙子の現在位置を開始位置として、オブジェクトのシーケンシャルコレクションから、指定された数の連続するオブジェクトを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in] ULONG                    celt,  
    [out, size_is(celt), length_is(*pceltFetched)]
        ObjectID                  objects[],  
    [out] ULONG                   *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 [in] 取得するオブジェクトの数。  
  
 `objects`  
 入出力値の配列 `ObjectID` 。各値は取得されたオブジェクトを表します。  
  
 `pceltFetched`  
 [out] `objects` 配列で実際に返されるモジュールの数へのポインター。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー** : CorProf.idl、CorProf.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorProfilerObjectEnum インターフェイス](icorprofilerobjectenum-interface.md)
