---
title: Null 許容参照型 - C# リファレンス
description: C# の Null 許容参照型とその使用方法について説明します
ms.date: 04/06/2020
ms.openlocfilehash: cb61b162b06faa51faabbcdd91e55618cdeaca73
ms.sourcegitcommit: 73aa9653547a1cd70ee6586221f79cc29b588ebd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "82102698"
---
# <a name="nullable-reference-types-c-reference"></a>Null 許容参照型 (C# リファレンス)

> [!NOTE]
> この記事では、Null 許容参照型について説明します。 また、[Null 許容値型](nullable-value-types.md)を宣言することもできます。

Null 許容参照型は、C# 8.0 以降、"*Null 許容認識コンテキスト*" にオプトインしたコードで使用できます。 Null 許容参照型、Null スタティック分析の警告、[Null 免除演算子](../operators/null-forgiving.md)は、オプションの言語機能です。 既定では、すべてオフになっています。 "*Null 許容コンテキスト*" は、プロジェクト レベルでビルド設定を使用して、またはコード内で pragma を使用して制御されます。

 Null 許容認識コンテキストでは、次の規則が使用されます。

- 参照型 `T`の変数は、Null 以外で初期化する必要があり、`null`の可能性がある値が割り当てられない場合があります。
- 参照型 `T?` の変数は、`null` で初期化することも、`null` を割り当てることもできます。ただし、逆参照する前に、`null` かどうかをチェックする必要があります。
- 型 `T?` の変数 `m` は、`m!` のように Null 免除演算子を適用する場合、Null ではないと見なされます。

Null 非許容参照型 `T` と Null 許容参照型 `T?` の区別は、コンパイラによる前述の規則の解釈によって適用されます。 型 `T` の変数と型 `T?` の変数は、同じ .NET 型で表されます。 次の例は、Null 非許容文字列と Null 許容文字列を宣言し、Null 免除演算子を使用して、値を Null 非許容文字列に割り当てます。

:::code language="csharp" source="snippets/NullableReferenceTypes.cs" id="SnippetCoreSyntax":::

変数 `notNull` と `nullable` は両方とも、<xref:System.String> 型で表されます。 Null 非許容型と Null 許容型は両方とも、同じ型に格納されるため、Null 許容参照型を使用できない場所がいくつかあります。 通常、Null 許容参照型は、基底クラスまたは実装されたインターフェイスとして使用できません。 Null 許容参照型は、オブジェクトの作成または型のテスト式で使用することはできません。 Null 許容参照型は、メンバー アクセス式の型にすることはできません。 次の例は、これらのコンストラクトを示します。

```csharp
public MyClass : System.Object? // not allowed
{
}

var nullEmpty = System.String?.Empty; // Not allowed
var maybeObject = new object?(); // Not allowed
try
{
    if (thing is string? nullableString) // not allowed
        Console.WriteLine(nullableString);
} catch (Exception? e) // Not Allowed
{
    Console.WriteLine("error");
}
```

## <a name="nullable-references-and-static-analysis"></a>Null 許容参照とスタティック分析

前のセクションの例は、Null 許容参照型の特性を示しています。 Null 許容参照型は新しいクラスの型ではなく、既存の参照型に対する注釈です。 コンパイラは、これらの注釈を使用して、ユーザーがコード内で発生する可能性のある Null 参照エラーを検出しやすくします。 Null 非許容参照型と Null 参照型の間には、ランタイムの違いはありません。 コンパイラは、Null 非許容参照型のランタイム チェックを追加しません。 この利点は、コンパイル時分析にあります。 コンパイラは、コード内で発生する可能性のある Null エラーの検出と修正に役立つ警告を生成します。 意図を宣言すると、コンパイラは、コードがその意図に違反したときに警告を発行します。

Null 許容の有効なコンテキストでは、コンパイラは、Null 許容と Null 非許容の両方の参照型の変数に対してスタティック分析を実行します。 コンパイラは、各参照変数の null 状態を "*null ではない*" または "*null かもしれない*" として追跡します。 Null 非許容参照の既定の状態は、"*null ではない*" です。 Null 許容参照の既定の状態は、"*null かもしれない*" です。

Null 非許容参照型の null 状態は "*null ではない*" であるため、この型は常に安全に逆参照できます。 この規則を適用するために、Null 非許容参照型が Null 以外の値に初期化されていない場合、コンパイラは警告を発行します。 ローカル変数は、宣言されている場所に割り当てる必要があります。 すべてのコンストラクターは、その本体または呼び出されるコンストラクター内で、またはフィールド初期化子を使用してすべてのフィールドに割り当てる必要があります。 状態が "*null かもしれない*" である参照に、Null 非許容参照が割り当てられている場合、コンパイラは警告を発行します。 しかし、Null 非許容参照は"*null ではない*" であるため、これらの変数が逆参照される場合、警告は変更されません。

Null 許容参照型は、`null`に初期化することも、割り当てることもできます。 したがって、スタティック分析では、変数が逆参照される前に、それが "*null ではない*" であることを確認する必要があります。 Null 許容参照が "*null かもしれない*" であると判断された場合、それを Null 非許容参照変数に割り当てることはできません。 次のクラスは、これらの警告の例を示します。

:::code language="csharp" source="snippets/NullableReferenceTypes.cs" id="SnippetClassWithNullable":::

次のスニペットは、このクラスを使用したときにコンパイラが警告を発行する場所を示します。

:::code language="csharp" source="snippets/NullableReferenceTypes.cs" id="SnippetLocalWarnings":::

上記の例は、参照変数の null 状態を判断するコンパイラのスタティック分析を示しています。 コンパイラは、null のチェックと割り当てに関する言語規則を適用して、その分析を通知します。  コンパイラは、メソッドまたはプロパティのセマンティクスについて想定することはできません。 null チェックを実行するメソッドを呼び出した場合、コンパイラは、それらのメソッドが変数の null 状態に影響することを認識できません。 API が引数と戻り値のセマンティクスについてコンパイラに通知するために追加できる属性がいくつかあります。 これらの属性は、.NET Core ライブラリ内の多数の一般的な API に適用されています。 たとえば、<xref:System.String.IsNullOrEmpty%2A> は更新され、コンパイラは、そのメソッドを null チェックとして正しく解釈します。 null 状態のスタティック分析に適用される属性の詳細については、[Null 許容属性](../attributes/nullable-analysis.md)に関する記事を参照してください。

## <a name="setting-the-nullable-context"></a>Null 許容コンテキストの設定

Null 許容コンテキストを制御するには、2 つの方法があります。 プロジェクト レベルでは、`<Nullable>enable</Nullable>` プロジェクトを追加できます。 単一の C# ソース ファイルでは、`#nullable enable` pragma を追加して、Null 許容コンテキストを有効にすることができます。 [Null 許容戦略の設定](../../nullable-migration-strategies.md) に関する記事を参照してください。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)に関する次の提案を参照してください。

- [Null 許容参照型](~/_csharplang/proposals/csharp-8.0/nullable-reference-types.md)
- [null 許容参照型仕様の下書き](~/_csharplang/proposals/csharp-8.0/nullable-reference-types-specification.md)

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [null 許容値型](nullable-value-types.md)
