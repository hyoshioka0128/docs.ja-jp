---
title: Xor 演算子
ms.date: 07/20/2015
f1_keywords:
- vb.Xor
helpviewer_keywords:
- exclusive OR operator [Visual Basic]
- logical exclusion
- operators [Visual Basic], exclusive or
- exclusion operator [Visual Basic]
- operators [Visual Basic], bitwise
- bitwise operators [Visual Basic], XOR operator
- Xor operator [Visual Basic]
- Xor keyword [Visual Basic]
- bitwise comparison [Visual Basic]
ms.assetid: 036000a9-3934-4e7f-a9d0-a816de3d84a6
ms.openlocfilehash: 999050314d674fa98833083d84796e471c22971d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406341"
---
# <a name="xor-operator-visual-basic"></a>Xor 演算子 (Visual Basic)
2 つの `Boolean` 式の場合は排他的論理和、2 つの数値式の場合はビットごとの排他を求めます。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = expression1 Xor expression2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `Boolean` または数値変数。 ブール値の比較の場合、`result` は 2 つの `Boolean` 値の排他的論理和 (排他的論理和演算) です。 ビットごとの演算の場合、`result` は 2 つの数値ビット パターンのビットごとの排他 (ビットごとの排他的論理和演算) を表す数値です。  
  
 `expression1`  
 必須です。 任意の `Boolean` または数値式。  
  
 `expression2`  
 必須です。 任意の `Boolean` または数値式。  
  
## <a name="remarks"></a>Remarks  
 ブール値の比較では、`expression1` と `expression2` のうち 1 つだけが `True` に評価される場合にのみ、`result` は `True` になります。 つまり、`expression1` と `expression2` とが逆の `Boolean` 値に評価される場合、かつその場合に限ります。 次の表は、`result` がどのように決定されるかを示しています。  
  
|`expression1` が次の場合|かつ、`expression2` が次の場合|`result` の値は次のようになります|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`False`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
> ブール値の比較では、`Xor` 演算子は常に両方の式を評価します。これには、プロシージャ呼び出しを含めることができます。 結果は常に両方のオペランドに依存するため、`Xor` に対応するショートサーキットはありません。 "*ショートサーキット*" 論理演算子については、「[AndAlso 演算子](andalso-operator.md)」、および「[OrElse 演算子](orelse-operator.md)」を参照してください。  
  
 ビットごとの演算の場合、`Xor` 演算子は、2 つの数値式でまったく同じ位置にあるビットのビットごとの比較を実行し、次の表に従って `result` に対応するビットを設定します。  
  
|`expression1` 内のビットが次の場合|かつ、`expression2` 内のビットが次の場合|`result` 内のビットは次のようになります|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|0|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
> 論理演算子とビット演算子は、他の算術演算子および関係演算子より優先順位が低いので、正確な実行を保証するために、ビットごとの演算はかっこで囲む必要があります。  
  
 たとえば、5 `Xor` 3 は 6 です。 なぜそのようになるのかを確認するには、5 と 3 をそれぞれのバイナリ表現 (101 および 011) に変換します。 次に、前の表を使用して、101 Xor 011 が 110 になることを確認します。これは 10 進数 6 のバイナリ表現です。  
  
## <a name="data-types"></a>データの種類  
 オペランドが 1 つの `Boolean` 式と 1 つの数値式で構成されている場合、Visual Basic では `Boolean` 式が数値に変換され (`True` の場合は –1、`False` の場合は 0)、ビットごとの演算が実行されます。  
  
 `Boolean` の比較の場合、結果のデータ型は `Boolean` になります。 ビットごとの比較の場合、結果のデータ型は `expression1` および `expression2` のデータ型に適した数値型になります。 [演算子の結果のデータ型](data-types-of-operator-results.md)に関するページ内の表 "関係とビットごとの比較" を参照してください。  
  
## <a name="overloading"></a>オーバーロード  
 `Xor` 演算子を "*オーバーロード*" できます。つまり、オペランドの型がクラスまたは構造体であるとき、そのクラスまたは構造体で、演算子の動作を再定義できます。 コード内で、そのようなクラスまたは構造体に対してこの演算子が使用されている場合は、再定義されたその動作を必ず理解してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Xor` 演算子を使用して、2 つの式の排他的論理和 (排他的論理和演算) を実行します。 結果は、それらの式のうちの 1 つだけが `True` であるかどうかを表す `Boolean` 値となります。  
  
 [!code-vb[VbVbalrOperators#40](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#40)]  
  
 前の例では、それぞれ `False`、`True`、および `False` の結果が生成されます。  
  
## <a name="example"></a>例  
 次の例では、`Xor` 演算子を使用して、2 つの数値式の個々のビットに対して排他的論理和 (排他的論理和演算) を実行します。 オペランド内の対応するビットのうちの 1 つだけが 1 に設定されている場合に、結果パターンのビットが設定されます。  
  
 [!code-vb[VbVbalrOperators#41](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#41)]  
  
 前の例では、それぞれ 2、12、14 の結果が生成されます。  
  
## <a name="see-also"></a>関連項目

- [論理演算子とビット処理演算子 (Visual Basic)](logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic の論理演算子とビット演算子](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
