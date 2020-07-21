---
title: ICorDebugProcess6::ProcessStateChanged メソッド
ms.date: 03/30/2017
ms.assetid: fb6d30d9-54f3-462b-8ebf-ce0440791ad5
ms.openlocfilehash: 6be216741e902b15efc3a3ece95cb4a4229960e3
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212849"
---
# <a name="icordebugprocess6processstatechanged-method"></a>ICorDebugProcess6::ProcessStateChanged メソッド
プロセスが実行されていることを[ICorDebug](icordebug-interface.md)に通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT ProcessStateChanged(   [in] CorDebugStateChange change);  
```  
  
## <a name="parameters"></a>パラメーター  
 `change`  
 から[ProcessStateChanged](icordebugprocess6-processstatechanged-method.md)列挙型のメンバー  
  
## <a name="remarks"></a>Remarks  
 デバッガーはこのメソッドを呼び出して、プロセスが実行されていることを[ICorDebug](icordebug-interface.md)に通知します。  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess6 インターフェイス](icordebugprocess6-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
