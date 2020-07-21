---
title: ICorDebugValue::GetSize メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugValue.GetSize
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue::GetSize
helpviewer_keywords:
- GetSize method, ICorDebugValue interface [.NET Framework debugging]
- ICorDebugValue::GetSize method [.NET Framework debugging]
ms.assetid: 445a9ee3-e050-4f3a-931a-96b0efb00110
topic_type:
- apiref
ms.openlocfilehash: 9ff7128f55236ae4d0c3a9067a279c496cfb6798
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396748"
---
# <a name="icordebugvaluegetsize-method"></a>ICorDebugValue::GetSize メソッド
この "ICorDebugValue" オブジェクトのサイズ (バイト単位) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSize (  
    [out] ULONG32   *pSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pSize`  
 入出力この値オブジェクトのサイズ (バイト単位)。  
  
## <a name="remarks"></a>解説  
 値の型が参照型の場合、このメソッドはオブジェクトのサイズではなく、ポインターのサイズを返します。  
  
 `ICorDebugValue::GetSize` `COR_E_OVERFLOW` 64 ビットプラットフォームで 4 GB を超えるオブジェクトの場合、メソッドはを返します。 4 GB を超えるオブジェクトには、代わりに[ICorDebugValue3:: GetSize64](icordebugvalue3-getsize64-method.md)メソッドを使用してください。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [GetSize64 メソッド](icordebugvalue3-getsize64-method.md)
