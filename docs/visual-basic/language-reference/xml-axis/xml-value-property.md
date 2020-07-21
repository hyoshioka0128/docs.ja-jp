---
title: XML Value プロパティ
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyExtensionValue
helpviewer_keywords:
- Value property [Visual Basic]
- Visual Basic code, accessing XML
- XML axis [Visual Basic], Value
- XML Value property [Visual Basic]
ms.assetid: 7ddd057a-a195-4e9b-ad8b-2ee0e615a20f
ms.openlocfilehash: 571d9130ef69df580bbba5d90bc8758b4b627196
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74349418"
---
# <a name="xml-value-property-visual-basic"></a>XML Value プロパティ (Visual Basic)

<xref:System.Xml.Linq.XElement> オブジェクト コレクションの最初の要素の値にアクセスできるようにします。

## <a name="syntax"></a>構文

```vb
object.Value
```

## <a name="parts"></a>指定項目

|用語|定義|  
|---|---|  
|`object`|必須です。 <xref:System.Xml.Linq.XElement> オブジェクトのコレクション。|  

## <a name="return-value"></a>戻り値

 コレクションの最初の要素の値を含む `String`、または `Nothing` (コレクションが空の場合)。

## <a name="remarks"></a>Remarks

 <xref:System.Xml.Linq.XElement.Value%2A> プロパティは、<xref:System.Xml.Linq.XElement> オブジェクト コレクションの最初の要素の値にアクセスしやすくします。 このプロパティは、コレクションに少なくとも 1 つのオブジェクトが含まれるかどうかをまず確認します。 コレクションが空の場合、このプロパティは `Nothing` を返します。 それ以外の場合は、コレクションの最初の要素の <xref:System.Xml.Linq.XElement.Value%2A> プロパティ値を返します。

> [!NOTE]
> "\@" 識別子を使用して XML 属性の値にアクセスすると、属性値は `String` として返されるため、<xref:System.Xml.Linq.XAttribute.Value%2A> プロパティを明示的に指定する必要はありません。

 コレクションの他の要素には、XML 拡張インデクサー プロパティを使用してアクセスできます。 詳細については、「[拡張インデクサー プロパティ](extension-indexer-property.md)」を参照してください。

## <a name="inheritance"></a>継承

 ユーザーのほとんどが <xref:System.Collections.Generic.IEnumerable%601> を実装する必要がないため、このセクションは無視できます。

 <xref:System.Xml.Linq.XElement.Value%2A> プロパティは、`IEnumerable(Of XElement)` を実装する型の拡張プロパティです。 この拡張プロパティのバインディングは、拡張メソッドのバインディングと似ています。つまり、いずれかのインターフェイスが型で実装され、"Value" という名前のプロパティが定義されていると、そのプロパティは拡張プロパティよりも優先されます。 言い換えると、この <xref:System.Xml.Linq.XElement.Value%2A> プロパティは、`IEnumerable(Of XElement)` を実装するクラスで新しいプロパティを定義してオーバーライドできます。

## <a name="example"></a>例

 次の例は、<xref:System.Xml.Linq.XElement.Value%2A> プロパティを使用して、<xref:System.Xml.Linq.XElement> オブジェクト コレクションの最初のノードにアクセスする方法を示しています。 この例では、子軸プロパティを使用して、`contact` オブジェクトにある `phone` という名前の子ノードすべてのコレクションを取得します。

 [!code-vb[VbXMLSamples#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#15)]

 このコードを実行すると、次のテキストが表示されます。

 `Phone number: 206-555-0144`

## <a name="example"></a>例

 次の例は、<xref:System.Xml.Linq.XAttribute> オブジェクトのコレクションから XML 属性の値を取得する方法を示しています。 この例では、属性軸プロパティを使用して、`phone` 要素すべての `type` 属性の値を表示します。

 [!code-vb[VbXMLSamples#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples7.vb#16)]

 このコードを実行すると、次のテキストが表示されます。

 ```console
 home
 work
```

## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- <xref:System.Collections.Generic.IEnumerable%601>
- [XML 軸プロパティ](index.md)
- [XML リテラル](../xml-literals/index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [拡張メソッド](../../programming-guide/language-features/procedures/extension-methods.md)
- [拡張インデクサー プロパティ](extension-indexer-property.md)
- [XML 子軸プロパティ](xml-child-axis-property.md)
- [XML 属性軸プロパティ](xml-attribute-axis-property.md)
