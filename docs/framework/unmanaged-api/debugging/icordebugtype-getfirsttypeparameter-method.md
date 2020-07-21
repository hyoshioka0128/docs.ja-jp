---
title: ICorDebugType::GetFirstTypeParameter メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetFirstTypeParameter
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetFirstTypeParameter
helpviewer_keywords:
- ICorDebugType::GetFirstTypeParameter method [.NET Framework debugging]
- GetFirstTypeParameter method [.NET Framework debugging]
ms.assetid: 35bb594f-af6a-4349-83fe-e98702674e03
topic_type:
- apiref
ms.openlocfilehash: da0097daea183c76f97f0b1966b313e1cb5a557b
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379951"
---
# <a name="icordebugtypegetfirsttypeparameter-method"></a>ICorDebugType::GetFirstTypeParameter メソッド
<xref:System.Type>このによって表される型の最初のパラメーターを表す、の型へのインターフェイスポインターを取得し `ICorDebugType` ます。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFirstTypeParameter (  
    [out] ICorDebugType   **value  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `value`  
 入出力最初のパラメーターを表すオブジェクトのアドレスへのポインター `ICorDebugType` 。  
  
## <a name="remarks"></a>Remarks  
 `GetFirstTypeParameter`型に関する追加情報には、最大で1つの型パラメーターが含まれる場合に、を呼び出すことができます。 具体的には、型が ELEMENT_TYPE_ARRAY、ELEMENT_TYPE_SZARRAY、ELEMENT_TYPE_BYREF、または ELEMENT_TYPE_PTR である場合に使用できます。これは、のように、の型[:: GetType](icordebugtype-gettype-method.md)メソッドによって示されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
