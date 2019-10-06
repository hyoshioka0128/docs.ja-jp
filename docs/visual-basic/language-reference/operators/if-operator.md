---
title: If 演算子 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.IfOperator
- IfOperator
helpviewer_keywords:
- ternary operators [Visual Basic]
- conditional execution
- If expressions [Visual Basic]
- conditional operator [Visual Basic]
- If Operator [Visual Basic]
ms.assetid: dd56c9df-7cd4-442c-9ba6-20c70ee44c8f
ms.openlocfilehash: 244c0598c65ba691decc09c36293799571211a40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701151"
---
# <a name="if-operator-visual-basic"></a>If 演算子 (Visual Basic)
は、ショートサーキット評価を使用して、条件に応じて2つの値のいずれかを返します。 @No__t-0 演算子は、3つの引数または2つの引数を指定して呼び出すことができます。  
  
## <a name="syntax"></a>構文  
  
```vb  
If( [argument1,] argument2, argument3 )  
```  
  
## <a name="if-operator-called-with-three-arguments"></a>3つの引数を指定して演算子が呼び出された場合  
 3つの引数を使用して `If` が呼び出された場合、1番目の引数は @no__t としてキャストできる値に評価される必要があります。 この `Boolean` の値によって、他の2つの引数のどちらが評価され、返されるかが決まります。 次の一覧は、3つの引数を使用して @no__t 0 演算子が呼び出された場合にのみ適用されます。  
  
## <a name="parts"></a>指定項目  
  
|項目|定義|  
|---|---|  
|`argument1`|必須。 `Boolean`。 他のどの引数を評価して返すかを決定します。|  
|`argument2`|必須。 `Object`。 @No__t-0 が `True` と評価された場合に評価され、返されます。|  
|`argument3`|必須。 `Object`。 @No__t-0 が `False` と評価された場合、または `argument1` が[Nothing](../../../visual-basic/language-reference/nothing.md)に評価される[null 許容](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)の `Boolean` 変数である場合に評価され、返されます。|  
  
 3つの引数を使用して呼び出される @no__t 0 演算子は、ショートサーキット評価を使用する点を除いて、`IIf` 関数と同様に機能します。 @No__t 0 関数は常に3つの引数すべてを評価しますが、3つの引数を持つ `If` 演算子は、そのうち2つだけを評価します。 最初の `If` 引数が評価され、結果は `Boolean` 値、`True` または `False` としてキャストされます。 値が `True` の場合、`argument2` が評価され、その値が返されますが、`argument3` は評価されません。 @No__t-0 式の値が-1 @no__t の場合、`argument3` が評価され、その値が返されますが、`argument2` は評価されません。 次の例では、3つの引数を使用する場合の `If` の使用方法を示します。  
  
 [!code-vb[VbVbalrOperators#100](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#100)]  
  
 次の例は、ショートサーキット評価の値を示しています。 この例では、変数 `number` を変数 @no__t 除算する2回の試行を示しています。ただし、`divisor` が0の場合を除きます。 この場合、0が返されます。実行時エラーが発生するため、除算を行わないでください。 @No__t-0 式ではショートサーキット評価が使用されるため、最初の引数の値に応じて、2番目または3番目の引数のいずれかが評価されます。 最初の引数が true の場合、除数はゼロではなく、2番目の引数を評価して除算を実行しても安全です。 最初の引数が false の場合は、3番目の引数のみが評価され、0が返されます。 したがって、除数が0の場合、除算は実行されず、エラーも発生しません。 ただし、`IIf` ではショートサーキット評価が使用されないため、最初の引数が false の場合でも2番目の引数が評価されます。 これにより、実行時の0除算エラーが発生します。  
  
 [!code-vb[VbVbalrOperators#101](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#101)]  
  
## <a name="if-operator-called-with-two-arguments"></a>2つの引数を指定して演算子が呼び出された場合  
 @No__t-0 の最初の引数は省略できます。 これにより、2つの引数のみを使用して演算子を呼び出すことができます。 次の一覧は、`If` 演算子が2つの引数を指定して呼び出された場合にのみ適用されます。  
  
## <a name="parts"></a>指定項目  
  
|項目|定義|  
|---|---|  
|`argument2`|必須。 `Object`。 参照または null 許容型である必要があります。 評価され、`Nothing` 以外に評価されたときに返されます。|  
|`argument3`|必須。 `Object`。 @No__t-0 が `Nothing` と評価された場合に評価され、返されます。|  
  
 @No__t-0 引数を省略した場合、最初の引数は参照または null 許容型である必要があります。 最初の引数が `Nothing` に評価された場合、2番目の引数の値が返されます。 それ以外の場合は、最初の引数の値が返されます。 次の例は、この評価のしくみを示しています。  
  
 [!code-vb[VbVbalrOperators#102](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class4.vb#102)]  
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.IIf%2A>
- [null 許容値型](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- [Nothing](../../../visual-basic/language-reference/nothing.md)
