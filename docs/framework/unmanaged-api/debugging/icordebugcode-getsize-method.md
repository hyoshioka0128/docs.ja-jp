---
title: ICorDebugCode::GetSize メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode.GetSize
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::GetSize
helpviewer_keywords:
- GetSize method, ICorDebugCode interface [.NET Framework debugging]
- ICorDebugCode::GetSize method [.NET Framework debugging]
ms.assetid: 115bc6de-f5e2-4e8e-bb38-c7cf54045434
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 89df0e9be0600b51dcc8a68c5aba3f06e86e1b53
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700809"
---
# <a name="icordebugcodegetsize-method"></a>ICorDebugCode::GetSize メソッド

この "コード" によって表されるバイナリコードのサイズ (バイト単位) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize (
    [out] ULONG32    *pcBytes
);
```

## <a name="parameters"></a>パラメーター

 `pcBytes`  
 入出力この @no__t 0 オブジェクトが表すバイナリコードのサイズ (バイト単位) へのポインター。

## <a name="requirements"></a>要件

 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。

 **ヘッダー:** CorDebug .idl、CorDebug. h

 **ライブラリ**CorGuids .lib

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
 
