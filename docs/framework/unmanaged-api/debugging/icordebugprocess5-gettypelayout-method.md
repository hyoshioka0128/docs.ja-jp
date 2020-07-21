---
title: ICorDebugProcess5::GetTypeLayout メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess5.GetTypeLayout
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess5::GetTypeLayout
helpviewer_keywords:
- ICorDebugProcess5::GetTypeLayout method [.NET Framework debugging]
- GetTypeLayout method, ICorDebugProcess5 interface [.NET Framework debugging]
ms.assetid: bd62f5d1-e874-41f1-81e5-a29a7572c15d
topic_type:
- apiref
ms.openlocfilehash: 861af4ba9c6f4d4bdb16abb9d4e1fd79debac59b
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205575"
---
# <a name="icordebugprocess5gettypelayout-method"></a>ICorDebugProcess5::GetTypeLayout メソッド
型識別子に基づいて、メモリ内のオブジェクトのレイアウトに関する情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeLayout(    [in] COR_TYPEID id,     [out] COR_TYPE_LAYOUT *pLayout);  
```  
  
## <a name="parameters"></a>パラメーター  
 `id`  
 からレイアウトが必要な型を指定する[COR_TYPEID](cor-typeid-structure.md)トークン。  
  
 `pLayout`  
 入出力メモリ内のオブジェクトのレイアウトに関する情報を格納している[COR_TYPE_LAYOUT](cor-type-layout-structure.md)構造体へのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドは、その `ICorDebugProcess5::GetTypeLayout` [COR_TYPEID](cor-typeid-structure.md)に基づいてオブジェクトに関する情報を提供します。これは、他の多くの[ICorDebugProcess5](icordebugprocess5-interface.md)メソッドによって返されます。 この情報は、メソッドによって設定される[COR_TYPE_LAYOUT](cor-type-layout-structure.md)構造体によって提供されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [COR_TYPE_LAYOUT 構造体](cor-type-layout-structure.md)
- [ICorDebugProcess5 インターフェイス](icordebugprocess5-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
