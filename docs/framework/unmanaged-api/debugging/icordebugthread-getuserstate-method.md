---
title: ICorDebugThread::GetUserState メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetUserState
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetUserState
helpviewer_keywords:
- GetUserState method, ICorDebugThread interface [.NET Framework debugging]
- ICorDebugThread::GetUserState method [.NET Framework debugging]
ms.assetid: ae0cfd73-8ead-4d36-9310-dccaac9db0bd
topic_type:
- apiref
ms.openlocfilehash: d1ff3427feb5dc8395bbb2fda78e3e93e1a1a8f0
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378857"
---
# <a name="icordebugthreadgetuserstate-method"></a>ICorDebugThread::GetUserState メソッド
このスレッドの現在のユーザー状態を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetUserState (  
    [out] CorDebugUserState   *pState  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pState`  
 入出力このスレッドの現在のユーザー状態を示す CorDebugUserState 列挙値のビットごとの組み合わせへのポインター。  
  
## <a name="remarks"></a>Remarks  
 スレッドのユーザー状態は、デバッグ中のプログラムによって検査されるときのスレッドの状態です。 スレッドに複数の状態ビットが設定されている可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
