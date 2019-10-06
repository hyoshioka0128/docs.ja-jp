---
title: Not 演算子 (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Not
helpviewer_keywords:
- Boolean expressions, negating
- operators [Visual Basic], bitwise
- negation operator [Visual Basic]
- inverse bit values in variables [Visual Basic]
- bitwise operators [Visual Basic], NOT operator
- bitwise comparison [Visual Basic]
- Not operator [Visual Basic]
- logical negation
- operators [Visual Basic], negation
ms.assetid: 8f2ea83c-d2ed-480a-a474-3042a1cad9b5
ms.openlocfilehash: 5ebc5f9dbf674a9a6560bd96b3e8c9edcae08a81
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701073"
---
# <a name="not-operator-visual-basic"></a>Not 演算子 (Visual Basic)
@No__t 0 式の場合は論理否定、数値式の場合はビットごとの否定を実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = Not expression  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須。 `Boolean` Or 数値式。  
  
 `expression`  
 必須。 `Boolean` Or 数値式。  
  
## <a name="remarks"></a>コメント  
 @No__t 0 の式の場合、次の表は `result` がどのように決定されるかを示しています。  
  
|が`expression`の場合|@No__t-0 の値はです。|  
|------------------------|------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 数値式の場合、`Not` 演算子は任意の数値式のビット値を反転し、次の表に従って `result` の対応するビットを設定します。  
  
|@No__t のビットが0の場合|@No__t-0 のビットはです。|  
|-------------------------------|----------------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
> 論理演算子とビット処理演算子は、他の算術演算子および関係演算子より優先順位が低いので、ビットごとの演算は、正確な実行を保証するためにかっこで囲む必要があります。  
  
## <a name="data-types"></a>データ型  
 ブール否定の場合、結果のデータ型は `Boolean` になります。 ビットごとの否定の場合、結果のデータ型は `expression` と同じになります。 ただし、expression が `Decimal` の場合、結果は-1 @no__t ます。  
  
## <a name="overloading"></a>オーバーロード  
 @No__t-0 演算子は*オーバーロード*できます。つまり、クラスまたは構造体のオペランドがそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Not` 演算子を使用して、`Boolean` 式の論理否定を実行します。 結果は、式の値の逆を表す @no__t 0 の値になります。  
  
 [!code-vb[VbVbalrOperators#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#33)]  
  
 前の例では、`False` と `True` の結果がそれぞれ生成されます。  
  
## <a name="example"></a>例  
 次の例では、`Not` 演算子を使用して、数値式の個々のビットの論理否定を実行します。 結果パターンのビットは、オペランドパターンの対応するビットの逆順 (符号ビットを含む) に設定されます。  
  
 [!code-vb[VbVbalrOperators#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#34)]  
  
 前の例では、それぞれ–11、–9、および–7の結果が生成されます。  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の論理演算子とビット処理演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
