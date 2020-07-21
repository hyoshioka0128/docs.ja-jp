---
title: ICorDebugComObjectValue::GetCachedInterfaceTypes メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugComObjectValue::GetCachedInterfaceTypes
api_location:
- mscordbi.dll
f1_keywords:
- ICorDebugComObjectValue::GetCachedInterfaceTypes
helpviewer_keywords:
- GetCachedInterface method, ICorDebugComObjectValue interface [.NET Framework debugging]
- ICorDebugComObjectValue::GetCachedInterface method [.NET Framework debugging]
ms.assetid: d492284f-d3c5-4614-adb8-d718d5042500
topic_type:
- apiref
ms.openlocfilehash: 6b02657012870de4d0f888f6c05b115b25073fa2
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892834"
---
# <a name="icordebugcomobjectvaluegetcachedinterfacetypes-method"></a>ICorDebugComObjectValue::GetCachedInterfaceTypes メソッド
現在のオブジェクトがキャストされた、またはとして使用されたインターフェイス型の列挙子を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCachedInterfaceTypes(  
    [in] BOOL bIInspectableOnly,  
    [out] ICorDebugTypeEnum **ppInterfacesEnum);  
```  
  
## <a name="parameters"></a>パラメーター  
 `bIInspectableOnly`  
 からメソッドが、ランタイム呼び出し可能ラッパー (RCW) によっ`IInspectable`てキャッシュされた Windows ランタイムインターフェイス (インターフェイス) またはすべての COM インターフェイスだけを返すかどうかを示す値。  
  
 `ppInterfacesEnum`  
 入出力に`bIInspectableOnly`従ってフィルター処理された、キャッシュされたインターフェイスの種類を表す、の型のオブジェクトへのアクセスを提供する、、の各型のオブジェクトへのアクセスを提供する、テキストを指すポインターです。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugComObjectValue のインターフェイス](icordebugcomobjectvalue-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
