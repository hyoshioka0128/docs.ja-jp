---
title: ICorDebugType::GetClass メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetClass
helpviewer_keywords:
- ICorDebugType::GetClass method [.NET Framework debugging]
- GetClass method, ICorDebugType interface [.NET Framework debugging]
ms.assetid: 2644f48b-db3c-429f-ae62-76f1c98a1af5
topic_type:
- apiref
ms.openlocfilehash: 878a57514af34730049864f17f4853c1237904c2
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379959"
---
# <a name="icordebugtypegetclass-method"></a>ICorDebugType::GetClass メソッド
インスタンスジェネリック型を表す、のクラスへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetClass (  
    [out] ICorDebugClass   **ppClass  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppClass`  
 入出力`ICorDebugClass`インスタンスジェネリック型を表すインターフェイスのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `GetClass`は、特定の条件下でのみ呼び出すことができます。 を[呼び出す前に](icordebugtype-gettype-method.md)、を呼び出して `GetClass` ください。 `ICorDebugType::GetType`が ELEMENT_TYPE_CLASS または ELEMENT_TYPE_VALUETYPE の CorElementType 値を返す場合は、を呼び出して、 `GetClass` ジェネリック型のインスタンス型を取得できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
