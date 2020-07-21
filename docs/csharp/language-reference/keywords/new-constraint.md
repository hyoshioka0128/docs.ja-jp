---
title: new 制約 - C# リファレンス
ms.date: 07/20/2015
helpviewer_keywords:
- new constraint keyword [C#]
ms.assetid: 58850b64-cb97-4136-be50-1f3bc7fc1da9
ms.openlocfilehash: 6f6d1b663d03dc9b3adf0e7055dcffacc79d83dc
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82795340"
---
# <a name="new-constraint-c-reference"></a>new 制約 (C# リファレンス)

`new` 制約は、ジェネリック クラス宣言内の型引数に、パブリックでパラメーターなしのコンストラクターが必要であることを指定します。 `new` 制約を使用する場合、型を抽象型にすることはできません。

`new` 制約は、次の例に示すように、ジェネリック クラスである型の新しいインスタンスを作成する場合に型パラメーターに適用されます。

[!code-csharp[csrefKeywordsOperator#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#5)]

`new()` 制約を別の制約と併用する場合、この制約を最後に指定する必要があります。

[!code-csharp[csrefKeywordsOperator#6](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsOperator/CS/csrefKeywordsOperators.cs#6)]

詳細については、「[型パラメーターの制約](../../programming-guide/generics/constraints-on-type-parameters.md)」を参照してください。

`new` キーワードは、[型のインスタンスの作成](../operators/new-operator.md)に使用することも、または[メンバーの宣言修飾子](new-modifier.md)として使用することもできます。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)の「[型パラメーターの制約](~/_csharplang/spec/classes.md#type-parameter-constraints)」セクションを参照してください。

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [ジェネリック](../../programming-guide/generics/index.md)
