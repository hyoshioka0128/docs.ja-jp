---
title: ICorDebugTypeEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugTypeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugTypeEnum::Next
helpviewer_keywords:
- ICorDebugTypeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugTypeEnum interface [.NET Framework debugging]
ms.assetid: d0fdeba3-c195-4ece-8caf-79b1f40025d2
topic_type:
- apiref
ms.openlocfilehash: 83adea3d659eea6d4af9ae364aad18df67e69c03
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396619"
---
# <a name="icordebugtypeenumnext-method"></a>ICorDebugTypeEnum::Next メソッド
によって指定された "の型" インスタンスの数を列挙から取得します。この数は `celt` 、現在の位置から開始します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in]  ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugType *values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から`ICorDebugType`取得するインスタンスの数。  
  
 `values`  
 入出力ポインターの配列。それぞれがオブジェクトを指し `ICorDebugType` ます。  
  
 `pceltFetched`  
 入出力実際に返されたインスタンスの数へのポインター `ICorDebugType` 。 が1の場合、この値は null `celt` になります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目
