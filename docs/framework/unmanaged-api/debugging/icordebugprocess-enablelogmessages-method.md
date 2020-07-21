---
title: ICorDebugProcess::EnableLogMessages メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugProcess.EnableLogMessages
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess::EnableLogMessages
helpviewer_keywords:
- ICorDebugProcess::EnableLogMessages method [.NET Framework debugging]
- EnableLogMessages method [.NET Framework debugging]
ms.assetid: 14a4e5a3-3eaf-4f53-9dd1-762726963a23
topic_type:
- apiref
ms.openlocfilehash: 3b850a462ce354b81f4406fce7fd9d8d9b6013d8
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83207903"
---
# <a name="icordebugprocessenablelogmessages-method"></a>ICorDebugProcess::EnableLogMessages メソッド
デバッガーへのログメッセージの転送を有効または無効にします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT EnableLogMessages([in]BOOL fOnOff);  
```  
  
## <a name="parameters"></a>パラメーター  
 `fOnOff`  
 [入力] `true`ログメッセージの転送を有効にします。`false`転送を無効にします。  
  
## <a name="remarks"></a>Remarks  
 このメソッドは、によって実行される場合にのみ有効です: [: CreateProcess managedcallback:: CreateProcess](icordebugmanagedcallback-createprocess-method.md)コールバックが発生します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
