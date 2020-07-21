---
title: 比較演算子
ms.date: 07/20/2015
f1_keywords:
- vb.<>
- vb.>=
- vb.<=
- vb.>
- vb.<
helpviewer_keywords:
- greater than or equal to operator [Visual Basic]
- '>= operator [Visual Basic]'
- = operator [Visual Basic]
- < operator [Visual Basic]
- less than operator [Visual Basic]
- relational operators [Visual Basic], syntax
- Like operator [Visual Basic]
- <> operator [Visual Basic]
- '> operator [Visual Basic]'
- equal operator [Visual Basic]
- less than or equal to operator [Visual Basic]
- symbols, operators
- greater than operator [Visual Basic]
- comparing values [Visual Basic]
- operators [Visual Basic], relational
- string comparison [Visual Basic]
- not equal to comparison operator [Visual Basic]
- <= operator [Visual Basic]
- operators [Visual Basic], comparison
- Is operator [Visual Basic]
- comparison operators [Visual Basic], Visual Basic
ms.assetid: d6cb12a8-e52e-46a7-8aaf-f804d634a825
ms.openlocfilehash: bcd51d70c5c7bd08991c7433e244316a82daa9da
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371792"
---
# <a name="comparison-operators-visual-basic"></a>比較演算子 (Visual Basic)
次に示すのは、Visual Basic で定義されている比較演算子です。

 `<` 演算子

 `<=` 演算子

 `>` 演算子

 `>=` 演算子

 `=` 演算子

 `<>` 演算子

 [Is 演算子](is-operator.md)

 [IsNot 演算子](isnot-operator.md)

 [Like 演算子](like-operator.md)

 これらの演算子は、2 つの式を比較して、両者が等しいかどうかを判断します。等しくない場合は、両者がどのように異なるかを判断します。 `Is`、`IsNot`、`Like` の詳細については、それぞれのヘルプ ページを参照してください。 このページでは、関係比較演算子について詳しく説明します。

## <a name="syntax"></a>構文
  
```vb
result = expression1 comparisonoperator expression2  
result = object1 [Is | IsNot] object2  
result = string Like pattern  
```  
  
## <a name="parts"></a>指定項目
 `result`  
 必須です。 比較の結果を表す `Boolean` 値です。

 `expression1`、`expression2`  
 必須です。 任意の式。

 `comparisonoperator`  
 必須です。 いずれかの関係比較演算子です。

 `object1`、`object2`  
 必須です。 いずれかの参照オブジェクト名です。

 `string`  
 必須です。 任意のブール型 ( `String` ) の式を指定します。

 `pattern`  
 必須です。 いずれかの `String` 式または文字の範囲です。

## <a name="remarks"></a>Remarks
 次の表に、関係比較演算子と、`result` が `True` か `False` かを決定する条件の一覧を示します。

|演算子|`True`:|`False`:|
|--------------|---------------|----------------|
|`<` (より小さい)|`expression1` < `expression2`|`expression1` >= `expression2`|
|`<=` (以下)|`expression1` <= `expression2`|`expression1` > `expression2`|
|`>` (より大きい)|`expression1` > `expression2`|`expression1` <= `expression2`|
|`>=` (以上)|`expression1` >= `expression2`|`expression1` < `expression2`|
|`=` (等しい)|`expression1` = `expression2`|`expression1` <> `expression2`|
|`<>` (等しくない)|`expression1` <> `expression2`|`expression1` = `expression2`|

> [!NOTE]
> [= 演算子](assignment-operator.md)は、代入演算子としても使用されます。

 `Is` 演算子、`IsNot` 演算子、および `Like` 演算子には、前の表の演算子とは異なる特定の比較機能があります。

## <a name="comparing-numbers"></a>数値の比較
 `Single` 型の式を `Double` 型のいずれかと比較すると、`Single` 式が `Double` に変換されます。 この動作は Visual Basic 6 で見られる動作とは逆です。

 同様に、`Decimal` 型の式を `Single` 型、または `Double` 型の式と比較すると、`Decimal` 式が `Single` または `Double` に変換されます。 `Decimal` 式の場合、1E-28 未満の小数値は失われる可能性があります。 このような小数値の損失によって、2 つの値が等しくない場合でも等しいと見なされることがあります。 このため、等値 (`=`) を使用して 2 つの浮動小数点変数を比較する場合は注意が必要です。 2 つの数値の差の絶対値が許容範囲の最小値より小さいかどうかをテストする方が安全です。

