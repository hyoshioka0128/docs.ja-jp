---
title: ICLRDebuggingLibraryProvider インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRDebuggingLibraryProvider
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDebuggingLibraryProvider
helpviewer_keywords:
- ICLRDebuggingLibraryProvider interface [.NET Framework debugging]
ms.assetid: 67739617-6add-41a9-9de5-a3200c3109ce
topic_type:
- apiref
ms.openlocfilehash: 77c2011ce677d1bd2823d47740782f48151b408a
ms.sourcegitcommit: d9c7ac5d06735a01c1fafe34efe9486734841a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82860284"
---
# <a name="iclrdebugginglibraryprovider-interface"></a>ICLRDebuggingLibraryProvider インターフェイス
には、提供[ライブラリのメソッド](iclrdebugginglibraryprovider-providelibrary-method.md)メソッドが含まれています。このメソッドは、共通言語ランタイムのバージョン固有のデバッグライブラリをオンデマンドで検索して読み込むことができるようにする、ライブラリプロバイダーのコールバックインターフェイスを取得します。  
  
## <a name="methods"></a>メソッド  
  
|Method|説明|  
|------------|-----------------|  
|[ProvideLibrary メソッド](iclrdebugginglibraryprovider-providelibrary-method.md)|デバッガーが、デバッグライブラリの読み込みに使用できるモジュールへのハンドルを提供できるようにします。|  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
- [デバッグ](index.md)
