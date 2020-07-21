---
title: ICorDebugThread::CreateEval メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.CreateEval
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::CreateEval
helpviewer_keywords:
- CreateEval method [.NET Framework debugging]
- ICorDebugThread::CreateEval method [.NET Framework debugging]
ms.assetid: 36605067-33d3-4579-9c72-fb0e551ab0f1
topic_type:
- apiref
ms.openlocfilehash: f66ef88646c314502dcb610cec8ce822cab1fca2
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379282"
---
# <a name="icordebugthreadcreateeval-method"></a>ICorDebugThread::CreateEval メソッド
このスレッドの機能を収集して公開する、表示されるオブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateEval (  
    [out] ICorDebugEval   **ppEval  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppEval`  
 入出力`ICorDebugEval`このスレッドの機能を収集して公開するオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 評価オブジェクトは、計算を実行する前に、スレッドに新しいチェーンをプッシュします。 これにより、評価が完了するまで、スレッドで現在実行されている計算が中断されます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
