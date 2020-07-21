---
title: ICorDebugManagedCallback::UpdateModuleSymbols メソッド
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback.UpdateModuleSymbols
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback::UpdateModuleSymbols
helpviewer_keywords:
- UpdateModuleSymbols method [.NET Framework debugging]
- ICorDebugManagedCallback::UpdateModuleSymbols method [.NET Framework debugging]
ms.assetid: 0863f644-58e8-45a0-b0c3-a28e99b20938
topic_type:
- apiref
ms.openlocfilehash: c0381cf924e44e581c8b275c9750cacba045cf1b
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84501782"
---
# <a name="icordebugmanagedcallbackupdatemodulesymbols-method"></a>ICorDebugManagedCallback::UpdateModuleSymbols メソッド
共通言語ランタイムモジュールのシンボルが変更されたことをデバッガーに通知します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT UpdateModuleSymbols (  
    [in] ICorDebugAppDomain *pAppDomain,  
    [in] ICorDebugModule    *pModule,  
    [in] IStream            *pSymbolStream  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 `pAppDomain`  
 からシンボルが変更されたモジュールを含むアプリケーションドメインを表す、コードのオブジェクトへのポインター。  
  
 `pModule`  
 からシンボルが変更されたモジュールを表す、のモジュールオブジェクトへのポインター。  
  
 `pSymbolStream`  
 から変更されたシンボルを格納している Win32 COM オブジェクトへのポインター `IStream` 。  
  
## <a name="remarks"></a>解説  
 このメソッドは、 [ISymUnmanagedReader::::](../diagnostics/isymunmanagedreader-updatesymbolstore-method.md) ISymUnmanagedReader [:::: 置き換え esyman store](../diagnostics/isymunmanagedreader-replacesymbolstore-method.md)を呼び出すことによって、モジュールのシンボルのデバッガービューを更新する機会を提供します。  
  
 このコールバックは、同じモジュールに対して複数回発生する可能性があります。  
  
 デバッガーは、バインドされていないソースレベルのブレークポイントをバインドしようとします。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [ICorDebugManagedCallback インターフェイス](icordebugmanagedcallback-interface.md)
