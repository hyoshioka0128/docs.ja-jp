---
title: ICorDebugAppDomain インターフェイス
ms.date: 03/30/2017
api_name:
- ICorDebugAppDomain
api_location:
- corguids.lib
api_type:
- COM
f1_keywords:
- ICorDebugAppDomain
helpviewer_keywords:
- ICorDebugAppDomain interface [.NET Framework debugging]
ms.assetid: be7ae711-1217-4a44-be40-166e29641b77
topic_type:
- apiref
ms.openlocfilehash: 140e67417f4fad552f972a93bc8c620b440b2370
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895170"
---
# <a name="icordebugappdomain-interface"></a>ICorDebugAppDomain インターフェイス

アプリケーション ドメインをデバッグするためのメソッドを提供します。 このインターフェイスは、というコントロールのサブクラスです。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[Attach メソッド](icordebugappdomain-attach-method.md)|デバッガーをアプリケーションドメインにアタッチします。|  
|[EnumerateAssemblies メソッド](icordebugappdomain-enumerateassemblies-method.md)|アプリケーションドメイン内のアセンブリの列挙子を取得します。|  
|[EnumerateBreakpoints メソッド](icordebugappdomain-enumeratebreakpoints-method.md)|アプリケーションドメイン内のすべてのアクティブなブレークポイントの列挙子を取得します。|  
|[EnumerateSteppers メソッド](icordebugappdomain-enumeratesteppers-method.md)|アプリケーションドメイン内のすべてのアクティブな steppers の列挙子を取得します。|  
|[GetId メソッド](icordebugappdomain-getid-method.md)|アプリケーションドメインの一意の ID を取得します。|  
|[GetModuleFromMetaDataInterface メソッド](icordebugappdomain-getmodulefrommetadatainterface-method.md)|指定されたメタデータインターフェイスを持つ、のモジュールオブジェクトを取得します。|  
|[GetName メソッド](icordebugappdomain-getname-method.md)|アプリケーションドメインの名前を取得します。|  
|[GetObject メソッド](icordebugappdomain-getobject-method.md)|共通言語ランタイム (CLR) アプリケーションドメインへのインターフェイスポインターを取得します。|  
|[GetProcess メソッド](icordebugappdomain-getprocess-method.md)|アプリケーションドメインを格納しているプロセスを取得します。|  
|[IsAttached メソッド](icordebugappdomain-isattached-method.md)|デバッガーがアプリケーションドメインにアタッチされているかどうかを判断します。|  
  
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
