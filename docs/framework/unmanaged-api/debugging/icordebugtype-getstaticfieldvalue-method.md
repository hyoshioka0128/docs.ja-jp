---
title: ICorDebugType::GetStaticFieldValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 62eb5d55-53ee-4fb3-8d47-7b6c96808f9e
topic_type:
- apiref
ms.openlocfilehash: 83ac91133b226e2ac263356941c3fc3288355e7e
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379933"
---
# <a name="icordebugtypegetstaticfieldvalue-method"></a>ICorDebugType::GetStaticFieldValue メソッド
指定したスタックフレーム内の指定したフィールドトークンによって参照される静的フィールドの値を格納する、ICorDebugValue オブジェクトへのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef        fieldDef,  
    [in]  ICorDebugFrame    *pFrame,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fieldDef`  
 から`mdFieldDef`静的フィールドを指定するトークンです。  
  
 `pFrame`  
 からスタックフレームを表す、テキストフレームへのポインター。  
  
 `ppValue`  
 入出力`ICorDebugValue`静的フィールドの値を格納しているのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 メソッドが使用されるのは、 `GetStaticFieldValue` 型が ELEMENT_TYPE_CLASS または ELEMENT_TYPE_VALUETYPE である場合です。この場合、は、"の[型:: GetType](icordebugtype-gettype-method.md)メソッドによって示されます。  
  
 非ジェネリック型の場合、によって実行される操作は、によって返される、によって `GetStaticFieldValue` 型: [: GetStaticFieldValue](icordebugclass-getstaticfieldvalue-method.md)を呼び出すことと同じになります。このクラスは、[テキスト:: getclass](icordebugtype-getclass-method.md)です。  
  
 ジェネリック型の場合、静的フィールド値は特定のインスタンス化に対して相対的になります。 また、静的フィールドがスレッド、コンテキスト、またはアプリケーションドメインに対して相対的である可能性がある場合は、デバッガーが適切な値を決定するためにスタックフレームが役立ちます。  
  
## <a name="remarks"></a>Remarks  
 `GetStaticFieldValue`は、の呼び出しによって `ICorDebugType::GetType` ELEMENT_TYPE_CLASS または ELEMENT_TYPE_VALUETYPE の値が返される場合にのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
