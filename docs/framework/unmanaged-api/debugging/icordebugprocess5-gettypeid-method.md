---
title: ICorDebugProcess5::GetTypeID メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugProcess5.GetTypeID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetTypeID
helpviewer_keywords:
- ICorDebugProcess5::GetTypeID method [.NET Framework debugging]
- GetTypeID method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: 47dbaea4-8857-462e-93ba-fff880fc9e50
topic_type:
- apiref
ms.openlocfilehash: 499e1fd859a66bb6992c6d02a46e38c514503bd8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205584"
---
# <a name="icordebugprocess5gettypeid-method"></a>ICorDebugProcess5::GetTypeID メソッド
オブジェクトのアドレスを[COR_TYPEID](cor-typeid-structure.md)識別子に変換します。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT GetTypeID(  
    [in] CORDB_ADDRESS obj,  
    [out] COR_TYPEID *pId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `obj`  
 からオブジェクトのアドレス。  
  
 `pId`  
 オブジェクトを識別する[COR_TYPEID](cor-typeid-structure.md)値へのポインター。  
  
## <a name="remarks"></a>解説  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
