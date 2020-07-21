---
title: '方法: 文字列の文字にアクセスする'
ms.date: 07/20/2015
helpviewer_keywords:
- strings [Visual Basic], accessing characters
- characters [Visual Basic], accessing in strings
ms.assetid: 02c5206c-ffab-494d-b648-3b2ea358dc34
ms.openlocfilehash: fa5920cfd25f61f6e6c7d5438ef7c0e38a48fa1e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401954"
---
# <a name="how-to-access-characters-in-strings-in-visual-basic"></a>方法: Visual Basic で文字列の文字にアクセスする
この例では、<xref:System.String.Chars%2A> プロパティを使用して、文字列内の指定された位置にある文字にアクセスする方法を示します。  
  
## <a name="example"></a>例  
 文字列の文字と文字列内でのそれらの文字の位置に関するデータがあると便利な場合があります。 文字列は文字 (`Char` インスタンス) の配列と考えることができます。<xref:System.String.Chars%2A> プロパティを使用して特定の文字のインデックスを参照することによって、その文字を取得できます。  
  
 [!code-vb[VbVbalrStrings#49](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#49)]  
  
 <xref:System.String.Chars%2A> プロパティの `index` パラメーターは 0 から始まります。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 <xref:System.String.Chars%2A> プロパティは、指定された位置の文字を返します。 ただし、一部の Unicode 文字は複数の文字で表すことができます。 Unicode 文字を操作する方法の詳細については、[文字列を文字の配列に変換する方法](how-to-convert-a-string-to-an-array-of-characters.md)に関する記事をご覧ください。  
  
 <xref:System.String.Chars%2A> プロパティは、`index` パラメーターが文字列の長さ以上である場合、またはゼロ未満の場合に、<xref:System.IndexOutOfRangeException> 例外をスローします。  
  
## <a name="see-also"></a>関連項目

- <xref:System.String.Chars%2A>
- [方法: 文字列を文字の配列に変換する](how-to-convert-a-string-to-an-array-of-characters.md)
- [Visual Basic で、文字列型とその他のデータ型との変換を行う](converting-between-strings-and-other-data-types.md)
- [文字列](index.md)
