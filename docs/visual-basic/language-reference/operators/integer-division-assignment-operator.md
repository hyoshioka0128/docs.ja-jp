---
title: '\= 演算子'
ms.date: 07/20/2015
f1_keywords:
- '\='
- vb.\=
helpviewer_keywords:
- '\= operator [Visual Basic]'
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator \= [Visual Basic]
- compound assignment statements [Visual Basic]
ms.assetid: 6f39915d-e398-4045-afcc-da6885e57b9c
ms.openlocfilehash: a546d8b0c9b3852386970f80d3da96794da2351c
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84370948"
---
# <a name="-operator"></a>\\= 演算子
変数またはプロパティの値を式の値で除算し、整数の結果を変数またはプロパティに代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty \= expression  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 任意の数値変数またはプロパティ。  
  
 `expression`  
 必須です。 任意の数式。  
  
## <a name="remarks"></a>Remarks  
 `\=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `\=` 演算子は、左側の変数またはプロパティの値を右側の値で除算し、整数の結果を左側の変数またはプロパティに代入します  
  
 整数除算の詳細については、「[\ 演算子 (Visual Basic)](integer-division-operator.md)」を参照してください。  
  
## <a name="overloading"></a>オーバーロード  
 `\` 演算子は "*オーバーロード*" できます。つまり、オペランドの型がクラスまたは構造体であるとき、そのクラスまたは構造体で、演算子の動作を再定義できます。 `\` 演算子をオーバーロードすると、`\=` 演算子の動作に影響します。 コードで、`\` をオーバーロードするクラスまたは構造体で `\=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`\=` 演算子を使用して 1 番目の `Integer` 変数を 2 番目の変数で除算し、整数の結果を 1 番目の変数に代入します。  
  
 [!code-vb[VbVbalrOperators#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#19)]  
  
## <a name="see-also"></a>関連項目

- [\ 演算子 (Visual Basic)](integer-division-operator.md)
- [/= 演算子 (Visual Basic)](floating-point-division-assignment-operator.md)
- [代入演算子](assignment-operators.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
