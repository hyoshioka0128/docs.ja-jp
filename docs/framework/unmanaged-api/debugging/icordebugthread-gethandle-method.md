---
title: ICorDebugThread::GetHandle メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.GetHandle
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::GetHandle
helpviewer_keywords:
- GetHandle method, ICorDebugThread interface [.NET Framework debugging]
- ICorDebugThread::GetHandle method [.NET Framework debugging]
ms.assetid: 172ef8c4-2ead-4cfc-bd2e-dee4fb7191cd
topic_type:
- apiref
ms.openlocfilehash: 16aafa439fc81c3606f98ca2ba860316ec46e0db
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379735"
---
# <a name="icordebugthreadgethandle-method"></a>ICorDebugThread::GetHandle メソッド
このスレッドのアクティブな部分の現在のハンドルを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetHandle (  
    [out] HTHREAD *phThreadHandle  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `phThreadHandle`  
 入出力このスレッドのアクティブな部分のハンドルである HTHREAD へのポインター。  
  
## <a name="remarks"></a>Remarks  
 ハンドルは、プロセスが実行されると変化する場合があり、スレッドのさまざまな部分で異なる場合があります。  
  
 このハンドルは、デバッグ API によって所有されています。 使用する前に、デバッガーがそれを複製する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
