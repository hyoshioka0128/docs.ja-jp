---
title: 'ICorDebugType2:: GetTypeID メソッド'
ms.date: 03/30/2017
api_name:
- ICorDebugType2.GetTypeID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetTypeID
helpviewer_keywords:
- GetTypeID method, ICorDebugType2 interface [.NET Framework debugging]
- ICorDebugType2.GetTypeID method [.NET Framework debugging]
ms.assetid: 0b933686-226e-4373-92b7-fac579ee7b1a
topic_type:
- apiref
ms.openlocfilehash: 1c11946bc5ea69a090091c014aba859935b48b36
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83396669"
---
# <a name="icordebugtype2gettypeid-method"></a>ICorDebugType2:: GetTypeID メソッド
この型の[COR_TYPEID](cor-typeid-structure.md)を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTypeID(  
    ([out] COR_TYPEID *id  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `id`  
 入出力このテキスト型の[COR_TYPEID](cor-typeid-structure.md)へのポインター。  
  
## <a name="return-value"></a>戻り値  
 戻り値は、成功の場合は `S_OK` で、失敗の場合は `HRESULT` コードです。 コードには `HRESULT` 次のものが含まれます。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|`S_OK`|メソッドが成功しました。 メソッドが有効な[COR_TYPEID](cor-typeid-structure.md)を取得しました。|  
|`CORDBG_E_CLASS_NOT_LOADED`|型が読み込まれていません。|  
|`CORDBG_E_UNSUPPORTED`|この型はサポートされていません。|  
  
## <a name="remarks"></a>解説  
 このメソッドは、ランタイムに読み込まれている可能性がある型を表す、または[COR_TYPEID](cor-typeid-structure.md)ランタイムに読み込まれていない可能性のある型を表す、、ランタイムに読み込まれた型を識別する不透明なハンドルとして機能する、の型からのマッピングを提供します。  
  
 によって表される型がまだ読み込まれていない場合、このメソッドはを返し `CORDBG_E_CLASS_NOT_LOADED` ます。  型がサポートされていない場合は、を返し `CORDBG_E_UNSUPPORTED` ます。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v462plus](../../../../includes/net-current-v462plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugType2 インターフェイス](icordebugtype2-interface.md)
