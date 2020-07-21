---
title: 論理演算子とビット処理演算子
ms.date: 07/20/2015
helpviewer_keywords:
- short-circuiting
- Boolean expressions
- logical operators [Visual Basic], Boolean expressions
- operators [Visual Basic], logical
- AndAlso operator [Visual Basic]
- Not operator [Visual Basic], Boolean expressions
- Xor operator [Visual Basic], Boolean expressions
- And operator [Visual Basic], logical operators
- logical operators [Visual Basic]
- expressions [Visual Basic], Boolean
- Or operator [Visual Basic], logical operators
- Visual Basic code, operators
- short-circuiting [Visual Basic], logical operators
- logical operators [Visual Basic], short-circuiting
- Visual Basic code, expressions
- logical operators [Visual Basic], binary
- OrElse operator [Visual Basic]
- logical operators [Visual Basic], unary
ms.assetid: ca474e13-567d-4b1d-a18b-301433705e57
ms.openlocfilehash: 19d3511363f19319c2bd8ce872b62c1462b1370f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403409"
---
# <a name="logical-and-bitwise-operators-in-visual-basic"></a>Visual Basic の論理演算子とビット処理演算子
論理演算子を使用すると、`Boolean` 式を比較し、`Boolean` の結果を返すことができます。 `And`、`Or`、`AndAlso`、`OrElse`、および `Xor` の各演算子は、2 つのオペランドを受け取るため、"*二項*" です。`Not` 演算子は、1 つのオペランドを受け取るため、"*単項*" です。 これらの演算子の一部を使用して、整数値に対してビットごとの論理演算を実行することもできます。  
  
## <a name="unary-logical-operator"></a>単項論理演算子  
 [Not 演算子](../../../language-reference/operators/not-operator.md)を使用すると、`Boolean` 式に対して論理的な "*否定*" を実行できます。 これにより、そのオペランドの反対の論理値が生成されます。 式が `True` に評価される場合、`Not` からは `False` が返されます。式が `False` に評価される場合、`Not` からは `True` が返されます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#77](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#77)]  
  
