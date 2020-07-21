---
title: <system.xml.serialization> 要素
description: この記事では、XML シリアル化を制御する最上位要素である <system.xml.serialization> 要素について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- system.xml.serialization element
- XML serialization, configuration
- <system.xml.serialization> element
ms.assetid: 3ce45919-388a-418c-8968-6df0372c73ec
ms.openlocfilehash: f69e80592e9321de64421b977a63b83d8be2ad9e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "84289487"
---
# <a name="systemxmlserialization-element"></a>\<system.xml.serialization> 要素

XML シリアル化を制御する最上位の要素です。 構成ファイルの詳細については、「[構成ファイル スキーマ](../../framework/configure-apps/file-schema/index.md)」を参照してください。

\<configuration>\
\<system.xml.serialization>

## <a name="syntax"></a>構文

```xml
<system.xml.serialization>
</system.xml.serialization>
```

## <a name="attributes-and-elements"></a>属性および要素

以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

なし。

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[\<dateTimeSerialization> 要素](datetimeserialization-element.md)|<xref:System.DateTime> オブジェクトのシリアル化モードを決定します。|
|[\<schemaImporterExtensions> 要素](schemaimporterextensions-element.md)|XSD の型を .NET Framework の型にマッピングするために <xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型を含みます。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[\<configuration> 要素](../../framework/configure-apps/file-schema/configuration-element.md)|共通言語ランタイムおよび .NET Framework アプリケーションで使用されるすべての構成ファイルのルート要素です。|

## <a name="example"></a>例

次のコード例は、<xref:System.DateTime> オブジェクトのシリアル化モードを指定し、XSD の型を .NET Framework の型にマッピングするために <xref:System.Xml.Serialization.XmlSchemaImporter> によって使用される型を追加する方法を示します。

```xml
<system.xml.serialization>
    <xmlSerializer checkDeserializeAdvances="false" />
    <dateTimeSerialization mode = "Local" />
    <schemaImporterExtensions>
        <add
        name = "MobileCapabilities"
        type = "System.Web.Mobile.MobileCapabilities,
        System.Web.Mobile, Version=2.0.0.0, Culture=neutral,
        PublicKeyToken=b03f5f6f11d40a3a" />
    </schemaImporterExtensions>
</system.xml.serialization>
```

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Serialization.XmlSchemaImporter>
- <xref:System.Xml.Serialization.Configuration.DateTimeSerializationSection.DateTimeSerializationMode>
- [構成ファイル スキーマ](../../framework/configure-apps/file-schema/index.md)
- [\<dateTimeSerialization> 要素](datetimeserialization-element.md)
- [\<schemaImporterExtensions> 要素](schemaimporterextensions-element.md)
- [\<schemaImporterExtensions> の \<add> 要素](add-element-for-schemaimporterextensions.md)
