---
title: ICorDebugManagedCallback3 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback3
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback3
helpviewer_keywords:
- ICorDebugManagedCallback3 interface [.NET Framework debugging]
ms.assetid: a95389d3-cf2e-47a4-9805-61426acc6b65
topic_type:
- apiref
ms.openlocfilehash: 63e3f166c4cbf17f4892dccf770343bfbf6e0284
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83209748"
---
# <a name="icordebugmanagedcallback3-interface"></a>ICorDebugManagedCallback3 インターフェイス
有効なカスタムのデバッガー通知が発生したことを示すコールバック メソッドを提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CustomNotification メソッド](icordebugmanagedcallback3-customnotification-method.md)|有効なカスタムデバッガー通知が発生したことを示します。|  
  
## <a name="remarks"></a>Remarks  
 このインターフェイスは、" [ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md) [" というインターフェイスを論理的](icordebugmanagedcallback-interface.md)に拡張したものです。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
- [ICorDebugManagedCallback2 インターフェイス](icordebugmanagedcallback2-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
