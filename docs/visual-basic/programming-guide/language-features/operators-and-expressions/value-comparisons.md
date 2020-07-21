---
title: 値の比較
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], comparing values
- Visual Basic code, operators
- Visual Basic code, expressions
- comparison operators [Visual Basic], comparing expressions
- numeric expressions
- operators [Visual Basic], comparison
- expressions [Visual Basic], comparing
ms.assetid: 60da0c76-9458-4afc-97e9-44a7939c064c
ms.openlocfilehash: 01816b5730cf4fda61f1737ce3ce00ab82f57da8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403396"
---
# <a name="value-comparisons-visual-basic"></a>値の比較 (Visual Basic)
比較演算子を使用すると、数値変数の値を比較する式を作成できます。 これらの式では、比較が true であるか false であるかに基づいて、`Boolean` 値が返されます。 このような式の例を次に示します。  
  
 `45 > 26`  
  
 `26 > 45`  
  
 最初の式は、45 が 26 より大きいため、`True` に評価されます。 2 番目の例は、26 が 45 より大きくないため、`False` に評価されます。  
  
 この方式で、数値式を比較することもできます。 次の例のように、比較する式自体を複合式にすることができます。  
  
 `x / 45 * (y +17) >= System.Math.Sqrt(z) / (p - (x * 16))`  
  
 前の複合式には、リテラル、変数、および関数呼び出しが含まれています。 比較演算子の両側の式が評価され、次に、結果の値が `>=` 比較演算子を使用して比較されます。 左側の式の値が、右側の式の値以上である場合、式全体が `True` に評価されます。それ以外の場合は、`False` に評価されます。  
  
 値を比較する式は、次の例に示すように、`If...Then` 構造で最もよく使用されます。  
  
 [!code-vb[VbVbalrOperators#84](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#84)]  
  
 `=` 記号は、比較演算子でもあり、代入演算子でもあります。 次の例に示すように、比較演算子として使用すると、左側の値が右側の値と等しいかどうかが評価されます。  
  
 [!code-vb[VbVbalrOperators#85](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#85)]  
  
 `If`、`While`、`Loop`、または `ElseIf` ステートメント内などの `Boolean` 値が必要な任意の場所や、`Boolean` 変数に値を代入したり渡したりする場合に、比較式を使用することもできます。 次の例では、比較式によって返される値が `Boolean` 変数に代入されています。  
  
 [!code-vb[VbVbalrOperators#86](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#86)]  
  
## <a name="see-also"></a>関連項目

- [ブール式](boolean-expressions.md)
- [演算子および式](index.md)
- [Visual Basic における比較演算子](comparison-operators.md)
- [方法: 数値を計算する](how-to-calculate-numeric-values.md)
- [Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)
