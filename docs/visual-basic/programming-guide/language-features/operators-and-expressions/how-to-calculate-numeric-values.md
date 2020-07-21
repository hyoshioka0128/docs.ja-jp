---
title: '方法: 数値を計算する'
ms.date: 07/20/2015
helpviewer_keywords:
- operator precedence
- operators [Visual Basic]
- expressions [Visual Basic], numeric
- calculations [Visual Basic], numeric expressions
- precedence [Visual Basic], of operators
- Visual Basic code, operators
- Visual Basic code, expressions
- numeric expressions
ms.assetid: ba6bf43d-bd96-49b8-b1de-4a7797551372
ms.openlocfilehash: 94b02693f308dcfcfa6983f2750a26d9d419f7be
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403460"
---
# <a name="how-to-calculate-numeric-values-visual-basic"></a>方法: 数値を計算する (Visual Basic)
数式を使用して数値を計算できます。 *数式*は、数値を表すリテラル、定数、変数、およびそれらの値に対して作用する演算子を含む式です。  
  
## <a name="calculating-numeric-values"></a>数値の計算  
  
#### <a name="to-calculate-a-numeric-value"></a>数値を計算するには  
  
- 1 つ以上の数値リテラル、定数、および変数を数式に組み合わせます。 次の例に、有効な数式をいくつか示します。  
  
     `93.217`  
  
     `System.Math.PI`  
  
     `counter`  
  
     `4 * (67 + i)`  
  
     最初の 3 行は、リテラル、定数、および変数を示しています。 それぞれがそれだけで有効な数式を形成しています。 最後の行は、2 つのリテラルを含む変数の組み合わせを示しています。  
  
     数式では、それだけで完全な Visual Basic ステートメントを形成するわけではないことに注意してください。 式は、完全なステートメントの一部として使用する必要があります。  
  
#### <a name="to-store-a-numeric-value"></a>数値を格納するには  
  
- 次の例に示すように、代入ステートメントを使用して、数式で表される値を変数に代入することができます。  
  
     [!code-vb[VbVbalrOperators#82](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#82)]  
  
     前の例では、等号演算子 (`=`) の右側にある式の値が、演算子の左側にある変数 `j` に代入されているため、`j` は 276 に評価されます。  
  
     詳細については、「[ステートメント](../../../language-reference/statements/index.md)」を参照してください。  
  
## <a name="multiple-operators"></a>複数の演算子  
 数式に複数の演算子が含まれている場合、それらが評価される順序は、演算子の優先順位のルールによって決まります。 演算子の優先順位のルールをオーバーライドするには、上の例のように、式をかっこで囲みます。囲まれた式は、最初に評価されます。  
  
#### <a name="to-override-normal-operator-precedence"></a>通常の演算子の優先順位をオーバーライドするには  
  
- かっこを使用して、最初に実行させる演算を囲みます。 次の例は、同じオペランドと演算子による 2 つの異なる結果を示しています。  
  
     [!code-vb[VbVbalrOperators#83](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#83)]  
  
     前の例では、`j` の計算で加算演算子 (`+`) が最初に実行されます。これは、`(67 + i)` を囲むかっこによって、通常の優先順位がオーバーライドされるためであり、`j` に代入される値は 276 (69 の 4 倍) になります。 `k` の計算では、通常の優先順位 (`+` の前に `*`) で演算子が実行されるので、`k` に代入される値は 270 (268 + 2) になります。  
  
     詳細については、「[Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [演算子および式](index.md)
- [値の比較](value-comparisons.md)
- [ステートメント](../../../language-reference/statements/index.md)
- [Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)
- [算術演算子](../../../language-reference/operators/arithmetic-operators.md)
- [演算子の効率のよい組み合わせ](efficient-combination-of-operators.md)
