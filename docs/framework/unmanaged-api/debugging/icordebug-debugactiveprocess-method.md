---
title: ICorDebug::DebugActiveProcess メソッド
ms.date: 03/30/2017
api_name:
- ICorDebug.DebugActiveProcess
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebug::DebugActiveProcess
helpviewer_keywords:
- DebugActiveProcess method [.NET Framework debugging]
- ICorDebug::DebugActiveProcess method [.NET Framework debugging]
ms.assetid: fdab0ade-7f56-4fa2-b3ef-f7a1d2852bba
topic_type:
- apiref
ms.openlocfilehash: 3630e25b6c24edaa366f1b0fae088e760e851fa4
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895407"
---
# <a name="icordebugdebugactiveprocess-method"></a>ICorDebug::DebugActiveProcess メソッド
デバッガーを既存のプロセスにアタッチします。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DebugActiveProcess (  
    [in]  DWORD               id,  
    [in]  BOOL                win32Attach,  
    [out] ICorDebugProcess    **ppProcess  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `id`  
 からデバッガーがアタッチされるプロセスの ID。  
  
 `win32Attach`  
 からデバッガーがプロセスの Win32 デバッガー `true`として動作し、アンマネージコールバックをディスパッチする必要がある場合にに設定されるブール値。それ以外`false`の場合は。  
  
 `ppProcess`  
 入出力デバッガーがアタッチされているプロセスを表す "いいプロセス" オブジェクトのアドレスへのポインター。  
  
## <a name="remarks"></a>解説  
 相互運用デバッグは、IA-64 ベースおよび AMD64 ベースのプラットフォームなど、Win9x および x86 以外のプラットフォームではサポートされていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebug インターフェイス](icordebug-interface.md)
