---
title: ICorDebugArrayValue::GetBaseIndicies メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugArrayValue.GetBaseIndicies
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugArrayValue::GetBaseIndicies
helpviewer_keywords:
- ICorDebugArrayValue::GetBaseIndicies method [.NET Framework debugging]
- GetBaseIndicies method [.NET Framework debugging]
ms.assetid: 868b339b-acdb-4fe0-91c7-b85f4fba99eb
topic_type:
- apiref
ms.openlocfilehash: 9aadbe7c6f18c6b15350267d1f9ecaa3a23cdd20
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895066"
---
# <a name="icordebugarrayvaluegetbaseindicies-method"></a>ICorDebugArrayValue::GetBaseIndicies メソッド
配列内の各次元のベースインデックスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetBaseIndicies (  
    [in] ULONG32          cdim,  
    [out, size_is(cdim), length_is(cdim)]
        ULONG32           indicies[]  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `cdim`  
 からこの`ICorDebugArrayValue`オブジェクトの次元数。 この値は、 `indicies`配列のサイズが`ICorDebugArrayValue`オブジェクトの次元数と同じであるため、配列のサイズでもあります。  
  
 `indicies`  
 入出力整数の配列。各整数は、この`ICorDebugArrayValue`オブジェクトの次元のベースインデックス (つまり開始インデックス) です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
