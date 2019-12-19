---
title: do - C# リファレンス
ms.custom: seodec18
ms.date: 05/28/2018
f1_keywords:
- do_CSharpKeyword
- do
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
ms.openlocfilehash: 5612cfb2462117ac431de9c702cd8137f495e5dc
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74551809"
---
# <a name="do-c-reference"></a>do (C# リファレンス)

`do` ステートメントでは、指定されたブール式が `true` と評価される間、ステートメントまたはステートメント ブロックが実行されます。 ループの各実行の後に式が評価されるため、`do-while` ループは 1 回以上実行されます。 [while](while.md) ループは、これとは異なり、0 回以上実行されます。

`do` ステートメント ブロック内の任意の位置で、[break](break.md) ステートメントを使用してループを抜けることができます。

[continue](continue.md) ステートメントを使用すると、`while` 式の評価に直接ステップ実行できます。 式の評価が `true` の場合、ループの最初のステートメントから実行が続行されます。 それ以外の場合、実行は、ループの後の最初のステートメントから続行されます。

また、[goto](goto.md)、[return](return.md)、[throw](throw.md) ステートメントのいずれかを使って `do-while` ループを終了することもできます。

## <a name="example"></a>例

`do` ステートメントの使用方法を次の例に示します。 **[実行]** を選択して、コード例を実行します。 その後に、コードを変更し、もう一度実行することができます。

[!code-csharp-interactive[do loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#4)]

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](/dotnet/csharp/language-reference/language-specification/introduction)」の [do ステートメント](~/_csharplang/spec/statements.md#the-do-statement)に関するセクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [while ステートメント](while.md)
