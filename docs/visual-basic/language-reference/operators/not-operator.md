---
title: Not 演算子
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
ms.openlocfilehash: 56cdeb80a217dbce15921eddd6a43d8d1b049376
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401460"
---
# <a name="not-operator-visual-basic"></a>Not 演算子 (Visual Basic)
`Boolean` 式の場合は論理否定、数値式の場合はビットごとの否定を求めます。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = Not expression  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `Boolean` または数値式。  
  
 `expression`  
 必須です。 任意の `Boolean` または数値式。  
  
## <a name="remarks"></a>Remarks  
 次の表は、`Boolean` 式で、`result` がどのように決定されるかを示しています。  
  
|`expression` が次の場合|`result` の値は次のようになります|  
|------------------------|------------------------------|  
|`True`|`False`|  
|`False`|`True`|  
  
 数値式の場合、`Not` 演算子は、次の表に従って数値式のビット値を反転させ、`result` に対応するビットを設定します。  
  
|`expression` 内のビットが次の場合|`result` 内のビットは次のようになります|  
|-------------------------------|----------------------------|  
|1|0|  
|0|1|  
  
> [!NOTE]
> 論理演算子とビット演算子は、他の算術演算子および関係演算子より優先順位が低いので、正確に実行するために、ビットごとの演算はかっこで囲む必要があります。  
  
## <a name="data-types"></a>データの種類  
 ブール値の否定の場合、結果のデータ型は `Boolean` になります。 ビットごとの否定の場合、結果のデータ型は `expression` のデータ型と同じになります。 ただし、式が `Decimal` の場合、結果は `Long` になります。  
  
## <a name="overloading"></a>オーバーロード  
 `Not` 演算子は "*オーバーロード*" できます。つまり、オペランドがあるクラスまたは構造体の型を持っているときに、そのクラスまたは構造体はその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を必ず理解してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、`Boolean` 式で `Not` 演算子を使用して論理否定を実行しています。 この結果は、式の値の反転を表す `Boolean` 値です。  
  
 [!code-vb[VbVbalrOperators#33](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#33)]  
  
 前の例では、それぞれ `False` と `True` の結果が生成されます。  
  
## <a name="example"></a>例  
 次の例では、`Not` 演算子を使用して、数値式の個々のビットの論理否定を実行しています。 結果パターンのビットは、オペランド パターンの対応するビットの反転に設定されます (符号ビットを含む)。  
  
 [!code-vb[VbVbalrOperators#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#34)]  
  
 前の例では、結果としてそれぞれ –11、–9、および –7 が生成されます。  
  
## <a name="see-also"></a>関連項目

- [論理/ビット演算子 (Visual Basic)](logical-bitwise-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic の論理演算子とビット演算子](../../programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
