---
title: <system.Net> 要素 (ネットワーク設定)
description: <system.Net> network settings 要素には、.NET Framework が .NET Framework のネットワークオプションに接続する方法を指定する設定が含まれています。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#system.Net
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.Net
helpviewer_keywords:
- system.Net element
- <system.Net> element
ms.assetid: 52de4d6c-b24d-44aa-ba7d-6b5061f1357e
ms.openlocfilehash: 9f18c7a3586948c03391d609f437e216a91bc27f
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504486"
---
# <a name="systemnet-element-network-settings"></a>\<system.Net> 要素 (ネットワーク設定)
.NET Framework がネットワークに接続する方法を指定するための設定が含まれています。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;**\<system.net>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<system.net>
</system.net>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[authenticationModules](authenticationmodules-element-network-settings.md)|インターネット要求を認証するために使用するモジュールを指定します。|  
|[connectionManagement](connectionmanagement-element-network-settings.md)|インターネットホストへの接続の最大数を指定します。|  
|[defaultProxy](defaultproxy-element-network-settings.md)|ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。|  
|[mailSettings](mailsettings-element-network-settings.md)|SMTP (Simple Mail Transport Protocol) メール送信オプションを構成します。|  
|[Requestcaching>](requestcaching-element-network-settings.md)|ネットワーク要求のキャッシュメカニズムを制御します。|  
|[設定](settings-element-network-settings.md)|および関連する子名前空間のクラスの基本的なネットワークオプションを構成し <xref:System.Net> ます。|  
|[webRequestModules](webrequestmodules-element-network-settings.md)|インターネットホストから情報を要求するために使用するモジュールを指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[configuration](../configuration-element.md)|すべての名前空間の設定が含まれます。|  
  
## <a name="remarks"></a>解説  
 [\<system.net>](system-net-element-network-settings.md)要素には、 <xref:System.Net> および関連する子名前空間のクラスの設定が含まれます。 この設定では、インターネットホストから情報を受信するための認証モジュール、接続管理、メール設定、プロキシサーバー、およびインターネット要求モジュールを構成します。  
  
## <a name="example"></a>例  
 次の例は、クラスによって使用される一般的な構成を示して <xref:System.Net> います。  
  
```xml  
<configuration>  
  <system.net>  
    <authenticationModules>  
      <add type="System.Net.DigestClient" />  
      <add type="System.Net.NegotiateClient" />  
      <add type="System.Net.KerberosClient" />  
      <add type="System.Net.NtlmClient" />  
      <add type="System.Net.BasicClient" />  
    </authenticationModules>  
    <connectionManagement>  
      <add address="*" maxconnection="2" />  
    </connectionManagement>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="true"  
        bypassonlocal="true"  
      />  
    </defaultProxy>  
    <webRequestModules>  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator"  
      />  
      <add prefix="https"  
           type="System.Net.HttpRequestCreator"  
      />  
      <add prefix="file"  
           type="System.Net.FileWebRequestCreator"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ネットワーク設定スキーマ](index.md)
