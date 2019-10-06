---
title: '\ 演算子 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.\
- '\'
helpviewer_keywords:
- division operator [Visual Basic], integer
- integer division operator [Visual Basic]
- zero, division by zero
- arithmetic operators [Visual Basic], division
- division [Visual Basic], by zero
- backslash (\) [Visual Basic]
- '\ operator [Visual Basic]'
- integer quotient
- math operators [Visual Basic]
- quotients, integer
- truncation [Visual Basic], integer division
ms.assetid: 4b0ee347-950c-45c9-8e23-54bc85df208e
ms.openlocfilehash: d1a46f99c21be007d33361ba095a3f0c52fe906c
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701147"
---
# <a name="-operator-visual-basic"></a>\ 演算子 (Visual Basic)
2つの数値を除算し、整数の結果を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
expression1 \ expression2  
```  
  
## <a name="parts"></a>指定項目  
 `expression1`  
 必須。 任意の数式。  
  
 `expression2`  
 必須。 任意の数式。  
  
## <a name="supported-types"></a>サポートされている型  
 符号なしの型および浮動小数点型およびを`Decimal`含む、すべての数値型。  
  
## <a name="result"></a>結果  
 結果は、剰余を破棄し`expression1` 、整数`expression2`部分のみを保持する、で除算した整数の商です。 これは*切り捨て*と呼ばれます。  
  
 結果のデータ型は、および`expression1` `expression2`のデータ型に適した数値型です。 「[演算子の結果のデータ型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)」の「整数演算」の表を参照してください。  
  
 [/演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)は、小数部の剰余を保持する完全な商を返します。  
  
## <a name="remarks"></a>コメント  
 除算を実行する前に、Visual Basic 浮動小数点数値式をに`Long`変換しようとしています。 `Option Strict` が`On`の場合は、コンパイラエラーが発生します。 が`Option Strict` <xref:System.OverflowException> の場合、値が [Long データ型](../../../visual-basic/language-reference/data-types/long-data-type.md)の範囲外の場合は、を指定できます。 `Off` @No__t-0 への変換は、銀行型*丸めの*対象にもなります。 詳細については、「[型変換関数](../../../visual-basic/language-reference/functions/type-conversion-functions.md)」の「小数部」を参照してください。  
  
 また`expression1`は`expression2`が[Nothing](../../../visual-basic/language-reference/nothing.md)に評価される場合、0として扱われます。  
  
## <a name="attempted-division-by-zero"></a>0による除算を試行しました  
 が`expression2` 0 に評価され`\`た場合、 <xref:System.DivideByZeroException>演算子は例外をスローします。 これは、オペランドのすべての数値データ型に当てはまります。  
  
> [!NOTE]
> @No__t-0 演算子は*オーバーロード*できます。つまり、クラスまたは構造体がそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では`\` 、演算子を使用して、整数除算を実行します。 結果は、2つのオペランドの整数の商を表す整数で、残りの部分は破棄されます。  
  
 [!code-vb[VbVbalrOperators#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#18)]  
  
 前の例の式では、それぞれ2、3、33、および-22 の値が返されます。  
  
## <a name="see-also"></a>関連項目

- [\\ = 演算子](../../../visual-basic/language-reference/operators/integer-division-assignment-operator.md)
- [/演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-operator.md)
- [Option Strict ステートメント](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [算術演算子](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の算術演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
