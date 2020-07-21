---
title: ICorDebugMemoryBuffer::GetStartAddress メソッド
ms.date: 03/30/2017
ms.assetid: f804d9ab-8c88-44f0-b278-5fcca7f87726
ms.openlocfilehash: 47369c744ee42fb03857a3e69063a04e4f509d0d
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83212348"
---
# <a name="icordebugmemorybuffergetstartaddress-method"></a>ICorDebugMemoryBuffer::GetStartAddress メソッド
メモリ バッファーの開始アドレスを取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetStartAddress(  
   [out] LPCVOID *address  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `address`  
 [out] メモリ バッファーの開始アドレスへのポインター。  
  
## <a name="remarks"></a>Remarks  
  
> [!WARNING]
> このメソッドは .NET ネイティブでのみ使用できます。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugMemoryBuffer インターフェイス](icordebugmemorybuffer-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
