---
ms.openlocfilehash: eafbdd2d42977381fb4d77748a3c9a2595ff2936
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620375"
---
### <a name="xmlserializer-fails-while-serializing-a-type-that-hides-an-accessible-member-with-an-inaccessible-one"></a>アクセス可能なメンバーを非表示にする型をアクセス不可のメンバーでシリアル化すると、XmlSerializer が失敗する

#### <a name="details"></a>説明

基本型で (パブリックなど) 以前はアクセス可能だった同じ名前のフィールドまたはプロパティを ("新しい" キーワードを使用して) 非表示にするアクセス不可のフィールドまたはプロパティが型に含まれている場合、派生型をシリアル化すると、<xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> が失敗する可能性があります。

#### <a name="suggestion"></a>提案される解決策

この問題は、新しい非表示メンバーを <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> にアクセスできるようにする (パブリックにするなど) ことで解決できます。または、次の構成設定で 4.0 <xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> の動作に戻します。これにより、問題が解決されます。<pre><code class="lang-xml">&lt;system.xml.serialization&gt;&#13;&#10;&lt;xmlSerializer useLegacySerializerGeneration=&quot;true&quot; /&gt;&#13;&#10;&lt;/system.xml.serialization&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream,System.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter,System.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Object,System.Xml.Serialization.XmlSerializationWriter)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter,System.Object)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.Stream,System.Object,System.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.IO.TextWriter,System.Object,System.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter,System.Object,System.Xml.Serialization.XmlSerializerNamespaces)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter,System.Object,System.Xml.Serialization.XmlSerializerNamespaces,System.String)?displayProperty=nameWithType></li><li><xref:System.Xml.Serialization.XmlSerializer.Serialize(System.Xml.XmlWriter,System.Object,System.Xml.Serialization.XmlSerializerNamespaces,System.String,System.String)?displayProperty=nameWithType></li></ul>|
