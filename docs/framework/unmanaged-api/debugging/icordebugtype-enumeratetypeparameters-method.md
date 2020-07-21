---
title: ICorDebugType::EnumerateTypeParameters メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugType.EnumerateTypeParameters
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::EnumerateTypeParameters
helpviewer_keywords:
- EnumerateTypeParameters method, ICorDebugType interface [.NET Framework debugging]
- ICorDebugType::EnumerateTypeParameters method [.NET Framework debugging]
ms.assetid: 1ee1f6e6-1bd7-4ebb-83b8-ff9a08ca03de
topic_type:
- apiref
ms.openlocfilehash: dc6bf4f02c49788e640c6e230f864e3ca8e71b0d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83380002"
---
# <a name="icordebugtypeenumeratetypeparameters-method"></a>ICorDebugType::EnumerateTypeParameters メソッド
<xref:System.Type>このテキストの型によって参照されるクラスのパラメーターを格納している、テキスト型へのインターフェイスポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateTypeParameters (  
    [out] ICorDebugTypeEnum   **ppTyParEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppTyParEnum`  
 入出力`ICorDebugTypeEnum`型のパラメーターを格納しているのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 を使用することができます、 `EnumerateTypeParameters` [corelementtype:: GetType](icordebugtype-gettype-method.md)によって返される corelementtype 値が ELEMENT_TYPE_CLASS、ELEMENT_TYPE_VALUETYPE、ELEMENT_TYPE_ARRAY、ELEMENT_TYPE_SZARRAY、ELEMENT_TYPE_BYREF、ELEMENT_TYPE_PTR、または ELEMENT_TYPE_FNPTR です。 パラメーターの数と順序は、型によって異なります。  
  
- ELEMENT_TYPE_CLASS または ELEMENT_TYPE_VALUETYPE: このメソッドが返すに格納されている型パラメーターの数 `ICorDebugTypeEnum` は、対応するクラスの仮引数の型パラメーターの数によって異なります。 たとえば、型がの場合、 `class Dict<String,int32>` はを `EnumerateTypeParameters` `ICorDebugTypeEnum` 表し、シーケンス内でを表すオブジェクトを含むを返し `String` `int32` ます。  
  
- ELEMENT_TYPE_FNPTR: に格納されている型パラメーターの数 `ICorDebugTypeEnum` が、関数で許容される引数の数を超えています。 に格納されている最初の型パラメーターは、関数の戻り値の型であり、 `ICorDebugTypeEnum` 後続の型パラメーターは関数のパラメーターです。  
  
- ELEMENT_TYPE_ARRAY、ELEMENT_TYPE_SZARRAY、ELEMENT_TYPE_BYREF、または ELEMENT_TYPE_PTR: 1 つの型パラメーターが返されます。 たとえば、型がなどの配列型である場合、 `int32[]` `EnumerateTypeParameters` はを `ICorDebugTypeEnum` 表すオブジェクトを含むを返し `int32` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
