---
title: ICorDebugModule::GetFunctionFromToken メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugModule.GetFunctionFromToken
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugModule::GetFunctionFromToken
helpviewer_keywords:
- GetFunctionFromToken method, ICorDebugModule interface [.NET Framework debugging]
- ICorDebugModule::GetFunctionFromToken method [.NET Framework debugging]
ms.assetid: 6fe12194-4ef7-43c1-9570-ade35ccf127a
topic_type:
- apiref
ms.openlocfilehash: a33b6ff308f3444496e5a1cb2e04f28e80305db5
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212582"
---
# <a name="icordebugmodulegetfunctionfromtoken-method"></a>ICorDebugModule::GetFunctionFromToken メソッド
メタデータトークンによって指定された関数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunctionFromToken(  
    [in] mdMethodDef methodDef,  
    [out] ICorDebugFunction **ppFunction  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `methodDef`  
 から`mdMethodDef`関数のメタデータを参照するメタデータトークン。  
  
 `ppFunction`  
 入出力関数を表す、のオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 渡された `GetFunctionFromToken` 値 `methodDef` が Microsoft 中間言語 (MSIL) メソッドを参照していない場合、メソッドは CORDBG_E_FUNCTION_NOT_IL HRESULT を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
