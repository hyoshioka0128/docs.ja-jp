---
title: ICorDebug::Terminate メソッド
ms.date: 03/30/2017
api_name:
- ICorDebug.Terminate
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::Terminate
helpviewer_keywords:
- Terminate method, ICorDebug interface [.NET Framework debugging]
- ICorDebug::Terminate method [.NET Framework debugging]
ms.assetid: fffe5616-0896-4426-ab5e-21869b514883
topic_type:
- apiref
ms.openlocfilehash: 44bb98f54debb129f951cc388fea81ca0f17b20c
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895318"
---
# <a name="icordebugterminate-method"></a>ICorDebug::Terminate メソッド
オブジェクトを`ICorDebug`終了します。  
  
> [!NOTE]
> `Terminate`デバッグされているすべてのプロセスに対して、 [ExitProcess Callback callback::](icordebugmanagedcallback-exitprocess-method.md) callback が受信されるまでは呼び出さないでください。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Terminate ();  
```  
  
## <a name="remarks"></a>解説  
 `Terminate`オブジェクトが不要になっ`ICorDebug`た場合は、を呼び出す必要があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebug インターフェイス](icordebug-interface.md)
