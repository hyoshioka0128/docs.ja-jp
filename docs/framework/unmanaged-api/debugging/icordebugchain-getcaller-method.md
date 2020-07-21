---
title: ICorDebugChain::GetCaller メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetCaller
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetCaller
helpviewer_keywords:
- ICorDebugChain::GetCaller method [.NET Framework debugging]
- GetCaller method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: d0b8ab4b-d7d2-4fa0-945f-3d2b87e7e991
topic_type:
- apiref
ms.openlocfilehash: a6d26924773e6ad505975402ec3ace150d02cc3a
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894615"
---
# <a name="icordebugchaingetcaller-method"></a>ICorDebugChain::GetCaller メソッド
このチェーンを呼び出したチェーンを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetCaller (  
    [out] ICorDebugChain      **ppChain  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppChain`  
 入出力呼び出し元チェーンを表す、のオブジェクトのアドレスへのポインター。  
  
 (このチェーンまたはデバッガーが呼び出し履歴を初期化した場合のように) このチェーンが自発的`ppChain`に呼び出された場合、は null になります。  
  
## <a name="remarks"></a>解説  
 呼び出しがスレッド間でマーシャリングされている場合は、呼び出し元のチェーンが別のスレッドに存在する可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
