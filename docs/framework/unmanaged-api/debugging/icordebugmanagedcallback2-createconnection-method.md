---
title: ICorDebugManagedCallback2::CreateConnection メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.CreateConnection
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::CreateConnection
helpviewer_keywords:
- CreateConnection method [.NET Framework debugging]
- ICorDebugManagedCallback2::CreateConnection method [.NET Framework debugging]
ms.assetid: 49e647be-9d63-4250-9d11-704e2a400d1b
topic_type:
- apiref
ms.openlocfilehash: 8e31f0a649fd1ca80d6557a0a7176549c67bf203
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501925"
---
# <a name="icordebugmanagedcallback2createconnection-method"></a>ICorDebugManagedCallback2::CreateConnection メソッド
新しい接続が作成されたことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CreateConnection (  
    [in] ICorDebugProcess     *pProcess,  
    [in] CONNID               dwConnectionId,  
    [in] WCHAR                *pConnName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pProcess`  
 から接続が作成されたプロセスを表す "いいプロセス" オブジェクトへのポインター  
  
 `dwConnectionId`  
 から新しい接続の ID。  
  
 `pConnName`  
 から新しい接続の名前へのポインター。  
  
## <a name="remarks"></a>解説  
 `CreateConnection`コールバックは、次のいずれかの場合に発生します。  
  
- デバッガーが接続を含むプロセスにアタッチする場合。 この場合、ランタイムは、 `CreateConnection` プロセス内の各接続に対して、イベントと、 [ICorDebugManagedCallback2:: ChangeConnection](icordebugmanagedcallback2-changeconnection-method.md)イベントを生成してディスパッチします。  
  
- ホストが[ホスティング API](../hosting/index.md)で[ICLRDebugManager:: beginconnection](../hosting/iclrdebugmanager-beginconnection-method.md)を呼び出すとき。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback2 インターフェイス](icordebugmanagedcallback2-interface.md)
- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
