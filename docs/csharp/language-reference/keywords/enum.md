---
title: enum キーワード - C# リファレンス
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- enum
- enum_CSharpKeyword
helpviewer_keywords:
- enum keyword [C#]
ms.assetid: bbeb9a0f-e9b3-41ab-b0a6-c41b1a08974c
ms.openlocfilehash: 639a3a01c9c4da13e0212bd0230acbd2af170b25
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74428520"
---
# <a name="enum-c-reference"></a>enum (C# リファレンス)

`enum` キーワードは、列挙型を宣言するために使用されます。列挙型は、列挙子リストと呼ばれる名前付き定数の集まりで構成される固有の型です。

通常、列挙型は名前空間内に直接定義して、名前空間内のすべてのクラスが共通の利便性でアクセスできるようにするのが最も適切です。 ただし、列挙型はクラスまたは構造体内に入れ子にすることもできます。

既定では、最初の列挙子の値は 0 で、後続の列挙子の値は 1 ずつ増加していきます。 たとえば、次の列挙型では、 `Sat` は `0`、 `Sun` は `1`、 `Mon` は `2`などとなります。

```csharp
enum Day {Sat, Sun, Mon, Tue, Wed, Thu, Fri};
```

列挙型では、次の例に示すように、初期化子を使用して既定値をオーバーライドできます。

```csharp
enum Day {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

この列挙型では、要素の並びは `0` からではなく、 `1` から開始します ただし、列挙型には値が 0 となる定数を含めておくことをお勧めします。 詳細については、[列挙型](../../programming-guide/enumeration-types.md)を参照してください。

すべての列挙型には基になる型があり、基になる型には任意の[整数数値型](../builtin-types/integral-numeric-types.md)を指定できます。 [char](../builtin-types/char.md)型は、列挙体の基になる型にできない型です。 列挙要素の基になる既定の型は [int](../builtin-types/integral-numeric-types.md)です。[byte](../builtin-types/integral-numeric-types.md)など、他の整数型の列挙型を宣言するには、次の例に示すように、識別子に続けてコロンを使用し、その後に型を記述します。

```csharp
enum Day : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
```

列挙型の変数には、基になる型の範囲内の任意の値を割り当てることができます。値は名前付き定数に限定されません。

`enum E` の既定値は、式 `(E)0`によって算出された値です。

> [!NOTE]
> 列挙子の名前に空白を使用することはできません。

基になる型は、列挙子ごとに割り当てるストレージの大きさを指定します。 ただし、 `enum` 型を整数型に変換するには、明示的なキャストが必要です。 たとえば、次のステートメントでは `enum` 型から [int](../builtin-types/integral-numeric-types.md) 型へのキャストを使用することで、列挙子 `Sun` を `int` 型の変数に代入します。

```csharp
int x = (int)Day.Sun;
```

ビット単位の `OR` 演算と組み合わせることができる要素を含む列挙型に <xref:System.FlagsAttribute?displayProperty=nameWithType> を適用すると、一部のツールを使用したときに、 `enum` の動作に属性が反映されます。 このような変更は、 <xref:System.Console> クラス メソッドや式エバリュエーターなどのツールを使用して確認できます。 (3 番目の使用例をご参照ください。)

## <a name="robust-programming"></a>信頼性の高いプログラミング

定数の場合と同様に、列挙型の個々の値へのすべての参照はコンパイル時に数値リテラルに変換されます。 これにより、「[定数](../../programming-guide/classes-and-structs/constants.md)」で説明しているように、バージョン管理の問題が発生する可能性があります。

新しいバージョンの列挙型に追加の値を割り当てるか、新しいバージョンの列挙型メンバーの値を変更すると、依存関係のあるソース コードに問題が発生することがあります。 列挙値は、 [switch](switch.md) ステートメントでよく使用されます。 `enum` 型に追加要素が追加されている場合、switch ステートメントの default セクションが予期せずに選択される場合があります。

作成したコードが他の開発者によって使用される場合は、新しい要素を `enum` 型に追加したときのコードの反応を規定するガイドラインを用意しておく必要があります。

## <a name="example"></a>例

次の例では、列挙型 `Day`を宣言しています。 2 つの列挙子は明示的に整数に変換され、整数変数に代入されます。

[!code-csharp[csrefKeywordsTypes#10](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#10)]

## <a name="example"></a>例

次の例では、基本型オプションを使用して `enum` 型をメンバーに持つ `long`を宣言しています。 列挙型の基になる型が `long`であっても、列挙型メンバーはキャストを使用して `long` 型に明示的に変換する必要があることにご注意ください。

[!code-csharp[csrefKeywordsTypes#11](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#11)]

## <a name="example"></a>例

次のコード例では、 <xref:System.FlagsAttribute?displayProperty=nameWithType> 宣言での `enum` 属性の使用とその効果を示します。

[!code-csharp[csrefKeywordsTypes#12](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#12)]

## <a name="comments"></a>コメント

この例では、 `Flags`を削除すると次の値が表示されます。

`5`

`5`

## <a name="c-language-specification"></a>C# 言語仕様

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [列挙型](../../programming-guide/enumeration-types.md)
- [C# のキーワード](index.md)
- [整数型](../builtin-types/integral-numeric-types.md)
- [組み込み型の一覧表](built-in-types-table.md)
- [列挙型の名前付け規則](../../../standard/design-guidelines/names-of-classes-structs-and-interfaces.md#naming-enumerations)
