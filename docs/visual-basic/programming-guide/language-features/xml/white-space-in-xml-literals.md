---
title: XML リテラルでの空白文字
ms.date: 07/20/2015
helpviewer_keywords:
- white space [XML in Visual Basic]
- XML literals [Visual Basic], white space
ms.assetid: dfe3a9ff-d69a-418e-a6b5-476f4ed84219
ms.openlocfilehash: b3caf7ac052f3fed3fe5427da0cc96bbdd955ea6
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360476"
---
# <a name="white-space-in-xml-literals-visual-basic"></a>XML リテラルでの空白文字 (Visual Basic)
Visual Basic コンパイラは、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] オブジェクトを作成するときに、XML リテラルから有意の空白文字のみを組み込みます。 意味のない空白文字は組み込まれません。  
  
## <a name="significant-and-insignificant-white-space"></a>有意の空白と意味のない空白  
 XML リテラルの空白文字は、次の 3 つの領域でのみ意味があります。  
  
- 属性値に含まれている場合。  
  
- 要素のテキスト コンテンツの一部であり、テキストに他の文字も含まれている場合。  
  
- 要素のテキスト コンテンツの埋め込み式に含まれている場合。  
  
 それ以外の場合、空白文字はコンパイラによって意味のないものとして扱われ、リテラルの [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] オブジェクトに含まれません。  
  
 XML リテラルに意味のない空白を含めるには、空白を含む文字列リテラルを含む埋め込み式を使用します。  
  
> [!NOTE]
> XML 要素リテラルに `xml:space` 属性が含まれている場合、Visual Basic コンパイラによって <xref:System.Xml.Linq.XElement> オブジェクトに属性が含まれますが、この属性を追加しても、コンパイラが空白を処理する方法は変わりません。  
  
## <a name="examples"></a>使用例  
 次の例には、2 つの XML 要素 (outer と inner) が含まれています。 どちらの要素にも、テキスト コンテンツ内に空白が含まれています。 outer 要素には空白と XML 要素しか含まれていないため、その空白は意味がありません。 inner 要素には空白とテキストが含まれているため、その空白は有意です。  
  
 [!code-vb[VbXMLSamples#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#29)]  
  
 このコードを実行すると、次のテキストが表示されます。  
  
```xml  
<outer>  
  <inner>  
                                          Inner text  
                                      </inner>  
</outer>  
```  
  
## <a name="see-also"></a>関連項目

- [Visual Basic での XML の作成](creating-xml.md)
