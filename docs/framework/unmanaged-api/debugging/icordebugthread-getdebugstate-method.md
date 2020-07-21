---
title: ICorDebugThread::GetDebugState メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetDebugState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetDebugState
helpviewer_keywords:
- GetDebugState method [.NET Framework debugging]
- ICorDebugThread::GetDebugState method [.NET Framework debugging]
ms.assetid: 9be27b0c-1d99-4722-b0d4-40cf6753ce5c
topic_type:
- apiref
ms.openlocfilehash: 13125f60f596cb8a80d9c42c51a979f632de494b
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379754"
---
# <a name="icordebugthreadgetdebugstate-method"></a>ICorDebugThread::GetDebugState メソッド
このスレッドオブジェクトの現在のデバッグ状態を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetDebugState (  
    [out] CorDebugThreadState   *pState  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pState`  
 入出力このスレッドの現在のデバッグ状態を示す CorDebugThreadState 列挙値のビットごとの組み合わせへのポインター。  
  
## <a name="remarks"></a>Remarks  
 プロセスが現在停止されている場合、は、 `pState` このスレッドの実際の現在の状態ではなく、プロセスが続行された場合に存在する可能性があるデバッグ状態を表します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
