---
title: ICorDebugObjectValue::GetClass メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugObjectValue.GetClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugObjectValue::GetClass
helpviewer_keywords:
- ICorDebugObjectValue::GetClass method [.NET Framework debugging]
- GetClass method, ICorDebugObjectValue interface [.NET Framework debugging]
ms.assetid: 5be25292-8357-445f-a09b-f997c0de761c
topic_type:
- apiref
ms.openlocfilehash: b0e8fd162ccc1cfc944fb870f493febfe2e5ef42
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207680"
---
# <a name="icordebugobjectvaluegetclass-method"></a>ICorDebugObjectValue::GetClass メソッド
このオブジェクト値のクラスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetClass (  
    [out] ICorDebugClass     **ppClass  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppClass`  
 入出力この "いい Objectvalue" オブジェクトによって表されるオブジェクト値のクラスを表す "のクラス" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `GetClass`および[ICorDebugValue:: GetType](icordebugvalue-gettype-method.md)メソッドはそれぞれ、値の型に関する情報を返します。これらはどちらも、ジェネリック対応[ICorDebugValue2:: GetExactType](icordebugvalue2-getexacttype-method.md)に置き換えられます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
