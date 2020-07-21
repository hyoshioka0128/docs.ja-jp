---
title: ICorDebugThread::GetID メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetID
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetID
helpviewer_keywords:
- ICorDebugThread::GetID method [.NET Framework debugging]
- GetID method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: f1de4584-92df-42f3-9da4-fca03a1c6821
topic_type:
- apiref
ms.openlocfilehash: d01936481ec139757566d5b96cb95ea887cb8c20
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378063"
---
# <a name="icordebugthreadgetid-method"></a>ICorDebugThread::GetID メソッド
このコンポーネントのアクティブな部分の現在のオペレーティングシステム識別子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetID (  
    [out] DWORD *pdwThreadId  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pdwThreadId`  
 入出力スレッドの識別子。  
  
## <a name="remarks"></a>Remarks  
 オペレーティングシステムの識別子は、プロセスの実行中に変更される可能性があり、スレッドのさまざまな部分に対して異なる値を指定できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
