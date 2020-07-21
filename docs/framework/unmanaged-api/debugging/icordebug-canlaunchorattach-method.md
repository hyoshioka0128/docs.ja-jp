---
title: ICorDebug::CanLaunchOrAttach メソッド
ms.date: 03/30/2017
api_name:
- ICorDebug.CanLaunchOrAttach
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::CanLaunchOrAttach
helpviewer_keywords:
- ICorDebug::CanLaunchOrAttach method [.NET Framework debugging]
- CanLaunchOrAttach method [.NET Framework debugging]
ms.assetid: ca7723db-7c07-4cdd-bd92-fba34928b623
topic_type:
- apiref
ms.openlocfilehash: 354df02b27e87550ba602fe102352455c227441b
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82859680"
---
# <a name="icordebugcanlaunchorattach-method"></a>ICorDebug::CanLaunchOrAttach メソッド
現在のコンピューターおよびランタイム構成のコンテキスト内で、新しいプロセスを起動するか、指定した既存のプロセスにアタッチするかを示す HRESULT を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT CanLaunchOrAttach (  
    [in] DWORD      dwProcessId,  
    [in] BOOL       win32DebuggingEnabled  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `dwProcessId`  
 から既存のプロセスの ID。  
  
 `win32DebuggingEnabled`  
 からWin32 デバッグ`true`を有効にして起動する場合、または win32 デバッグを有効にしてアタッチする場合は、を渡します。それ以外の`false`場合は、を渡します。  
  
## <a name="return-value"></a>戻り値  
 現在のコンピューターと実行時の構成に関する情報を指定して、デバッグサービスによって新しいプロセスの起動または特定のプロセスへのアタッチが可能かどうかを判断する場合は S_OK します。 使用できる HRESULT 値は次のとおりです。  
  
- S_OK  
  
- CORDBG_E_DEBUGGING_NOT_POSSIBLE  
  
- CORDBG_E_KERNEL_DEBUGGER_PRESENT  
  
- CORDBG_E_KERNEL_DEBUGGER_ENABLED  
  
## <a name="remarks"></a>解説  
 このメソッドは純粋な情報です。 インターフェイスは、によって`CanLaunchOrAttach`返される値に関係なく、プロセスの起動やアタッチを停止することはありません。  
  
 Win32 デバッグが有効になっている状態で起動する場合、または Win32 `true`デバッグ`win32DebuggingEnabled`を有効にしてアタッチする場合は、にを渡します。 このオプションを使用`CanLaunchOrAttach`すると、によって返される HRESULT が異なる場合があります。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebug インターフェイス](icordebug-interface.md)
