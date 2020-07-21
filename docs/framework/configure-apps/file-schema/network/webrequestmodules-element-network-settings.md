---
title: <webRequestModules> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/webRequestModules
- http://schemas.microsoft.com/.NetConfiguration/v2.0#webRequestModules
helpviewer_keywords:
- webRequestModules element
- <webRequestModules> element
ms.assetid: 1263de11-3e0a-4f94-97c9-710b2ae53817
ms.openlocfilehash: 7f2805283f89e6165d336b3e593d34054e02115d
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "79154544"
---
# <a name="webrequestmodules-element-network-settings"></a>\<webRequestModules> 要素 (ネットワーク設定)
ネットワークホストから情報を要求するために使用するモジュールを指定します。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)  
&nbsp;&nbsp;&nbsp;&nbsp;\<webRequestModules>  
  
## <a name="syntax"></a>構文  
  
```xml  
<webRequestModules>
</webRequestModules>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[add](add-element-for-webrequestmodules-network-settings.md)|アプリケーションにカスタム Web 要求モジュールを追加します。|  
|[オフ](clear-element-for-webrequestmodules-network-settings.md)|アプリケーションから、登録されているすべての Web 要求モジュールを削除します。|  
|[remove](remove-element-for-webrequestmodules-network-settings.md)|アプリケーションからカスタム Web 要求モジュールを削除します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[system.net](system-net-element-network-settings.md)|.NET Framework がネットワークに接続する方法を指定するための設定が含まれています。|  
  
## <a name="remarks"></a>解説  
 要素は、 `webRequestModules` <xref:System.Net.WebRequest> ネットワークホストに対する情報要求を処理するために、クラスの子孫を登録します。 Web 要求モジュールは、インターフェイスを実装する必要があり <xref:System.Net.IWebRequestCreate> ます。  
  
 .NET Framework には、、、およびで始まる Uri の Web 要求モジュールが含まれてい `http://` `https://` `file://` ます。 既定のモジュールをオーバーライドするには、構成ファイルにカスタムモジュールを登録する必要があります。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、既定の HTTP モジュールを登録します。 Version および PublicKeyToken の値は、指定されたモジュールの正しい値に置き換える必要があります。  
  
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
- <xref:System.Net.IWebRequestCreate>
- [ネットワーク設定スキーマ](index.md)
