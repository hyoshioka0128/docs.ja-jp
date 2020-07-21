---
title: ICorDebugAssembly インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugAssembly
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugAssembly
helpviewer_keywords:
- ICorDebugAssembly interface [.NET Framework debugging]
ms.assetid: 9d657a28-6984-4c5e-8a54-89d20080baff
topic_type:
- apiref
ms.openlocfilehash: d9e2236b944137de82bb056820f81014febfcc5f
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82894894"
---
# <a name="icordebugassembly-interface"></a>ICorDebugAssembly インターフェイス

アセンブリを表します。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[EnumerateModules メソッド](icordebugassembly-enumeratemodules-method.md)|アセンブリに格納されているモジュールの列挙子を取得します。|  
|[GetAppDomain メソッド](icordebugassembly-getappdomain-method.md)|この`ICorDebugAssembly`インスタンスを含むアプリケーションドメインへのインターフェイスポインターを取得します。|  
|[GetCodeBase メソッド](icordebugassembly-getcodebase-method.md)|.NET Framework の現在のバージョンでは実装されていません。|  
|[GetName メソッド](icordebugassembly-getname-method.md)|アセンブリの名前を取得します。|  
|[GetProcess メソッド](icordebugassembly-getprocess-method.md)|アセンブリが実行されている、のプロセスインスタンスを取得します。|  
  
## <a name="remarks"></a>解説  
  
> [!NOTE]
> このインターフェイスは、コンピューター間またはプロセス間でのリモート呼び出しをサポートしていません。  
  
## <a name="requirements"></a>必要条件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** CorDebug.idl、CorDebug.h  
  
 **ライブラリ:** CorGuids.lib  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [デバッグのインターフェイス](debugging-interfaces.md)
