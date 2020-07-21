---
title: XML Attribute Axis Property
ms.date: 07/20/2015
f1_keywords:
- vb.XmlPropertyAttributeAxis
helpviewer_keywords:
- attribute axis property [Visual Basic]
- Visual Basic code, accessing XML
- XML attribute axis property [Visual Basic]
- XML axis [Visual Basic], attribute
- XML [Visual Basic], accessing
ms.assetid: 7a4777e1-0618-4de9-9510-fb9ace2bf4db
ms.openlocfilehash: 3f60190a949856cb2bbc2eba09d097c09089bea7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84408433"
---
# <a name="xml-attribute-axis-property-visual-basic"></a>XML 属性軸プロパティ (Visual Basic)
<xref:System.Xml.Linq.XElement> オブジェクトの属性の値または <xref:System.Xml.Linq.XElement> オブジェクト コレクションの最初の要素にアクセスできるようにします。  
  
## <a name="syntax"></a>構文  
  
```vb  
object.@attribute  
' -or-  
object.@<attribute>  
```  
  
## <a name="parts"></a>指定項目  
 `object`  
 必須です。 <xref:System.Xml.Linq.XElement> オブジェクトまたは <xref:System.Xml.Linq.XElement> オブジェクトのコレクション。  
  
 .@  
 必須です。 属性軸プロパティの先頭を表します。  
  
 <  
 任意。 Visual Basic で `attribute` が有効な識別子ではない場合に、属性の名前の先頭を表します。  
  
 `attribute`  
 必須です。 アクセスする属性の名前。[`prefix`:]`name` の形式で指定します。  
  
|パーツ|説明|  
|----------|-----------------|  
|`prefix`|任意。 属性の XML 名前空間プレフィックス。 `Imports` ステートメントを使用して定義されているグローバル XML 名前空間を指定する必要があります。|  
|`name`|必須です。 ローカル属性名。 「[宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)」を参照してください。|  
  
 \>  
 任意。 Visual Basic で `attribute` が有効な識別子ではない場合に、属性の名前の末尾を表します。  
  
## <a name="return-value"></a>戻り値  
 `attribute` の値を格納する文字列。 属性名が存在しない場合は `Nothing` が返されます。  
  
## <a name="remarks"></a>Remarks  
 XML 属性軸プロパティを使用すると、名前を指定して、<xref:System.Xml.Linq.XElement> オブジェクトまたは <xref:System.Xml.Linq.XElement> オブジェクト コレクションの最初の要素から属性値にアクセスできます。 名前を使って属性値を取得することも、新しい名前の前に @ 識別子を指定して新しい属性を要素に追加することもできます。  
  
 @ 識別子を使用して XML 属性を参照すると、属性値は文字列として返されるため、<xref:System.Xml.Linq.XAttribute.Value%2A> プロパティを明示的に指定する必要がありません。  
  
 XML 属性の名前付けルールは、Visual Basic 識別子の名前付けルールとは異なります。 名前が有効な Visual Basic 識別子ではない XML 属性にアクセスするには、山かっこ (\< and >) で名前を囲みます。  
  
## <a name="xml-namespaces"></a>XML 名前空間  
 属性軸プロパティの名前では、`Imports` ステートメントを使用してグローバルに宣言されている XML 名前空間プレフィックスのみを使用できます。 XML 要素リテラル内でローカルに宣言されている XML 名前空間プレフィックスは使用できません。 詳細については、「[Imports ステートメント (XML 名前空間)](../statements/imports-statement-xml-namespace.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例は、`type` という名前の XML 属性の値を、`phone` という名前の XML 要素のコレクションから取得する方法を示しています。  
  
 [!code-vb[VbXMLSamples#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#12)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
 `<phoneTypes>`  
  
 `<type>home</type>`  
  
 `<type>work</type>`  
  
 `</phoneTypes>`  
  
## <a name="example"></a>例  
 次の例は、XML 要素の属性を、宣言によって XML の一部として作成する方法と、<xref:System.Xml.Linq.XElement> オブジェクトのインスタンスに属性を追加して動的に作成する方法の両方を示しています。 `type` 属性は宣言によって作成され、`owner` 属性は動的に作成されています。  
  
 [!code-vb[VbXMLSamples#44](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#44)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
```xml  
<phone type="home" owner="Harris, Phyllis">206-555-0144</phone>  
```  
  
## <a name="example"></a>例  
 次の例では、山かっこ構文を使用して、Visual Basic の有効な識別子ではない、`number-type` という名前の XML 属性値を取得します。  
  
 [!code-vb[VbXMLSamples#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples5.vb#13)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
 `Phone type: work`  
  
## <a name="example"></a>例  
 次の例では、`ns` を名前空間プレフィックスとして宣言します。 その後、この名前空間のプレフィックスを使用して XML リテラルを作成し、修飾名が "`ns:name`" の最初の子ノードにアクセスします。  
  
 [!code-vb[VbXMLSamples#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples6.vb#14)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
 `Phone type: home`  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- [XML 軸プロパティ](index.md)
- [XML リテラル](../xml-literals/index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [宣言する XML 要素と属性の名前](../../programming-guide/language-features/xml/names-of-declared-xml-elements-and-attributes.md)
