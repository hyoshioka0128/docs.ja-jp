---
title: ICorDebugComObjectValue::GetCachedInterfacePointers メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue::GetCachedInterfacePointers
api_location:
- mscordbi.dll
f1_keywords:
- ICorDebugComObjectValue::GetCachedInterfacePointers
helpviewer_keywords:
- ICorDebugComObjectValue::GetCachedInterfacePointers method [.NET Framework debugging]
- GetCachedInterfacePointers method, ICorDebugComObjectValue interface [.NET Framework debugging]
ms.assetid: 08dbd558-bd39-4263-94c2-71e70687aaf0
topic_type:
- apiref
ms.openlocfilehash: fa22c17ed7d5bcd689f21d2d855d9be7a6a8e164
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892805"
---
# <a name="icordebugcomobjectvaluegetcachedinterfacepointers-method"></a>ICorDebugComObjectValue::GetCachedInterfacePointers メソッド
現在のランタイム呼び出し可能ラッパー (RCW) にキャッシュされている生のインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCachedInterfacePointers(  
    [in] BOOL bIInspectableOnly,  
    [in] ULONG32 celt,  
    [out] ULONG32 *pceltFetched,  
    [out, size_is(celt), length_is(*pceltFetched) CORDB_ADDRESS *ptrs);  
```  
  
## <a name="parameters"></a>パラメーター  
 `bIInspectableOnly`  
 からメソッドが、ランタイム呼び出し可能ラッパー (RCW) によって`IInspectable`キャッシュされた Windows ランタイムインターフェイス (インターフェイス) またはすべての COM インターフェイスだけを返すかどうかを示す値。  
  
 `celt`  
 からアドレスを取得するオブジェクトの数。  
  
 `pceltFetched`  
 入出力で実際に`ptrs`返される値`CORDB_ADDRESS`の数へのポインター。  
  
 `ptrs`  
 キャッシュされたインターフェイスオブジェクトのアドレスを格納`CORDB_ADDRESS`している値の配列の開始アドレスへのポインター。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugComObjectValue のインターフェイス](icordebugcomobjectvalue-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
