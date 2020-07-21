---
title: ICorDebugEval2::CreateValueForType メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.CreateValueForType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::CreateValueForType
helpviewer_keywords:
- CreateValueForType method [.NET Framework debugging]
- ICorDebugEval2::CreateValueForType method [.NET Framework debugging]
ms.assetid: ea38ae20-7e0a-427a-be77-d78fae719d82
topic_type:
- apiref
ms.openlocfilehash: fd7acaa8bcb4d53893855bcd25ff68cf26e30354
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976162"
---
# <a name="icordebugeval2createvaluefortype-method"></a>ICorDebugEval2::CreateValueForType メソッド
初期値が0または null の、指定した型の新しい ICorDebugValue へのポインターを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateValueForType (  
    [in] ICorDebugType         *pType,  
    [out] ICorDebugValue       **ppValue  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pType`  
 から型を表す、の型のオブジェクトへのポインター。  
  
 `ppValue`  
 入出力値を表す`ICorDebugValue`オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `CreateValueForType`一般化[Okeval:: CreateValue](icordebugeval-createvalue-method.md) 。など`List<int>`の構築された型を含む任意のオブジェクトの種類を指定できます。 このメソッドの唯一の目的は、関数の評価に渡すことができる値を生成することです。  
  
 型はクラスまたは値型である必要があります。 このメソッドを使用して配列値や文字列値を作成することはできません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
