---
title: ICorDebugController::HasQueuedCallbacks メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugController.HasQueuedCallbacks
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::HasQueuedCallbacks
helpviewer_keywords:
- HasQueuedCallbacks method [.NET Framework debugging]
- ICorDebugController::HasQueuedCallbacks method [.NET Framework debugging]
ms.assetid: 0d6a1cd9-370b-4462-adbf-e3980e897ea7
topic_type:
- apiref
ms.openlocfilehash: bd656445c2451d0583ddbc45e71c9e090bb80305
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82892776"
---
# <a name="icordebugcontrollerhasqueuedcallbacks-method"></a>ICorDebugController::HasQueuedCallbacks メソッド
マネージコールバックが、指定されたスレッドに対して現在キューに登録されているかどうかを示す値を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT HasQueuedCallbacks (  
    [in] ICorDebugThread *pThread,  
    [out] BOOL           *pbQueued  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pThread`  
 からスレッドを表す "ツールスレッド" オブジェクトへのポインター。  
  
 `pbQueued`  
 入出力マネージコールバックが、指定さ`true`れたスレッドに対して現在キューに格納されている場合は、値を指すポインター。それ以外`false`の場合は。  
  
 パラメーターに null が指定されて`HasQueuedCallbacks`いる場合`true` 、は、現在マネージコールバックが任意のスレッドに対してキューに置かれている場合、を返します。 `pThread`  
  
## <a name="remarks"></a>解説  
 コールバックは[、次の](icordebugcontroller-continue-method.md)ように表示されるたびに1つずつディスパッチされます。 デバッガーでは、同時に発生する複数のデバッグイベントを報告する場合に、このフラグをチェックできます。  
  
 デバッグイベントがキューに登録されている場合は、既に発生しているため、デバッガーはキュー全体をドレインして、デバッグ対象の状態を確認する必要があります。 (を`ICorDebugController::Continue`呼び出してキューをドレインします)。たとえば、キューにスレッド*x*の2つのデバッグイベントが含まれており、デバッガーが最初のデバッグイベントの後にスレッド`ICorDebugController::Continue` *x*を中断した後にを呼び出すと、スレッドが中断されていても、スレッド*x*の2番目のデバッグイベントがディスパッチされます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目
