---
title: + 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.+
helpviewer_keywords:
- arithmetic operators [Visual Basic], addition
- + operator
- concatenation operators [Visual Basic], syntax
- strings [Visual Basic], concatenating
- sum operator [Visual Basic]
ms.assetid: 5694778f-0a2c-4539-8009-f66f318fb46d
ms.openlocfilehash: 6ae3feae6ecb63b82426f2aa69359625bbffcec8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372117"
---
# <a name="-operator-visual-basic"></a>+ 演算子 (Visual Basic)
2 つの数値を加算するか、数値式の正の値を返します。 2 つの文字列式の連結にも使用できます。  
  
## <a name="syntax"></a>構文  
  
```vb
expression1 + expression2
```
  
or

```vb  
+expression1  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`expression1`|必須です。 任意の数値または文字列の式。|  
|`expression2`|`+` 演算子が負の値を計算する場合を除き、必須です。 任意の数値または文字列の式。|  
  
## <a name="result"></a>結果  
 `expression1` と `expression2` が両方とも数値の場合、結果はそれらの算術和になります。  
  
 `expression2` がない場合、`+` 演算子は、変更されていない式の値の "*単項*" 恒等演算子です。 この意味では、この演算は `expression1` の符号を維持するため、`expression1` が負の場合は、結果が負になります。  
  
 `expression1` と `expression2` が両方とも文字列の場合、結果はそれらの値の連結です。  
  
 `expression1` と `expression2` の型が混在している場合、実行される処理は、その型、内容、および [Option Strict ステートメント](../statements/option-strict-statement.md)の設定によって異なります。 詳細については、「Remarks」の表を参照してください。  
  
## <a name="supported-types"></a>サポートされている型  
 すべての数値型。これには、符号なしおよび浮動小数点の型、`Decimal`、`String` が含まれます。  
  
## <a name="remarks"></a>Remarks  
 一般に、`+` は可能な場合は算術加算を実行し、両方の式が文字列である場合にのみ連結します。  
  
 どちらの式も `Object` でない場合、Visual Basic では次の処理が実行されます。  
  
|式のデータ型|コンパイラによる処理|  
|---|---|  
|両方の式が数値データ型 (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`、`Decimal`、`Single`、または `Double`) である|加算します。 結果のデータ型は、`expression1` および `expression2` のデータ型に適した数値型です。 「[演算子の結果のデータ型](data-types-of-operator-results.md)」の「整数の算術演算」の表を参照してください。|  
|両方の式の型が `String` である|連結します。|  
|一方の式は数値データ型であり、もう一方は文字列である|`Option Strict` が `On` である場合は、コンパイラ エラーが発生します。<br /><br /> `Option Strict` が `Off` である場合は、`String` を `Double` に暗黙的に変換して、加算します。<br /><br /> `String` を `Double` に変換できない場合は、<xref:System.InvalidCastException> 例外をスローします。|  
|一方の式は数値データ型であり、もう一方は [Nothing](../nothing.md) である|`Nothing` を 0 と評価して加算します。|  
|一方の式は文字列であり、もう一方は `Nothing` である|`Nothing` を "" と評価して連結します。|  
  
 一方の式が `Object` 式の場合、Visual Basic では次の処理が実行されます。  
  
|式のデータ型|コンパイラによる処理|  
|---|---|  
|`Object` 式は数値を保持し、もう一方は数値データ型である|`Option Strict` が `On` である場合は、コンパイラ エラーが発生します。<br /><br /> `Option Strict` が `Off` である場合は、加算します。|  
|`Object` 式は数値を保持し、もう一方は `String` 型である|`Option Strict` が `On` である場合は、コンパイラ エラーが発生します。<br /><br /> `Option Strict` が `Off` である場合は、`String` を `Double` に暗黙的に変換して、加算します。<br /><br /> `String` を `Double` に変換できない場合は、<xref:System.InvalidCastException> 例外をスローします。|  
|`Object` 式は文字列を保持し、もう一方は数値データ型である|`Option Strict` が `On` である場合は、コンパイラ エラーが発生します。<br /><br /> `Option Strict` が `Off` である場合は、文字列 `Object` を `Double` に暗黙的に変換して、加算します。<br /><br /> 文字列 `Object` を `Double` に変換できない場合は、<xref:System.InvalidCastException> 例外をスローします。|  
|`Object` 式は文字列を保持し、もう一方は `String` 型である|`Option Strict` が `On` である場合は、コンパイラ エラーが発生します。<br /><br /> `Option Strict` が `Off` である場合、`Object` を `String` に暗黙的に変換して、連結します。|  
  
 両方の式が `Object` 式の場合、Visual Basic は次の処理を実行します (`Option Strict Off` のみ)。  
  
|式のデータ型|コンパイラによる処理|  
|---|---|  
|両方の `Object` 式が数値を保持している|加算します。|  
|両方の `Object` 式の型が `String` である|連結します。|  
|一方の `Object` 式は数値を保持し、もう一方は文字列を保持している|文字列 `Object` を `Double` に暗黙的に変換して、加算します。<br /><br /> 文字列 `Object` を数値に変換できない場合は、<xref:System.InvalidCastException> 例外をスローします。|  
  
 いずれかの`Object` 式が [Nothing](../nothing.md) または <xref:System.DBNull> と評価される場合、 `+` 演算子はそれを値が "" である `String` として扱います。  
  
> [!NOTE]
> `+` 演算子を使用すると、加算と文字列連結のどちらが発生するか判断できない可能性があります。 連結には `&` 演算子を使用してあいまいさをなくし、自己文書化コードを実現してください。  
  
## <a name="overloading"></a>オーバーロード  
 `+` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`+` 演算子を使用して数値を加算します。 オペランドが両方とも数値の場合、Visual Basic は演算結果を計算します。 算術結果は、2 つのオペランドの和を表します。  
  
 [!code-vb[VbVbalrOperators#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#6)]  
  
 `+` 演算子を使用して、文字列を連結することもできます。 オペランドが両方とも文字列の場合は、Visual Basic はそれらを連結します。 連結の結果は、2 つのオペランドがその順番どおりの内容で構成されている 1 つの文字列を表します。  
  
 オペランドの型が混在する場合、結果は [Option Strict ステートメント](../statements/option-strict-statement.md)の設定によって異なります。 次の例は、`Option Strict` が `On` である場合の結果を示しています。  
  
 [!code-vb[VbVbalrOperators#53](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class3.vb#53)]  
  
 [!code-vb[VbVbalrOperators#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#50)]  
[!code-vb[VbVbalrOperators#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#51)]  
  
 次の例は、`Option Strict` が `Off` である場合の結果を示しています。  
  
 [!code-vb[VbVbalrOperators#54](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#54)]  
  
 [!code-vb[VbVbalrOperators#50](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#50)]  
[!code-vb[VbVbalrOperators#52](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class2.vb#52)]  
  
 あいまいさをなくすために、連結には、`+` の代わりに `&` 演算子を使用してください。  
  
## <a name="see-also"></a>関連項目

- [& 演算子](concatenation-operator.md)
- [連結演算子](concatenation-operators.md)
- [算術演算子](arithmetic-operators.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
- [Option Strict ステートメント](../statements/option-strict-statement.md)
