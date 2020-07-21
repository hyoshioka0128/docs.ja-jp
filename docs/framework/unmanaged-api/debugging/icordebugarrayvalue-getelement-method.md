---
title: ICorDebugArrayValue::GetElement メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetElement
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetElement
helpviewer_keywords:
- GetElement method [.NET Framework debugging]
- ICorDebugArrayValue::GetElement method [.NET Framework debugging]
ms.assetid: 7ac3cba5-c282-402e-b7ef-b46634f5176b
topic_type:
- apiref
ms.openlocfilehash: 7a52e61f41bd1d7f68523dd16f70010ffbba401e
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895033"
---
# <a name="icordebugarrayvaluegetelement-method"></a>ICorDebugArrayValue::GetElement メソッド
指定された配列要素の値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetElement (  
    [in]  ULONG32          cdim,  
    [in, size_is(cdim), length_is(cdim)]
         ULONG32           indices[],  
    [out] ICorDebugValue   **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cdim`  
 からこの`ICorDebugArrayValue`オブジェクトの次元数。  
  
 この値は、 `indices`配列のサイズが`ICorDebugArrayValue`オブジェクトの次元数と同じであるため、配列のサイズでもあります。  
  
 `indices`  
 からインデックス値の配列。それぞれが`ICorDebugArrayValue`オブジェクトのディメンション内の位置を指定します。  
  
 この値を null にすることはできません。  
  
 `ppValue`  
 入出力指定した要素の値を表す ICorDebugValue オブジェクトのアドレスへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
