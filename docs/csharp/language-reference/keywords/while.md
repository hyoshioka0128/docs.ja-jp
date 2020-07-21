---
title: while - C# リファレンス
ms.date: 05/28/2018
f1_keywords:
- while_CSharpKeyword
- while
helpviewer_keywords:
- while keyword [C#]
ms.assetid: 72a0765c-6852-4aca-b327-4a11cb7f5c59
ms.openlocfilehash: af616c2381b993f86296cbfa43a01ba2f9e000c2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401863"
---
# <a name="while-c-reference"></a>while (C# リファレンス)

`while` ステートメントでは、指定されたブール式が `true` と評価される間に、ステートメントまたはステートメント ブロックが実行されます。 ループの各実行の前に式が評価されるため、`while` ループは 0 回以上実行されます。 [do](do.md) ループは、これとは異なり、1 回以上実行されます。

`while` ステートメント ブロック内の任意の位置で、[break](break.md) ステートメントを使用してループを抜けることができます。

[continue](continue.md) ステートメントを使用すると、`while` 式の評価に直接ステップ実行できます。 式の評価が `true` の場合、ループの最初のステートメントから実行が続行されます。 それ以外の場合、実行は、ループの後の最初のステートメントから続行されます。

また、[goto](goto.md)、[return](return.md)、[throw](throw.md) ステートメントのいずれかを使って `while` ループを終了することもできます。

## <a name="example"></a>例

`while` ステートメントの使用方法を次の例に示します。 **[実行]** を選択して、コード例を実行します。 その後に、コードを変更し、もう一度実行することができます。

[!code-csharp-interactive[while loop example](snippets/IterationKeywordsExamples.cs#3)]

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](/dotnet/csharp/language-reference/language-specification/introduction)」の [while ステートメント](~/_csharplang/spec/statements.md#the-while-statement)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [do ステートメント](do.md)
