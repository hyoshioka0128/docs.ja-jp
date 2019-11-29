---
title: '方法: XML 子要素にアクセスする'
ms.date: 07/20/2015
helpviewer_keywords:
- XML axis [Visual Basic], child
- child axis property [Visual Basic]
- XML child axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: 6689eb36-c471-469f-a82d-099ab8197b25
ms.openlocfilehash: af5ea809cb0777b16230f20e133764dd5f1f86d9
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74332339"
---
# <a name="how-to-access-xml-child-elements-visual-basic"></a>方法 : XML 子要素にアクセスする (Visual Basic)
この例では、子軸プロパティを使用して、XML 要素内で指定された名前を持つすべての XML 子要素にアクセスする方法を示します。 具体的には、<xref:System.Xml.Linq.XElement.Value%2A> プロパティを使用して、`name` 子軸プロパティが返すコレクション内の最初の要素の値を取得します。 子軸プロパティ `name` は、`contact` オブジェクト内の `phone` という名前のすべての子要素を取得します。 また、この例では、`phone` 子軸プロパティを使用して、`contact` オブジェクトに含まれる `phone` という名前のすべての子要素にアクセスします。  
  
## <a name="example"></a>例  
 [!code-vb[VbXMLSamples#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples4.vb#10)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System.Xml.Linq> 名前空間への参照  
  
## <a name="see-also"></a>参照

- <xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>
- [XML 子軸プロパティ](../../../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md)
- [XML Value プロパティ](../../../../visual-basic/language-reference/xml-axis/xml-value-property.md)
- [Visual Basic での XML へのアクセス](../../../../visual-basic/programming-guide/language-features/xml/accessing-xml.md)
- [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)
