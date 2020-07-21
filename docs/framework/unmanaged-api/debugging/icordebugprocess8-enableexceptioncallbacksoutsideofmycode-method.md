---
title: ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode メソッド
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: b3af44ec-7d41-425b-aed9-0c4379e5cbe9
ms.openlocfilehash: e54dd051f0dbd9c1964d381c2e05189c375fa66d
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210138"
---
# <a name="icordebugprocess8enableexceptioncallbacksoutsideofmycode-method"></a>ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode メソッド
[.NET Framework 4.6 以降のバージョンでサポートされています]  
  
 特定の種類の[ICorDebugManagedCallback2](icordebugmanagedcallback2-interface.md)例外コールバックを有効または無効にします。  
  
## <a name="syntax"></a>構文  
  
```cpp
HRESULT EnableExceptionCallbacksOutsideOfMyCode(  
   [in] BOOL enableExceptionsOutsideOfJMC  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `enableExceptionsOutsideOfJMC`  
 [入力]  
  
## <a name="remarks"></a>Remarks  
 `enableExceptionsOutsideOfJMC` の値が `false` の場合:  
  
- デバッガーへのコールバックでは DEBUG_EXCEPTION_FIRST_CHANCE 例外は発生しません。  
  
- 例外がユーザー コードにエスケープされることがない場合 (つまり、例外の発生から例外ハンドラーへのパスで、JustMyCode または JMC とマークされているメソッドがない場合)、DEBUG_EXCEPTION_CATCH_HANDLER_FOUND 例外は発生しません。  
  
 `enableExceptionsOutsideOfJMC` の既定値は `true`です。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugProcess8 インターフェイス](icordebugprocess8-interface.md)
- [デバッグのインターフェイス](debugging-interfaces.md)
