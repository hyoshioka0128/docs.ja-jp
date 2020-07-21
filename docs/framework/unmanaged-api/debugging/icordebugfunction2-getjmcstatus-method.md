---
title: ICorDebugFunction2::GetJMCStatus メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugFunction2.GetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugFunction2::GetJMCStatus
helpviewer_keywords:
- ICorDebugFunction2::GetJMCStatus method [.NET Framework debugging]
- GetJMCStatus method [.NET Framework debugging]
ms.assetid: 840a71ed-bf5a-4f5e-8ed6-762222b34493
topic_type:
- apiref
ms.openlocfilehash: 56dc5f87b32b3aaa0bfbb69541d5a01ae26606ab
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83213236"
---
# <a name="icordebugfunction2getjmcstatus-method"></a>ICorDebugFunction2::GetJMCStatus メソッド
この ICorDebugFunction2 オブジェクトによって表される関数がユーザーコードとしてマークされているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetJMCStatus (  
    [out] BOOL   *pbIsJustMyCode  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pbIsJustMyCode`  
 入出力`true`この関数がユーザーコードとしてマークされている場合は、ブール値へのポインター。それ以外の場合は、値は `false` です。  
  
## <a name="remarks"></a>Remarks  
 このによって表される関数を `ICorDebugFunction2` デバッグできない場合、 `pbIsJustMyCode` は常にになり `false` ます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
