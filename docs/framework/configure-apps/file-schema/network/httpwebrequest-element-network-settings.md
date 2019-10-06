---
title: <httpWebRequest> 要素 (ネットワーク設定)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest
- http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest
helpviewer_keywords:
- <httpWebRequest> element
- httpWebRequest element
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
ms.openlocfilehash: fa00aed2cd1e96ec788d4bc9c1c63f20561d8d1c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71698184"
---
# <a name="httpwebrequest-element-network-settings"></a>\<httpWebRequest > 要素 (ネットワーク設定)
Web 要求パラメーターをカスタマイズします。  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t 47 >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t @ no__t @no__t @ no__t-3[ **-6 設定 >** ](settings-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t @ no__t @ no__t-5 **\<httpWebRequest >** を行います。  
  
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
  
|**属性**|**[説明]**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|応答ヘッダーの最大長を kb 単位で指定します。 既定値は 64 です。 値が-1 の場合は、応答ヘッダーにサイズ制限が適用されないことを示します。|  
|`maximumErrorResponseLength`|エラー応答の最大長を kb 単位で指定します。 既定値は 64 です。 値が-1 の場合は、エラー応答にサイズ制限が適用されないことを示します。|  
|`maximumUnauthorizedUploadLength`|未承認のエラーコードへの応答としてのアップロードの最大長をバイト単位で指定します。 既定値は -1 です。 値-1 は、アップロード時にサイズ制限が適用されないことを示します。|  
|`useUnsafeHeaderParsing`|Unsafe ヘッダーの解析が有効かどうかを指定します。 既定値は `false` です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**[説明]**|  
|-----------------|---------------------|  
|[settings](settings-element-network-settings.md)|<xref:System.Net> 名前空間の基本的なネットワーク オプションを構成します。|  
  
## <a name="remarks"></a>コメント  
 既定では、.NET Framework は URI 解析に RFC 2616 を厳密に適用します。 一部のサーバー応答には、禁止されたフィールドの制御文字が含まれる場合があります。これにより、<xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> のメソッドが <xref:System.Net.WebException> をスローします。 **Useunsafeheaderparsing 解析**が**true**に設定されている場合、<xref:System.Net.HttpWebRequest.GetResponse?displayProperty=nameWithType> は、この場合はをスローしません。ただし、アプリケーションは、いくつかの形式の URI 解析攻撃に対して脆弱になります。 最適な解決策は、応答に制御文字が含まれないようにサーバーを変更することです。  
  
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
