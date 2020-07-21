---
title: ICorDebugReferenceValue::GetValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugReferenceValue.GetValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugReferenceValue::GetValue
helpviewer_keywords:
- GetValue method, ICorDebugReferenceValue interface [.NET Framework debugging]
- ICorDebugReferenceValue::GetValue method [.NET Framework debugging]
ms.assetid: 5da07f99-6c70-46ec-b997-5ab6fb7106cd
topic_type:
- apiref
ms.openlocfilehash: 6417be4ab7c74d885edffad41085edca27bcf1ce
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378585"
---
# <a name="icordebugreferencevaluegetvalue-method"></a>ICorDebugReferenceValue::GetValue メソッド
参照先のオブジェクトの現在のメモリアドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetValue (  
    [out] CORDB_ADDRESS   *pValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pValue`  
 入出力このは、 `CORDB_ADDRESS` この参照値オブジェクトが指すオブジェクトのアドレスを指定する値へのポインターです。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
