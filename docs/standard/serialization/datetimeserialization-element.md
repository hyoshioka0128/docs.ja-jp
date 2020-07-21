---
title: <dateTimeSerialization> 要素
description: この記事では、DateTime オブジェクトのシリアル化モードを決定する <dateTimeSerialization> 要素について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- dateTimeSerialization element
- XML serialization, configuration
- <dateTimeSerialization> element
ms.assetid: 90fda55c-7730-41e9-bc4b-6423a4b920af
ms.openlocfilehash: a2684ab72c1fb109d711e333e01836d3399caf86
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84289643"
---
# <a name="datetimeserialization-element"></a>\<dateTimeSerialization> 要素
<xref:System.DateTime> オブジェクトのシリアル化モードを決定します。  
  
 \<configuration>  
\<dateTimeSerialization>  
  
## <a name="syntax"></a>構文  
  
```xml  
<dateTimeSerialization  
    mode = "Roundtrip|Local"  
/>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|----------------|-----------------|  
|`mode`|任意。 シリアル化モードを指定します。 <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode> 値のいずれかに設定します。 既定値は **RoundTrip** です。|  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|system.xml.serialization|XML シリアル化を制御する最上位の要素です。|  
  
## <a name="remarks"></a>Remarks  
 .NET Framework の 1.0、1.1、2.0、およびそれ以降のバージョンで、このプロパティが **Local** に設定されている場合、<xref:System.DateTime> オブジェクトは常に現地時刻として書式設定されます。 つまり、ローカル タイム ゾーンの情報が、シリアル化されたデータに必ず組み込まれます。 .NET Framework の以前のバージョンとの互換性を保証するには、このプロパティを **Local** に設定します。  
  
 このプロパティが **Roundtrip** に設定されているバージョン 2.0 以降の .NET Framework では、<xref:System.DateTime> オブジェクトが調べられ、タイム ゾーンがローカル、UTC、または未指定のいずれであるかが特定されます。 その後、この特定された情報を保持する形で、<xref:System.DateTime> オブジェクトがシリアル化されます。 これは既定の動作であり、.NET Framework の以前のバージョンと通信を行わない、すべての新しいアプリケーションで推奨されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.DateTime>
- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [構成ファイル スキーマ](../../framework/configure-apps/file-schema/index.md)
- [\<schemaImporterExtensions> 要素](schemaimporterextensions-element.md)
- [\<schemaImporterExtensions> の \<add> 要素](add-element-for-schemaimporterextensions.md)
- [\<system.xml.serialization> 要素](system-xml-serialization-element.md)
