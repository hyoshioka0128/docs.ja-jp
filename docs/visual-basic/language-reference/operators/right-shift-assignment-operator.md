---
title: '>>= 演算子'
ms.date: 07/20/2015
f1_keywords:
- vb.>>=
helpviewer_keywords:
- assignment statements [Visual Basic], compound
- statements [Visual Basic], compound assignment
- operator >>= [Visual Basic]
- compound assignment statements [Visual Basic]
- '>>= operator [Visual Basic]'
ms.assetid: 2bcd9abb-7a8c-4229-b75d-8816ff1dc700
ms.openlocfilehash: c3afe2bcc4b9732b5afd34df1b83eaebe707b3f5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409297"
---
# <a name="-operator-visual-basic"></a>>>= 演算子 (Visual Basic)
変数またはプロパティの値に算術右シフトを実行し、結果をその変数またはプロパティに戻して代入します。  
  
## <a name="syntax"></a>構文  
  
```vb  
variableorproperty >>= amount  
```  
  
## <a name="parts"></a>指定項目  
 `variableorproperty`  
 必須です。 整数型の変数またはプロパティ (`SByte`、`Byte`、`Short`、`UShort`、`Integer`、`UInteger`、`Long`、`ULong`)。  
  
 `amount`  
 必須です。 `Integer` に拡大されるデータ型の数値式。  
  
## <a name="remarks"></a>Remarks  
 `>>=` 演算子の左側の要素には、単純なスカラー変数、プロパティ、または配列の要素を指定できます。 変数またはプロパティを [ReadOnly](../modifiers/readonly.md) にすることはできません。  
  
 `>>=` 演算子は、まず変数またはプロパティの値に対して算術右シフトを実行します。 次に、この演算子はその演算の結果を変数またはプロパティに戻して代入します。  
  
 算術シフトは循環ではありません。つまり、結果の一方の端からシフトされたビットはもう一方の端には再入されません。 算術右シフトでは、右端のビット位置を超えてシフトされたビットは破棄され、左端ビットは左側の空いたビット位置に移されます。 したがって、`variableorproperty` に負の値がある場合、空いている位置は 1 に設定されます。 `variableorproperty` が正の場合、またはそのデータ型が符号なしの型の場合、空いている位置は 0 に設定されます。  
  
## <a name="overloading"></a>オーバーロード  
 [>> 演算子](right-shift-operator.md)は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 `>>` 演算子をオーバーロードすると、`>>=` 演算子の動作に影響します。 コードで、`>>` をオーバーロードするクラスまたは構造体で `>>=` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`>>=` 演算子を使用して、`Integer` 変数のビット パターンを、指定された桁数だけ右にシフトし、結果をその変数に代入します。  
  
 [!code-vb[VbVbalrOperators#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>関連項目

- [>> 演算子](right-shift-operator.md)
- [代入演算子](assignment-operators.md)
- [ビット シフト演算子](bit-shift-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [ステートメント](../../programming-guide/language-features/statements.md)
