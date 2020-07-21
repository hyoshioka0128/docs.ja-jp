---
title: Or 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.Or
helpviewer_keywords:
- Or operator [Visual Basic]
- operators [Visual Basic], bitwise
- inclusive Or operator [Visual Basic]
- bitwise operators [Visual Basic], OR operator
- Or keyword [Visual Basic]
- operators [Visual Basic], inclusive or
- operators [Visual Basic], disjunction
- bitwise comparison [Visual Basic]
- logical disjunction
- disjunction operator [Visual Basic]
ms.assetid: 41ed6905-bf3d-468a-9e3b-03c10d461891
ms.openlocfilehash: 657b2a473b23789a8ba25fbd11c6b83538fa7803
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401421"
---
# <a name="or-operator-visual-basic"></a>Or 演算子 (Visual Basic)
2 つの `Boolean` 式の場合は論理和演算、2 つの数値式の場合はビットごとの論理和演算を実行します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = expression1 Or expression2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `Boolean` または数値式。 `Boolean` の比較の場合、`result` は 2 つの `Boolean` 値の包含論理和演算となります。 ビットごとの演算の場合、`result` は 2 つの数値ビット パターンのビットごとの包含論理和演算を表す数値です。  
  
 `expression1`  
 必須です。 任意の `Boolean` または数値式。  
  
 `expression2`  
 必須です。 任意の `Boolean` または数値式。  
  
## <a name="remarks"></a>Remarks  
 `Boolean` の比較では、`expression1` と `expression2` の両方が `False` に評価された場合にのみ、`result` は `False` になります。 次の表は、`result` がどのように決定されるかを示しています。  
  
|`expression1` が次の場合|かつ、`expression2` が次の場合|`result` の値は次のようになります|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
> `Boolean` の比較では、`Or` 演算子は常に両方の式を評価します。これには、プロシージャ呼び出しの実行を含めることができます。 [OrElse 演算子](orelse-operator.md)は "*ショートサーキット*" を実行します。つまり、`expression1` が `True` の場合、`expression2` は評価されません。  
  
 ビットごとの演算の場合、`Or` 演算子は、2 つの数値式でまったく同じ位置にあるビットのビットごとの比較を実行し、次の表に従って `result` に対応するビットを設定します。  
  
|`expression1` 内のビットが次の場合|かつ、`expression2` 内のビットが次の場合|`result` 内のビットは次のようになります|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|1|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
> 論理およびビット処理演算子は、他の算術演算子および関係演算子より優先順位が低いので、正確に実行するために、ビットごとの演算はかっこで囲む必要があります。  
  
## <a name="data-types"></a>データの種類  
 オペランドが 1 つの `Boolean` 式と 1 つの数値式で構成されている場合、Visual Basic は `Boolean` 式を数値に変換し (`True` の場合は 1、`False` の場合は 0)、ビットごとの演算を実行します。  
  
 `Boolean` の比較の場合、結果のデータ型は `Boolean` になります。 ビットごとの比較の場合、結果のデータ型は `expression1` および `expression2` のデータ型に適した数値型になります。 「[演算子の結果のデータ型](data-types-of-operator-results.md)」の「関係とビットごとの比較」の表を参照してください。  
  
## <a name="overloading"></a>オーバーロード  
 `Or` 演算子は "*オーバーロード*" できます。つまり、オペランドがクラスまたは構造体の型を持っているときに、クラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Or` 演算子を使用して、2 つの式の包含論理和演算を実行します。 結果は、2 つの式のいずれかが `True` かどうかを表す `Boolean` 値です。  
  
 [!code-vb[VbVbalrOperators#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#35)]  
  
 前の例では、それぞれ `True`、`True`、`False` の結果が生成されます。  
  
## <a name="example"></a>例  
 次の例では、`Or` 演算子を使用して、2 つの数値式の個々のビットに対して包含論理和演算を実行します。 オペランドの対応するビットのいずれかが 1 に設定されている場合、結果パターンのビットが設定されます。  
  
 [!code-vb[VbVbalrOperators#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#36)]  
  
 前の例では、それぞれ 10、14、14 の結果が生成されます。  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [OrElse 演算子](orelse-operator.md)
- [Visual Basic の論理演算子とビット処理演算子](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
