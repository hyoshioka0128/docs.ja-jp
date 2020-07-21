---
title: OrElse 演算子
ms.date: 07/20/2015
f1_keywords:
- OrElse
- vb.OrElse
helpviewer_keywords:
- short-circuiting
- operators [Visual Basic], short-circuiting
- operators [Visual Basic], disjunction
- short-circuit evaluation
- OrElse operator [Visual Basic]
ms.assetid: 253803d8-05b0-47d7-b213-abd222847779
ms.openlocfilehash: 3095a11523eeb8ec531c7f312fca74d2a070c92f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401408"
---
# <a name="orelse-operator-visual-basic"></a>OrElse 演算子 (Visual Basic)
2 つの式の短絡包含的論理和を求めます。  
  
## <a name="syntax"></a>構文  
  
```vb
result = expression1 OrElse expression2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意のブール型 ( `Boolean` ) の式を指定します。  
  
 `expression1`  
 必須です。 任意のブール型 ( `Boolean` ) の式を指定します。  
  
 `expression2`  
 必須です。 任意のブール型 ( `Boolean` ) の式を指定します。  
  
## <a name="remarks"></a>Remarks  
 コンパイルされたコードが、ある式の評価を別の式の結果に応じてバイパスできる場合、論理演算は "*短絡*" であると言われます。 最初に評価された式の結果によって演算の最終結果が決まる場合、最終結果を変更できないため、2 番目の式を評価する必要はありません。 バイパスされた式が複雑な場合や、プロシージャ呼び出しが関係している場合に、短絡によってパフォーマンスを向上させることができます。  
  
 いずれかまたは両方の式が `True` に評価される場合、`result` は `True` です。 次の表は、`result` がどのように決定されるかを示しています。  
  
|`expression1` が次の場合|かつ、`expression2` が次の場合|`result` の値は次のとおり|  
|-------------------------|--------------------------|------------------------------|  
|`True`|(評価されていない)|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
## <a name="data-types"></a>データの種類  
 `OrElse` 演算子は [Boolean データ型](../data-types/boolean-data-type.md)に対してのみ定義されます。 Visual Basic は、式を評価する前に、必要に応じて各オペランドを `Boolean` に変換します。 結果を数値型に代入すると、Visual Basic によって `Boolean` からその型への変換が行われ、`False` が `0` になり、`True` が `-1` になります。
詳細については、[ブール型変換](../data-types/boolean-data-type.md#type-conversions)に関する記事をご覧ください。
  
## <a name="overloading"></a>オーバーロード  
 [Or 演算子](or-operator.md)と [IsTrue 演算子](istrue-operator.md)は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、このクラスまたは構造体はその動作を再定義できます。 `Or` と `IsTrue` の演算子をオーバーロードすると、`OrElse` 演算子の動作に影響します。 コードで、`Or` と `IsTrue` をオーバーロードするクラスまたは構造体で `OrElse` を使用する場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`OrElse` 演算子を使用して、2 つの式の論理和を求めます。 結果は、2 つの式のいずれかが true かどうかを表す `Boolean` 値です。 最初の式が `True` 場合、2 番目の式は評価されません。  
  
 [!code-vb[VbVbalrOperators#37](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#37)]  
  
 前の例では、それぞれ `True`、`True`、`False` の結果が得られます。 `firstCheck` の計算では、最初の式が既に `True` であるため、2 番目の式は評価されません。 ただし、2 番目の式は `secondCheck` の計算で評価されます。  
  
## <a name="example"></a>例  
 次の例は、2 つのプロシージャ呼び出しを含む `If`...`Then` ステートメントを示しています。 最初の呼び出しで `True` が返された場合、2 番目のプロシージャは呼び出されません。 コードのこのセクションの実行時に常に実行する必要がある重要なタスクを 2 番目のプロシージャが実行すると場合、予期しない結果が生じる可能性があります。  
  
 [!code-vb[VbVbalrOperators#38](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#38)]  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Or 演算子](or-operator.md)
- [IsTrue 演算子](istrue-operator.md)
- [Visual Basic の論理演算子とビット演算子](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
