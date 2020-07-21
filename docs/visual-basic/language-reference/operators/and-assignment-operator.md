---
title: '&amp;= 演算子'
ms.date: 07/20/2015
f1_keywords:
- vb.&=
helpviewer_keywords:
- operator &=
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- '&= operator [Visual Basic]'
- compound assignment statements [Visual Basic]
ms.assetid: 0cf262fc-1a05-419a-a503-60013f111c8a
ms.openlocfilehash: db42f7be7225b866eacf5b73066754e91cd1a0f7
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371987"
---
# <a name="amp-operator-visual-basic"></a>&amp;= 演算子 (Visual Basic)
`String` 式を `String` 変数またはプロパティに連結し、結果をその変数またはプロパティに代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty &= expression  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 任意の `String` 変数またはプロパティ。  
  
 `expression`  
 必須です。 任意のブール型 ( `String` ) の式を指定します。  
  
## <a name="remarks"></a>Remarks  
 `&=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。 `&=` 演算子は、右側の `String` 式を左側の `String` 変数またはプロパティに連結し、結果を左側の変数またはプロパティに代入します。  
  
## <a name="overloading"></a>オーバーロード  
 [& 演算子](concatenation-operator.md)は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体はその動作を再定義できます。 `&` 演算子をオーバーロードすると、`&=` 演算子の動作に影響します。 コードで、`&` をオーバーロードするクラスまたは構造体で `&=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`&=` 演算子を使用して 2 つの `String` 変数を連結し、その結果を最初の変数に代入します。  
  
 [!code-vb[VbVbalrOperators#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#3)]  
  
## <a name="see-also"></a>関連項目

- [& 演算子](concatenation-operator.md)
- [+= 演算子](addition-assignment-operator.md)
- [代入演算子](assignment-operators.md)
- [連結演算子](concatenation-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
