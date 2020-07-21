---
title: ICorRuntimeHost インターフェイス
ms.date: 03/30/2017
api_name:
- ICorRuntimeHost
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICorRuntimeHost
helpviewer_keywords:
- ICorRuntimeHost interface [.NET Framework hosting]
ms.assetid: 4369533d-7834-4497-bc37-bfea0ad737b1
topic_type:
- apiref
ms.openlocfilehash: 4b8018bb84dea08987d91f351b1ab0d9f3b48c56
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84503901"
---
# <a name="icorruntimehost-interface"></a>ICorRuntimeHost インターフェイス
ホストが共通言語ランタイム (CLR) を明示的に開始および停止し、アプリケーションドメインの作成と構成、既定のドメインへのアクセス、およびプロセスで実行されているすべてのドメインの列挙を行うことができるようにするメソッドを提供します。  
  
 .NET Framework バージョン2.0 では、このインターフェイスは[ICLRRuntimeHost](iclrruntimehost-interface.md)によって置き換えられます。  
  
## <a name="methods"></a>メソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[CloseEnum メソッド](icorruntimehost-closeenum-method.md)|ドメイン列挙子をドメインリストの先頭にリセットします。|  
|[CreateDomain メソッド](icorruntimehost-createdomain-method.md)|アプリケーションドメインを作成します。 呼び出し元は、型のインターフェイスポインターを <xref:System._AppDomain> 型のインスタンスに受信し <xref:System.AppDomain?displayProperty=nameWithType> ます。|  
|[CreateDomainEx メソッド](icorruntimehost-createdomainex-method.md)|アプリケーションドメインを作成します。 このメソッドを使用すると、呼び出し元は IAppDomainSetup インスタンスを渡して、返されたインスタンスの追加の機能を構成でき <xref:System._AppDomain> ます。|  
|[CreateDomainSetup メソッド](icorruntimehost-createdomainsetup-method.md)|インスタンスへの型のインターフェイスポインターを取得し `IAppDomainSetup` <xref:System.AppDomainSetup> ます。 `IAppDomainSetup`アプリケーションドメインを作成する前に構成するためのメソッドを提供します。|  
|[CreateEvidence メソッド](icorruntimehost-createevidence-method.md)|型のインターフェイスポインターを取得します <xref:System.Security.Principal.IIdentity> 。これにより、ホストは、 [createdomain](icorruntimehost-createdomain-method.md)または[createdomainex](icorruntimehost-createdomainex-method.md)に渡すセキュリティ証拠を作成できます。|  
|[CreateLogicalThreadState メソッド](icorruntimehost-createlogicalthreadstate-method.md)|使用しないでください。|  
|[CurrentDomain メソッド](icorruntimehost-currentdomain-method.md)|<xref:System._AppDomain>現在のスレッドに読み込まれているドメインを表す型のインターフェイスポインターを取得します。|  
|[DeleteLogicalThreadState メソッド](icorruntimehost-deletelogicalthreadstate-method.md)|使用しないでください。|  
|[EnumDomains メソッド](icorruntimehost-enumdomains-method.md)|現在のプロセス内のドメインの列挙子を取得します。|  
|[GetConfiguration メソッド](icorruntimehost-getconfiguration-method.md)|ホストが CLR のコールバック構成を指定できるようにするオブジェクトを取得します。|  
|[GetDefaultDomain メソッド](icorruntimehost-getdefaultdomain-method.md)|<xref:System._AppDomain>現在のプロセスの既定のドメインを表す型のインターフェイスポインターを取得します。|  
|[LocksHeldByLogicalThread メソッド](icorruntimehost-locksheldbylogicalthread-method.md)|使用しないでください。|  
|[MapFile メソッド](icorruntimehost-mapfile-method.md)|指定されたファイルをメモリにマップします。 このメソッドは、互換性のために残されています。|  
|[NextDomain メソッド](icorruntimehost-nextdomain-method.md)|列挙体の次のドメインへのインターフェイスポインターを取得します。|  
|[Start メソッド](icorruntimehost-start-method.md)|CLR を開始します。|  
|[Stop メソッド](icorruntimehost-stop-method.md)|現在のプロセスのランタイムでコードの実行を停止します。|  
|[SwitchInLogicalThreadState メソッド](icorruntimehost-switchinlogicalthreadstate-method.md)|使用しないでください。|  
|[SwitchOutLogicalThreadState メソッド](icorruntimehost-switchoutlogicalthreadstate-method.md)|使用しないでください。|  
|[UnloadDomain メソッド](icorruntimehost-unloaddomain-method.md)|現在のプロセスから、指定されたアプリケーションドメインをアンロードします。|  
  
## <a name="requirements"></a>要件  
 **:**「[システム要件](../../get-started/system-requirements.md)」を参照してください。  
  
 **ヘッダー:** Mscoree.dll  
  
 **ライブラリ:** Mscoree.dll にリソースとして含まれています  
  
 **.NET Framework のバージョン:** 1.0、1.1  
  
## <a name="see-also"></a>関連項目

- <xref:System.AppDomain>
- [ホスティング](index.md)
- [ICLRRuntimeHost インターフェイス](iclrruntimehost-interface.md)
- [ランタイム ホスト](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/a51xd4ze(v=vs.100))
- [ホスト インターフェイス](hosting-interfaces.md)
- [CorRuntimeHost コクラス](corruntimehost-coclass.md)
