---
title: ICorDebugProcessEnum::Next メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcessEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcessEnum::Next
helpviewer_keywords:
- Next method, ICorDebugProcessEnum interface [.NET Framework debugging]
- ICorDebugProcessEnum::Next method [.NET Framework debugging]
ms.assetid: 4ac7077c-8d88-49c4-b360-b3af0c541c63
topic_type:
- apiref
ms.openlocfilehash: d00a5f71ac7e47d78deebca0e46350e465964c72
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210099"
---
# <a name="icordebugprocessenumnext-method"></a>ICorDebugProcessEnum::Next メソッド
現在の位置から開始して、指定された数の処理インスタンスを列挙から取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Next (  
    [in]  ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)]  
        ICorDebugProcess *processes[],  
    [out] ULONG *pceltFetched  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `celt`  
 から`ICorDebugProcess`取得するインスタンスの数。  
  
 `processes`  
 入出力ポインターの配列。各ポインターは、 `ICorDebugProcess` プロセスを表すオブジェクトを指します。  
  
 `pceltFetched`  
 入出力実際に返されたインスタンスの数へのポインター `ICorDebugProcess` 。 が1の場合、この値は null `celt` になります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
