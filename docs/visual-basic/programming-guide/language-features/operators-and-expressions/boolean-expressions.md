---
title: Boolean 式
ms.date: 07/20/2015
helpviewer_keywords:
- short-circuiting
- Boolean expressions
- logical operators [Visual Basic], Boolean expressions
- expressions [Visual Basic], Boolean
- expression evaluation [Visual Basic], Boolean expressions
- operators [Visual Basic], short-circuiting
- Visual Basic code, operators
- short-circuit evaluation
- logical operators [Visual Basic], short-circuiting
- operators [Visual Basic], Boolean
- Visual Basic code, expressions
ms.assetid: d3d90406-55c8-4404-8143-50fd7f0d0d1a
ms.openlocfilehash: 8d34eb4c8b14bb4754f2a3cf5b6f9a7601aa4662
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388959"
---
# <a name="boolean-expressions-visual-basic"></a>Boolean 式 (Visual Basic)
*ブール式*は、[ブール データ型](../../../language-reference/data-types/boolean-data-type.md) (`True` または `False`) の値に評価される式です。 `Boolean` 式では、複数の形式を使用できます。 最もシンプルなのは、次の例に示すように、`Boolean` 変数の値を `Boolean` リテラルに対して直接比較することです。  
  
 [!code-vb[VbVbalrOperators#87](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#87)]  
  
## <a name="two-meanings-of-the--operator"></a>= 演算子の 2 つの意味  
 代入ステートメント `newCustomer = True` は、前の例の式と同じように見えますが、別の関数を実行し、使い方が異なります。 前の例では、式 `newCustomer = True` はブール値を表し、`=` 記号は比較演算子として解釈されます。 スタンドアロン ステートメントでは、`=` 記号は代入演算子として解釈され、右側の値が左側の変数に代入されます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#88](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#88)]  
  
 詳細については、「[値の比較](value-comparisons.md)」と「[ステートメント](../../../language-reference/statements/index.md)」を参照してください。  
  
## <a name="comparison-operators"></a>比較演算子  
 `=`、`<`、`>`、`<>`、`<=`、`>=` などの比較演算子によって、演算子の左側の式が演算子の右側の式と比較され、結果が `True` または `False` として評価されることによって、ブール式が生成されます。 次の例を使って説明します。  
  
 `42 < 81`  
  
 42 は 81 未満であるため、前の例のブール式は `True` に評価されます。 この種類の式の詳細については、「[値の比較](value-comparisons.md)」を参照してください。  
  
### <a name="comparison-operators-combined-with-logical-operators"></a>論理演算子と組み合わせた比較演算子  
 論理演算子を使用して比較式を組み合わせると、より複雑なブール式を生成できます。 次の例では、論理演算子と共に比較演算子を使用する方法を示しています。  
  
 `x > y And x < 1000`  
  
 前の例では、式全体の値は、`And` 演算子の両側の式の値によって決まります。 両方の式が `True` である場合、式全体が `True` に評価されます。 いずれかの式が `False` である場合、式全体が `False` に評価されます。  
  
## <a name="short-circuiting-operators"></a>ショートサーキット演算子  
 論理演算子 `AndAlso` および `OrElse` では、*ショートサーキット*と呼ばれる動作が見られます。 ショートサーキット演算子では、左オペランドが最初に評価されます。 左オペランドで式全体の値が判断された場合、右の式を評価せずにプログラムの実行が続行されます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#89](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#89)]  
  
 前の例では、演算子によって左の式 `45 < 12` が評価されます。 左の式は `False` に評価されるため、論理式全体が `False` に評価される必要があります。 このため、プログラムの実行では、右の式 `testFunction(3)` が評価されることなく、`If` ブロック内のコードの実行がスキップされます。 この例では、左の式によって式全体が False とされたため、`testFunction()` は呼び出されません。  
  
 同様に、`OrElse` を使用する論理式の左の式が `True` に評価された場合、左の式で式全体が既に検証済みであるため、右の式が評価されずに、次のコード行に実行が進みます。  
  
### <a name="comparison-with-non-short-circuiting-operators"></a>非ショートサーキット演算子との比較  
 一方、論理演算子 `And` と `Or` が使用された場合、論理演算子の両側が評価されます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#90](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#90)]  
  
 前の例では、左の式が `False` に評価されても `testFunction()` が呼び出されます。  
  
## <a name="parenthetical-expressions"></a>かっこで囲まれた式  
 かっこを使用して、ブール式の評価順序を制御できます。 かっこで囲まれた式は最初に評価されます。 複数レベルの入れ子の場合は、最も深い入れ子になった式が優先されます。 かっこ内では、演算子の優先順位のルールに従って、評価が行われます。 詳細については、「[Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)
- [値の比較](value-comparisons.md)
- [ステートメント](../statements.md)
- [比較演算子](../../../language-reference/operators/comparison-operators.md)
- [演算子の効率のよい組み合わせ](efficient-combination-of-operators.md)
- [Visual Basic における演算子の優先順位](../../../language-reference/operators/operator-precedence.md)
- [Boolean データ型](../../../language-reference/data-types/boolean-data-type.md)
