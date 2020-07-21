---
title: ICorDebugManagedCallback2::Exception メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2.Exception
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2::Exception
helpviewer_keywords:
- ICorDebugManagedCallback2::Exception method [.NET Framework debugging]
- Exception method, ICorDebugManagedCallback2 interface [.NET Framework debugging]
ms.assetid: 78b0f14f-2fae-4e63-8412-4df119ee8468
topic_type:
- apiref
ms.openlocfilehash: 612b63ba9aa3504cab5196932293946d486955ce
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83210203"
---
# <a name="icordebugmanagedcallback2exception-method"></a>ICorDebugManagedCallback2::Exception メソッド
例外ハンドラーの検索が開始されたことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT Exception (  
    [in] ICorDebugAppDomain   *pAppDomain,  
    [in] ICorDebugThread      *pThread,  
    [in] ICorDebugFrame       *pFrame,  
    [in] ULONG32              nOffset,  
    [in] CorDebugExceptionCallbackType dwEventType,  
    [in] DWORD                dwFlags  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 から例外がスローされたスレッドを含むアプリケーションドメインを表す、のオブジェクトへのポインター。  
  
 `pThread`  
 から例外がスローされたスレッドを表す、スレッドオブジェクトへのポインター。  
  
 `pFrame`  
 からパラメーターによって決定される、フレームを表すテキストボックスオブジェクトへのポインター `dwEventType` 。 詳細については、「解説」の表を参照してください。  
  
 `nOffset`  
 からパラメーターによって決定されるオフセットを指定する整数 `dwEventType` 。 詳細については、「解説」の表を参照してください。  
  
 `dwEventType`  
 からこの例外コールバックの種類を指定する Cordebugexceptioncallback Type 列挙体の値。  
  
 `dwFlags`  
 から例外に関する追加情報を指定する[Cordebugexceptionflags](cordebugexceptionflags-enumeration.md)列挙値  
  
## <a name="remarks"></a>Remarks  
 `Exception`コールバックは、例外処理プロセスの検索フェーズ中にさまざまなポイントで呼び出されます。 つまり、例外のアンワインド中に複数回呼び出すことができます。  
  
 処理されている例外は、パラメーターによって参照されているスレッドオブジェクトから取得でき `pThread` ます。  
  
 特定のフレームとオフセットは、パラメーターによって次のように決定され `dwEventType` ます。  
  
|`dwEventType` の値|`pFrame` の値|`nOffset` の値|  
|----------------------------|-----------------------|------------------------|  
|DEBUG_EXCEPTION_FIRST_CHANCE|例外をスローしたフレーム。|フレーム内の命令ポインター。|  
|DEBUG_EXCEPTION_USER_FIRST_CHANCE|スローされた例外のポイントに最も近いユーザーコードフレーム。|フレーム内の命令ポインター。|  
|DEBUG_EXCEPTION_CATCH_HANDLER_FOUND|Catch ハンドラーを格納しているフレーム。|Catch ハンドラーの先頭の MSIL (Microsoft 中間言語) オフセット。|  
|DEBUG_EXCEPTION_UNHANDLED|NULL|未定義です。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback2 インターフェイス](icordebugmanagedcallback2-interface.md)
- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
