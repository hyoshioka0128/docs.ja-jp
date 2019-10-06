---
title: ICorDebugCodeEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCodeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCodeEnum::Next
helpviewer_keywords:
- ICorDebugCodeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: 644ece86-384d-4c63-9fba-52c789616ff7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 076b5d628dfe83decdbbe2f5e74c50e08262c580
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700693"
---
# <a name="icordebugcodeenumnext-method"></a>ICorDebugCodeEnum::Next メソッド

現在の位置から開始して、指定した数の "コード" インスタンスを列挙から取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next (
    [in] ULONG  celt,
    [out, size_is(celt), length_is(*pceltFetched)]
        ICorDebugCode *values[],
    [out] ULONG *pceltFetched
);
```

## <a name="parameters"></a>パラメーター

 `celt`  
 から取得する @no__t 0 のインスタンスの数。

 `values`  
 入出力ポインターの配列。それぞれが @no__t 0 のオブジェクトを指します。

 `pceltFetched`  
 入出力実際に返された @no__t 0 のインスタンスの数へのポインター。 @No__t-0 が1の場合、この値は null になることがあります。

## <a name="requirements"></a>要件

 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。

 **ヘッダー:** CorDebug .idl、CorDebug. h

 **ライブラリ**CorGuids .lib

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
 
