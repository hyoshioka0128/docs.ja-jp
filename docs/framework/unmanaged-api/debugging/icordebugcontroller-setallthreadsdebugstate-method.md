---
title: ICorDebugController::SetAllThreadsDebugState メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugController.SetAllThreadsDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::SetAllThreadsDebugState
helpviewer_keywords:
- SetAllThreadsDebugState method [.NET Framework debugging]
- ICorDebugController::SetAllThreadsDebugState method [.NET Framework debugging]
ms.assetid: bdda4bd7-4743-4d58-a22b-8067e967db95
topic_type:
- apiref
ms.openlocfilehash: c2e8aaa2774e3e2699a73c40804391ca245047b1
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976591"
---
# <a name="icordebugcontrollersetallthreadsdebugstate-method"></a>ICorDebugController::SetAllThreadsDebugState メソッド
プロセス内のすべてのマネージスレッドのデバッグ状態を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetAllThreadsDebugState (  
    [in] CorDebugThreadState  state,  
    [in] ICorDebugThread      *pExceptThisThread  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `state`  
 からデバッグ用のスレッドの状態を指定する "CorDebugThreadState" 列挙の値。  
  
 `pExceptThisThread`  
 からデバッグ状態設定から除外されるスレッドを表す "のスレッド" オブジェクトへのポインター。 この値が null の場合、スレッドは除外されません。  
  
## <a name="remarks"></a>Remarks  
 メソッド`SetAllThreadsDebugState`は、 [EnumerateThreads メソッド](icordebugcontroller-enumeratethreads-method.md)によって表示されないスレッドに影響を与える可能性があり`SetAllThreadsDebugState`ます。そのため、メソッドを使用`SetAllThreadsDebugState`して中断されたスレッドは、メソッドを使用して再開する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
