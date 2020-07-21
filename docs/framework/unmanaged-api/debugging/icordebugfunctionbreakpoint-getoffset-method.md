---
title: ICorDebugFunctionBreakpoint::GetOffset メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFunctionBreakpoint.GetOffset
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunctionBreakpoint::GetOffset
helpviewer_keywords:
- ICorDebugFunctionBreakpoint::GetOffset method [.NET Framework debugging]
- GetOffset method, ICorDebugFunctionBreakpoint interface [.NET Framework debugging]
ms.assetid: e619eae4-3ac3-4c37-bba4-55e59989b9cb
topic_type:
- apiref
ms.openlocfilehash: 0f6fe5d7eb5926d48809bb6490ba75df9d4a5033
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213154"
---
# <a name="icordebugfunctionbreakpointgetoffset-method"></a>ICorDebugFunctionBreakpoint::GetOffset メソッド
関数内のブレークポイントのオフセットを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetOffset (  
    [out] ULONG32  *pnOffset  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pnOffset`  
 入出力ブレークポイントのオフセットへのポインター。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
