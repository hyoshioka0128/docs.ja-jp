---
title: ICorDebugCode::IsIL メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugCode.IsIL
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCode::IsIL
helpviewer_keywords:
- ICorDebugCode::IsIL method [.NET Framework debugging]
- IsIL method [.NET Framework debugging]
ms.assetid: 132ef8cc-d938-43f3-b8f2-e3b97c0ceb33
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 0a81f4a53954c559ab12e27bcf039b7b1a1804cc
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700795"
---
# <a name="icordebugcodeisil-method"></a>ICorDebugCode::IsIL メソッド

この "コードが、Microsoft 中間言語 (MSIL) でコンパイルされたコードを表しているかどうかを示す値を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsIL (
    [out] BOOL       *pbIL
);
```

## <a name="parameters"></a>パラメーター
 `pbIL`  
 [out] `true` @no__t が MSIL でコンパイルされたコードを表している場合は0。それ以外の場合は、`false` です。

## <a name="requirements"></a>要件

 **・** [システム要件](../../get-started/system-requirements.md)に関するページを参照してください。  

 **ヘッダー:** CorDebug .idl、CorDebug. h  

 **ライブラリ**CorGuids .lib  

 **.NET Framework のバージョン:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
 
