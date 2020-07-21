---
title: ICorDebugStepper::Deactivate メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.Deactivate
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::Deactivate
helpviewer_keywords:
- Deactivate method [.NET Framework debugging]
- ICorDebugStepper::Deactivate method [.NET Framework debugging]
ms.assetid: 855f4199-b62d-40ce-998e-1eb4a1772142
topic_type:
- apiref
ms.openlocfilehash: 760f69baf311cf320e9c358ba1c45c942934f1a5
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379393"
---
# <a name="icordebugstepperdeactivate-method"></a>ICorDebugStepper::Deactivate メソッド
この ICorDebugStepper は、受け取った最後のステップコマンドをキャンセルします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Deactivate ();  
```  
  
## <a name="remarks"></a>Remarks  
 最後に受信したステップコマンドが取り消された後に、新しいステップ実行コマンドが発行される場合があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
