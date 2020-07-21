---
title: '- 演算子'
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
ms.openlocfilehash: 6539beb5cf8078281357445e2391fac189208087
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406355"
---
# <a name="--operator-visual-basic"></a>- 演算子 (Visual Basic)
2 つの数値式の差、またはある数値式の負の値を返します。  
  
## <a name="syntax"></a>構文  
  
```vb  
expression1 – expression2
```
  
or

```vb  
–expression1  
```  
  
## <a name="parts"></a>指定項目  
 `expression1`  
 必須です。 任意の数式。  
  
 `expression2`  
 `–` 演算子で負の値を求める場合を除き、必須です。 任意の数式。  
  
## <a name="result"></a>結果  
 結果は、`expression1` と `expression2` の差、または `expression1` の符号を反転した値になります。  
  
 結果のデータ型は `expression1` および `expression2` のデータ型に適した数値型になります。 「[演算子の結果のデータ型](data-types-of-operator-results.md)」の「整数演算」の表を参照してください。  
  
## <a name="supported-types"></a>サポートされている型  
 すべての数値型。 これには、符号なしおよび浮動小数点の型と `Decimal` が含まれます。  
  
## <a name="remarks"></a>Remarks  
 前述の構文で示した最初の使用法では、`–` 演算子は、2 つの数値式の差を求める "*バイナリ*" 算術減算演算子です。  
  
 前述の構文で示した 2 番目の使用法では、`–` 演算子は、式の負の値に対する "*単項*" 否定演算子です。 この意味では、否定は、`expression1` が負の場合に結果が正になるように、`expression1` の符号を反転させることです。  
  
 いずれかの式が [Nothing](../nothing.md) と評価される場合、`–` 演算子はそれを 0 として扱います。  
  
> [!NOTE]
> `–` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、このクラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`–` 演算子を使用して、2 つの数値の差を計算して返します。次に、数値の符号を反転させます。  
  
 [!code-vb[VbVbalrOperators#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#10)]  
  
 これらのステートメントの実行後、`binaryResult` には124.45 が格納委され、`unaryResult` には –334.90 が格納されます。  
  
## <a name="see-also"></a>関連項目

- [-= 演算子 (Visual Basic)](subtraction-assignment-operator.md)
- [算術演算子](arithmetic-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic における算術演算子](../../programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)
