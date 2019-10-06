---
title: Null 許容値型 - C# プログラミング ガイド
ms.custom: seodec18
description: C# の Null 許容値型とその使用方法について説明します
ms.date: 09/26/2019
helpviewer_keywords:
- nullable value types [C#]
ms.assetid: e473cb01-28ca-42be-9cea-f717055d72c6
ms.openlocfilehash: b8b52e7fb34adf65d5c76d59811ea6dd0ab16a98
ms.sourcegitcommit: da2dd2772fcf32b44eb18b1cbe8affd17b1753c9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396218"
---
# <a name="nullable-value-types-c-programming-guide"></a>Null 許容値型 (C# プログラミング ガイド)

Null 許容値型は、<xref:System.Nullable%601?displayProperty=nameWithType> 構造体のインスタンスです。 Null 許容値型は、基になる型 `T` のすべての値と、追加の [null](../../language-reference/keywords/null.md) 値を表すことができます。 基になる型 `T` は Null 非許容のあらゆる[値の型](../../language-reference/keywords/value-types.md)にすることができます。 `T` を参照型にすることはできません。

> [!NOTE]
> C# 8.0 で、Null 許容参照型機能が導入されました。 詳細については、「[null 許容参照型](../../nullable-references.md)」を参照してください。 Null 許容値型は、C# 2 から使用できます。

たとえば、`null` または <xref:System.Int32.MinValue?displayProperty=nameWithType> から <xref:System.Int32.MaxValue?displayProperty=nameWithType> のいずれかの整数値を `Nullable<int>` および [true](../../language-reference/keywords/true-literal.md)、[false](../../language-reference/keywords/false-literal.md) に、または `null` を `Nullable<bool>` に割り当てることができます。

Null 許容値型は基になる型の未定義の値を表す必要があるときに使用します。 ブール値変数は `true` と `false` の 2 つの値しか持つことができません。 "未定義の" 値はありません。 多くのプログラミング アプリケーションの中でも特にデータベース操作では、変数値が未定義か、ない場合があります。 たとえば、データベース フィールドには、true や false の値が入力されている場合や、値がまったく入力されていない場合があります。 その場合は、`Nullable<bool>` 型を使用します。

Null 許容値型には次の特性があります。

- Null 許容値型は、`null` 値を割り当てることができる、値型の変数を表します。

- 構文 `T?` は `Nullable<T>` の短縮形です。 この 2 つの形式は同義であり、どちらでも使用できます。

- Null 許容値型に値を割り当てる方法は、基になる値の型の場合と同じです。たとえば、`int? x = 10;` や `double? d = 4.108;` と指定します。 `null` 値を `int? x = null;` のように割り当てることもできます。

- null かどうかを確認して値を取得するには、<xref:System.Nullable%601.HasValue%2A?displayProperty=nameWithType> と <xref:System.Nullable%601.Value%2A?displayProperty=nameWithType> の読み取り専用プロパティを使用します。たとえば、`if (x.HasValue) y = x.Value;` と指定します。

  - <xref:System.Nullable%601.HasValue%2A> プロパティは、変数に値が含まれる場合は `true` を返し、`null` の場合は `false` を返します。

  - <xref:System.Nullable%601.Value%2A> プロパティは、<xref:System.Nullable%601.HasValue%2A> で `true` が返される場合に値を返します。 それ以外の場合は、<xref:System.InvalidOperationException> がスローされます。

- Null 許容値型では `==` 演算子と `!=` 演算子も使用できます。たとえば、`if (x != null) y = x.Value;` のように指定します。 `a` と `b` の両方が null の場合、`a == b` は `true` と評価されます。

- C# 7.0 以降では、[パターン マッチング](../../pattern-matching.md#the-is-type-pattern-expression)を使用して Null 許容型の値を調べて取得することができます (`if (x is int valueOfX) y = valueOfX;`)。

- `T?` の既定値は <xref:System.Nullable%601.HasValue%2A> プロパティが `false` を返すインスタンスです。

- Null 許容型の値が `null` である場合に、基になる値の型の割り当てられた値、または[既定](../../language-reference/keywords/default-values-table.md)値のどちらかを返すには、<xref:System.Nullable%601.GetValueOrDefault> メソッドを使用します。

- Null 許容型の値が `null` である場合に、割り当てられた値、または指定された既定値のどちらかを返すには、<xref:System.Nullable%601.GetValueOrDefault(%600)> メソッドを使用します。

- Null 許容型の値に基づいて基になる値の型の変数に値を割り当てるには、[Null 合体演算子](../../language-reference/operators/null-coalescing-operator.md) `??` を使用します (例: `int? x = null; int y = x ?? -1;`)。 例では、`x` が `null` であるため、`y` の結果値は `-1` です。

- 2 つの値の型の間でユーザー定義の変換を定義している場合は、それに対応する null 許容型で同じ変換を使用することもできます。

- 入れ子になった Null 許容値型は許可されません。 次の行はコンパイルされません。`Nullable<Nullable<int>> n;`

詳細については、「[Null 許容値型の使用 (C# プログラミング ガイド)](using-nullable-types.md)」と「[方法: Null 許容値型を識別する (C# プログラミング ガイド)](how-to-identify-a-nullable-type.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [C# プログラミング ガイド](../index.md)
- [??演算子](../../language-reference/operators/null-coalescing-operator.md)
- [null 許容値型 (Visual Basic)](../../../visual-basic/programming-guide/language-features/data-types/nullable-value-types.md)
- <xref:System.Nullable%601?displayProperty=nameWithType>
- <xref:System.Nullable?displayProperty=nameWithType>
