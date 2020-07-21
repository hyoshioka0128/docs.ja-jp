---
title: ICorDebugValueEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugValueEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValueEnum::Next
helpviewer_keywords:
- ICorDebugValueEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugValueEnum interface [.NET Framework debugging]
ms.assetid: f5ef94dd-dfee-49d3-a398-b110f8906dd8
topic_type:
- apiref
ms.openlocfilehash: db1721fed6414310556ceac493275e069a781ac8
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397139"
---
# <a name="icordebugvalueenumnext-method"></a>ICorDebugValueEnum::Next メソッド
現在の位置から開始して、指定した数の "ICorDebugValue" インスタンスを列挙から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in]  ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugValue *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から`ICorDebugValue`取得するインスタンスの数。  
  
 `values`  
 入出力ポインターの配列。それぞれがオブジェクトを指し `ICorDebugValue` ます。  
  
 `pceltFetched`  
 入出力実際に返されたインスタンスの数へのポインター `ICorDebugValue` 。 が1の場合、この値は null `celt` になります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
