---
title: ICorDebugChain::GetActiveFrame メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugChain.GetActiveFrame
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugChain::GetActiveFrame
helpviewer_keywords:
- ICorDebugChain::GetActiveFrame method [.NET Framework debugging]
- GetActiveFrame method, ICorDebugChain interface [.NET Framework debugging]
ms.assetid: 36887017-670b-4f21-b406-8fab956f84a3
topic_type:
- apiref
ms.openlocfilehash: 2f67188539d5ad5523c255fbc663e990e1b8245f
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894675"
---
# <a name="icordebugchaingetactiveframe-method"></a>ICorDebugChain::GetActiveFrame メソッド
チェーンのアクティブな (つまり、最新の) フレームを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetActiveFrame (  
    [out] ICorDebugFrame   **ppFrame  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppFrame`  
 入出力チェーン上のアクティブな (つまり、最新の) フレームを表す、の各フレームオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 使用できるマネージスタックフレームがない場合`ppFrame` 、は null に設定されます。  
  
 アクティブなフレームが使用できない場合、呼び出しは成功し`ppFrame` 、は null になります。 CHAIN_ENTER_UNMANAGED によって開始されるチェーンと、CHAIN_CLASS_INIT によって開始されるチェーンに対して、アクティブなフレームは使用できません。 CorDebugChainReason 列挙体を参照してください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
