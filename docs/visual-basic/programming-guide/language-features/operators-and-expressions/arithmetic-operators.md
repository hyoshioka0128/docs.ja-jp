---
title: 算術演算子
ms.date: 07/20/2015
helpviewer_keywords:
- type safety
- operators [Visual Basic], bitwise
- operators [Visual Basic], bit-shift
- bitwise operators [Visual Basic]
- bit-shift operators [Visual Basic]
- zero, division by zero
- operators [Visual Basic], arithmetic
- division [Visual Basic], by zero
- Visual Basic code, operators
- arithmetic operators [Visual Basic], about arithmetic operators
ms.assetid: 325dac7a-ea4f-41d5-8b48-f6e904211569
ms.openlocfilehash: d5f79f3e45fc887dcb32c959f04703253ade198c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84389037"
---
# <a name="arithmetic-operators-in-visual-basic"></a>Visual Basic における算術演算子
算術演算子は、リテラル、変数、その他の式、関数およびプロパティの呼び出し、および定数によって表される数値の計算に関連する一般的な算術演算の多くを実行するために使用されます。 また、算術演算子で分類されるのはビット シフト演算子です。これは、オペランドの個々のビットのレベルで機能し、ビット パターンを左または右にシフトします。  
  
## <a name="arithmetic-operations"></a>算術演算  
 次の例に示すように、[+ 演算子](../../../language-reference/operators/addition-operator.md)を使用して式の中の 2 つの値を加算したり、[- 演算子 (Visual Basic)](../../../language-reference/operators/subtraction-operator.md) を使用して 1 つの値を別の値から減算したりできます。  
  
 [!code-vb[VbVbalrOperators#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#57)]  
  
 また、否定でも [- 演算子 (Visual Basic)](../../../language-reference/operators/subtraction-operator.md) を使用しますが、次の例に示すように、オペランドは 1 つだけです。  
  
 [!code-vb[VbVbalrOperators#58](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#58)]  
  
 乗算と除算では、次の例に示すように、それぞれ [* 演算子](../../../language-reference/operators/multiplication-operator.md)と [/ 演算子 (Visual Basic)](../../../language-reference/operators/floating-point-division-operator.md) を使用します。  
  
 [!code-vb[VbVbalrOperators#59](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#59)]  
  
 指数では、次の例に示すように、[^ 演算子](../../../language-reference/operators/exponentiation-operator.md)を使用します。  
  
 [!code-vb[VbVbalrOperators#60](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#60)]  
  
 整数除算は、[\ 演算子 (Visual Basic)](../../../language-reference/operators/integer-division-operator.md) を使用して実行されます。 整数除算は商を返します。これは、除数が余りを考慮せずに被除数に分割できる回数を表す整数です。 除数と被除数は両方とも、この演算子の整数型 (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、および `ULong`) である必要があります。 その他のすべての型は、最初に整数型に変換する必要があります。 整数除算の例を次に示します。  
  
 [!code-vb[VbVbalrOperators#61](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#61)]  
  
 剰余演算は、[Mod 演算子](../../../language-reference/operators/mod-operator.md)を使用して実行されます。 この演算子は、除数を被除数に整数回除算した後の剰余を返します。 除数と被除数の両方が整数型の場合、戻り値は整数です。 除数と被除数が浮動小数点型の場合は、戻り値も浮動小数点です。 次の例でその動作を示します。  
  
 [!code-vb[VbVbalrOperators#62](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#62)]  
  
 [!code-vb[VbVbalrOperators#63](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#63)]  
  
### <a name="attempted-division-by-zero"></a>0 による除算を試行  
 0 による除算の結果は、関連するデータ型によって異なります。 整数除算 (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`) では、.NET Framework は <xref:System.DivideByZeroException> 例外をスローします。 `Decimal` または `Single` データ型の除算演算では、.NET Framework は <xref:System.DivideByZeroException> 例外もスローします。  
  
 `Double` データ型を含む浮動小数点除算では、例外はスローされず、結果は被除数に応じて <xref:System.Double.NaN>、<xref:System.Double.PositiveInfinity>、または <xref:System.Double.NegativeInfinity> を表すクラス メンバーになります。 次の表は、`Double` 値を 0 で除算しようとした場合のさまざまな結果をまとめたものです。  
  
|被除数データ型|除数データ型|除算される値|結果|  
|---|---|---|---|  
|`Double`|`Double`|0|<xref:System.Double.NaN> (数学的に定義された数値ではありません)|  
|`Double`|`Double`|> 0|<xref:System.Double.PositiveInfinity>|  
|`Double`|`Double`|\< 0|<xref:System.Double.NegativeInfinity>|  
  
 <xref:System.DivideByZeroException> 例外をキャッチした場合は、そのメンバーを使用して処理することができます。 たとえば、<xref:System.Exception.Message%2A> プロパティは、例外のメッセージ テキストを保持します。 詳しくは、「[Try...Catch...Finally ステートメント](../../../language-reference/statements/try-catch-finally-statement.md)」をご覧ください。  
  
## <a name="bit-shift-operations"></a>ビット シフト演算  
 ビット シフト演算は、ビット パターンに対して算術左シフトを実行します。 パターンは左側のオペランドに含まれていますが、右側のオペランドは、パターンをシフトする位置の数を指定します。 パターンを右にシフトするには [>> 演算子](../../../language-reference/operators/right-shift-operator.md)を使用し、左にシフトするには [<< 演算子](../../../language-reference/operators/left-shift-operator.md)を使用します。  
  
 パターンのオペランドのデータ型は、`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、または `ULong` である必要があります。 シフト数のオペランドのデータ型は、`Integer` であるか、`Integer` に拡大変換する必要があります。  
  
 算術シフトは循環ではありません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 シフトによって空いたビット位置は、次のように設定されます。  
  
- 算術左シフトの場合は 0  
  
- 正の数の算術右シフトの場合は 0  
  
- 符号なしのデータ型 (`Byte`、`UShort`、`UInteger`、`ULong`) の算術右シフトの場合は 0  
  
- 負の数 (`SByte`、`Short`、`Integer`、または `Long`) の算術右シフトの場合は 1  
  
 次の例では、`Integer` 値を左右にシフトします。  
  
 [!code-vb[VbVbalrOperators#64](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#64)]  
  
 算術シフトではオーバーフロー例外は生成されません。  
  
## <a name="bitwise-operations"></a>ビットごとの演算  
 論理演算子に加えて、`Not`、`Or`、`And`、および `Xor` は、数値に対して使用する場合にビットごとの算術演算も実行します。 詳細については、「[Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)」の「ビットごとの演算」を参照してください。  
  
## <a name="type-safety"></a>タイプ セーフ  
 通常、オペランドは同じ型である必要があります。 たとえば、`Integer` 変数を使用して加算を行う場合は、それを別の `Integer` 変数に追加し、その結果を `Integer` 型の変数にも代入する必要があります。  
  
 タイプセーフなコーディングを確実に行うための 1 つの方法として、[Option Strict ステートメント](../../../language-reference/statements/option-strict-statement.md)を使用する方法があります。 `Option Strict On` を設定すると、Visual Basic では、*タイプセーフな*変換が自動的に実行されます。 たとえば、`Double` 変数に `Integer` 変数を追加し、その値を `Double` 変数に代入しようとすると、データを失うことなく `Integer` 値を `Double` に変換できるため、操作は正常に続行されます。 一方、タイプセーフでない変換では、`Option Strict On` でコンパイラ エラーが発生します。 たとえば、`Double` 変数に `Integer` 変数を追加し、その値を `Integer` 変数に代入しようとすると、コンパイラ エラーが発生します。これは、`Double` 変数を型 `Integer` に暗黙的に変換できないためです。  
  
 ただし、`Option Strict Off` を設定した場合、Visual Basic は暗黙的な縮小変換を行うことができますが、予期しないデータまたは精度の損失が発生する可能性があります。 このため、運用コードを記述するときには `Option Strict On` を使用することをお勧めします。 詳細については、「 [Widening and Narrowing Conversions](../data-types/widening-and-narrowing-conversions.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [算術演算子](../../../language-reference/operators/arithmetic-operators.md)
- [ビット シフト演算子](../../../language-reference/operators/bit-shift-operators.md)
- [Visual Basic における比較演算子](comparison-operators.md)
- [Visual Basic の連結演算子](concatenation-operators.md)
- [Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)
- [演算子の効率のよい組み合わせ](efficient-combination-of-operators.md)
