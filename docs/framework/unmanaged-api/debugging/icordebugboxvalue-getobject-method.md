---
title: ICorDebugBoxValue::GetObject メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugBoxValue.GetObject
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBoxValue::GetObject
helpviewer_keywords:
- ICorDebugBoxValue::GetObject method [.NET Framework debugging]
- GetObject method, ICorDebugBoxValue interface [.NET Framework debugging]
ms.assetid: 3a867a5b-bf94-493f-a4f5-b28685cf5325
topic_type:
- apiref
ms.openlocfilehash: 401f052b881c1a0cfa065ba60c93aca1706f34f4
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894781"
---
# <a name="icordebugboxvaluegetobject-method"></a>ICorDebugBoxValue::GetObject メソッド
ボックス化された値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetObject (  
    [out] ICorDebugObjectValue **ppObject  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppObject`  
 入出力ボックス化された値を表す、ボックス化された値を表すオブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
