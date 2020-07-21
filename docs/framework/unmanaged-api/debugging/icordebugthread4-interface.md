---
title: ICorDebugThread4 インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugThread4
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugThread4
helpviewer_keywords:
- ICorDebugThread4 interface [.NET Framework debugging]
ms.assetid: a8c7719a-322b-4133-8566-4c27218dc104
topic_type:
- apiref
ms.openlocfilehash: a0d6f3e109f92ad44eeeb1b1dec05e53015992a6
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83378358"
---
# <a name="icordebugthread4-interface"></a>ICorDebugThread4 インターフェイス
スレッドのブロック情報を提供します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[GetBlockingObjects メソッド](icordebugthread4-getblockingobjects-method.md)|スレッドブロック情報を提供する[CorDebugBlockingObject](cordebugblockingobject-structure.md)構造体の順序付けられた列挙体を提供します。|  
|[HadUnhandledException メソッド](icordebugthread4-hadunhandledexception-method.md)|スレッドで未処理の例外が発生したかどうかを示します。|  
|[GetCurrentCustomDebuggerNotification メソッド](icordebugthread4-getcurrentcustomdebuggernotification-method.md)|現在のスレッドの現在の[ICorDebugManagedCallback3:: CustomNotification](icordebugmanagedcallback3-customnotification-method.md)オブジェクトを取得します。|  
  
## <a name="remarks"></a>Remarks  
 このインターフェイスは、ICorDebugThread2、 [ICorDebugThread3](icordebugthread3-interface.md)の各インターフェイスの論理的な拡張機能です。  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
