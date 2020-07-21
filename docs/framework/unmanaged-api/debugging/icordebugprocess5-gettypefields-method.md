---
title: ICorDebugProcess5::GetTypeFields メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.GetTypeFields
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetTypeFields
helpviewer_keywords:
- GetTypeFields method, ICorDebugProcess5 interface [.NET Framework debugging]
- ICorDebugProcess5::GetTypeFields method [.NET Framework debugging]
ms.assetid: 6a0ad3ee-dacb-47e9-abae-4536bcc4804b
topic_type:
- apiref
ms.openlocfilehash: a2c7f7b722abac6acf71d3b64276862441695a5f
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212790"
---
# <a name="icordebugprocess5gettypefields-method"></a>ICorDebugProcess5::GetTypeFields メソッド
型に属しているフィールドに関する情報を提供します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeFields(  
    [in] COR_TYPEID id,  
    [in] ULONG32 celt,  
    [out] COR_FIELD fields[],
    [out] ULONG32 *pceltNeeded  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `id`  
 からフィールド情報を取得する型の識別子。  
  
 `celt`  
 からフィールド情報を取得する[COR_FIELD](cor-field-structure.md)オブジェクトの数。  
  
 `fields`  
 入出力型に属するフィールドに関する情報を提供する[COR_FIELD](cor-field-structure.md)オブジェクトの配列。  
  
 `pceltNeeded`  
 入出力に含まれている[COR_FIELD](cor-field-structure.md)オブジェクトの数へのポインター `fields` 。  
  
## <a name="remarks"></a>Remarks  
 パラメーターは、 `celt` メソッドがデータを設定するために使用するフィールドの数を指定し `fields` ます。フィールドの値に対応する必要があり `COR_TYPE_LAYOUT::numFields` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
