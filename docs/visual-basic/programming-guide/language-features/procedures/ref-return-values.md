---
title: 参照戻り値
ms.date: 04/28/2017
helpviewer_keywords:
- variables [Visual Basic]
- ref return values [Visual Basic]
- ref returns [Visual Basic]
ms.assetid: 5ef0cc69-eb3a-4a67-92a2-78585f223cb5
ms.openlocfilehash: f2a92c584dbb12a322e28435d797fa4d7c2f6dbb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186933"
---
# <a name="support-for-reference-return-values-visual-basic"></a>参照戻り値のサポート (Visual Basic)

C# 7.0 以降の C# 言語では、"*参照戻り値*" がサポートされています。 参照戻り値は、メソッドに参照渡しされる引数の逆と考えると理解しやすくなります。 参照渡しされた引数が変更されると、変更は呼び出し元の変数の値に反映されます。 メソッドが参照戻り値を呼び出し元に返すと、呼び出し元によって参照戻り値に加えられた変更が、呼び出されたメソッドのデータに反映されます。

Visual Basic では、参照戻り値を使用するメソッドを作成することはできませんが、参照戻り値を使用することは可能です。 つまり、参照戻り値を使用してメソッドを呼び出し、その戻り値を変更できます。参照戻り値に対する変更は、呼び出されたメソッドのデータに反映されます。

## <a name="modifying-the-ref-return-value-directly"></a>参照戻り値を直接変更する

常に成功し、`ByRef` パラメーターがないメソッドの場合、参照戻り値を直接変更できます。 これを行うには、参照戻り値を返す式に新しい値を割り当てます。

次の C# の例では、内部値をインクリメントし、それを参照戻り値として返す `NumericValue.IncrementValue` メソッドを定義しています。

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/ref-returns1.cs)]

次の Visual Basic の例では、この参照戻り値が呼び出し元によって変更されます。 `NumericValue.IncrementValue` メソッド呼び出しを含む行では、メソッドに値を割り当てていないことに注意してください。 代わりに、メソッドによって返される参照戻り値に値を割り当てます。

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/programming-guide/language-features/procedures/use-ref-returns1.vb)]

## <a name="using-a-helper-method"></a>ヘルパー メソッドを使用する

メソッド呼び出しの参照戻り値を直接変更することが必ずしも望ましいとは限らない場合もあります。 たとえば、文字列を返す検索メソッドは、常に一致するものを見つけるとは限りません。 その場合、検索が成功した場合にのみ、参照戻り値を変更します。

次の C# の例はこのシナリオを示しています。 C# で記述された `Sentence` クラスを定義し、指定された部分文字列で始まる文の次の単語を検索する `FindNext` メソッドを含めます。 文字列は参照戻り値として返され、参照によりメソッドに渡される `Boolean` 変数は検索が成功したかどうかを示します。 参照戻り値は、返された値を読み取るだけでなく、呼び出し元がそれを変更することもでき、その変更が `Sentence` クラスの内部に含まれるデータに反映されることを示しています。

[!code-csharp[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-returns.cs)]

この例での参照戻り値の直接変更は信頼できません。メソッド呼び出しで一致するものが見つからず、文の最初の単語が返される可能性があるためです。 その場合、呼び出し元は文の最初の単語を誤って変更することになります。 これは、呼び出し元が `null` (Visual Basic では `Nothing`) を返すことによって防ぐことができる場合があります。 ただし、その場合、値が `Nothing` の文字列を変更しようとすると、<xref:System.NullReferenceException> がスローされます。 呼び出し元が <xref:System.String.Empty?displayProperty=nameWithType> を返すことによって防ぐことができる場合もありますが、そのためには、値が <xref:System.String.Empty?displayProperty=nameWithType> である文字列変数を呼び出し元で定義する必要があります。 呼び出し元はその文字列を変更できますが、変更された文字列は `Sentence` クラスによって格納された文の単語と関係がないため、変更自体に何の意味もありません。

このシナリオに対応する最良の方法は、ヘルパー メソッドに対して参照戻り値を参照渡しにすることです。 ヘルパー メソッドには、メソッド呼び出しが成功したかどうかを判断し、成功した場合は参照戻り値を変更するロジックを含めます。 次の例は考えられる実装を示しています。

[!code-vb[Ref-Return](../../../../../samples/snippets/visualbasic/getting-started/ref-return-helper.vb#1)]

## <a name="see-also"></a>関連項目

- [引数の値渡しと参照渡し](passing-arguments-by-value-and-by-reference.md)
- [Visual Basic におけるプロシージャ](index.md)
