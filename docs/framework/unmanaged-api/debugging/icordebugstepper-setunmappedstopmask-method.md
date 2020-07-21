---
title: ICorDebugStepper::SetUnmappedStopMask メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.SetUnmappedStopMask
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::SetUnmappedStopMask
helpviewer_keywords:
- ICorDebugStepper::SetUnmappedStopMask method [.NET Framework debugging]
- SetUnmappedStopMask method [.NET Framework debugging]
ms.assetid: b1211981-e90c-4e05-8def-fa18d85ad9ab
topic_type:
- apiref
ms.openlocfilehash: ef458fda8e8b7e75f92a4b3c06eabec106180d23
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379258"
---
# <a name="icordebugsteppersetunmappedstopmask-method"></a>ICorDebugStepper::SetUnmappedStopMask メソッド
実行が停止するマップされていないコードの種類を指定する値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT SetUnmappedStopMask (  
    [in] CorDebugUnmappedStop   mask  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `mask`  
 からデバッガーが実行を停止するマップされていないコードの種類を指定する CorDebugUnmappedStop 列挙値。  
  
 既定値は STOP_OTHER_UNMAPPED です。 STOP_UNMANAGED 値は、相互運用機能デバッグでのみ有効です。  
  
## <a name="remarks"></a>Remarks  
 デバッガーは、Microsoft 中間言語 (MSIL) への対応するマッピングがない just-in-time (JIT) コンパイルを検出すると、マップされていないコードの型を指定するフラグが設定されている場合、実行を停止します。それ以外の場合、ステップ実行は透過的に続行されます。  
  
 デバッガーがステッパを使用してメソッドを入力しない場合、マップされていないコードは必ずしもステップオーバーされません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
