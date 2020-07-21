---
title: connectionManagement の <add> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/connectionManagement/add
helpviewer_keywords:
- <add> element, connectionManagement
- <connectionManagement>, add element
- add element, connectionManagement
- connectionManagement, add element
ms.assetid: 856bf57d-1c63-46c7-a178-03d97b0a4149
ms.openlocfilehash: 093b68d31e03094bedefa96a2f2d53eb3d84edf0
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155012"
---
# <a name="add-element-for-connectionmanagement-network-settings"></a>connectionManagement の \<add> 要素 (ネットワーク設定)
IP アドレスまたは DNS 名を接続管理リストに追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<connectionManagement>**](connectionmanagement-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文  
  
```xml  
<add
  address="address expression"
  maxconnection="integer"
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`address`|IP アドレスまたは DNS 名を記述する文字列。|  
|`maxconnection`|サーバーに対して許可される接続の最大数。 値が指定されていない場合、既定値は 2 です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[connectionManagement](connectionmanagement-element-network-settings.md)|ネットワーク ホストへの接続の最大数を指定します。|  
  
## <a name="remarks"></a>解説  
 `address` 属性の値は、すべての接続を示すアスタリスク、または形式が `<schema>://<idn_hostname>[:<port>]` の文字列である必要があります。  
  
 HTTP API に渡される URI に Unicode が含まれる場合、punicode 文字列を返す可能性がある <xref:System.Uri.DnsSafeHost%2A> を使用して名前が内部的に変換されます (動作は現行 IDN 構成によって異なる)。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、サーバーへの4つの接続 `www.contoso.com` と、他のすべてのサーバーへの2つの接続を使用するようにアプリケーションを構成します。  
  
```xml  
<configuration>  
  <system.net>  
    <connectionManagement>  
      <add address="http://www.contoso.com" maxconnection="4" />  
      <add address="*" maxconnection="2" />  
    </connectionManagement>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.ServicePoint>
- <xref:System.Net.ServicePointManager>
- [ネットワーク設定スキーマ](index.md)
