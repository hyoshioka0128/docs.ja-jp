---
title: ICorDebugType::GetType メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetType
helpviewer_keywords:
- ICorDebugType::GetType method [.NET Framework debugging]
- GetType method, ICorDebugType interface [.NET Framework debugging]
ms.assetid: d6e64534-4d47-4ad0-a340-7590e07e2b4a
topic_type:
- apiref
ms.openlocfilehash: ac42c6254182ea775377a448a54d527b234c97dc
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379928"
---
# <a name="icordebugtypegettype-method"></a>ICorDebugType::GetType メソッド
<xref:System.Type>このコンポーネント型によって表される共通言語ランタイム (CLR) のネイティブ型を記述する CorElementType 値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetType (  
    [out] CorElementType   *ty  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ty`  
 入出力`CorElementType`このが表す CLR を示す列挙体の値へのポインター <xref:System.Type> `ICorDebugType` 。  
  
## <a name="remarks"></a>Remarks  
 の値 `ty` が ELEMENT_TYPE_CLASS または ELEMENT_TYPE_VALUETYPE の場合は、インスタンス type [:: getclass](icordebugtype-getclass-method.md)メソッドを呼び出してジェネリック型の型を取得することができます。それ以外の場合は、を呼び出さないで `ICorDebugType::GetClass` ください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
