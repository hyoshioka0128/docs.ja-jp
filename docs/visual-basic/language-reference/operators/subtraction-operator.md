---
title: '- 演算子 (Visual Basic)'
ms.date: 07/20/2015
f1_keywords:
- vb.Negate
- vb.-
helpviewer_keywords:
- operator [Visual Basic]
- operators [Visual Basic], subtraction
- operators [Visual Basic], difference
- negation operator [Visual Basic]
- operators [Visual Basic], arithmetic
- subtraction operator [Visual Basic], syntax
- arithmetic operators [Visual Basic], subtraction
- difference operator [Visual Basic]
- math operators [Visual Basic]
- operators [Visual Basic], negation
- minus operator [Visual Basic]
ms.assetid: bff2c368-662d-4c92-ac87-1d9bdfd3426a
ms.openlocfilehash: 5f6b6b67e2999d380cfca078a43162b3e1db2206
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701302"
---
# <a name="--operator-visual-basic"></a>- 演算子 (Visual Basic)
2つの数値式の差、または数値式の負の値を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
expression1 – expression2
```
  
または

```vb  
–expression1  
```  
  
## <a name="parts"></a>指定項目  
 `expression1`  
 必須。 任意の数式。  
  
 `expression2`  
 @No__t-0 演算子が負の値を計算する場合を除き、必須です。 任意の数式。  
  
## <a name="result"></a>結果  
 結果として、`expression1` と `expression2` の差、または `expression1` の符号が反転された値が返されます。  
  
 結果のデータ型は、および`expression1` `expression2`のデータ型に適した数値型です。 「[演算子の結果のデータ型](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)」の「整数演算」の表を参照してください。  
  
## <a name="supported-types"></a>サポートされている型  
 すべての数値型。 これには、符号なしおよび浮動小数点`Decimal`型とが含まれます。  
  
## <a name="remarks"></a>コメント  
 前に示した構文に示されている最初の使用法では、`–` 演算子は2つの数値式の差を表す*二項*算術減算演算子です。  
  
 前に示した構文に示されている2番目の使用法では、`–` 演算子は、式の負の値を表す*単項*否定演算子です。 この意味では、否定は `expression1` の符号を反転することで構成され、`expression1` が負の場合は結果が正になります。  
  
 いずれかの式が[Nothing](../../../visual-basic/language-reference/nothing.md)と評価された場合、`–` 演算子はそれを0として扱います。  
  
> [!NOTE]
> @No__t-0 演算子は*オーバーロード*できます。つまり、クラスまたは構造体がそのクラスまたは構造体の型を持つ場合に、クラスまたは構造体がその動作を再定義できます。 コードでこのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`–` 演算子を使用して、2つの数値の差を計算して返し、その後で数値を否定します。  
  
 [!code-vb[VbVbalrOperators#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#10)]  
  
 これらのステートメントの実行後、`binaryResult` には124.45 が含まれ、`unaryResult` は–334.90 を含みます。  
  
## <a name="see-also"></a>関連項目

- [-= 演算子 (Visual Basic)](../../../visual-basic/language-reference/operators/subtraction-assignment-operator.md)
- [算術演算子](../../../visual-basic/language-reference/operators/arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [機能別の演算子一覧](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Visual Basic の算術演算子](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
