---
title: 構造体型 - C# リファレンス
ms.date: 04/21/2020
f1_keywords:
- struct_CSharpKeyword
helpviewer_keywords:
- struct keyword [C#]
- struct type [C#]
- structure type [C#]
ms.assetid: ff3dd9b7-dc93-4720-8855-ef5558f65c7c
ms.openlocfilehash: dbe9b47625589de834b7a8021640885ca0920b96
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "82021269"
---
# <a name="structure-types-c-reference"></a>構造体型 (C# リファレンス)

"*構造体型*" (または "*構造体型*") とは、データおよび関連する機能をカプセル化できる[値の型](value-types.md)です。 構造体型を定義するには、`struct` キーワードを使用します。

[!code-csharp[struct example](snippets/StructType.cs#StructExample)]

構造体型には、"*値のセマンティクス*" があります。 つまり、構造体型の変数には、型のインスタンスが含まれます。 既定では、変数値が代入時にコピーされ、引数がメソッドに渡され、メソッドの結果が返されます。 構造体型の変数の場合は、型のインスタンスがコピーされます。 詳細については、[値の型](value-types.md)に関するページを参照してください。

通常は、構造体型を使用して、ほとんどまたはまったく動作を提供しない小さなデータ中心型を設計します。 たとえば、.NET では、構造体型を使用して数値 ([整数](integral-numeric-types.md)と[実数](floating-point-numeric-types.md)の両方)、[ブール値](bool.md)、[Unicode 文字](char.md)、[時刻インスタンス](xref:System.DateTime)が表現されます。 型の動作に重点を置いている場合は、[class](../keywords/class.md) を定義することを検討してください。 クラス型には "*参照セマンティクス*" があります。 つまり、クラス型の変数には、インスタンス自体ではなく、型のインスタンスへの参照が含まれています。

構造体型には値セマンティクスがあるため、"*変更不可*" の構造体型を定義することをお勧めします。

## <a name="readonly-struct"></a>`readonly` 構造体

C# 7.2 以降では、構造体型が変更不可であることを宣言するには、`readonly` 修飾子を使用します。

[!code-csharp[readonly struct](snippets/StructType.cs#ReadonlyStruct)]

`readonly` 構造体のすべてのデータ メンバーを、次のように読み取り専用にする必要があります。

- すべてのフィールド宣言には、[`readonly` 修飾子が必要です](../keywords/readonly.md)
- 自動的に実装されるプロパティも含めて、すべてのプロパティは、読み取り専用である必要があります

それにより、`readonly` 構造体のどのメンバーも構造体の状態を変更しないことが保証されます。

> [!NOTE]
> `readonly` 構造体でも、変更可能な参照型のデータ メンバーは、それ自身の状態を変更できます。 たとえば、<xref:System.Collections.Generic.List%601> インスタンスを置き換えることはできませんが、新しい要素をそれに追加することはできます。

## <a name="readonly-instance-members"></a>`readonly` インスタンス メンバー

C# 8.0 以降では、`readonly` 修飾子を使用して、インスタンス メンバーで構造体の状態を変更しないことを宣言することもできます。 構造体の型全体を `readonly` として宣言できない場合は、`readonly` 修飾子を使用して、構造体の状態を変更しないインスタンス メンバーをマークします。 `readonly` 構造体では、すべてのインスタンス メンバーは暗黙的に `readonly` です。

`readonly` インスタンス メンバー内では、構造体のインスタンス フィールドに割り当てることはできません。 ただし、`readonly` メンバーから非 `readonly` メンバーを呼び出すことができます。 その場合、コンパイラを使用して構造体インスタンスのコピーを作成し、そのコピーで非 `readonly` メンバーを呼び出します。 その結果、元の構造インスタンスは変更されません。

通常、`readonly` 修飾子を次の種類のインスタンス メンバーに適用します。

- メソッド:

  [!code-csharp[readonly method](snippets/StructType.cs#ReadonlyMethod)]

  <xref:System.Object?displayProperty=nameWithType> で宣言されたメソッドをオーバーライドするメソッドに `readonly` 修飾子を適用することもできます。

  [!code-csharp[readonly override](snippets/StructType.cs#ReadonlyOverride)]

- プロパティとインデクサー:

  [!code-csharp[readonly property get](snippets/StructType.cs#ReadonlyProperty)]

  プロパティまたはインデクサーの両方のアクセサーに `readonly` 修飾子を適用する必要がある場合は、プロパティまたはインデクサーの宣言でそれを適用します。

  > [!NOTE]
  > プロパティの宣言に `readonly` 修飾子が存在するかどうかに関係なく、コンパイラによって[自動実装プロパティ](../../programming-guide/classes-and-structs/auto-implemented-properties.md)の `get` アクセサーが `readonly` として宣言されます。

`readonly` 修飾子を構造体型の静的メンバーに適用することはできません。

パフォーマンスの最適化のためにコンパイラで `readonly` 修飾子を使用する場合があります。 詳細については、「[安全で効率的な C# コードを記述する](../../write-safe-efficient-code.md)」をご覧ください。

## <a name="limitations-with-the-design-of-a-structure-type"></a>構造体型の設計に関する制限事項

構造体型を設計する場合は、[class](../keywords/class.md) 型と同じ機能を使用できますが、次の例外があります。

- パラメーターなしのコンストラクターを宣言することはできません。 すべての構造体型には、型の[既定値](default-values.md)を生成する暗黙的なパラメーターなしのコンストラクターが既に備わっています。

- インスタンス フィールドまたはプロパティを、それらの宣言で初期化することはできません。 ただし、[static](../keywords/static.md) または [const](../keywords/const.md) フィールド、あるいは静的プロパティについては、それらの宣言で初期化することができます。

- 構造体型のコンストラクターでは、型のすべてのインスタンス フィールドを初期化する必要があります。

- 構造体型は、他のクラスまたは構造体型から継承することができないほか、クラスのベースとすることもできません。 ただし、構造体型では [interfaces](../keywords/interface.md) を実装することができます。

- 構造体型内で[ファイナライザー](../../programming-guide/classes-and-structs/destructors.md)を宣言することはできません。

## <a name="instantiation-of-a-structure-type"></a>構造体型のインスタンス化

C# では、宣言された変数を使用するには、事前にこれを初期化する必要があります。 構造体型の変数は ([null 許容値型](nullable-value-types.md)の変数でない限り) `null` とすることができないため、対応する型のインスタンスをインスタンス化する必要があります。 それにはいくつかの方法があります。

通常は、[`new`](../operators/new-operator.md) 演算子を使用して適切なコンストラクターを呼び出すことによって、構造体型をインスタンス化します。 すべての構造体型に、少なくとも 1 つのコンストラクターがあります。 それは暗黙的なパラメーターなしのコンストラクターであり、型の[既定値](default-values.md)を生成するものです。 また、[既定の値式](../operators/default.md)を使用して、型の既定値を生成することもできます。

構造体型のすべてのインスタンス フィールドにアクセスできる場合は、それを `new` 演算子なしでインスタンス化することもできます。 その場合は、インスタンスを初めて使用する前に、すべてのインスタンス フィールドを初期化する必要があります。 その方法を次の例に示します。

[!code-csharp[without new](snippets/StructType.cs#WithoutNew)]

[組み込みの値型](value-types.md#built-in-value-types)の場合は、対応するリテラルを使用して型の値を指定します。

## <a name="passing-structure-type-variables-by-reference"></a>構造体型の変数を参照渡しする

構造体型の変数を引数としてメソッドに渡す場合、またはメソッドから構造体型の値を返す場合は、構造体型のインスタンス全体がコピーされます。 これは、大規模な構造体型を必要とするハイパフォーマンスのシナリオの場合、ご利用のコードのパフォーマンスに影響を与える可能性があります。 値のコピーを回避するには、構造体型の変数を参照渡しします。 引数を参照渡しする必要があることを示すには、[`ref`](../keywords/ref.md#passing-an-argument-by-reference)、[`out`](../keywords/out-parameter-modifier.md)、または [`in`](../keywords/in-parameter-modifier.md) のメソッド パラメーター修飾子を使用します。 メソッドの結果を参照渡しによって返すには、[ref 戻り値](../../programming-guide/classes-and-structs/ref-returns.md)を使用します。 詳細については、「[安全で効率的な C# コードを記述する](../../write-safe-efficient-code.md)」をご覧ください。

## <a name="ref-struct"></a>`ref` 構造体

C# 7.2 以降、`ref` 修飾子は、構造体型の宣言内で使用できます。 `ref` 構造体型のインスタンスはスタック上に割り当てられます。マネージド ヒープにエスケープすることはできません。 これを確実にするために、コンパイラでは次のように `ref` 構造体型の使用が制限されます。

- `ref` 構造体を配列の要素型にすることはできません。
- `ref` 構造体をクラスまたは非 `ref` 構造体のフィールドの宣言型にすることはできません。
- `ref` 構造体ではインターフェイスを実装できません。
- `ref` 構造体を <xref:System.ValueType?displayProperty=nameWithType> または <xref:System.Object?displayProperty=nameWithType> にボックス化することはできません。
- `ref` 構造体を型引数にすることはできません。
- `ref` 構造体変数を[ラムダ式](../../programming-guide/statements-expressions-operators/lambda-expressions.md)または[ローカル関数](../../programming-guide/classes-and-structs/local-functions.md)でキャプチャすることはできません。
- `ref` 構造体変数を [`async`](../keywords/async.md) メソッド内で使用することはできません。 ただし、<xref:System.Threading.Tasks.Task> または <xref:System.Threading.Tasks.Task%601> を返す場合など、同期メソッドで `ref` 構造体変数を使用することはできます。
- `ref` 構造体変数を[反復子](../../iterators.md)内で使用することはできません。

通常、`ref` 構造体型のデータ メンバーも含む型が必要な場合は、`ref` 構造体型を定義します。

[!code-csharp[ref struct](snippets/StructType.cs#RefStruct)]

`ref` 構造体を [`readonly`](#readonly-struct) として宣言するには、型宣言内で `readonly` 修飾子と `ref` 修飾子を組み合わせます (`readonly` 修飾子は `ref` 修飾子よりも前にある必要があります)。

[!code-csharp[readonly ref struct](snippets/StructType.cs#ReadonlyRef)]

.NET では、`ref` 構造体の例として <xref:System.Span%601?displayProperty=nameWithType> と <xref:System.ReadOnlySpan%601?displayProperty=nameWithType> があります。

## <a name="conversions"></a>変換

どの構造体型にも ([`ref` 構造体](#ref-struct)型を除く)、<xref:System.ValueType?displayProperty=nameWithType> 型と <xref:System.Object?displayProperty=nameWithType> 型の間に[ボックス化およびボックス化解除](../../programming-guide/types/boxing-and-unboxing.md)の変換が存在します。 また、構造体型と、これによって実装されるインターフェイスとの間にも、ボックス化とボックス化解除の変換が存在します。

## <a name="c-language-specification"></a>C# 言語仕様

詳細については、[C# 言語仕様](~/_csharplang/spec/introduction.md)の「[構造体](~/_csharplang/spec/structs.md)」セクションを参照してください。

C# 7.2 以降で導入された機能の詳細については、次の機能の提案に関するメモを参照してください。

- [Readonly 構造体](~/_csharplang/proposals/csharp-7.2/readonly-ref.md#readonly-structs)
- [Readonly インスタンスのメンバー](~/_csharplang/proposals/csharp-8.0/readonly-instance-members.md)
- [ref-like 型のコンパイル時の安全性](~/_csharplang/proposals/csharp-7.2/span-safety.md)

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [デザインのガイドライン - クラスまたは構造体の選択](../../../standard/design-guidelines/choosing-between-class-and-struct.md)
- [デザインのガイドライン - 構造体のデザイン](../../../standard/design-guidelines/struct.md)
- [クラスと構造体](../../programming-guide/classes-and-structs/index.md)
