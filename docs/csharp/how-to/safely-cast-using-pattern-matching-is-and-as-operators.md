---
title: パターン マッチング、is 演算子、as 演算子を使用して安全にキャストする方法
description: パターン マッチングの手法を利用し、変数を別の型に安全にキャストする方法について説明します。 パターン マッチング、is 演算子、as 演算子を利用し、型を安全に変換できます。
ms.date: 09/05/2018
helpviewer_keywords:
- cast operators [C#], as and is operators
- as operator [C#]
- is operator [C#]
ms.openlocfilehash: f10ce837057cc61b84130f237a13af708849dfc5
ms.sourcegitcommit: 7137e12f54c4e83a94ae43ec320f8cf59c1772ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/10/2020
ms.locfileid: "84662967"
---
# <a name="how-to-safely-cast-by-using-pattern-matching-and-the-is-and-as-operators"></a>パターン マッチング、is 演算子、as 演算子を使用して安全にキャストする方法

オブジェクトはポリモーフィックであるため、基本クラス型の変数で派生[型](../programming-guide/types/index.md)を保持できます。 派生型のインスタンス メンバーにアクセスするには、値を[キャスト](../programming-guide/types/casting-and-type-conversions.md)して派生型に戻す必要があります。 ただし、キャストでは、<xref:System.InvalidCastException> がスローされるリスクが生まれます。 C# には、[パターン マッチング](../pattern-matching.md) ステートメントがあります。これは成功する場合のみという条件でキャストを実行します。 C# には、値が特定の型であることをテストする [is](../language-reference/operators/type-testing-and-cast.md#is-operator) 演算子と [as](../language-reference/operators/type-testing-and-cast.md#as-operator) 演算子もあります。

パターン マッチングに `is` ステートメントを使用する方法の例を次に示します。

:::code language="csharp" source="../../../samples/snippets/csharp/how-to/safelycast/patternmatching/Program.cs" id="PatternMatchingIs":::

上記のサンプルでは、パターン マッチング構文のいくつかの機能が示されています。 `if (a is Mammal m)` ステートメントにより、テストと初期化の割り当てが結合されます。 この割り当ては、テストに成功した場合にのみ行われます。 変数 `m` は、それが割り当てられている埋め込み `if` ステートメントでのみ範囲に入ります。 後で同じメソッドで `m` にアクセスすることはできません。 前の例では、[`as` 演算子](../language-reference/operators/type-testing-and-cast.md#as-operator)を使用してオブジェクトを指定した型に変換する方法も示されています。

次の例で示されているように、[null 許容値型](../language-reference/builtin-types/nullable-value-types.md)に値があるかどうかをテストする目的で同じ構文を使用することもできます。

:::code language="csharp" source="../../../samples/snippets/csharp/how-to/safelycast/nullablepatternmatching/Program.cs" id="PatternMatchingNullable":::

上記のサンプルでは、変換で使用するパターン マッチング構文の他の機能が示されています。 `null` 値を具体的に探すことで null パターンの変数をテストできます。 変数のランタイム値が `null` のとき、`is` ステートメントで型を確認すると必ず `false` が返されます。 パターン マッチング `is` ステートメントでは、`int?` や `Nullable<int>` など、null 許容値型が許可されませんが、他の値の型についてはテストできます。 前の例の `is` パターンは null 許容値型に限定されません。 また、これらのパターンを使用して、参照型の変数に値があるか、`null` であるかをテストすることもできます。

上の例では、変数をさまざまな型の 1 つにすることができる `switch` ステートメントで型パターンを使用する方法も示されています。

変数が特定の型かどうかのテストだけを行い、それを新しい変数に代入しない場合は、参照型と null 許容値型に対して `is` 演算子と `as` 演算子を使用できます。 次のコードでは、パターン マッチングが導入される前に C# 言語に含まれていた `is` ステートメントと `as` ステートメントを使用し、変数が指定の型かどうかをテストする方法が示されています。

:::code language="csharp" source="../../../samples/snippets/csharp/how-to/safelycast/asandis/Program.cs" id="IsAndAs":::

ご覧のとおり、このコードとパターン マッチング コードを比較することで、テストと割り当てが 1 回のステートメントで組み合わされ、パターン マッチング構文がより強固になります。 可能な限り、パターン マッチングを使用してください。
