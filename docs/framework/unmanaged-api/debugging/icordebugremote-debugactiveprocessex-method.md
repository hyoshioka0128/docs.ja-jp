---
title: ICorDebugRemote::DebugActiveProcessEx メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugRemote.DebugActiveProcessEx
api_location:
- CorDebug.dll
api_type:
- COM
f1_keywords:
- ICorDebugRemoteTarget::DebugActiveProcessEx
helpviewer_keywords:
- ICorDebugRemote::DebugActiveProcessEx method [.NET Framework debugging]
- DebugActiveProcessEx method, ICorDebugRemote interface [.NET Framework debugging]
ms.assetid: b0df5c5d-9a2e-47bf-894c-6f8a9fe24a1f
topic_type:
- apiref
ms.openlocfilehash: b95e9f3a0d584511a2bcf156ed2c50a98f96d071
ms.sourcegitcommit: d6bd7903d7d46698e9d89d3725f3bb4876891aa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83379061"
---
# <a name="icordebugremotedebugactiveprocessex-method"></a>ICorDebugRemote::DebugActiveProcessEx メソッド
デバッガーでリモートコンピューター上のプロセスを起動します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DebugActiveProcessEx (  
    [in]  ICorDebugRemoteTarget *   pRemoteTarget,  
    [in]  DWORD                     dwProcessId,  
    [in]  BOOL                      fWin32Attach,  
    [out] ICorDebugProcess **       ppProcess  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pRemoteTarget`  
 からツールの[ターゲットインターフェイス](icordebugremotetarget-interface.md)を指すポインター。 このパラメーターは、プロセスが実行されているコンピューターを決定するために使用されます。  
  
 `id`  
 からデバッガーがアタッチされるプロセスの ID。  
  
 `win32Attach`  
 [入力] `true`デバッガーがプロセスの Win32 デバッガーとして動作し、アンマネージコールバックをディスパッチする必要がある場合は。それ以外の場合は `false` 。  
  
 `ppProcess`  
 入出力デバッガーがアタッチされているプロセスを表す "いいプロセス" オブジェクトのアドレスへのポインター。  
  
## <a name="return-value"></a>戻り値  
 S_OK  
 リモートコンピューター上のプロセスに正常にアタッチされました。  
  
 E_FAIL (またはその他の E_ リターン コード)  
 リモートコンピューター上のプロセスにアタッチできません。  
  
## <a name="remarks"></a>Remarks  
 混合モードのデバッグは、Silverlight ではサポートされていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:** 4.5、4、3.5 SP1  
  
## <a name="see-also"></a>関連項目

- [ICorDebugRemote インターフェイス](icordebugremote-interface.md)
- [ICorDebug インターフェイス](icordebug-interface.md)

- [デバッグのインターフェイス](debugging-interfaces.md)
