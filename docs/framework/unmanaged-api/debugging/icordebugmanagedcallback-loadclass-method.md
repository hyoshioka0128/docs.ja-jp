---
title: ICorDebugManagedCallback::LoadClass メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.LoadClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::LoadClass
helpviewer_keywords:
- ICorDebugManagedCallback::LoadClass method [.NET Framework debugging]
- LoadClass method [.NET Framework debugging]
ms.assetid: e58dac7b-85c3-41ca-b9aa-3a7fc9ae6680
topic_type:
- apiref
ms.openlocfilehash: 5d35ab4610ffa04d15dd2404fdf8010308bcb42a
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212735"
---
# <a name="icordebugmanagedcallbackloadclass-method"></a>ICorDebugManagedCallback::LoadClass メソッド
クラスが読み込まれたことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT LoadClass (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugClass     *c  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 からクラスが読み込まれたアプリケーションドメインを表す、のオブジェクトへのポインター。  
  
 `c`  
 からクラスを表す、のオブジェクトへのポインター。  
  
## <a name="remarks"></a>Remarks  
 このコールバックは、クラスを含むモジュールに対してクラスの読み込みが有効になっている場合にのみ発生します。 動的モジュールでは、クラスの読み込みが常に有効になっています。  
  
 `LoadClass`コールバックは、動的モジュールで新しく生成されたクラスにブレークポイントをバインドするための適切な時間を提供します。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [UnloadClass メソッド](icordebugmanagedcallback-unloadclass-method.md)
- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
