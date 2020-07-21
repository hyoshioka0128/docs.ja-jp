---
title: ICorDebugExceptionObjectValue::EnumerateExceptionCallStack メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugExceptionObjectValue.EnumerateExceptionCallStack
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugExceptionObjectValue::EnumerateExceptionCallStack
helpviewer_keywords:
- EnumerateExceptionCallStack method, ICorDebugExceptionObjectValue interface [.NET Framework debugging]
- ICorDebugExceptionObjectValue::EnumerateExceptionCallStack method [.NET Framework debugging]
ms.assetid: 00c64533-15dd-47f4-bb97-fe80a1ebadef
topic_type:
- apiref
ms.openlocfilehash: e45b180ac6d943d89740ad7ae10500ea4ad1aa9c
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82975967"
---
# <a name="icordebugexceptionobjectvalueenumerateexceptioncallstack-method"></a>ICorDebugExceptionObjectValue::EnumerateExceptionCallStack メソッド
例外オブジェクトに埋め込まれている呼び出し履歴に対する列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnumerateExceptionCallStack(  
    [out] ICorDebugExceptionObjectCallStackEnum **ppCallStackEnum  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 ppCallStackEnum  
 入出力マネージ例外オブジェクトのスタックトレース列挙[ICorDebugExceptionObjectCallStackEnum](icordebugexceptionobjectcallstackenum-interface.md)子である、というコードのアドレスへのポインターを示します。  
  
## <a name="remarks"></a>Remarks  
 呼び出し履歴情報が使用できない場合、メソッドは`S_OK`を返します。また、は、値が0の有効な列挙[子です。](icordebugexceptionobjectcallstackenum-interface.md) メソッドがスタックトレース情報を取得できない場合、戻り値は`E_FAIL`であり、列挙子は返されません。  
  
 の[例外](icordebugexceptionobjectcallstackenum-interface.md)オブジェクトの`_stackTrace`フィールドからスタックトレースデータをデコードするには、のオブジェクトを使用します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugExceptionObjectValue インターフェイス](icordebugexceptionobjectvalue-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
