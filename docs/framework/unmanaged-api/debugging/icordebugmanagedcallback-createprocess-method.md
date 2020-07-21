---
title: ICorDebugManagedCallback::CreateProcess メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.CreateProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::CreateProcess
helpviewer_keywords:
- ICorDebugManagedCallback::CreateProcess method [.NET Framework debugging]
- CreateProcess method, ICorDebugManagedCallback interface [.NET Framework debugging]
ms.assetid: 8e89d5ee-e4e3-4738-8302-0b7d1cf4846e
topic_type:
- apiref
ms.openlocfilehash: 0e9ed8054711297173e880c9eecb12c3f5bd0a68
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207134"
---
# <a name="icordebugmanagedcallbackcreateprocess-method"></a>ICorDebugManagedCallback::CreateProcess メソッド
プロセスが初めてアタッチまたは開始されたときにデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateProcess (  
    [in] ICorDebugProcess *pProcess  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pProcess`  
 からアタッチまたは開始されたプロセスを表す、のオブジェクトへのポインター。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、共通言語ランタイムが初期化されるまで呼び出されません。 ほとんどの[ICorDebug](icordebug-interface.md)メソッドは、コールバックの前に CORDBG_E_NOTREADY を返し `CreateProcess` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
