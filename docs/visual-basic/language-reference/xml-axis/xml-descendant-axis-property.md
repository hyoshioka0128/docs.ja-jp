---
title: XML Descendant Axis Property
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyDescendantsAxis
helpviewer_keywords:
- Visual Basic code, accessing XML
- XML descendant axis property [Visual Basic]
- descendant axis property [Visual Basic]
- XML axis [Visual Basic], descendant
- XML [Visual Basic], accessing
ms.assetid: a178f85b-5d54-438f-8479-40b62af6fe76
ms.openlocfilehash: 52544619171dbc7034baeb5feb61395d81096387
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400254"
---
# <a name="xml-descendant-axis-property-visual-basic"></a>XML 子孫軸プロパティ (Visual Basic)

<xref:System.Xml.Linq.XElement> オブジェクト、<xref:System.Xml.Linq.XDocument> オブジェクト、<xref:System.Xml.Linq.XElement> オブジェクトのコレクション、または <xref:System.Xml.Linq.XDocument> オブジェクトのコレクションの子孫にアクセスできるようにします。

## <a name="syntax"></a>構文

```vb
object...<descendant>
```

## <a name="parts"></a>指定項目

`object` 必須。 <xref:System.Xml.Linq.XElement> オブジェクト、<xref:System.Xml.Linq.XDocument> オブジェクト、<xref:System.Xml.Linq.XElement> オブジェクトのコレクション、または <xref:System.Xml.Linq.XDocument> オブジェクトのコレクションです。

`...<` 必須。 子孫軸プロパティの開始を示します。

`descendant` 必須。 アクセスする子孫ノードの名前です。[`prefix:]name` の形式で指定します。

|パーツ|説明|
|----------|-----------------|
|`prefix`|任意。 子孫ノードの XML 名前空間プレフィックスです。 `Imports` ステートメントを使用して定義されているグローバル XML 名前空間にする必要があります。|
|`name`|必須です。 子孫ノードのローカル名。 「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。|

`>` 必須。 子孫軸プロパティの終了を示します。

## <a name="return-value"></a>戻り値

<xref:System.Xml.Linq.XElement> オブジェクトのコレクション。

## <a name="remarks"></a>Remarks

XML 子孫軸プロパティを使用すると、<xref:System.Xml.Linq.XElement> オブジェクト、<xref:System.Xml.Linq.XDocument> オブジェクト、<xref:System.Xml.Linq.XElement> オブジェクトのコレクション、または <xref:System.Xml.Linq.XDocument> オブジェクトのコレクションから子孫ノードに名前でアクセスできます。 返されるコレクションの最初の子孫ノードの値にアクセスするには、XML の `Value` プロパティを使用します。 詳細については、「[XML Value プロパティ](xml-value-property.md)」を参照してください。

Visual Basic コンパイラによって、子孫軸プロパティが <xref:System.Xml.Linq.XContainer.Descendants%2A> メソッドの呼び出しに変換されます。

## <a name="xml-namespaces"></a>XML 名前空間

子孫軸プロパティの名前では、`Imports` ステートメントでグローバルに宣言されている XML 名前空間のみを使用できます。 XML 要素リテラル内でローカルに宣言されている XML 名前空間は使用できません。 詳細については、「[Imports ステートメント (XML 名前空間)](../statements/imports-statement-xml-namespace.md)」を参照してください。

## <a name="example"></a>例

次の例は、`contacts` オブジェクトから、`name` という名前の最初の子孫ノードの値と、`phone` という名前のすべての子孫ノードの値にアクセスする方法を示しています。

[!code-vb[VbXMLSamples#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples11.vb#25)]

このコードを実行すると、次のテキストが表示されます。

`Name: Patrick Hines`

`Home Phone = 206-555-0144`

## <a name="example"></a>例

次の例では、`ns` を名前空間プレフィックスとして宣言します。 その後、この名前空間のプレフィックスを使用して XML リテラルを作成し、修飾名 `ns:name` を持つ最初の子ノードの値にアクセスします。

[!code-vb[VbXMLSamples#26](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples12.vb#26)]

このコードを実行すると、次のテキストが表示されます。

`Name: Patrick Hines`

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- [XML 軸プロパティ](index.md)
- [XML リテラル](../xml-literals/index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
