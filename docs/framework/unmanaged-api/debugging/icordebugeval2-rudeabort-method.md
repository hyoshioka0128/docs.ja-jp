---
title: ICorDebugEval2::RudeAbort メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugEval2.RudeAbort
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval2::RudeAbort
helpviewer_keywords:
- ICorDebugEval2::RudeAbort method [.NET Framework debugging]
- RudeAbort method, ICorDebugEval2 interface [.NET Framework debugging]
ms.assetid: 02468edf-d32b-4cb3-aaa8-3dd2abfc8b25
topic_type:
- apiref
ms.openlocfilehash: e901c65824ee8d6949c79c7778944148c0d9eb28
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976058"
---
# <a name="icordebugeval2rudeabort-method"></a>ICorDebugEval2::RudeAbort メソッド
この`ICorDebugEval2`が現在実行している計算を中止します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT RudeAbort ();  
```  
  
## <a name="remarks"></a>Remarks  
 `RudeAbort`は、エバリュエーターによって保持されているロックを解放しないため、デバッグセッションは安全ではない状態のままになります。 このメソッドは細心の注意を払って呼び出してください。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
