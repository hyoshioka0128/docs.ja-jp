---
title: ICorDebugThread2::GetTaskID メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread2.GetTaskID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread2::GetTaskID
helpviewer_keywords:
- ICorDebugThread2::GetTaskID method [.NET Framework debugging]
- GetTaskID method [.NET Framework debugging]
ms.assetid: 6ba3c6ee-4ba1-4c98-bf1e-8531acd3da09
topic_type:
- apiref
ms.openlocfilehash: 841af546cc3586529fe290c69e686438f634b90d
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83377783"
---
# <a name="icordebugthread2gettaskid-method"></a>ICorDebugThread2::GetTaskID メソッド
このスレッドで実行されているタスクの識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetTaskID (  
    [out] TASKID  *pTaskId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pTaskId`  
 入出力この ICorDebugThread2 オブジェクトによって表されるスレッド上で実行されているタスクの識別子へのポインター。  
  
## <a name="remarks"></a>Remarks  
 スレッドが接続に関連付けられている場合にのみ、スレッドでタスクを実行できます。 `GetTaskID``pTaskId`スレッドが接続に関連付けられていない場合は、で0を返します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
