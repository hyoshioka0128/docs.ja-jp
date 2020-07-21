---
title: readonly キーワード - C# リファレンス
ms.date: 04/14/2020
f1_keywords:
- readonly_CSharpKeyword
- readonly
helpviewer_keywords:
- readonly keyword [C#]
ms.assetid: 2f8081f6-0de2-4903-898d-99696c48d2f4
ms.openlocfilehash: 66a096e8831f72a2216e8ba5dd9866046504624f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84368622"
---
# <a name="readonly-c-reference"></a>readonly (C# リファレンス)

`readonly` キーワードは、次の 4 つのコンテキストで使用できる修飾子です。

- [フィールドの宣言](#readonly-field-example)では、`readonly` は、フィールドへの割り当てが、宣言の一部として、または同じクラスのコンストラクター内でのみ可能であることを示します。 readonly フィールドは、フィールドの宣言とコンストラクターで複数回割り当ておよび再割り当てを行うことができます。
  
  `readonly` フィールドは、コンストラクターが終了した後で割り当てることはできません。 この規則は、値型と参照型では意味が異なります。
  
  - 値型にはそのデータが直接含まれるため、`readonly` 値型のフィールドは変更できません。
  - 参照型にはそのデータへの参照が含まれるため、`readonly` 参照型のフィールドは、常に同じオブジェクトを参照する必要があります。 そのオブジェクトは不変ではありません。 `readonly` 修飾子があると、フィールドを参照型の別のインスタンスで置き換えることはできません。 ただし、フィールドのインスタンス データを読み取り専用フィールドで変更することは禁止されません。

  > [!WARNING]
  > 変更可能な参照型である外部から参照できる読み取り専用フィールドを含む外部から参照できる型はセキュリティの脆弱性があり、警告 [CA2104](/visualstudio/code-quality/ca2104) がトリガーされる可能性があります: "読み取り専用の変更可能な参照型を宣言しません"。

- `readonly struct` 型定義では、`readonly` は構造体型が変更不可であることを示します。 詳細については、「[構造体型](../builtin-types/struct.md)」の記事の「[`readonly` 構造体](../builtin-types/struct.md#readonly-struct)」セクションを参照してください。
- 構造体型内のインスタンス メンバー宣言では、`readonly` は、インスタンス メンバーによって構造体の状態が変更されないことを示します。 詳細については、[構造体型](../builtin-types/struct.md)に関する記事の「[`readonly` インスタンス メンバー](../builtin-types/struct.md#readonly-instance-members)」セクションを参照してください。
- [`ref readonly` メソッドの戻り値](#ref-readonly-return-example)では、`readonly` 修飾子は、メソッドが参照を返し、その参照への書き込みが許可されないことを示します。

`readonly struct` と `ref readonly` のコンテキストは、C# 7.2 で追加されました。 `readonly` 構造体メンバーは、C# 8.0 で追加されました。

## <a name="readonly-field-example"></a>読み取り専用フィールドの例

この例では、`year` フィールドの値は、クラス コンストラクターで値が割り当てられていても `ChangeYear` メソッドでは変更できません。

[!code-csharp[Readonly Field example](snippets/ReadonlyKeywordExamples.cs#ReadonlyField)]

`readonly` のフィールドに値を割り当てることができるのは、次のコンテキスト内に限られます。

- 値が宣言で初期化される場合。次に例を示します。

  ```csharp
  public readonly int y = 5;
  ```

- インスタンス フィールド宣言を含むクラスのインスタンス コンストラクター内。
- 静的フィールド宣言を含むクラスの静的コンストラクター内。

また、これらのコンストラクター コンテキスト内でのみ、`readonly` フィールドを [out](out-parameter-modifier.md) パラメーターまたは [ref](ref.md) パラメーターとして渡すことができます。

> [!NOTE]
> `readonly` キーワードは [const](const.md) キーワードとは異なります。 `const` フィールドは、フィールドの宣言でしか初期化できません。 `readonly` フィールドは、フィールドの宣言と任意のコンストラクターで複数回割り当てることができます。 このため、`readonly` フィールドは、使用するコンストラクターに応じて異なる値を持つことができます。 また、次の例のように、`const` フィールドがコンパイル時定数であるのに対し、`readonly` フィールドは実行時定数として使用できます。
>
> ```csharp
> public static readonly uint timeStamp = (uint)DateTime.Now.Ticks;
> ```

[!code-csharp[Initialize readonly Field example](snippets/ReadonlyKeywordExamples.cs#InitReadonlyField)]

上の例で、次の例のようなステートメントを使うものとします。

```csharp
p2.y = 66;        // Error
```

この場合、次のコンパイル エラー メッセージが表示されます。

**読み取り専用フィールドに割り当てることはできません (コンストラクター、変数初期化子では可)**

## <a name="ref-readonly-return-example"></a>ref readonly の戻り値の例

`ref return`での `readonly` 修飾子は、返される参照を変更できないことを示します。 次の例は、origin に参照を返します。 `readonly` 修飾子を使用して、呼び出し元が origin を変更できないことを示しています。

[!code-csharp[readonly return example](snippets/ReadonlyKeywordExamples.cs#ReadonlyReturn)]

返される型を `readonly struct` にする必要はありません。 `ref` で返すことができる任意の型を、`ref readonly` で返すことができます。

## <a name="c-language-specification"></a>C# 言語仕様

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

言語仕様の提案を参照することもできます。

- [readonly ref と readonly struct](~/_csharplang/proposals/csharp-7.2/readonly-ref.md)
- [readonly 構造体メンバー](~/_csharplang/proposals/csharp-8.0/readonly-instance-members.md)

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [C# のキーワード](index.md)
- [修飾子](index.md)
- [const](const.md)
- [フィールド](../../programming-guide/classes-and-structs/fields.md)