## <a name="binary-logical-operators"></a>二項論理演算子  
 [And 演算子](../../../language-reference/operators/and-operator.md)を使用すると、2 つの `Boolean` 式に対して "*論理積*" を実行できます。 両方の式が `True` に評価される場合、`And` からは `True` が返されます。 式の少なくとも 1 つが `False` に評価される場合、`And` からは `False` が返されます。  
  
 [Or 演算子](../../../language-reference/operators/or-operator.md)を使用すると、2 つの `Boolean` 式に対して "*論理和*" または "*論理包含*" を実行できます。 いずれかの式が `True` に評価されるか、または両方が `True` に評価される場合、`Or` からは `True` が返されます。 どちらの式も `True` に評価されない場合、`Or` からは `False` が返されます。  
  
 [Xor 演算子](../../../language-reference/operators/xor-operator.md)を使用すると、2 つの `Boolean` 式に対して "*排他的論理和*" を実行できます。 両方ではなく 1 つの式のみが `True` に評価される場合、`Xor` からは `True` が返されます。 両方の式が `True` に評価されるか、両方が `False` に評価される場合、`Xor` からは `False` が返されます。  
  
 次の例は、`And`、`Or`、および `Xor` の各演算子を示しています。  
  
 [!code-vb[VbVbalrOperators#78](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#78)]  
  
## <a name="short-circuiting-logical-operations"></a>短絡論理演算  
 [AndAlso 演算子](../../../language-reference/operators/andalso-operator.md)を使用すると、2 つの `Boolean` 式に対して論理積も実行されるという点で、`And` 演算子とよく似ています。 この 2 つの主な違いは、`AndAlso` が "*短絡*" 動作を示すことです。 `AndAlso` 式の 1 つ目の式が `False` に評価される場合、最終結果を変更できないため、2 つ目の式は評価されず、`AndAlso` からは `False` が返されます。  
  
 同様に、[OrElse 演算子](../../../language-reference/operators/orelse-operator.md)を使用すると、2 つの `Boolean` 式に対して短絡論理和を実行できます。 `OrElse` 式の 1 つ目の式が `True` に評価される場合、最終結果を変更できないため、2 つ目の式は評価されず、`OrElse` からは `True` が返されます。  
  
### <a name="short-circuiting-trade-offs"></a>短絡のトレードオフ  
 短絡を使用すると、論理演算の結果を変更できない式が評価されないため、パフォーマンスを向上させることができます。 ただし、その式で追加のアクションが実行される場合、短絡によってそれらのアクションはスキップされます。 たとえば、式に `Function` プロシージャへの呼び出しが含まれている場合、式が短絡されると、そのプロシージャは呼び出されず、`Function` に含まれる追加のコードは実行されません。 そのため、この関数はたまにしか実行されず、正しくテストされない可能性があります。 また、プログラム ロジックは `Function` のコードに依存する場合があります。  
  
 次の例は、`And`、`Or`、およびそれらに対応する短絡演算の違いを示しています。  
  
 [!code-vb[VbVbalrOperators#81](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#81)]  
  
 [!code-vb[VbVbalrOperators#80](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#80)]  
  
 [!code-vb[VbVbalrOperators#79](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#79)]  
  
 前の例では、呼び出しが短絡されると、`checkIfValid()` 内の一部の重要なコードが実行されないことに注意してください。 `12 > 45` から `False` が返される場合でも、1 つ目の `If` ステートメントでは `checkIfValid()` が呼び出されます。これは、`And` では短絡が実行されないためです。 2 つ目の `If` ステートメントでは `checkIfValid()` が呼び出されません。これは、`12 > 45` から `False` が返されると、`AndAlso` によって 2 つ目の式が短絡されるためです。 `12 < 45` から `True` が返される場合でも、3 つ目の `If` ステートメントでは `checkIfValid()` が呼び出されます。これは、`Or` では短絡が実行されないためです。 4 つ目の `If` ステートメントでは `checkIfValid()` が呼び出されません。これは、`12 < 45` から `True` が返されると、`OrElse` によって 2 つ目の式が短絡されるためです。  
  
## <a name="bitwise-operations"></a>ビットごとの演算  
 ビットごとの演算では、2 つの整数値がバイナリ (base 2) 形式で評価されます。 対応する位置にあるビットが比較され、比較に基づいて値が割り当てられます。 `And` 演算子の例を次に示します。  
  
 [!code-vb[VbVbalrConcepts#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrConcepts/VB/Class1.vb#2)]  
  
 前の例では、`x` の値を 1 に設定しています。 これは次の理由によるものです。  
  
- 値はバイナリとして扱われます。  
  
     バイナリ形式の 3 = 011  
  
     バイナリ形式の 5 = 101  
  
- `And` 演算子を使用すると、バイナリ表現を一度に 1 つのバイナリ位置 (ビット) ずつ比較できます。 特定の位置の両方のビットが 1 の場合、結果のその位置に 1 が配置されます。 いずれかのビットが 0 の場合、結果のその位置に 0 が配置されます。 前の例では、これは次のように機能します。  
  
     011 (バイナリ形式の 3)  
  
     101 (バイナリ形式の 5)  
  
     001 (バイナリ形式の結果)  
  
- 結果は 10 進として扱われます。 値 001 は 1 のバイナリ表現であるため、`x` = 1 です。  
  
 ビットごとの `Or` 演算は似ていますが、比較されるビットのいずれか、または両方が 1 の場合、結果ビットに 1 が割り当てられる点が異なります。 `Xor` を使用すると、比較されたビットの (両方ではなく) いずれかが 1 の場合、結果ビットに 1 が割り当てられます。 `Not` を使用すると、1 つのオペランドを受け取り、符号ビットを含むすべてのビットが反転され、その値が結果に割り当てられます。 つまり、符号付き正数の場合、`Not` からは常に負の値が返され、負数の場合、`Not` からは常に正または 0 の値が返されます。  
  
 `AndAlso` 演算子と `OrElse` 演算子はビットごとの演算をサポートしていません。  
  
> [!NOTE]
> ビットごとの演算は、整数型に対してのみ実行できます。 ビットごとの演算を進める前に、浮動小数点値を整数型に変換する必要があります。  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](../../../language-reference/operators/logical-bitwise-operators.md)
- [ブール式](boolean-expressions.md)
- [Visual Basic における算術演算子](arithmetic-operators.md)
- [Visual Basic における比較演算子](comparison-operators.md)
- [Visual Basic の連結演算子](concatenation-operators.md)
- [演算子の効率のよい組み合わせ](efficient-combination-of-operators.md)
