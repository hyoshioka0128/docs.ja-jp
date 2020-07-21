---
title: ICorDebugBreakpointEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugBreakpointEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugBreakpointEnum::Next
helpviewer_keywords:
- Next method, ICorDebugBreakpointEnum interface [.NET Framework debugging]
- ICorDebugBreakpointEnum::Next method [.NET Framework debugging]
ms.assetid: 2e6bbaea-79ba-448c-a0e3-7c90fc7c2939
topic_type:
- apiref
ms.openlocfilehash: af90886390b59932d3ae146a70fc2901ec1c378d
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894662"
---
# <a name="icordebugbreakpointenumnext-method"></a>ICorDebugBreakpointEnum::Next メソッド
現在の位置から開始して、指定した数の ICorDebugBreakpoint インスタンスを列挙から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in] ULONG  celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugBreakpoint *breakpoints[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から取得するインスタンス`ICorDebugBreakpoint`の数。  
  
 `breakpoints`  
 入出力ポインターの配列。各ポインターは、ブレークポイントを`ICorDebugBreakpoint`表すオブジェクトを指します。  
  
 `pceltFetched`  
 入出力実際に返されたインスタンス`ICorDebugBreakpoint`の数へのポインター。 が1の場合`celt` 、この値は null になります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
