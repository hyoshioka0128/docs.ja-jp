---
title: ICorDebugFrame::GetFunction メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFrame.GetFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFrame::GetFunction
helpviewer_keywords:
- GetFunction method, ICorDebugFrame interface [.NET Framework debugging]
- ICorDebugFrame::GetFunction method [.NET Framework debugging]
ms.assetid: 879d2311-0ff1-4616-a8b3-959ea5868b2e
topic_type:
- apiref
ms.openlocfilehash: 7bf73266f0269cfcd5371c5155856800036cc066
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209839"
---
# <a name="icordebugframegetfunction-method"></a>ICorDebugFrame::GetFunction メソッド
このスタックフレームに関連付けられているコードを格納している関数を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetFunction (  
    [out] ICorDebugFunction  **ppFunction  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppFunction`  
 入出力このスタックフレームに関連付けられているコードを格納している関数を表す、オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `GetFunction`フレームが特定の関数に関連付けられていない場合、メソッドは失敗する可能性があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
