---
title: ICorDebugStepper::StepRange メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugStepper.StepRange
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugStepper::StepRange
helpviewer_keywords:
- StepRange method [.NET Framework debugging]
- ICorDebugStepper::StepRange method [.NET Framework debugging]
ms.assetid: b9776112-6e6d-4708-892a-8873db02e16f
topic_type:
- apiref
ms.openlocfilehash: b040d9454a5a3a0d550bb645953c783357419f73
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379489"
---
# <a name="icordebugsteppersteprange-method"></a>ICorDebugStepper::StepRange メソッド
この ICorDebugStepper は、含まれているスレッドを1ステップずつ実行し、指定した範囲の最後のコードに到達したときにを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT StepRange (  
    [in] BOOL     bStepIn,  
    [in, size_is(cRangeCount)] COR_DEBUG_STEP_RANGE ranges[],  
    [in] ULONG32  cRangeCount  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `bStepIn`  
 から`true`スレッド内で呼び出される関数にステップインするには、をに設定します。 関数を `false` ステップオーバーするには、をに設定します。  
  
 `ranges`  
 からCOR_DEBUG_STEP_RANGE 構造体の配列。それぞれが範囲を指定します。  
  
 `cRangeCount`  
 [in] `ranges` 配列のサイズ。  
  
## <a name="remarks"></a>Remarks  
 `StepRange`メソッドは[ICorDebugStepper:: Step](icordebugstepper-step-method.md)メソッドと同様に機能しますが、指定された範囲外のコードに到達するまでは完了しない点が異なります。  
  
 これは、一度に1つの命令をステップ実行するよりも効率的です。 範囲は、ステッパのフレームの先頭からのオフセットペアのリストとして指定されます。  
  
 範囲は、メソッドの MSIL (Microsoft 中間言語) コードに対する相対値です。 [ICorDebugStepper:: SetRangeIL](icordebugstepper-setrangeil-method.md)をで呼び出し、 `false` メソッドのネイティブコードを基準として範囲を設定します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
