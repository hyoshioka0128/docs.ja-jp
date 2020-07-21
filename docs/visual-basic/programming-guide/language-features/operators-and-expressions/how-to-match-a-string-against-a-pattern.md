---
title: '方法: 文字列がパターンに一致するかを調べる'
ms.date: 07/20/2015
helpviewer_keywords:
- comparison operators [Visual Basic], comparing strings
- pattern matching
- strings [Visual Basic], comparing
- string comparison [Visual Basic], operators
- Visual Basic code, operators
- pattern matching [Visual Basic], string comparison
- string comparison [Visual Basic]
- Like operator [Visual Basic], pattern matching
- pattern matching, empty strings
- operators [Visual Basic], comparison
ms.assetid: 19a83804-b5af-4739-928b-ac93e64e457f
ms.openlocfilehash: d8a3c363d1a443db4a0b7633e380562af1913aca
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403447"
---
# <a name="how-to-match-a-string-against-a-pattern-visual-basic"></a>方法: 文字列がパターンに一致するかどうかを調べる (Visual Basic)

[文字列データ型](../../../language-reference/data-types/string-data-type.md)の式がパターンを満たしているかどうかを確認するには、[Like 演算子](../../../language-reference/operators/like-operator.md)を使用できます。

`Like` は 2 つのオペランドを受け取ります。 左オペランドは文字列式であり、右オペランドは照合に使用されるパターンを含む文字列です。 `Like` からは、文字列式がパターンを満たしているかどうかを示す `Boolean` 値が返されます。

文字列式の各文字を、特定の文字、ワイルドカード文字、文字リスト、または文字範囲と照合できます。 パターン文字列内の指定の位置は、文字列式で照合される文字の位置に対応しています。

## <a name="to-match-a-character-in-the-string-expression-against-a-specific-character"></a>文字列式の文字を特定の文字と照合するには

特定の文字をパターン文字列に直接含めます。 一部の特殊文字は角かっこ (`[ ]`) で囲む必要があります。 詳細については、「[Like 演算子](../../../language-reference/operators/like-operator.md)」を参照してください。

次の例では、`myString` が 1 つの文字 `H` で構成されているかどうかをテストします。

[!code-vb[VbVbalrOperators#70](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#70)]

## <a name="to-match-a-character-in-the-string-expression-against-a-wildcard-character"></a>文字列式の文字をワイルドカード文字と照合するには

パターン文字列に疑問符 (`?`) を含めます。 この位置にある任意の有効な文字が一致と見なされます。

次の例では、`myString` が、1 つの文字 `W` と、それに続く任意の値のちょうど 2 つの文字で構成されているかどうかをテストします。

[!code-vb[VbVbalrOperators#71](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#71)]

## <a name="to-match-a-character-in-the-string-expression-against-a-list-of-characters"></a>文字列式の文字を文字のリストと照合するには

角かっこ (`[ ]`) をパターン文字列に含め、角かっこの内側に文字のリストを含めます。 文字をコンマやその他の区切り記号で区切らないでください。 リスト内の任意の 1 文字が一致と見なされます。

次の例では、`myString` が、任意の有効な文字と、それに続く `A`、`C`、または `E` のいずれか 1 文字のみで構成されるかどうかをテストします。

[!code-vb[VbVbalrOperators#72](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#72)]

この照合では、大文字と小文字が区別されることに注意してください。

## <a name="to-match-a-character-in-the-string-expression-against-a-range-of-characters"></a>文字列式の文字を文字の範囲と照合するには

パターン文字列に角かっこ (`[ ]`) を含め、角かっこ内にハイフン (`–`) で区切られた範囲内の最小文字と最大文字を含めます。 範囲内の任意の 1 文字が一致と見なされます。

次の例では、`myString` が、文字 `num` と、それに続く `i`、`j`、`k`、`l`、`m`、または `n` のいずれか 1 文字のみで構成されるかどうかをテストします。

[!code-vb[VbVbalrOperators#73](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#73)]

この照合では、大文字と小文字が区別されることに注意してください。

## <a name="matching-empty-strings"></a>空の文字列の照合

`Like` では、シーケンス `[]` は長さゼロの文字列 (`""`) として扱われます。 `[]` を使用して文字列式全体が空かどうかをテストできますが、文字列式の特定の位置が空であるかどうかをテストすることはできません。 空の位置がテストする必要があるオプションの 1 つである場合は、`Like` を複数回使用できます。

### <a name="to-match-a-character-in-the-string-expression-against-a-list-of-characters-or-no-character"></a>文字列式の文字を文字のリストまたは文字なしと照合するには

1. 同じ文字列式で `Like` 演算子を 2 回呼び出し、2 つの呼び出しを [Or 演算子](../../../language-reference/operators/or-operator.md)または [OrElse 演算子](../../../language-reference/operators/orelse-operator.md)のいずれかを使用して接続します。

2. 1 つ目の `Like` 句のパターン文字列には、角かっこ (`[ ]`) で囲んだ文字リストを含めます。

3. 2 つ目の `Like` 句のパターン文字列には、対象の位置に文字を配置しないでください。

    次の例では、7 桁の電話番号 `phoneNum` (ちょうど 3 桁の数字、それに続くスペース、ハイフン (`–`)、ピリオド (`.`)、またはまったく文字なし、それに続くちょうど 4 桁の数字) をテストします。

    [!code-vb[VbVbalrOperators#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#74)]

## <a name="see-also"></a>関連項目

- [比較演算子](../../../language-reference/operators/comparison-operators.md)
- [演算子および式](index.md)
- [Like 演算子](../../../language-reference/operators/like-operator.md)
- [String データ型](../../../language-reference/data-types/string-data-type.md)
