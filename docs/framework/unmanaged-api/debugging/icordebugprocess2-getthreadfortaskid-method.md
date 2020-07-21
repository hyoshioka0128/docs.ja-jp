---
title: ICorDebugProcess2::GetThreadForTaskID メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.GetThreadForTaskID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::GetThreadForTaskID
helpviewer_keywords:
- ICorDebugProcess2::GetThreadForTaskId method [.NET Framework debugging]
- GetThreadForTaskID method [.NET Framework debugging]
ms.assetid: 32d54a5b-8ad3-405b-a1b9-0936a3b49d1e
topic_type:
- apiref
ms.openlocfilehash: 89be29c770098d92ce3c47f7c45b1bb8580f2edb
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213518"
---
# <a name="icordebugprocess2getthreadfortaskid-method"></a>ICorDebugProcess2::GetThreadForTaskID メソッド
指定した id を持つタスクが実行されているスレッドを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetThreadForTaskID (  
    [in]  TASKID            taskid,  
    [out] ICorDebugThread2  **ppThread  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `taskid`  
 からタスクの識別子です。  
  
 `ppThread`  
 入出力取得するスレッドを表す ICorDebugThread2 オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 ホストは、 [ICLRTask:: SetTaskIdentifier](../hosting/iclrtask-settaskidentifier-method.md)メソッドを使用してタスク識別子を設定できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
