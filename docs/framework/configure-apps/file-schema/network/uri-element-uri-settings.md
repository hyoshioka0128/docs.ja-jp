---
title: <uri> 要素 (Uri 設定)
ms.date: 03/30/2017
ms.assetid: c22bab8b-477c-4ae4-8498-65ad409e0847
ms.openlocfilehash: a492baf9951466383ca0277a2927b8554e5bb332
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "71697438"
---
# <a name="uri-element-uri-settings"></a>\<uri> 要素 (Uri 設定)
.NET Framework が、uniform resource identifier (Uri) を使用して表された web アドレスを処理する方法を指定する設定が含まれます。  
  
[**\<configuration>**](../configuration-element.md)  
&nbsp;&nbsp;**\<uri>**  
  
## <a name="syntax"></a>構文  
  
```xml  
<uri>  
</uri>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[idn](idn-element-uri-settings.md)|国際化ドメイン名 (IDN) の解析がドメイン名に適用されるかどうかを指定します。|  
|[Iriparsing>](iriparsing-element-uri-settings.md)|国際化リソース識別子 (IRI) の解析を適用する <xref:System.Uri> かどうか、および iri 解析規則を適用するかどうかを指定します。|  
|[schemeSettings](schemesettings-element-uri-settings.md)|<xref:System.Uri> が特定のスキームに解析される方法を指定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[configuration](../configuration-element.md)|すべての名前空間の設定が含まれます。|  
  
## <a name="remarks"></a>解説  
 要素には、 `uri` <xref:System.Uri> 名前空間のクラスによって使用されるクラスのメンバーの設定が含まれ <xref:System.Net> ます。 この設定により、IRI と IDN のサポートが構成されます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、 <xref:System.Uri> IRI 解析と IDN 名をサポートするためにクラスによって使用される構成を示しています。 また、この例では、すべてのスキーム設定をクリアした後、http スキームに対してパーセントでエンコードされたパス区切り記号をエスケープしないためのサポートを追加します。  
  
### <a name="code"></a>コード  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
    <schemeSettings>  
      <clear/>  
      <add name="http" genericUriParserOptions="DontUnescapePathDotsAndSlashes"/>  
    </schemeSettings>  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- [ネットワーク設定スキーマ](index.md)
