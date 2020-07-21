---
title: <defaultProxy> 要素 (ネットワーク設定)
description: <defaultProxy>ネットワーク設定要素は、.NET Framework でハイパーテキスト転送プロトコル (HTTP) プロキシサーバーを構成します。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#defaultProxy
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy
helpviewer_keywords:
- defaultProxy element
- <defaultProxy> element
ms.assetid: 9d663c4b-07b4-4f6f-9b12-efbd3630354f
ms.openlocfilehash: 85004d49ce7605b050709a3019592ec696a7bada
ms.sourcegitcommit: 6219b1e1feccb16d88656444210fed3297f5611e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2020
ms.locfileid: "85141632"
---
# <a name="defaultproxy-element-network-settings"></a>\<defaultProxy> 要素 (ネットワーク設定)
ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;**\<defaultProxy>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<defaultProxy  
  enabled="True|False"  
  useDefaultCredentials="True|False">  
    <bypasslist>...</bypasslist>  
    <proxy>...</proxy>  
    <module>...</module>  
</defaultProxy>
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|`enabled`|Web プロキシが使用されているかどうかを指定します。 既定値は `True` です。|  
|`useDefaultCredentials`|このホストに対する既定の資格情報が Web プロキシにアクセスするために使用されるかどうかを指定します。 既定値は `False` です。|  
  
### <a name="child-elements"></a>子要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[bypasslist](bypasslist-element-network-settings.md)|プロキシを使用しないアドレスを記述する一連の正規表現を提供します。|  
|[第](module-element-network-settings.md)|新しいプロキシ モジュールをアプリケーションに追加します。|  
|[rpcproxy](proxy-element-network-settings.md)|プロキシ サーバーを定義します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|.NET Framework がネットワークに接続する方法を指定するための設定が含まれています。|  
  
## <a name="remarks"></a>注釈  
 defaultProxy 要素が空の場合、Internet Explorer のプロキシ設定が使用されます。 この動作は、.NET Framework Version 1.1 とは異なります。  
  
 [モジュール](module-element-network-settings.md)要素で非パブリック型が指定されている場合、型がクラスから派生していない場合、 <xref:System.Net.IWebProxy> このオブジェクトのパラメーターなしのコンストラクターの例外が発生した場合、またはシステム指定の既定のプロキシを取得中に例外が発生した場合は、例外がスローされます。 例外の <xref:System.Exception.InnerException%2A> プロパティに、このエラーの根本原因に関する詳細情報が含まれています。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、Internet Explorer プロキシの既定値を使用して、プロキシアドレスを指定し、ローカルアクセスと contoso.com に対してプロキシをバイパスします。  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <proxy  
        usesystemdefault="True"  
        proxyaddress="http://192.168.1.10:3128"  
        bypassonlocal="True"  
      />  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
