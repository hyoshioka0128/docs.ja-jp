---
title: <idn> 要素 (Uri 設定)
ms.date: 03/30/2017
ms.assetid: 16c8e869-1791-4cf5-9244-3d3c738f60ec
ms.openlocfilehash: 369decf8551c76293ca513b8a3e58b4142a74773
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64592758"
---
# <a name="idn-element-uri-settings"></a>\<idn> 要素 (Uri 設定)
ドメイン名に国際化ドメイン名 (IDN) 解析が適用されるかどうかを指定します。  
  
## <a name="schema-hierarchy"></a>スキーマの階層  
 [\<configuration> 要素](../../../../../docs/framework/configure-apps/file-schema/configuration-element.md)  
  
 [\<Uri> 要素 (Uri 設定)](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)  
  
 [\<idn>](../../../../../docs/framework/configure-apps/file-schema/network/idn-element-uri-settings.md)  
  
## <a name="syntax"></a>構文  
  
```xml  
<idn  
  enabled="All|AllExceptIntranet|None"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|`enabled`|国際化ドメイン名 (IDN) 解析がドメイン名に適用される場合、既定値は none を指定します。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|**要素**|**説明**|  
|-----------------|---------------------|  
|[Uri](../../../../../docs/framework/configure-apps/file-schema/network/uri-element-uri-settings.md)|.NET Framework での uniform resource identifier (Uri) を使用して表現された web アドレスの処理方法を指定する設定が含まれています。|  
  
## <a name="remarks"></a>Remarks  
 既存の<xref:System.Uri>クラスは、.NET Framework 3.5 で拡張されています。 3.0 SP1、および 2.0 SP1 国際リソース識別子 (IRI) および国際化ドメイン名 (IDN) をサポートします。 IRI と IDN 明確には、現在のユーザーに、.NET Framework 2.0 の動作から変更は表示されないをサポートします。 これにより、.NET Framework の以前のバージョンとのアプリケーションの互換性を保証します。  
  
 IRI のサポートを有効にするのには、次の 2 つの変更が必要です。  
  
1. .NET Framework 2.0 のディレクトリの machine.config ファイルに次の行を追加します。  
  
    ```xml  
    <section name="uri" type="System.Configuration.UriSection, System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
    ```  
  
2. 国際化ドメイン名 (IDN) 解析のドメイン名に適用するかどうか、および IRI 解析規則を適用する必要があるかどうかを指定します。 これは、machine.config ファイルまたは app.config ファイルで指定できます。  
  
 IDN を使用する DNS サーバーによって可能な値は 3 つです。  
  
- idn を有効になっている = All  
  
     この値は、任意の Unicode ドメイン名を等価の Punycode (IDN 名) に変換されます。  
  
- idn を有効になっている AllExceptIntranet を =  
  
     この値は、等価の Punycode (IDN 名) を使用するローカルのイントラネットではなく、すべての Unicode ドメイン名に変換されます。 ここでローカルのイントラネットで国際名を処理するために、イントラネットに使用される DNS サーバーは、Unicode の名前解決をサポートする必要があります。  
  
- idn を有効になっている = なし  
  
     この値は Punycode を使用する Unicode ドメイン名を変換できません。 これは、.NET Framework 2.0 の動作と一貫した既定値です。  
  
 IDN を有効にすると、ドメイン名に含まれるすべての Unicode のラベルが Punycode のラベルに変換されます。 Punycode 名には ASCII 文字のみが含まれ、常に xn-- プレフィックスで始まります。 この理由は、ほとんどの DNS サーバーは ASCII 文字しかサポートしていないため、インターネットで既存の DNS サーバーをサポートするためです (RFC 3940 を参照)。  
  
### <a name="configuration-files"></a>構成ファイル  
 この要素は、アプリケーション構成ファイルまたはマシン構成ファイル (Machine.config) で使用できます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例で使用する構成を示しています、<xref:System.Uri>解析する IRI と IDN 名をサポートするクラス。  
  
### <a name="code"></a>コード  
  
```xml  
<configuration>  
  <uri>  
    <idn enabled="All" />  
    <iriParsing enabled="true" />  
  </uri>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Configuration.IdnElement?displayProperty=nameWithType>
- <xref:System.Configuration.UriSection?displayProperty=nameWithType>
- [ネットワーク設定スキーマ](../../../../../docs/framework/configure-apps/file-schema/network/index.md)