### <a name="floating-point-imprecision"></a>浮動小数点おける誤差
 浮動小数点数を操作する場合、それらがメモリ内で常に正確な表現が使用されているとは限らないことに注意してください。 これにより、値の比較や [Mod 演算子](mod-operator.md)などの特定の演算によって、予期しない結果につながる可能性があります。 詳細については、「[データ型のトラブルシューティング](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)」を参照してください。

## <a name="comparing-strings"></a>文字列の比較
 文字列を比較すると、文字列式はアルファベット順の並べ替え順序に基づいて評価されます。これは、`Option Compare` の設定によって異なります。

 `Option Compare Binary` の文字列比較は、文字の内部バイナリ表現から派生した並べ替え順序に基づきます。 並べ替え順序はコード ページによって決まります。 次の例は、一般的なバイナリの並べ替え順序を示しています。

 `A < B < E < Z < a < b < e < z < À < Ê < Ø < à < ê < ø`

 `Option Compare Text` の文字列比較は、アプリケーションのロケールによって決まる、大文字と小文字を区別しないテキストの並べ替え順序に基づきます。 前の例で `Option Compare Text` を設定して文字を並べ替えると、次のテキストの並べ替え順序が適用されます。

 `(A=a) < (À= à) < (B=b) < (E=e) < (Ê= ê) < (Ø = ø) < (Z=z)`

### <a name="locale-dependence"></a>ロケール依存性
 `Option Compare Text` を設定すると、文字列比較の結果が、アプリケーションが実行されているロケールによって変わる場合があります。 2 文字の比較では、あるロケールで等しくても、別のロケールでは等しくならない場合があります。 ログオン試行を受け入れるかどうかなど、重要な決定を行うために文字列比較を使用している場合は、ロケールの感度に関する警告が表示されます。 `Option Compare Binary` を設定するか、ロケールを考慮する <xref:Microsoft.VisualBasic.Strings.StrComp%2A> を呼び出すことを検討してください。

## <a name="typeless-programming-with-relational-comparison-operators"></a>関係比較演算子を使用した型宣言を省略したプログラミング
 `Object` 式での関係比較演算子の使用は、`Option Strict On` では許可されていません。 `Option Strict` が `Off` であり、`expression1` または `expression2` が `Object` 式の場合、実行時の型によって比較方法が決まります。 次の表に、オペランドの実行時の型に応じた、式の比較方法と比較結果を示します。

|オペランドが次の場合|比較|
|---------------------|-------------------|
|両方とも `String`|文字列の並べ替え特性に基づいて比較を並べ替えます。|
|両方とも数値|オブジェクトが `Double` に変換され、数値比較が実行されます。|
|1 つが数値、1 つが `String`|`String` は `Double` に変換され、数値比較が実行されます。 `String` を `Double` に変換できない場合、<xref:System.InvalidCastException> がスローされます。|
|一方または両方が `String` 以外の参照型|<xref:System.InvalidCastException> がスローされます。|

 数値比較では、`Nothing` を 0 として扱います。 文字列比較では、`Nothing` を `""` (空の文字列) として扱います。

## <a name="overloading"></a>オーバーロード
 関係比較演算子 (`<`、 `<=`、`>`、`>=`、`=`、`<>`) は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、そのクラスまたは構造体は動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこれらの演算子が使用される場合は、再定義された動作を理解しておいてください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。

 [= 演算子](assignment-operator.md)は、代入演算子としてではなく、関係比較演算子としてのみオーバーロードできます。

## <a name="example"></a>例
 次の例は、式を比較するために使用する関係比較演算子のさまざまな用途を示します。 関係比較演算子は、記述された式が `True` に評価されるかどうかを表す `Boolean` の結果を返します。 文字列に `>` 演算子と `<` 演算子を適用すると、文字列の通常のアルファベット順の並べ替え順序を使用して比較が行われます。 この順序は、ロケールの設定によって異なります。 並べ替えで大文字と小文字を区別するかどうかは、[Option Compare](../statements/option-compare-statement.md) の設定によって異なります。

 [!code-vb[VbVbalrOperators#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#1)]

 前の例では、最初の比較によって `False` が返され、残りの比較で `True` が返されています。

## <a name="see-also"></a>関連項目

- <xref:System.InvalidCastException>
- [= 演算子](assignment-operator.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [トラブルシューティング (データ型)](../../programming-guide/language-features/data-types/troubleshooting-data-types.md)
- [Visual Basic における比較演算子](../../programming-guide/language-features/operators-and-expressions/comparison-operators.md)
