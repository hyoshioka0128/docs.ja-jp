---
title: AndAlso 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.AndAlso
- AndAlso
helpviewer_keywords:
- short-circuiting
- AndAlso operator [Visual Basic]
- operators [Visual Basic], short-circuiting
- operators [Visual Basic], conjunction
- short-circuit evaluation
ms.assetid: bbc15191-b374-495b-9b8f-7b8c2f4388eb
ms.openlocfilehash: 8b67897956a21d06d465cf206856354d2e3f9d68
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371935"
---
# <a name="andalso-operator-visual-basic"></a>AndAlso 演算子 (Visual Basic)
2 つの式の短絡論理積を求めます。  
  
## <a name="syntax"></a>構文  
  
```vb
result = expression1 AndAlso expression2  
```  
  
## <a name="parts"></a>指定項目  
  
|用語|定義|  
|---|---|  
|`result`|必須です。 任意のブール型 ( `Boolean` ) の式を指定します。 結果は、2 つの式の比較の `Boolean` 結果です。|  
|`expression1`|必須です。 任意のブール型 ( `Boolean` ) の式を指定します。|  
|`expression2`|必須です。 任意のブール型 ( `Boolean` ) の式を指定します。|  
  
## <a name="remarks"></a>Remarks  
 コンパイルされたコードが、ある式の評価を別の式の結果に応じてバイパスできる場合、論理演算は "*短絡*" であると言われます。 最初に評価された式の結果によって演算の最終結果が決まる場合、最終結果を変更できないため、2 番目の式を評価する必要はありません。 バイパスされた式が複雑な場合や、プロシージャ呼び出しが関係している場合に、短絡によってパフォーマンスを向上させることができます。  
  
 両方の式が `True` に評価される場合、`result` は `True` です。 次の表は、`result` の判定方法を示しています。  
  
|`expression1` が次の場合|かつ、`expression2` が次の場合|`result` の値は次のとおり|  
|---|---|---|  
|`True`|`True`|`True`|  
|`True`|`False`|`False`|  
|`False`|(評価されていない)|`False`|  
  
## <a name="data-types"></a>データの種類  
 `AndAlso` 演算子は [Boolean データ型](../data-types/boolean-data-type.md)に対してのみ定義されます。 Visual Basic は、式を評価する前に、必要に応じて各オペランドを `Boolean` に変換します。 結果を数値型に代入すると、Visual Basic によって `Boolean` からその型への変換が行われ、`False` が `0` になり、`True` が `-1` になります。
詳細については、[ブール型変換](../data-types/boolean-data-type.md#type-conversions)に関する記事をご覧ください。
  
## <a name="overloading"></a>オーバーロード  
 [And 演算子](and-operator.md)と [IsFalse 演算子](isfalse-operator.md)は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体はその動作を再定義できます。 `And` と `IsFalse` の演算子をオーバーロードすると、`AndAlso` 演算子の動作に影響します。 コードで、`And` と `IsFalse` をオーバーロードするクラスまたは構造体で `AndAlso` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`AndAlso` 演算子を使用して、2 つの式の論理積を求めます。 結果は、結合した式全体が真かどうかを表す `Boolean` 値です。 最初の式が `False` の場合、2 番目の式は評価されません。  
  
 [!code-vb[VbVbalrOperators#24](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#24)]  
  
 前の例では、それぞれ `True`、`False`、`False` の結果が生成されます。 `secondCheck` の計算では、最初の式が既に `False` であるため、2 番目の式は評価されません。 ただし、2 番目の式は `thirdCheck` の計算で評価されます。  
  
## <a name="example"></a>例  
 次の例は、配列の要素の中から特定の値を検索する `Function` プロシージャを示しています。 配列が空の場合、または配列の長さが超過した場合、`While` ステートメントは、検索値に対する配列要素のテストを行いません。  
  
 [!code-vb[VbVbalrOperators#25](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#25)]  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [And 演算子](and-operator.md)
- [IsFalse 演算子](isfalse-operator.md)
- [Visual Basic の論理演算子とビット処理演算子](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
