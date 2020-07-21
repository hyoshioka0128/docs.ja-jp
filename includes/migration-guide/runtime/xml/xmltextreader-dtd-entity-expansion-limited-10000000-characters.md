---
ms.openlocfilehash: fdec6671cbf2dae0d72dfaec07f162058b38cf9d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620510"
---
### <a name="xmltextreader-dtd-entity-expansion-is-limited-to-10000000-characters"></a>XmlTextReader DTD エンティティの拡張が、10,000, 000 文字に制限される

#### <a name="details"></a>説明

DTD エンティティの拡張は 10,000,000 文字までに制限されるようになりました。 DTD エンティティの展開を使用しない XML ファイルの読み込みや、制限された DTD エンティティの展開を使用した XML ファイルの読み込みは、影響を受けません。 DTD エンティティの展開が 10,000,000 文字を超えるファイルは読み込みに失敗し、例外をスローします。

#### <a name="suggestion"></a>提案される解決策

DTD エンティティの拡張の制限が 10,000, 000 では低すぎる場合には、<xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities> プロパティで値をオーバーライドできます。 適切な <xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities?displayProperty=fullName> 値を持つ <xref:System.Xml.XmlReaderSettings?displayProperty=fullName> を、<xref:System.Xml.XmlReaderSettings?displayProperty=fullName> を受け取る <code>XmlReader.Create</code> に渡すことができます (<xref:System.Xml.XmlReader.Create(System.String,System.Xml.XmlReaderSettings)> など)

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Xml.XmlTextReader?displayProperty=nameWithType></li><li><xref:System.Xml.XmlTextReader.%23ctor></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.IO.Stream)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.IO.Stream,System.Xml.XmlNameTable)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.IO.Stream,System.Xml.XmlNodeType,System.Xml.XmlParserContext)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.IO.TextReader)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.IO.TextReader,System.Xml.XmlNameTable)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.IO.Stream)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.IO.Stream,System.Xml.XmlNameTable)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.IO.TextReader)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.IO.TextReader,System.Xml.XmlNameTable)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.Xml.XmlNameTable)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.String,System.Xml.XmlNodeType,System.Xml.XmlParserContext)></li><li><xref:System.Xml.XmlTextReader.%23ctor(System.Xml.XmlNameTable)></li></ul>|
