---
title: ICorDebugValue::GetAddress メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugValue.GetAddress
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugValue::GetAddress
helpviewer_keywords:
- ICorDebugValue::GetAddress method [.NET Framework debugging]
- GetAddress method, ICorDebugValue interface [.NET Framework debugging]
ms.assetid: a247c792-45e1-4538-9e1f-b46acca4a463
topic_type:
- apiref
ms.openlocfilehash: 467ba53f90081f0c3499fb22acab96b5e380a3f4
ms.sourcegitcommit: 046a9c22487551360e20ec39fc21eef99820a254
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/14/2020
ms.locfileid: "83395840"
---
# <a name="icordebugvaluegetaddress-method"></a>ICorDebugValue::GetAddress メソッド
この "ICorDebugValue" オブジェクトのアドレスを取得します。このオブジェクトはデバッグ中です。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetAddress (  
    [out] CORDB_ADDRESS   *pAddress  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAddress`  
 入出力`CORDB_ADDRESS`この値オブジェクトのアドレスを指定するオブジェクトへのポインター。  
  
## <a name="remarks"></a>解説  
 値が使用できない場合は、0 (ゼロ) が返されます。 これは、値がレジスタの少なくとも一部の場合、またはガベージコレクターハンドル () に格納されている場合に発生する可能性が `GCHandle` あります。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
