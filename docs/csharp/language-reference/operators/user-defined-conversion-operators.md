---
title: ユーザー定義の変換演算子 - C# リファレンス
description: C# でカスタムの暗黙的および明示的な型変換を定義する方法について説明します。
ms.date: 07/09/2019
f1_keywords:
- explicit_CSharpKeyword
- implicit_CSharpKeyword
helpviewer_keywords:
- explicit keyword [C#]
- implicit keyword [C#]
- conversion operator [C#]
- user-defined conversion [C#]
ms.openlocfilehash: 25f042dec5fd5594b7e166cc064394e90db01c27
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73036116"
---
# <a name="user-defined-conversion-operators-c-reference"></a>ユーザー定義の変換演算子 (C# リファレンス)

ユーザー定義型では、別の型との間にカスタムの暗黙的または明示的な変換を定義できます。

暗黙的変換では特別な構文を呼び出す必要はなく、代入やメソッド呼び出しなど、さまざまな状況で発生する可能性があります。 事前に定義された C# の暗黙的な変換は常に成功し、例外がスローされることはありません。 ユーザー定義の暗黙的な変換も同様に動作します。 カスタムの変換によって例外がスローされたり情報が失われたりする可能性がある場合は、明示的な変換として定義します。

ユーザー定義の変換は、[is](type-testing-and-cast.md#is-operator) および [as](type-testing-and-cast.md#as-operator) 演算子からは考慮されません。 ユーザー定義の明示的な変換を呼び出すには、[キャスト演算子 ()](type-testing-and-cast.md#cast-operator-) を使用します。

暗黙的または明示的な変換を定義するには、`operator` とそれぞれ `implicit` または `explicit` のキーワードを使用します。 変換を定義する型は、その変換のソース型またはターゲット型のいずれかである必要があります。 2 つのユーザー定義型間の変換は、2 つの型のどちらでも定義できます。

次の例は、暗黙的な変換と明示的な変換を定義する方法を示しています。

[!code-csharp[implicit an explicit conversions](~/samples/csharp/language-reference/operators/UserDefinedConversions.cs)]

また、事前に定義された C# 演算子をオーバーロードするには `operator` キーワードも使用します。 詳細については、「[演算子のオーバーロード](operator-overloading.md)」を参照してください。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、「[C# 言語仕様](~/_csharplang/spec/introduction.md)」の次のセクションを参照してください。

- [変換演算子](~/_csharplang/spec/classes.md#conversion-operators)
- [ユーザー定義の変換](~/_csharplang/spec/conversions.md#user-defined-conversions)
- [暗黙的な変換](~/_csharplang/spec/conversions.md#implicit-conversions)
- [明示的な変換](~/_csharplang/spec/conversions.md#explicit-conversions)

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# 演算子](index.md)
- [演算子のオーバーロード](operator-overloading.md)
- [型テストとキャスト演算子](type-testing-and-cast.md)
- [キャストと型変換](../../programming-guide/types/casting-and-type-conversions.md)
- [Chained user-defined explicit conversions in C#](https://blogs.msdn.microsoft.com/ericlippert/2007/04/16/chained-user-defined-explicit-conversions-in-c/) (C# でのユーザー定義の明示的変換の連結)
