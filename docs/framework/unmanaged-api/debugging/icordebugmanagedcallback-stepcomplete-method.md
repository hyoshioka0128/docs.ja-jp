---
title: ICorDebugManagedCallback::StepComplete メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.StepComplete
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::StepComplete
helpviewer_keywords:
- StepComplete method [.NET Framework debugging]
- ICorDebugManagedCallback::StepComplete method [.NET Framework debugging]
ms.assetid: 5e1f2c47-81df-4530-826d-96489cd68719
topic_type:
- apiref
ms.openlocfilehash: 89b010706222ad44bccabd94191c42a888584944
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212660"
---
# <a name="icordebugmanagedcallbackstepcomplete-method"></a>ICorDebugManagedCallback::StepComplete メソッド
ステップが完了したことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StepComplete (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugThread     *pThread,  
    [in] ICorDebugStepper    *pStepper,  
    [in] CorDebugStepReason   reason  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 からステップが完了したスレッドを含むアプリケーションドメインを表す、のオブジェクトへのポインター。  
  
 `pThread`  
 からステップが完了したスレッドを表す、のスレッドオブジェクトへのポインター。  
  
 `pStepper`  
 からコード実行のステップを表す ICorDebugStepper オブジェクトへのポインター。  
  
 `reason`  
 から個々のステップの結果を示す CorDebugStepReason 列挙値。  
  
## <a name="remarks"></a>Remarks  
 デバッグが終了しない限り、必要に応じてステップを続行するためにステッパを使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
