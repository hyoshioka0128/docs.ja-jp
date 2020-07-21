---
title: -= 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.-=
helpviewer_keywords:
- -= operator [Visual Basic]
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator -=
- compound assignment statements [Visual Basic]
ms.assetid: 5ead0c37-ae50-48f7-8435-8e341d81cae1
ms.openlocfilehash: 4f403cd8a28f8d9d0ba1d24b0792a352a9c961db
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406406"
---
# <a name="--operator-visual-basic"></a>-= 演算子 (Visual Basic)
変数またはプロパティの値から式の値を減算し、その結果を変数またはプロパティに代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty -= expression  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 任意の数値変数またはプロパティ。  
  
 `expression`  
 必須です。 任意の数式。  
  
## <a name="remarks"></a>Remarks  
 `-=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `-=` 演算子は、まず、式の値 (演算子の右側) を変数またはプロパティの値 (演算子の左側) から減算します。 次に、演算子はその演算の結果を変数またはプロパティに代入します。  
  
## <a name="overloading"></a>オーバーロード  
 [- 演算子 (Visual Basic)](subtraction-operator.md) は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体はその動作を再定義できます。 `-` 演算子をオーバーロードすると、`-=` 演算子の動作に影響します。 コードで、`-` をオーバーロードするクラスまたは構造体で `-=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`-=` 演算子を使用して、ある `Integer` 変数を別の変数から減算し、その結果を後者の変数に代入します。  
  
 [!code-vb[VbVbalrOperators#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#11)]  
  
## <a name="see-also"></a>関連項目

- [- 演算子 (Visual Basic)](subtraction-operator.md)
- [代入演算子](assignment-operators.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
