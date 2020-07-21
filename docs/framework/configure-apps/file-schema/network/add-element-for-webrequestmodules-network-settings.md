---
title: webRequestModules の <add> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules/add
- http://schemas.microsoft.com/.NetConfiguration/v2.0#add
helpviewer_keywords:
- <webRequestModules>, add element
- webRequestModules, add element
- add element, webRequestModules
- <add> element, webRequestModules
ms.assetid: 47ec4adc-f39f-4bcd-8680-1ec21fd26890
ms.openlocfilehash: f4edce948033478aab59a2aff61abadc55a327ce
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79155025"
---
# <a name="add-element-for-webrequestmodules-network-settings"></a>webRequestModules の \<add> 要素 (ネットワーク設定)
アプリケーションにカスタム Web 要求モジュールを追加します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<webRequestModules>**](webrequestmodules-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<add>**

## <a name="syntax"></a>構文  
  
```xml  
<add
  prefix="URI prefix"
  type="type_fullname, assembly_fullname"
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`prefix`|この Web 要求モジュールによって処理される要求の URI プレフィックス。|  
|`type`|<xref:System.Type.FullName%2A> <xref:System.Reflection.Assembly.FullName%2A> この Web 要求モジュールを実装するコンマで区切られた、完全修飾型名 (プロパティによって示されます) とアセンブリ名 (プロパティによって示されます)。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[webRequestModules](webrequestmodules-element-network-settings.md)|ネットワークホストから情報を要求するために使用するモジュールを指定します。|  
  
## <a name="remarks"></a>解説  
 属性は、 `prefix` 指定された Web 要求モジュールを使用する URI プレフィックスを定義します。 通常、Web 要求モジュールは、HTTP や FTP などの特定のプロトコルを処理するように登録されますが、サーバー上の特定のサーバーまたはパスへの要求を処理するように登録できます。  
  
 Web 要求モジュールは、URI 照合プレフィックスがメソッドに渡されたときに作成され <xref:System.Net.WebRequest.Create%2A?displayProperty=nameWithType> ます。  
  
 属性の値は、 `prefix` 有効な URI の先頭の文字である必要があります。 たとえば、`http` または `http://www.contoso.com` です。
  
 属性の値は、 `type` 有効な型名と、それに対応するアセンブリ名をコンマで区切って指定する必要があります。
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、HTTP 用のカスタム Web 要求モジュールを登録します。 Version および PublicKeyToken の値は、指定されたモジュールの正しい値に置き換える必要があります。  
  
```xml  
<configuration>  
  <system.net>  
    <webRequestModules>  
      <add prefix="http"  
           type="System.Net.HttpRequestCreator, System, Version=2.0.3600.0,  
           Culture=neutral, PublicKeyToken=b77a5c561934e089"  
      />  
    </webRequestModules>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.WebRequest>
- [ネットワーク設定スキーマ](index.md)
