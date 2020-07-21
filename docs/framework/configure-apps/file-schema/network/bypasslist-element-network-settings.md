---
title: <bypasslist> 要素 (ネットワーク設定)
description: <bypasslist>ネットワーク設定要素は、.NET Framework でプロキシを使用しないアドレスを記述する一連の正規表現を提供します。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#bypasslist
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist
helpviewer_keywords:
- bypasslist element
- <bypasslist> element
ms.assetid: 124446b7-abb1-4e5e-a492-b64398f268f1
ms.openlocfilehash: 42b6ddf4c3d09bcf8ef0ada105cefedccc63b505
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504629"
---
# <a name="bypasslist-element-network-settings"></a>\<bypasslist> 要素 (ネットワーク設定)
プロキシを使用しないアドレスを記述する一連の正規表現を提供します。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<defaultProxy>**](defaultproxy-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<bypasslist>**

## <a name="syntax"></a>構文  
  
```xml  
<bypasslist>
</bypasslist>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[add](add-element-for-bypasslist-network-settings.md)|プロキシバイパス一覧に IP アドレスまたは DNS 名を追加します。|  
|[オフ](clear-element-for-bypasslist-network-settings.md)|バイパスリストをクリアします。|  
|[remove](remove-element-for-bypasslist-network-settings.md)|プロキシバイパスリストから IP アドレスまたは DNS 名を削除します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[defaultProxy](defaultproxy-element-network-settings.md)|ハイパーテキスト転送プロトコル (HTTP: Hypertext Transfer Protocol) プロキシ サーバーを構成します。|  
  
## <a name="remarks"></a>解説  
 バイパスリストには、 <xref:System.Net.WebRequest> インスタンスがプロキシサーバー経由ではなく直接アクセスする uri を記述する正規表現が含まれています。  
  
 この要素に正規表現を指定する場合は、注意が必要です。 正規表現 "[a-z] + \\ . contoso \\ .com" は、contoso.com ドメイン内の任意のホストと一致しますが、contoso.com.cpandl.com ドメイン内の任意のホストとも一致します。 Contoso.com ドメイン内のホストのみを一致させるには、アンカー ("$"): "[a-z] + \\ . contoso \\ .com $" を使用します。  
  
 正規表現の詳細については、「」を参照してください。[正規表現を .NET Framework](../../../../standard/base-types/regular-expressions.md)します。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例では、バイパスリストに2つのアドレスを追加します。 最初のは、contoso.com ドメイン内のすべてのサーバーのプロキシをバイパスします。2つ目は、IP アドレスが192.168 で始まるすべてのサーバーのプロキシをバイパスします。  
  
```xml  
<configuration>  
  <system.net>  
    <defaultProxy>  
      <bypasslist>  
        <add address="[a-z]+\.contoso\.com$" />  
        <add address="192\.168\.\d{1,3}\.\d{1,3}" />  
      </bypasslist>  
    </defaultProxy>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](index.md)
