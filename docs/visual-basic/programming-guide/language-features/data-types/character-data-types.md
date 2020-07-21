---
title: 文字データ型
ms.date: 07/20/2015
helpviewer_keywords:
- data types [Visual Basic], character
- String data type [Visual Basic], character data types
- character data types [Visual Basic]
- Char data type [Visual Basic], character data types
- data types [Visual Basic], choosing
ms.assetid: 902479ef-1679-47fc-9911-0c1c5008226c
ms.openlocfilehash: 33dd4c62776ae8c5ec0ce0a6d0858a7ed0d047fb
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401993"
---
# <a name="character-data-types-visual-basic"></a>文字データ型 (Visual Basic)
Visual Basic には、印刷や表示が可能な文字を処理するための "*文字データ型*" が用意されています。 どちらも Unicode 文字を処理しますが、`Char` は 1 つの文字を保持するのに対し、`String` は不特定数の文字を含みます。  
  
 Visual Basic データ型を並べて比較している表を、[データ型](../../../language-reference/data-types/index.md)に関するページで参照してください。  
  
## <a name="char-type"></a>Char 型  
 `Char` データ型は、1 つの 2 バイト (16 ビット) Unicode 文字です。 常に変数が厳密に 1 つの文字を格納する場合は、`Char` として宣言します。 次に例を示します。  
  
 [!code-vb[VbVbalrCharTypes#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrchartypes/vb/module1.vb#1)]
  
 `Char` または `String` 変数に含めることができる値は、"*コード ポイント*"、つまり Unicode 文字セットの文字コードです。 Unicode 文字には、基本的な ASCII 文字セット、その他のさまざまなアルファベット文字、アクセント記号、通貨記号、分数、分音記号、数学記号、および技術用記号が含まれます。  
  
> [!NOTE]
> Unicode 文字セットでは、"*サロゲート ペア*" (1 つのコード ポイントを表すために 2 つの 16 ビット値を必要とする) のためにコード ポイント D800 から DFFF (10 進数では 55296 から 55551) が予約されています。 `Char` 変数はサロゲート ペアを保持できません。`String` は 2 つの位置を使用してこのようなペアを保持します。  
  
 詳細については、「[文字型 (Char)](../../../language-reference/data-types/char-data-type.md)」を参照してください。  
  
## <a name="string-type"></a>文字列の種類  
 `String` データ型は、0 個以上の 2 バイト (16 ビット) Unicode 文字のシーケンスです。 変数が不特定数の文字を含む可能性がある場合は、`String` として宣言します。 次に例を示します。  
  
 [!code-vb[VbVbalrCharTypes#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalrchartypes/vb/module1.vb#2)]
  
 詳細については、「[文字列型 (String)](../../../language-reference/data-types/string-data-type.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [基本データ型](elementary-data-types.md)
- [複合データ型](composite-data-types.md)
- [Generic Types in Visual Basic](generic-types.md)
- [Value Types and Reference Types](value-types-and-reference-types.md)
- [Visual Basic における型変換](type-conversions.md)
- [トラブルシューティング (データ型)](troubleshooting-data-types.md)
- [型文字](type-characters.md)
