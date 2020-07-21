---
title: ICorDebugDebugEvent::GetThread メソッド
ms.date: 03/30/2017
ms.assetid: 4f2e9a2c-8369-4a07-a881-ad5422626353
ms.openlocfilehash: acce18517c105739417fc734b49ff004ca9546dc
ms.sourcegitcommit: fff146ba3fd1762c8c432d95c8b877825ae536fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82976379"
---
# <a name="icordebugdebugeventgetthread-method"></a>ICorDebugDebugEvent::GetThread メソッド
イベントが発生したスレッドを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetThread(  
        [out]ICorDebugThread **ppThread  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 ppThread  
 [出力] イベントが発生したスレッドを表す ICorDebugThread オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!NOTE]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugDebugEvent インターフェイス](icordebugdebugevent-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
