---
title: '\ 演算子'
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
ms.openlocfilehash: 1f8095afc5f096928b946607adc715af49827022
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370883"
---
# <a name="-operator-visual-basic"></a>\ 演算子 (Visual Basic)
2 つの数値の商を計算し、結果を整数で返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
expression1 \ expression2  
```  
  
## <a name="parts"></a>指定項目  
 `expression1`  
 必須です。 任意の数式。  
  
 `expression2`  
 必須です。 任意の数式。  
  
## <a name="supported-types"></a>サポートされている型  
 すべての数値型。これには、符号なしおよび浮動小数点型と `Decimal` が含まれます。  
  
## <a name="result"></a>結果  
 結果は、`expression1` を `expression2` で除算した整数の商で、小数部分はすべて破棄され、整数部分のみ保持されます。 これは "*切り捨て*" と呼ばれます。  
  
 結果のデータ型は `expression1` および `expression2` のデータ型に適した数値型になります。 「[演算子の結果のデータ型](data-types-of-operator-results.md)」の「整数演算」の表を参照してください。  
  
 [/演算子 (Visual Basic)](floating-point-division-operator.md) は、小数部分の剰余を保持する完全な商を返します。  
  
## <a name="remarks"></a>Remarks  
 除算を実行する前に、Visual Basic は浮動小数点数値式を `Long` に変換しようとします。 `Option Strict` が `On` の場合は、コンパイラ エラーが発生します。 `Option Strict` が `Off` の場合、値が [Long データ型](../data-types/long-data-type.md)の範囲外の場合は <xref:System.OverflowException> が発生する可能性があります。 `Long` への変換は、"*銀行型丸め*" の対象にもなります。 詳細については、「[データ型変換関数](../functions/type-conversion-functions.md)」の「小数部」を参照してください。  
  
 `expression1` または `expression2` が [Nothing](../nothing.md) に評価される場合、0 として扱われます。  
  
## <a name="attempted-division-by-zero"></a>0 除算を試行した場合  
 `expression2` が 0 に評価される場合、`\` 演算子は <xref:System.DivideByZeroException> 例外をスローします。 これは、オペランドのすべての数値データ型に当てはまります。  
  
> [!NOTE]
> `\` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`\` 演算子を使用して整数除算を実行します。 結果は、2 つのオペランドの整数商を表す整数で、剰余は破棄されます。  
  
 [!code-vb[VbVbalrOperators#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#18)]  
  
 上の例の式では、それぞれ 2、3、33、-22 の値が返されます。  
  
## <a name="see-also"></a>関連項目

- [\\= 演算子](integer-division-assignment-operator.md)
- [/ 演算子 (Visual Basic)](floating-point-division-operator.md)
- [Option Strict ステートメント](../statements/option-strict-statement.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
