---
title: 宣言する XML 要素と属性の名前
ms.date: 07/20/2015
helpviewer_keywords:
- declarations [XML in Visual Basic]
- element names [XML in Visual Basic]
- names in XML literals [Visual Basic]
- attribute names [XML in Visual Basic]
- XML literals [Visual Basic], element names
ms.assetid: cc110118-b6cf-4ff9-a4e4-6233c90c9fbf
ms.openlocfilehash: 043243eeee7c24d8c63105047fa3e7e0ed58c7b0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84374669"
---
# <a name="names-of-declared-xml-elements-and-attributes-visual-basic"></a>宣言する XML 要素と属性の名前 (Visual Basic)
このトピックでは、XML リテラルで XML 要素と属性に名前を付けるための Visual Basic ガイドラインを示します。  XML リテラルでは、ローカル名を指定することも修飾名を指定することもできます。 修飾名は、XML 名前空間プレフィックス、コロン、およびローカル名から成ります。 XML 名前空間プレフィックスの詳細については、「[XML 要素リテラル](../../../language-reference/xml-literals/xml-element-literal.md)」を参照してください。  
  
## <a name="rules"></a>ルール  
 Visual Basic での要素または属性のローカル名は、次の規則に従う必要があります。  
  
- 名前空間で始めることができます。 先頭は英文字またはアンダースコア (`_`) にする必要があります。  
  
- アルファベット文字、10 進数字、アンダースコア、ピリオド (.)、ハイフン (-) のみを含める必要があります。  
  
- 文字の長さは 1,024 文字以内とする必要があります。  
  
- 名前に表示されるコロンは、名前空間の境界を示します。 したがって、コロンを使用できるのは、特定の名前の XML 名前空間を指定する場合のみとなります。  
  
 さらに、次のガイドラインに従う必要があります。  
  
- XML 1.0 仕様では、文字列 "xml" の大文字小文字のどのバリエーションで始まる名前もすべて予約されています。 したがって、要素名と属性名にはこれらの名前を使用しないでください。  
  
### <a name="name-length-guidelines"></a>名前の長さのガイドライン  
 現実問題として、名前は、可能な限り短くしながらも、要素の性質を明確に特定するものにする必要があります。 これにより、コードの読みやすさが向上し、行の長さとソース ファイルのサイズが減少します。  
  
 ただし、要素について、またコードでのその使用方法について適切に説明できないような短い名前にはしないでください。 これはコードの読みやすさのために重要です。 他の誰かが理解しようとするとき、または自分自身がそれを記述して長い時間が経過してからそれを見た場合に、適切な要素名であれば時間を節約できます。  
  
## <a name="case-sensitivity-in-names"></a>名前の大文字と小文字の区別  
 XML 要素名では大文字と小文字が区別されます。 つまり、英字の大文字と小文字の違いしかない 2 つの名前を比較した場合、Visual Basic コンパイラではそれらを異なる名前と解釈します。 たとえば、`ABC` と `abc` は別々の要素を示していると解釈されます。  
  
## <a name="xml-namespaces"></a>XML 名前空間  
 XML 要素リテラルを作成するときに、要素名に XML 名前空間プレフィックスを指定できます。 詳細については、「[XML 要素リテラル](../../../language-reference/xml-literals/xml-element-literal.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic での XML の作成](creating-xml.md)
- [XML 要素リテラル](../../../language-reference/xml-literals/xml-element-literal.md)
