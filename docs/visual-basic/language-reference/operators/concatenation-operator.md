---
title: '&amp; 演算子'
ms.date: 07/20/2015
f1_keywords:
- vb.&
helpviewer_keywords:
- And (&) operator
- ampersand operator (&)
- '& operator'
- concatenation operators [Visual Basic], syntax
- strings [Visual Basic], concatenating
ms.assetid: fefc3d00-cbf1-475c-8c5e-6fb213b3f85a
ms.openlocfilehash: d778c0c99d6d074fe8b73aaf3660074643e7e136
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84371610"
---
# <a name="amp-operator-visual-basic"></a>&amp; 演算子 (Visual Basic)
2 つの式の文字列連結を生成します。  
  
## <a name="syntax"></a>構文  
  
```vb  
result = expression1 & expression2  
```  
  
## <a name="parts"></a>指定項目  
 `result`  
 必須です。 任意の `String` または `Object` 変数。  
  
 `expression1`  
 必須です。 `String` に拡大変換されるデータ型を持つ任意の式。  
  
 `expression2`  
 必須です。 `String` に拡大変換されるデータ型を持つ任意の式。  
  
## <a name="remarks"></a>Remarks  
 `expression1` または `expression2` のデータ型が `String` ではなく `String` に拡大変換される場合は、`String` に変換されます。 いずれのデータ型も `String` に拡大変換されない場合、コンパイラはエラーを生成します。  
  
 `result` のデータ型は `String` です。 いずれかまたは両方の式が [Nothing](../nothing.md) に評価される場合、または値が <xref:System.DBNull.Value?displayProperty=nameWithType> の場合は、"" の値を持つ文字列として扱われます。  
  
> [!NOTE]
> `&` 演算子は "*オーバーロード*" できます。つまり、オペランドの型がクラスまたは構造体であるとき、そのクラスまたは構造体でその動作を再定義できます。 コードで、そのようなクラスまたは構造体に対してこの演算子が使用される場合は、再定義された動作を理解していることを確認してください。 詳細については、「 [Operator Procedures](../../programming-guide/language-features/procedures/operator-procedures.md)」を参照してください。  
  
> [!NOTE]
> アンパサンド (&) 文字は `Long` 型として変数を識別するためにも使用できます。 詳細については、「[型文字](../../programming-guide/language-features/data-types/type-characters.md)」を参照してください。  
  
## <a name="example"></a>例  
 この例では、`&` 演算子を使用して、文字列の連結を強制的に実行します。 結果は、2 つの文字列オペランドの連結を表す文字列値になります。  
  
 [!code-vb[VbVbalrOperators#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#2)]  
  
## <a name="see-also"></a>関連項目

- [& = 演算子](and-assignment-operator.md)
- [連結演算子](concatenation-operators.md)
- [Visual Basic における演算子の優先順位](operator-precedence.md)
- [機能別の演算子一覧](operators-listed-by-functionality.md)
- [Visual Basic の連結演算子](../../programming-guide/language-features/operators-and-expressions/concatenation-operators.md)
