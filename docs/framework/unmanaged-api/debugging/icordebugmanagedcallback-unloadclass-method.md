---
title: ICorDebugManagedCallback::UnloadClass メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.UnloadClass
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::UnloadClass
helpviewer_keywords:
- ICorDebugManagedCallback::UnloadClass method [.NET Framework debugging]
- UnloadClass method [.NET Framework debugging]
ms.assetid: 66a59b18-ce9a-41f4-b23b-4dd6753d6d36
topic_type:
- apiref
ms.openlocfilehash: a7b71170f58ddfe0295da28b8c9fc73286b074e6
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212270"
---
# <a name="icordebugmanagedcallbackunloadclass-method"></a>ICorDebugManagedCallback::UnloadClass メソッド
クラスがアンロードされていることをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UnloadClass (  
    [in] ICorDebugAppDomain  *pAppDomain,  
    [in] ICorDebugClass      *c  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 からクラスを含むアプリケーションドメインを表す、のオブジェクトへのポインター。  
  
 `c`  
 からクラスを表す、のオブジェクトへのポインター。  
  
## <a name="remarks"></a>Remarks  
 この呼び出しの後にクラスを参照することはできません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [LoadClass メソッド](icordebugmanagedcallback-loadclass-method.md)
- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
