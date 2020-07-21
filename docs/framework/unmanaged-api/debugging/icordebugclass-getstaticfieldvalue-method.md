---
title: ICorDebugClass::GetStaticFieldValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugClass.GetStaticFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass::GetStaticFieldValue
helpviewer_keywords:
- GetStaticFieldValue method, ICorDebugClass interface [.NET Framework debugging]
- ICorDebugClass::GetStaticFieldValue method [.NET Framework debugging]
ms.assetid: 56e718b4-fabd-418b-a5b3-3cc33c745683
topic_type:
- apiref
ms.openlocfilehash: d4a254853256e1a1440f5588418b94e39eabcc9a
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894105"
---
# <a name="icordebugclassgetstaticfieldvalue-method"></a>ICorDebugClass::GetStaticFieldValue メソッド
指定された静的フィールドの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStaticFieldValue (  
    [in]  mdFieldDef         fieldDef,  
    [in]  ICorDebugFrame     *pFrame,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fieldDef`  
 から取得する`Def`フィールドを参照するフィールドトークン。  
  
 `pFrame`  
 からスレッド、コンテキスト、またはアプリケーションドメインの静的を区別するために使用されるフレームを表す、テキストフレームオブジェクトへのポインター。  
  
 静的フィールドがスレッド、コンテキスト、またはアプリケーションドメインに対する相対パスである場合、フレームによって適切な値が決定されます。  
  
 `ppValue`  
 入出力静的フィールドの値を表す ICorDebugValue オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 パラメーター化された型の場合、静的フィールドの値は、特定のインスタンス化に対する相対値になります。 したがって、クラスコンストラクターが型<xref:System.Type>のパラメーターを受け取る場合は、ではなく、の[ICorDebugType::GetStaticFieldValue](icordebugtype-getstaticfieldvalue-method.md) `ICorDebugClass::GetStaticFieldValue`型を呼び出す必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
