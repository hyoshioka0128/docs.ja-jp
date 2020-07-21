---
title: '*= 演算子'
ms.date: 07/20/2015
f1_keywords:
- vb.*=
helpviewer_keywords:
- operator *=
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- '*= operator [Visual Basic]'
- compound assignment statements [Visual Basic]
ms.assetid: 96c86509-6eb8-4682-8226-3852e049376f
ms.openlocfilehash: b06ebcb4f4100a0621f52a769543c0fb24fbb4bf
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401499"
---
# <a name="-operator-visual-basic"></a>*= 演算子 (Visual Basic)
変数またはプロパティの値を式の値で乗算し、その結果を変数またはプロパティに代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty *= expression  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 任意の数値変数またはプロパティ。  
  
 `expression`  
 必須です。 任意の数式。  
  
## <a name="remarks"></a>Remarks  
 `*=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `*=` 演算子は、最初に (演算子の右側にある) 式の値に、(演算子の左側にある) 変数またはプロパティの値を乗算します。 次に、その演算の結果を変数またはプロパティに代入します。  
  
## <a name="overloading"></a>オーバーロード  
 [* 演算子](multiplication-operator.md)は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 `*` 演算子をオーバーロードすると、`*=` 演算子の動作に影響します。 コードで、`*` をオーバーロードするクラスまたは構造体で `*=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`*=` 演算子を使用して、最初の `Integer` 変数に 2 番目の変数を乗算し、その結果を最初の変数に代入します。  
  
 [!code-vb[VbVbalrOperators#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [* 演算子](multiplication-operator.md)
- [代入演算子](assignment-operators.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
