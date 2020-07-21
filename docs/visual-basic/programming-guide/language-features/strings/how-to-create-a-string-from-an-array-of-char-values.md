---
title: '方法: Char 値の配列から文字列を作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- examples [Visual Basic], arrays
- examples [Visual Basic], Char data type
ms.assetid: 69f94e85-d57c-4ccc-a62a-426e829f5c5e
ms.openlocfilehash: d9ec897467f0caac0afc089a028516c0316a2bda
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410594"
---
# <a name="how-to-create-a-string-from-an-array-of-char-values-visual-basic"></a>方法: 方法: char 値の配列から文字列を作成する (Visual Basic)
この例では、個々の文字から文字列 "abcd" を作成します。  
  
## <a name="example"></a>例  
 [!code-vb[VbVbalrStrings#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#61)]  
  
## <a name="compile-the-code"></a>コードのコンパイル  
 このメソッドには特別な要件はありません。  
  
 引用符で囲まれた単一の文字の後に単一の `c` が続く構文 `"a"c` を使用して、文字リテラルが作成されます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 文字列に null 文字 (`Chr(0)` に相当) が含まれていると、文字列を使用したときに予期しない結果が生じます。 文字列に nulll 文字を含めることはできますが、状況によっては、nulll 文字に続く文字が表示されなくなります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.String>
- [Char データ型](../../../language-reference/data-types/char-data-type.md)
- [データの種類](../data-types/index.md)
