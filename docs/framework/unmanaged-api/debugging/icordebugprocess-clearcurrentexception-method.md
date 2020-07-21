---
title: ICorDebugProcess::ClearCurrentException メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.ClearCurrentException
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::ClearCurrentException
helpviewer_keywords:
- ClearCurrentException method, ICorDebugProcess interface [.NET Framework debugging]
- ICorDebugProcess::ClearCurrentException method [.NET Framework debugging]
ms.assetid: 9e02ee1a-e495-4578-bfb5-b946274bede7
topic_type:
- apiref
ms.openlocfilehash: b8d20de990ff4a27a82590342494a307c986457e
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207390"
---
# <a name="icordebugprocessclearcurrentexception-method"></a>ICorDebugProcess::ClearCurrentException メソッド
指定されたスレッドで現在のアンマネージ例外をクリアします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ClearCurrentException([in] DWORD threadID);  
```  
  
## <a name="parameters"></a>パラメーター  
 `threadID`  
 から現在のアンマネージ例外がクリアされるスレッドの ID。  
  
## <a name="remarks"></a>Remarks  
 スレッドがアンマネージ例外を報告し[たときに](icordebugcontroller-continue-method.md)、デバッグ対象では無視する必要がある場合は、このメソッドを呼び出します。 これにより、所定のスレッドで未処理の帯域内 (IB) イベントと帯域外 (OOB) イベントの両方がクリアされます。 すべての OOB ブレークポイントと単一ステップの例外は、自動的にクリアされます。  
  
 スレッドで現在のマネージ例外をインターセプトするには、 [ICorDebugThread2:: InterceptCurrentException](icordebugthread2-interceptcurrentexception-method.md)を使用します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
