---
title: 比較演算子
ms.date: 07/20/2015
helpviewer_keywords:
- comparison operators [Visual Basic], comparing strings
- comparison operators [Visual Basic], comparing objects
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- string comparison [Visual Basic], operators
- objects [Visual Basic], comparing
- numbers [Visual Basic], comparing
- Visual Basic code, operators
- string comparison [Visual Basic]
- numeric values [Visual Basic], comparing
- comparison operators [Visual Basic], comparing numeric values
- operators [Visual Basic], comparison
ms.assetid: 0b570339-5407-474f-8421-e183a8b303ee
ms.openlocfilehash: 7a93928ff95e307c64149da7ab21476ffd4fa77d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388830"
---
# <a name="comparison-operators-in-visual-basic"></a>Visual Basic における比較演算子
比較演算子は、2 つの式を比較し、それらの値の関係を表す `Boolean` 値を返します。 数値を比較するための演算子、文字列を比較するための演算子、およびオブジェクトを比較するための演算子があります。 ここでは、3 種類のすべての演算子について説明します。  
  
## <a name="comparing-numeric-values"></a>数値の比較  
 Visual Basic は、6 つの数値比較演算子を使用して数値を比較します。 各演算子は、数値として評価される 2 つの式をオペランドとして受け取ります。 次の表に、演算子の一覧とそれぞれの例を示します。  
  
|演算子|テストされた条件|使用例|  
|--------------|----------------------|--------------|  
|`=` (等値)|最初の式の値が 2 番目の式の値と等しいかどうかを示します。|`23`   `=`   `33    ' False`<br /><br /> `23`   `=`   `23    ' True`<br /><br /> `23`   `=`   `12    ' False`|  
|`<>` (非等値)|最初の式の値が 2 番目の式の値と等しくないかどうかを示します。|`23`   `<>`   `33    ' True`<br /><br /> `23`   `<>`   `23    ' False`<br /><br /> `23`   `<>`   `12    ' True`|  
|`<` (より小さい)|最初の式の値が 2 番目の式の値より小さいかどうかを示します。|`23`   `<`   `33    ' True`<br /><br /> `23`   `<`   `23    ' False`<br /><br /> `23`   `<`   `12    ' False`|  
|`>` (より大きい)|最初の式の値が 2 番目の式の値より大きいかどうかを示します。|`23`   `>`   `33    ' False`<br /><br /> `23`   `>`   `23    ' False`<br /><br /> `23`   `>`   `12    ' True`|  
|`<=` (以下)|最初の式の値が 2 番目の式の値以下であるかどうかを示します。|`23`   `<=`   `33    ' True`<br /><br /> `23`   `<=`   `23    ' True`<br /><br /> `23`   `<=`   `12    ' False`|  
|`>=` (以上)|最初の式の値が 2 番目の式の値以上であるかどうかを示します。|`23`   `>=`   `33    ' False`<br /><br /> `23`   `>=`   `23    ' True`<br /><br /> `23`   `>=`   `12    ' True`|  
  
## <a name="comparing-strings"></a>文字列の比較  
 Visual Basic は、[Like 演算子](../../../language-reference/operators/like-operator.md)および数値比較演算子を使用して文字列を比較します。 `Like` 演算子を使用すると、パターンを指定できます。 その後、文字列がパターンと比較され、一致する場合、結果は `True` です。 それ以外の場合、結果は `False` です。 数値演算子を使用すると、次の例に示すように、並べ替え順序に基づいて `String` 値を比較できます。  
  
 `"73" < "9"`  
  
 `' The result of the preceding comparison is True.`  
  
 前の例の結果は、最初の文字列の最初の文字が 2 番目の文字列の最初の文字の前にあるため、`True` です。 最初の文字が等しい場合、比較は両方の文字列の次の文字に続き、以下同様に続きます。 次の例に示すように、等値演算子を使用して文字列の等価性をテストすることもできます。  
  
 `"734" = "734"`  
  
 `' The result of the preceding comparison is True.`  
  
 "aa" や "aaa" のように、ある文字列が別の文字列のプレフィックスである場合、長い文字列は短い文字列よりも大きいと見なされます。 次の例を使って説明します。  
  
 `"aaa" > "aa"`  
  
 `' The result of the preceding comparison is True.`  
  
 並べ替え順序は、`Option Compare` の設定に応じて、バイナリ比較またはテキスト比較のいずれかに基づきます。 詳細については、「[Option Compare ステートメント](../../../language-reference/statements/option-compare-statement.md)」を参照してください。  
  
## <a name="comparing-objects"></a>オブジェクトの比較  
 Visual Basic は、[Is 演算子](../../../language-reference/operators/is-operator.md)および [IsNot 演算子](../../../language-reference/operators/isnot-operator.md)を使用して 2 つのオブジェクト参照変数を比較します。 これらの演算子のいずれかを使用して、2 つの参照変数が同じオブジェクト インスタンスを参照しているかどうかを判断できます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#65](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#65)]  
  
 前の例では、両方の変数が同じインスタンスを参照しているため、`x Is y` は `True` と評価されます。 この結果を次の例と比較してください。  
  
 [!code-vb[VbVbalrOperators#66](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#66)]  
  
 前の例では、`x Is y` は `False` と評価されます。これは、変数が同じ型のオブジェクトを参照しているにもかかわらず、その型の異なるインスタンスを参照しているためです。  
  
 同じインスタンスを指していない 2 つのオブジェクトをテストする場合は、`IsNot` 演算子を使用すると、`Not` と `Is` の文法的にぎこちない組み合わせを回避できます。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#67](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#67)]  
  
 前の例では、`If a IsNot b` は `If Not a Is b` に相当します。  
  
### <a name="comparing-object-type"></a>オブジェクトの種類の比較  
 `TypeOf`...`Is` 式を使用して、オブジェクトが特定の型であるかどうかをテストできます。 構文は次のとおりです。  
  
 `TypeOf <objectexpression> Is <typename>`  
  
 `typename` がインターフェイス型を指定するとき、オブジェクトがインターフェイス型を実装している場合、`TypeOf`...`Is` 式は `True` を返します。 `typename` がクラス型の場合、オブジェクトが指定されたクラスのインスタンスであるか、または指定されたクラスから派生したクラスのインスタンスである場合、式は `True` を返します。 次の例を使って説明します。  
  
 [!code-vb[VbVbalrOperators#68](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#68)]  
  
 前の例では、`TypeOf x Is Control` 式は `True` と評価されます。これは、`x` の型が `Button` であり、`Control` から継承されているためです。  
  
 詳細については、「[TypeOf 演算子](../../../language-reference/operators/typeof-operator.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [値の比較](value-comparisons.md)
- [比較演算子](../../../language-reference/operators/comparison-operators.md)
- [演算子](../../../language-reference/operators/index.md)
- [Visual Basic における算術演算子](arithmetic-operators.md)
- [Visual Basic の連結演算子](concatenation-operators.md)
- [Visual Basic の論理演算子とビット処理演算子](logical-and-bitwise-operators.md)
