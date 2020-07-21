---
title: XML での埋め込み式
ms.date: 07/20/2015
f1_keywords:
- vb.XmlEmbeddedExpression
helpviewer_keywords:
- embedded expressions [Visual Basic]
- LINQ to XML [Visual Basic], embedded expressions
- XML literals [Visual Basic], embedded expressions
ms.assetid: bf2eb779-b751-4b7c-854f-9f2161482352
ms.openlocfilehash: d4ff9442aa82a3eb46d56500159562174646ea58
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410258"
---
# <a name="embedded-expressions-in-xml-visual-basic"></a>XML での埋め込み式 (Visual Basic)
埋め込み式を使用すると、実行時に評価される式を含む XML リテラルを作成できます。 埋め込み式の構文は `<%=` `expression` `%>` となります。これは ASP.NET で使用される構文と同じです。  
  
 たとえば、XML 要素リテラルを作成して、埋め込み式をリテラル テキスト コンテンツと組み合わせることができます。  
  
 [!code-vb[VbXMLSamples#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#27)]  
  
 `isbnNumber` に整数 12345 が含まれていて、`modifiedDate` に日付 3/5/2006 が含まれている場合、このコードを実行すると、`book` の値は次のようになります。  
  
```xml  
<book category="fiction" isbn="12345">  
  <modifiedDate>3/5/2006</modifiedDate>  
</book>  
```  
  
## <a name="embedded-expression-location-and-validation"></a>埋め込み式の場所と検証  
 埋め込み式は、XML リテラル式内の特定の場所でのみ使用できます。 このような式の場所により、式から返すことができる型と `Nothing` の処理方法が制御されます。 次の表では、埋め込み式の許可される場所と型について説明します。  
  
|リテラル内の場所|式の型|`Nothing` の処理|  
|---|---|---|  
|XML 要素名|<xref:System.Xml.Linq.XName>|Error|  
|XML 要素のコンテンツ|`Object` または `Object` の配列|無視|  
|XML 要素の属性名|<xref:System.Xml.Linq.XName>|属性値も `Nothing` でない限り、エラー。|  
|XML 要素の属性値|`Object`|属性の宣言を無視|  
|XML 要素の属性|<xref:System.Xml.Linq.XAttribute> または <xref:System.Xml.Linq.XAttribute> のコレクション|無視|  
|XML ドキュメントのルート要素|<xref:System.Xml.Linq.XElement>、または 1 つの <xref:System.Xml.Linq.XElement> オブジェクトと任意の数の <xref:System.Xml.Linq.XProcessingInstruction> および <xref:System.Xml.Linq.XComment> オブジェクトから成るコレクション|無視|  
  
- XML 要素名での埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#32](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#32)]  
  
- XML 要素のコンテンツでの埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#33)]  
  
- XML 要素の属性名での埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#34)]  
  
- XML 要素の属性値での埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#35)]  
  
- XML 要素属性での埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#36)]  
  
- XML ドキュメントのルート要素での埋め込み式の例を次に示します。  
  
     [!code-vb[VbXMLSamples#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#37)]  
  
 `Option Strict` を有効にすると、各埋め込み式の型が必須の型に拡大変換されていることがコンパイラによって検査されます。 XML ドキュメントのルート要素の場合は唯一の例外となり、コードの実行時に検証されます。 `Option Strict` なしでコンパイルする場合は、`Object` 型の式を埋め込むことができ、その型は実行時に検証されます。  
  
 コンテンツが省略可能な場所では、`Nothing` を含む埋め込み式は無視されます。 つまり、XML リテラルを使用する前に、要素のコンテンツ、属性値、および配列要素が `Nothing` になっていないことを確認する必要はありません。 要素名や属性名などの必須の値を `Nothing` にすることはできません。  
  
 特定の型のリテラル内に埋め込み式を使用する方法の詳細については、[XML ドキュメント リテラル](../../../language-reference/xml-literals/xml-document-literal.md)に関するページ、および [XML 要素リテラル](../../../language-reference/xml-literals/xml-element-literal.md)に関するページを参照してください。  
  
## <a name="scoping-rules"></a>スコープの規則  
 各 XML リテラルはコンパイラによって、適切なリテラル型のコンストラクター呼び出しに変換されます。 XML リテラル内のリテラル コンテンツと埋め込み式は、引数としてコンストラクターに渡されます。 これは、XML リテラルで使用できる Visual Basic プログラミング要素はすべて、その埋め込み式でも使用できることを意味します。  
  
 XML リテラル内では、`Imports` ステートメントで宣言された XML 名前空間プレフィックスにアクセスできます。 `xmlns` 属性を使用すれば、要素内で、新しい XML 名前空間プレフィックスを宣言することも、既存の XML 名前空間プレフィックスをシャドウすることもできます。 その要素の子ノードでは新しい名前空間を使用できますが、埋め込み式内の XML リテラルではそれを使用できません。  
  
> [!NOTE]
> `xmlns` 名前空間属性を使用して XML 名前空間プレフィックスを宣言する場合は、属性値を定数文字列とする必要があります。 この点で、`xmlns` 属性を使用することは、`Imports` ステートメントを使用して XML 名前空間を宣言することに似ています。 埋め込み式を使用して XML 名前空間の値を指定することはできません。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic での XML の作成](creating-xml.md)
- [XML ドキュメント リテラル](../../../language-reference/xml-literals/xml-document-literal.md)
- [XML 要素リテラル](../../../language-reference/xml-literals/xml-element-literal.md)
- [Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)
- [Imports ステートメント (.NET 名前空間および型)](../../../language-reference/statements/imports-statement-net-namespace-and-type.md)
- [XML リテラルの概要](xml-literals-overview.md)
