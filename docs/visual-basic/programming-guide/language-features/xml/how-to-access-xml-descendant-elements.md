---
title: '方法: XML 子孫要素にアクセスする'
ms.date: 07/20/2015
helpviewer_keywords:
- XML descendent axis property [Visual Basic]
- XML axis [Visual Basic], descendent
- descendent axis property [Visual Basic]
- XML [Visual Basic], accessing
ms.assetid: aabfa258-4112-4e7e-bab9-403f96072ef7
ms.openlocfilehash: 03c403aa3c187b0b9d2006104eccaa1f9cd8aec5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84392637"
---
# <a name="how-to-access-xml-descendant-elements-visual-basic"></a>方法: XML 子孫要素にアクセスする (Visual Basic)
この例では、子孫軸プロパティを使用して、指定した名前を持ち、XML 要素の下に含まれているすべての XML 要素にアクセスする方法を示しています。 特に、`Value` プロパティを使用して、`name` 子孫軸プロパティによって返されるコレクション内の最初の要素の値を取得します。 `name` 子孫軸プロパティでは、`contacts` オブジェクトに含まれる `name` という名前のすべての要素を取得します。 また、この例では、`phone` 子孫軸プロパティを使用して、`contacts` オブジェクトに含まれている `phone` という名前のすべての子孫にアクセスしています。  
  
## <a name="example"></a>例  
 [!code-vb[VbXMLSamples#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples13.vb#31)]  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System.Xml.Linq> 名前空間への参照  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType>
- [XML 子孫軸プロパティ](../../../language-reference/xml-axis/xml-descendant-axis-property.md)
- [XML Value プロパティ](../../../language-reference/xml-axis/xml-value-property.md)
- [Visual Basic での XML へのアクセス](accessing-xml.md)
- [XML](index.md)
