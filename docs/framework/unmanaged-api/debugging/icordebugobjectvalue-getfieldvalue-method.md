---
title: ICorDebugObjectValue::GetFieldValue メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetFieldValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetFieldValue
helpviewer_keywords:
- ICorDebugObjectValue::GetFieldValue method [.NET Framework debugging]
- GetFieldValue method [.NET Framework debugging]
ms.assetid: c96770b0-3e09-47bb-bd29-20353b043459
topic_type:
- apiref
ms.openlocfilehash: 660bc13e8109994f59444c0adebbc97f54de0b43
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207589"
---
# <a name="icordebugobjectvaluegetfieldvalue-method"></a>ICorDebugObjectValue::GetFieldValue メソッド
このオブジェクト値について、指定したクラスの指定したフィールドの値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFieldValue (  
    [in]  ICorDebugClass     *pClass,  
    [in]  mdFieldDef         fieldDef,  
    [out] ICorDebugValue     **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pClass`  
 からフィールド値を取得する対象のクラスを表す "表示クラス" オブジェクトへのポインター。  
  
 `fieldDef`  
 から`mdFieldDef`フィールドを記述するメタデータを参照するトークン。  
  
 `ppValue`  
 入出力指定したフィールドの値を表す "ICorDebugValue" オブジェクトへのポインター。  
  
## <a name="remarks"></a>Remarks  
 パラメーターで指定されたクラスは、 `pClass` オブジェクト値のクラスの階層内に存在する必要があり、フィールドはそのクラスのフィールドである必要があります。  
  
 `GetFieldValue`ジェネリックオブジェクトとジェネリッククラスでは、メソッドは引き続き成功します。 たとえば、MyDictionary \< v> \< がディクショナリ文字列 v> から継承し、オブジェクト値が mydictionary int32> 型である場合、 \< `ICorDebugClass` ディクショナリ K のオブジェクトを渡すと、 \< V> は dictionary 文字列, int32> のフィールドを正常に取得し \< ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
