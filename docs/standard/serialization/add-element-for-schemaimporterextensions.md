---
title: <schemaImporterExtensions> の <add> 要素
description: <add> 要素は、XSD の型を .NET Framework の型にマッピングするために XmlSchemaImporter クラスで使用される型を追加します。
ms.date: 03/30/2017
helpviewer_keywords:
- XML serialization, configuration
- <add> element for <schemaImporterExtensions> element
ms.assetid: c828a558-094b-441e-9065-790b87315fa0
ms.openlocfilehash: 6fd8113ad39a22c927035fca574151ae8f002685
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84288330"
---
# <a name="add-element-for-schemaimporterextensions"></a>\<schemaImporterExtensions> の \<add> 要素
XSD 型を .NET Framework 型に対応付けるために、<xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型を追加します。 構成ファイルの詳細については、「[構成ファイル スキーマ](../../framework/configure-apps/file-schema/index.md)」を参照してください。  
  
 \<configuration>  
\<system.xml.serialization>  
\<schemaImporterExtensions>  
\<add>  
  
## <a name="syntax"></a>構文  
  
```xml  
<add name = "typeName" type="fully qualified type [,Version=version number] [,Culture=culture] [,PublicKeyToken= token]"/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|**name**|インスタンスの検索に使用される簡易名。|  
|**type**|必須です。 追加するスキーマ拡張クラスを指定します。 **type** 属性の値は 1 行で指定し、完全修飾型名を含める必要があります。 アセンブリをグローバル アセンブリ キャッシュ (GAC: Global Assembly Cache) に配置する場合は、バージョン、カルチャ、およびアセンブリの署名に使用した公開キーのトークンも含める必要があります。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|\<schemaImporterExtensions>|<xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型が含まれます。|  
  
## <a name="example"></a>例  
 型を対応付けるときに XmlSchemaImporter が使用できる拡張の型を追加するコード例を次に示します。  
  
```xml  
<configuration>  
  <system.xml.serialization>  
    <schemaImporterExtensions>  
       <add name="contoso" type="System.Web.Mobile.MobileCapabilities,
       System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a" />
    </schemaImporterExtensions>  
  </system.xml.serialization>  
</configuration>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- [\<system.xml.serialization> 要素](system-xml-serialization-element.md)
- [\<schemaImporterExtensions> 要素](schemaimporterextensions-element.md)
