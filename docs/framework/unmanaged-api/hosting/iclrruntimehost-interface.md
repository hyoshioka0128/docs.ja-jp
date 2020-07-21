---
title: ICLRRuntimeHost インターフェイス
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost
helpviewer_keywords:
- ICLRRuntimeHost interface [.NET Framework hosting]
ms.assetid: cb0c5f65-3791-47bc-b833-2f84f4101ba5
topic_type:
- apiref
ms.openlocfilehash: 72caac0aafe7f9c5919057a6ad2565258aec6a50
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504083"
---
# <a name="iclrruntimehost-interface"></a>ICLRRuntimeHost インターフェイス
.NET Framework バージョン1で提供される[ICorRuntimeHost](icorruntimehost-interface.md)インターフェイスと同様の機能を提供します。次の変更点があります。  
  
- ホストコントロールインターフェイスを設定するための[Sethostcontrol](iclrruntimehost-sethostcontrol-method.md)メソッドの追加。  
  
- によって提供されるいくつかのメソッドの省略 `ICorRuntimeHost` 。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[ExecuteApplication メソッド](iclrruntimehost-executeapplication-method.md)|新しいドメインでアクティブ化するアプリケーションを指定するために、マニフェストベースの ClickOnce 配置シナリオで使用されます。|  
|[ExecuteInAppDomain メソッド](iclrruntimehost-executeinappdomain-method.md)|指定し <xref:System.AppDomain> たマネージコードを実行するを指定します。|  
|[ExecuteInDefaultAppDomain メソッド](iclrruntimehost-executeindefaultappdomain-method.md)|指定したアセンブリ内で、指定した型の指定したメソッドを呼び出します。|  
|[GetCLRControl メソッド](iclrruntimehost-getclrcontrol-method.md)|ホストが共通言語ランタイム (CLR) の側面をカスタマイズするために使用できる、 [ICLRControl](iclrcontrol-interface.md)型のインターフェイスポインターを取得します。|  
|[GetCurrentAppDomainId メソッド](iclrruntimehost-getcurrentappdomainid-method.md)|現在実行中のの数値識別子を取得し <xref:System.AppDomain> ます。|  
|[SetHostControl メソッド](iclrruntimehost-sethostcontrol-method.md)|ホストコントロールインターフェイスを設定します。 を呼び出す前に、を呼び出す必要があり `SetHostControl` `Start` ます。|  
|[Start メソッド](iclrruntimehost-start-method.md)|CLR をプロセスに初期化します。|  
|[Stop メソッド](iclrruntimehost-stop-method.md)|ランタイムによるコードの実行を停止します。|  
|[UnloadAppDomain メソッド](iclrruntimehost-unloadappdomain-method.md)|指定した <xref:System.AppDomain> 数値識別子に対応するをアンロードします。|  
  
## <a name="remarks"></a>解説  
 .NET Framework 4 以降では、 [ICLRMetaHost](iclrmetahost-interface.md)インターフェイスを使用して[ICLRRuntimeInfo](iclrruntimeinfo-interface.md)インターフェイスへのポインターを取得し、 [ICLRRuntimeInfo:: getinterface](iclrruntimeinfo-getinterface-method.md)メソッドを呼び出して、へのポインターを取得し `ICLRRuntimeHost` ます。 以前のバージョンの .NET Framework では、ホストは `ICLRRuntimeHost` [Corbindtoruntimeex](corbindtoruntimeex-function.md)または[Corbindtoの entruntime](corbindtocurrentruntime-function.md)を呼び出すことによって、インスタンスへのポインターを取得します。 .NET Framework バージョン2.0 で提供されるテクノロジの実装を提供するには、の代わりにを使用する必要があり `ICLRRuntimeHost` `ICorRuntimeHost` ます。  
  
> [!IMPORTANT]
> マニフェストベースのアプリケーションをアクティブ化するには、 [Executeapplication](iclrruntimehost-executeapplication-method.md)メソッドを呼び出す前に[Start](iclrruntimehost-start-method.md)メソッドを呼び出さないでください。 `Start`メソッドが最初に呼び出された場合、 `ExecuteApplication` メソッドの呼び出しは失敗します。  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>関連項目

- [CorBindToCurrentRuntime 関数](corbindtocurrentruntime-function.md)
- [CorBindToRuntimeEx 関数](corbindtoruntimeex-function.md)
- [ICLRControl インターフェイス](iclrcontrol-interface.md)
- [ICorRuntimeHost インターフェイス](icorruntimehost-interface.md)
- [ホスト インターフェイス](hosting-interfaces.md)
- [CLRRuntimeHost コクラス](clrruntimehost-coclass.md)
