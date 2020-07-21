---
title: 匿名型またはタプル型の選択
description: 匿名型またはタプル型を選択する適切なタイミングについて学習します。
author: IEvangelist
ms.author: dapine
ms.date: 07/01/2020
ms.technology: dotnet-standard
ms.openlocfilehash: 9c186133a639faf187c89d872856d860a20f5a2d
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174219"
---
# <a name="choosing-between-anonymous-and-tuple-types"></a>匿名型またはタプル型の選択

適切な型を選択するには、他の型と比較し、その使いやすさ、パフォーマンス、およびトレードオフを考慮する必要があります。 匿名型は C# 3.0 以降に使用できるようになりましたが、ジェネリック <xref:System.Tuple%602?displayProperty=nameWithType> 型は .NET Framework 4.0 で導入されました。 その後、<xref:System.ValueTuple%602?displayProperty=nameWithType> など、言語レベルのサポートで新しいオプションが導入されています。これにより、名前が示すように、匿名型の柔軟性を持つ値の型が提供されます。 この記事では、ある型よりもう一方を選択する適切なタイミングについて学習します。

## <a name="usability-and-functionality"></a>使いやすさと機能

匿名型は、C# 3.0 で統合言語クエリ (LINQ) 式と共に導入されました。 LINQ では、開発者は多くの場合、クエリからの結果を、操作するオブジェクトから選択されたいくつかのプロパティを保持する匿名型に射影します。 <xref:System.DateTime> オブジェクトの配列をインスタンス化し、2 つのプロパティを持つ匿名型に射影して、それらを反復処理する以下の例について考えてみます。

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var anonymous in
             dates.Select(
                 date => new { Formatted = $"{date:MMM dd, yyyy hh:mm zzz}", date.Ticks }))
{
    Console.WriteLine($"Ticks: {anonymous.Ticks}, formatted: {anonymous.Formatted}");
}
```

匿名型は、[`new`](../../csharp/language-reference/operators/new-operator.md) 演算子を使用してインスタンス化され、プロパティの名前と型は宣言から推論されます。 同じアセンブリ内の複数の匿名オブジェクト初期化子で、同じ順序で同じ名前と型を持つプロパティのシーケンスを指定した場合、コンパイラではそのオブジェクトを同じ型のインスタンスとして処理します。 これらのオブジェクトは、コンパイラで生成された同一の型情報を共有します。

前の C# スニペットでは、次のコンパイラによって生成された C# クラスと同様に、2 つのプロパティを持つ匿名型を射影しています。

```csharp
internal sealed class f__AnonymousType0
{
    public string Formatted { get; }
    public long Ticks { get; }

    public f__AnonymousType0(string formatted, long ticks)
    {
        Formatted = formatted;
        Ticks = ticks;
    }
}
```

詳細については、「[匿名型](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)」を参照してください。 LINQ クエリに射影する場合、タプルと同じ機能が存在します。プロパティを選択して、タプルにすることができます。 これらのタプルは、匿名型の場合と同様に、クエリを通過します。 次は、`System.Tuple<string, long>` を使用する以下の例を考えてみます。

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var tuple in
            dates.Select(
                date => new Tuple<string, long>($"{date:MMM dd, yyyy hh:mm zzz}", date.Ticks)))
{
    Console.WriteLine($"Ticks: {tuple.Item2}, formatted: {tuple.Item1}");
}
```

<xref:System.Tuple%602?displayProperty=nameWithType> では、インスタンスで `Item1`や `Item2` などの番号付きの項目プロパティが公開されます。 プロパティ名では序数のみが提供されるため、これらのプロパティ名を使用すると、プロパティ値の意図を理解するのがより難しくなる場合があります。 さらに、`System.Tuple` 型は参照 `class` 型となります。 しかし、<xref:System.ValueTuple%602?displayProperty=nameWithType> は `struct` 型の値です。 次の C# スニペットでは、`ValueTuple<string, long>` を使用して射影します。 この場合、リテラル構文を使用して割り当てられます。

```csharp-interactive
var dates = new[]
{
    DateTime.UtcNow.AddHours(-1),
    DateTime.UtcNow,
    DateTime.UtcNow.AddHours(1),
};

foreach (var (formatted, ticks) in
            dates.Select(
                date => (Formatted: $"{date:MMM dd, yyyy at hh:mm zzz}", date.Ticks)))
{
    Console.WriteLine($"Ticks: {ticks}, formatted: {formatted}");
}
```

タプルの詳細については、「[タプル型 (C# リファレンス)](../../csharp/language-reference/builtin-types/value-tuples.md)」または「[タプル (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/tuples.md)」を参照してください。

上記の例はすべて機能的には同等ですが、その使いやすさと基盤となる実装にはわずかな違いがあります。

## <a name="tradeoffs"></a>トレードオフ

<xref:System.Tuple>、および匿名型より優先して、常に <xref:System.ValueTuple> を使用することはできますが、考慮すべきトレードオフがあります。 <xref:System.ValueTuple> 型は変更可能ですが、<xref:System.Tuple> は読み取り専用です。 匿名型は式ツリーで使用できますが、タプルは使用できません。 次の表に、主ないくつかの相違点の概要を示します。

### <a name="key-differences"></a>主な相違点

| 名前                     | アクセス修飾子 | 種類     | カスタム メンバー名 | 分解のサポート | 式ツリーのサポート |
|--------------------------|-----------------|----------|----------------------|------------------------|-------------------------|
| 匿名型          | `internal`      | `class`  | ✔️                   | ❌                     | ✔️                     |
| <xref:System.Tuple>      | `public`        | `class`  | ❌                   | ❌                     | ✔️                     |
| <xref:System.ValueTuple> | `public`        | `struct` | ✔️                   | ✔️                     | ❌                     |

### <a name="serialization"></a>シリアル化

型を選択する際の重要な考慮事項の 1 つは、シリアル化する必要があるかどうかです。 シリアル化とは、オブジェクトの状態を永続化または転送できる形式に変換するプロセスのことです。 詳細については、[シリアル化](../../csharp/programming-guide/concepts/serialization/index.md)に関するページを参照してください。 シリアル化が重要な場合、`class` や `struct` の作成は、匿名型やタプル型よりも優先されます。

## <a name="performance"></a>パフォーマンス

これらの型の間のパフォーマンスは、シナリオによって異なります。 大きな影響は、割り当てとコピーの間のトレードオフに関係します。 ほとんどのシナリオでは、影響は小さくなります。 大きな影響が生じる可能性がある場合は、決定を知らせるために測定する必要があります。

## <a name="conclusion"></a>まとめ

開発者がタプル型または匿名型を選択する際に、考慮すべきいくつかの要素があります。 一般的には、[式ツリー](../../csharp/expression-trees.md)を操作せず、タプル構文に慣れている場合は、<xref:System.ValueTuple> を選択します。これは、名前プロパティに柔軟性のある値型が提供されるためです。 式ツリーを操作し、名前プロパティの方が好ましい場合は、匿名型を選択します。 それ以外の場合は、<xref:System.Tuple> を使用します。

## <a name="see-also"></a>関連項目

- [匿名型](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
- [式ツリー](../../csharp/expression-trees.md)
- [タプル型 (C# リファレンス)](../../csharp/language-reference/builtin-types/value-tuples.md)
- [タプル (Visual Basic)](../../visual-basic/programming-guide/language-features/data-types/tuples.md)
- [型のデザインのガイドライン](../design-guidelines/type.md)
