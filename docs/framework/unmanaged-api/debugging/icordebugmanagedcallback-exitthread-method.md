---
title: ICorDebugManagedCallback::ExitThread メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.ExitThread
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::ExitThread
helpviewer_keywords:
- ExitThread method [.NET Framework debugging]
- ICorDebugManagedCallback::ExitThread method [.NET Framework debugging]
ms.assetid: 62db708b-6cf0-45c5-b897-4b5c75bd2505
topic_type:
- apiref
ms.openlocfilehash: 3ba1280aa44a9445f6af7fe9a8769b7cdc7edb66
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83205245"
---
# <a name="icordebugmanagedcallbackexitthread-method"></a>ICorDebugManagedCallback::ExitThread メソッド
マネージコードを実行していたスレッドが終了したことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ExitThread (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugThread    *thread  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 からマネージスレッドを含むアプリケーションドメインを表す、コードの Appdomain オブジェクトへのポインター。  
  
 `thread`  
 からマネージスレッドを表す、コードスレッドオブジェクトへのポインター。  
  
## <a name="remarks"></a>Remarks  
 `ExitThread`コールバックが発生すると、スレッドはスレッド列挙に表示されなくなります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
