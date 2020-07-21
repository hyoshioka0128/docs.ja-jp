---
title: 構成 (インターネット アプリケーションを)
description: .NET Framework で <system.Net> 要素を使用して、インターネット アプリケーションを構成する方法について学習します。 この記事にはコード例が含まれます。
ms.date: 03/30/2017
helpviewer_keywords:
- downloading Internet resources, default proxy
- sending data, default proxy
- receiving data, default proxy
- downloading Internet resources, configuring Internet applications
- protocol-specific modules
- custom authentication modules
- receiving data, configuring Internet applications
- configuration settings [.NET Framework], Internet applications
- requesting data from Internet, configuring Internet applications
- requesting data from Internet, default proxy
- response to Internet request, default proxy
- Internet, configuring Internet applications
- response to Internet request, configuring Internet applications
- default proxy
- network resources, default proxy
- sending data, configuring Internet applications
- network resources, configuring Internet applications
- Internet, default proxy
ms.assetid: bb707c72-eed2-4a82-8800-c9e68df2fd4f
ms.openlocfilehash: 760a4ac7cec9abeabfc372c3be5bd3860a6fb03a
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502640"
---
# <a name="configuring-internet-applications"></a>構成 (インターネット アプリケーションを)
[\<system.Net> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/system-net-element-network-settings.md) 構成要素には、アプリケーションのネットワーク構成情報が含まれています。 [\<system.Net> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/system-net-element-network-settings.md) 要素を使用すると、プロキシ サーバーを設定し、接続管理パラメーターを設定し、カスタム認証および要求モジュールをアプリケーションに含めることができます。  
  
 [\<defaultProxy> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/defaultproxy-element-network-settings.md) 要素は、`GlobalProxySelection` クラスによって返されるプロキシ サーバーを定義します。 独自の <xref:System.Net.HttpWebRequest.Proxy%2A> プロパティが特定の値に設定されていない <xref:System.Net.HttpWebRequest> はすべて、既定のプロキシを使用します。 プロキシ アドレスを設定するだけでなく、プロキシを使用しないサーバー アドレスの一覧を作成し、ローカル アドレスにプロキシを使用しないように指定できます。  
  
 Microsoft Internet Explorer の設定は構成の設定と組み合わせて使用され、構成の設定が優先されることに注意してください。  
  
 次の例では、既定のプロキシ サーバー アドレスを `http://proxyserver` に設定し、ローカル アドレスにプロキシを使用しないようにし、contoso.com ドメインにあるサーバーへのすべての要求でプロキシをバイパスするように指定しています。  
  
```xml  
<configuration>  
    <system.net>  
        <defaultProxy>  
            <proxy  
                usesystemdefault = "false"  
                proxyaddress = "http://proxyserver:80"  
                bypassonlocal = "true"  
            />  
            <bypasslist>  
                <add address="http://[a-z]+\.contoso\.com/" />  
            </bypasslist>  
        </defaultProxy>  
    </system.net>  
</configuration>  
```  
  
 特定のサーバーまたは他のすべてのサーバーに対して行うことができる持続接続の数を構成するには、[\<connectionManagement> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/connectionmanagement-element-network-settings.md) 要素を使用します。 次の例では、サーバー `www.contoso.com` への 2 つの持続接続、IP アドレス 192.168.1.2 を持つサーバーへの 4 つの持続接続、および他のすべてのサーバーへの 1 つの持続接続が使用されるようにアプリケーションを構成します。  
  
```xml  
<configuration>  
    <system.net>  
        <connectionManagement>  
            <add address="http://www.contoso.com" maxconnection="2" />  
            <add address="192.168.1.2" maxconnection="4" />  
            <add address="*" maxconnection="1" />  
        </connectionManagement>  
    </system.net>  
</configuration>  
```  
  
 カスタム認証モジュールは、[\<authenticationModules> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/authenticationmodules-element-network-settings.md) 要素で構成されます。 カスタム認証モジュールは <xref:System.Net.IAuthenticationModule> インターフェイスを実装する必要があります。  
  
 次の例では、カスタム認証モジュールを構成します。  
  
```xml  
<configuration>  
    <system.net>  
        <authenticationModules>  
            <add type="MyAuthModule, MyAuthModule.dll" />  
        </authenticationModules>  
    </system.net>  
</configuration>  
```  
  
 [\<webRequestModules> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/webrequestmodules-element-network-settings.md) 要素を使用し、カスタム プロトコル固有のモジュールを使用してインターネット リソースから情報を要求するように、アプリケーションを構成することができます。 指定されたモジュールは <xref:System.Net.IWebRequestCreate> インターフェイスを実装する必要があります。 既定の HTTP、HTTPS、およびファイル要求モジュールは、次の例のように、構成ファイルでカスタム モジュールを指定してオーバーライドすることができます。  
  
```xml  
<configuration>  
    <system.net>  
        <webRequestModules>  
            <add  
                prefix="HTTP"  
                type = "MyHttpRequest.dll, MyHttpRequestCreator"  
            />  
        </webRequestModules>  
    </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [.NET Framework のネットワーク プログラミング](index.md)
- [ネットワーク設定スキーマ](../configure-apps/file-schema/network/index.md)
- [\<system.Net> 要素 (ネットワーク設定)](../configure-apps/file-schema/network/system-net-element-network-settings.md)
