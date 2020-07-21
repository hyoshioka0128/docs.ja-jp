---
title: <httpWebRequest> 要素 (ネットワーク設定)
description: <httpWebRequest>ネットワーク設定要素は、.NET Framework 内の Web 要求パラメーターをカスタマイズします。
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: 59ab425dcef8ac5283035910a9d78a89a16be8b1
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/08/2020
ms.locfileid: "84504590"
---
# <a name="httpwebrequest-element-network-settings"></a>\<httpWebRequest> 要素 (ネットワーク設定)
Web 要求パラメーターをカスタマイズします。  

[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.net>**](system-net-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<settings>**](settings-element-network-settings.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<httpWebRequest>**

## <a name="syntax"></a>構文  
  
```xml  
<httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**属性**|**説明**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|応答ヘッダーの最大長を kb 単位で指定します。 既定値は、64 です。 値が-1 の場合は、応答ヘッダーにサイズ制限が適用されないことを示します。|  
|`maximumErrorResponseLength`|エラー応答の最大長を kb 単位で指定します。 既定値は、64 です。 値が-1 の場合は、エラー応答にサイズ制限が適用されないことを示します。|  
|`maximumUnauthorizedUploadLength`|未承認のエラーコードへの応答としてのアップロードの最大長をバイト単位で指定します。 既定値は -1 です。 値 -1 は、アップロード情報にサイズ制限が適用されないことを示します。|  
|`useUnsafeHeaderParsing`|Unsafe ヘッダーの解析が有効かどうかを指定します。 既定値は `false` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[設定](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>解説  
 既定では、.NET Framework は URI 解析に RFC 2616 を厳密に適用します。 一部のサーバー応答には、禁止されたフィールドの制御文字が含まれる場合があります。これにより、 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> メソッドはをスローし <xref:System.Net.WebException> ます。 **Useunsafeheaderparsing**が**true**に設定されている場合、 <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> はこの場合にをスローしません。ただし、アプリケーションは、いくつかの形式の URI 解析攻撃に対して脆弱になります。 最適な解決策は、応答に制御文字が含まれないようにサーバーを変更することです。  
  
## <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
 次の例は、通常の最大ヘッダー長より大きいを指定する方法を示しています。  
  
```xml  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>
- [ネットワーク設定スキーマ](index.md)
