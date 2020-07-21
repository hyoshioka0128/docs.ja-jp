---
title: = 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.Assign
- vb.=
helpviewer_keywords:
- = operator [Visual Basic]
- = assignment statements [Visual Basic]
ms.assetid: 2dac2e49-86c8-42f8-80c1-458452fb5e29
ms.openlocfilehash: 516cb21e02d9fb2cd4b8d72282bb74163e1fb14b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371766"
---
# <a name="-operator-visual-basic"></a>= 演算子 (Visual Basic)
変数またはプロパティに値を代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty = value  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 任意の書き込み可能な変数または任意のプロパティ。  
  
 `value`  
 任意のリテラル、定数、または式。  
  
## <a name="remarks"></a>Remarks  
 等号 (`=`) の左側の要素として、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。 `=` 演算子は、右辺の値を左辺の変数またはプロパティに代入します。  
  
> [!NOTE]
> `=` 演算子は、比較演算子としても使用されます。 詳細については、「[比較演算子](comparison-operators.md)」を参照してください。  
  
## <a name="overloading"></a>オーバーロード  
 `=` 演算子は、代入演算子としてではなく、関係比較演算子としてのみオーバーロードできます。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 代入演算子の例を次に示します。 右辺の値が左辺の変数に代入されます。  
  
 [!code-vb[VbVbalrOperators#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#9)]  
  
## <a name="see-also"></a>関連項目

- [& = 演算子](and-assignment-operator.md)
- [*= 演算子](multiplication-assignment-operator.md)
- [+= 演算子](addition-assignment-operator.md)
- [-= 演算子 (Visual Basic)](subtraction-assignment-operator.md)
- [/= 演算子 (Visual Basic)](floating-point-division-assignment-operator.md)
- [\\= 演算子](integer-division-assignment-operator.md)
- [^= 演算子](exponentiation-assignment-operator.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
- [比較演算子](comparison-operators.md)
- [ReadOnly](../modifiers/readonly.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
