---
title: ICorDebugValue3::GetSize64 メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugValue3::GetSize64
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue3::GetSize64
helpviewer_keywords:
- GetSize64 method, ICorDebugValue3 interface [.NET Framework debugging]
- ICorDebugValue3::GetSize64 method [.NET Framework debugging]
ms.assetid: fee56a29-3154-4192-958d-71da2ced3740
topic_type:
- apiref
ms.openlocfilehash: 6eb26de83a6cdce47477e6cb3dffd6a94d889975
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83397025"
---
# <a name="icordebugvalue3getsize64-method"></a>ICorDebugValue3::GetSize64 メソッド
この[ICorDebugValue3](icordebugvalue3-interface.md)オブジェクトのサイズ (バイト単位) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetSize64(  
    [out] ULONG64 *pSize  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pSize  
 入出力このオブジェクトのサイズ (バイト単位) へのポインター。  
  
## <a name="remarks"></a>解説  
 この値の型が参照型の場合、このメソッドはオブジェクトのサイズではなく、ポインターのサイズを返します。  
  
 メソッドは、 `ICorDebugValue3::GetSize` その出力パラメーターの型の[ICorDebugValue:: GetSize](icordebugvalue-getsize-method.md)メソッドとは異なります。 [ICorDebugValue:: GetSize](icordebugvalue-getsize-method.md)では、出力パラメーターはです。では、は `ULONG32` `ICorDebugValue3::GetSize` `ULONG64` です。 これにより、 [ICorDebugValue3](icordebugvalue3-interface.md)インターフェイスは、2gb を超える配列のサイズを報告できます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugValue3 インターフェイス](icordebugvalue3-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
