---
title: ICorDebugThread::CreateStepper メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugThread.CreateStepper
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread::CreateStepper
helpviewer_keywords:
- ICorDebugThread::CreateStepper method [.NET Framework debugging]
- CreateStepper method, ICorDebugThread interface [.NET Framework debugging]
ms.assetid: 4657443f-dd12-431b-a648-175c23f13c83
topic_type:
- apiref
ms.openlocfilehash: a74d32478bc88ee634fa5ff9b61ac2059bc8e302
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379715"
---
# <a name="icordebugthreadcreatestepper-method"></a>ICorDebugThread::CreateStepper メソッド
この ICorDebugStepper スレッドのアクティブなフレームをステップ実行できるようにする、オブジェクトを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateStepper (  
    [out] ICorDebugStepper **ppStepper  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `ppStepper`  
 入出力`ICorDebugStepper`このスレッドのアクティブフレームのステップ実行を可能にするオブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
 アクティブなフレームはアンマネージコードである場合があります。  
  
 `ICorDebugStepper`実際のステップ実行には、インターフェイスを使用する必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]
