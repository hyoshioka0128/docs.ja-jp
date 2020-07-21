---
title: XML ドキュメント リテラル
ms.date: 07/20/2015
f1_keywords:
- vb.XmlLiteralDocument
helpviewer_keywords:
- XML document literal [Visual Basic]
- XML literals [Visual Basic], document
- XML documents [Visual Basic], creating
- document literal [Visual Basic]
ms.assetid: f7bbee56-0911-41de-b907-96f20450137b
ms.openlocfilehash: 3a2182d2937827bc8dc45e22307a3668420261a2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400203"
---
# <a name="xml-document-literal-visual-basic"></a>XML ドキュメント リテラル (Visual Basic)
<xref:System.Xml.Linq.XDocument> オブジェクトを表すリテラル。  
  
## <a name="syntax"></a>構文  
  
```xml  
<?xml version="1.0" [encoding="encoding"] [standalone="standalone"] ?>  
[ piCommentList ]  
rootElement  
[ piCommentList ]  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`encoding`|任意。 ドキュメントが使用するエンコードを宣言するリテラル テキスト。|  
|`standalone`|任意。 リテラル テキスト。 "yes" または "no" にする必要があります。|  
|`piCommentList`|任意。 XML 処理命令と XML コメントのリスト。 次の形式を使用します。<br /><br /> `piComment [` `piComment` `... ]`<br /><br /> 各 `piComment` に次のいずれかを指定できます。<br /><br /> -   [XML 処理命令リテラル](xml-processing-instruction-literal.md)。<br />-   [XML コメント リテラル](xml-comment-literal.md)。|  
|`rootElement`|必須です。 ドキュメントのルート要素。 形式は次のいずれかです。<br /><br /> <ul><li>[XML 要素リテラル](xml-element-literal.md)。</li><li>`<%=` `elementExp` `%>` 形式の埋め込み式。 `elementExp` は次のいずれかを返します。<br /><br /> <ul><li><xref:System.Xml.Linq.XElement> オブジェクト。</li><li>1 つの <xref:System.Xml.Linq.XElement> オブジェクトと、任意の数の <xref:System.Xml.Linq.XProcessingInstruction> および <xref:System.Xml.Linq.XComment> オブジェクトを含むコレクション。</li></ul></li></ul><br /> 詳細については、「[XML での埋め込み式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)」を参照してください。|  
  
## <a name="return-value"></a>戻り値  
 <xref:System.Xml.Linq.XDocument> オブジェクト。  
  
## <a name="remarks"></a>Remarks  
 リテラルの先頭にある XML 宣言によって、XML ドキュメント リテラルが特定されます。 各 XML ドキュメント リテラルにルート XML 要素が 1 つ必要ですが、XML 処理命令と XML コメントは任意の数を挿入できます。  
  
 XML ドキュメント リテラルは、XML 要素には記述できません。  
  
> [!NOTE]
> XML リテラルは、行連結文字を使用せずに、複数行にまたがることができます。 これにより、XML ドキュメントからコンテンツをコピーして、Visual Basic プログラムに直接貼り付けることができます。  
  
 XML ドキュメント リテラルは、Visual Basic コンパイラによって、<xref:System.Xml.Linq.XDocument.%23ctor%2A> コンストラクターおよび <xref:System.Xml.Linq.XDeclaration.%23ctor%2A> コンストラクターへの呼び出しに変換されます。  
  
## <a name="example"></a>例  
 次の例で作成する XML ドキュメントには、XML 宣言、処理命令、コメント、および別の要素を含む要素が含まれます。  
  
 [!code-vb[VbXMLSamples#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#30)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XElement>
- <xref:System.Xml.Linq.XProcessingInstruction>
- <xref:System.Xml.Linq.XComment>
- <xref:System.Xml.Linq.XDocument>
- [XML 処理命令リテラル](xml-processing-instruction-literal.md)
- [XML コメント リテラル](xml-comment-literal.md)
- [XML 要素リテラル](xml-element-literal.md)
- [XML リテラル](index.md)
- [Visual Basic での XML の作成](../../programming-guide/language-features/xml/creating-xml.md)
- [XML での埋め込み式](../../programming-guide/language-features/xml/embedded-expressions-in-xml.md)
