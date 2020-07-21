---
title: += 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.+=
helpviewer_keywords:
- += operator [Visual Basic]
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- += operator [Visual Basic], appending strings
- compound assignment statements [Visual Basic]
ms.assetid: d3e959f4-85d4-4e47-87c4-77b62335a5b3
ms.openlocfilehash: c2ce384901a9f0207e8279a5a07a88600c875e7f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84372208"
---
# <a name="-operator-visual-basic"></a>+= 演算子 (Visual Basic)
数値式の値を数値変数またはプロパティの値に加算し、結果をその変数またはプロパティに代入します。 また、`String` 式を `String` 変数またはプロパティに連結し、結果をその変数またはプロパティに代入するために使用することもできます。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty += expression  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 任意の数値または `String` 変数またはプロパティ。  
  
 `expression`  
 必須です。 任意の数値または `String` 式。  
  
## <a name="remarks"></a>Remarks  
 `+=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `+=` 演算子は、右側の値を左側の変数またはプロパティに追加し、その結果を左側の変数またはプロパティに代入します。 `+=` 演算子を使用して、右側の `String` 式を左側の `String` 変数またはプロパティに連結し、その結果を左側の変数またはプロパティに代入することもできます。  
  
> [!NOTE]
> `+=` 演算子を使用すると、加算と文字列連結のどちらが行われるのか判断できない可能性があります。 あいまいさをなくし、自己文書化コードを実現するために、連結には `&=` 演算子を使用してください。  
  
 コンパイル環境で厳密なセマンティクスが適用されている場合、この代入演算子は拡大変換を暗黙的に実行しますが、縮小変換は実行しません。 これらの変換の詳細については、「[拡大変換と縮小変換](../../programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)」を参照してください。 厳密なセマンティクスおよび寛容なセマンティクスの詳細については、「[Option Strict ステートメント](../statements/option-strict-statement.md)」を参照してください。  
  
 寛容なセマンティクスが許可されている場合、`+=` 演算子は、`+` 演算子によって実行されるものと同じ各種変換 (文字列変換および数値変換) を暗黙的に実行します。 これらの変換の詳細については、「[+ 演算子](addition-operator.md)」を参照してください。  
  
## <a name="overloading"></a>オーバーロード  
 `+` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、このクラスまたは構造体はその動作を再定義できます。 `+` 演算子をオーバーロードすると、`+=` 演算子の動作に影響します。 コードで、`+` をオーバーロードするクラスまたは構造体に `+=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`+=` 演算子を使用して、ある変数の値を別の値と結合します。 最初の部分では `+=` を数値変数と共に使用して、ある値を別の値に追加します。 2 番目の部分では、`+=` を `String` 変数と共に使用して、ある値を別の値と連結します。 どちらの場合も、結果は最初の変数に代入されます。  
  
 [!code-vb[VbVbalrOperators#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#7)]  
  
 [!code-vb[VbVbalrOperators#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#8)]  
  
 `num1` の値は 13 になり、`str1` の値は "103" になりました。  
  
## <a name="see-also"></a>関連項目

- [+ 演算子](addition-operator.md)
- [代入演算子](assignment-operators.md)
- [算術演算子](arithmetic-operators.md)
- [連結演算子](concatenation-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
