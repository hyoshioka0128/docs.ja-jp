---
title: 型パラメーターの制約 - C# プログラミング ガイド
ms.date: 04/12/2018
helpviewer_keywords:
- generics [C#], type constraints
- type constraints [C#]
- type parameters [C#], constraints
- unbound type parameter [C#]
ms.openlocfilehash: 4c4554c808ab15776f3217c257e0a60119ea2338
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84368362"
---
# <a name="constraints-on-type-parameters-c-programming-guide"></a>型パラメーターの制約 (C# プログラミング ガイド)

制約では、型引数に必要な機能をコンパイラに通知します。 制約のない型引数は、任意の型にすることができます。 コンパイラは、.NET 型の最終的な基底クラスになる、<xref:System.Object?displayProperty=nameWithType> のメンバーを見なすことができるだけです。 詳細については、「[制約を使用する理由](#why-use-constraints)」を参照してください。 クライアント コードが制約を満たさない型を使用している場合、コンパイラではエラーが発行されます。 制約を指定するには、`where` コンテキスト キーワードを使用します。 次の表では、7 種類の制約を一覧しています。

|制約|説明|
|----------------|-----------------|
|`where T : struct`|この型引数は null 非許容値型である必要があります。 null 許容値型の詳細については、「[null 許容値型](../../language-reference/builtin-types/nullable-value-types.md)」を参照してください。 すべての値の型にはアクセス可能なパラメーターなしのコンストラクターがあるため、`struct` 制約は `new()` 制約を意味し、`new()` 制約と組み合わせることはできません。 `struct` 制約を `unmanaged` 制約と組み合わせることはできません。|
|`where T : class`|この型引数は参照型である必要があります。 この制約は、任意のクラス、インターフェイス、デリゲート、または配列型にも適用されます。 C# 8.0 以降の null 許容コンテキストでは、`T` は null 非許容の参照型である必要があります。 |
|`where T : class?`|型の引数は、null 許容または null 非許容の参照型である必要があります。 この制約は、任意のクラス、インターフェイス、デリゲート、または配列型にも適用されます。|
|`where T : notnull`|この型引数は null 非許容型である必要があります。 引数は、C# 8.0 以降の null 非許容参照型、または null 非許容値型にできます。 |
|`where T : unmanaged`|この型引数は null 非許容で[アンマネージド型](../../language-reference/builtin-types/unmanaged-types.md)である必要があります。 `unmanaged` 制約は `struct` 制約を意味し、`struct` 制約とも `new()` 制約とも組み合わせることはできません。|
|`where T : new()`|この型引数には、パラメーターなしのパブリック コンストラクターが必要です。 `new()` 制約を別の制約と併用する場合、この制約を最後に指定する必要があります。 `new()` 制約は、`struct` や `unmanaged` 制約と組み合わせることはできません。|
|`where T :` *\<base class name>*|この型引数は、指定された基底クラスであるか、そのクラスから派生している必要があります。 C# 8.0 以降の null 許容コンテキストでは、`T` は指定の基底クラスから派生した null 非許容の参照型である必要があります。 |
|`where T :` *\<base class name>?*|この型引数は、指定された基底クラスであるか、そのクラスから派生している必要があります。 C# 8.0 以降の null 許容コンテキストでは、`T` は指定の基底クラスから派生した null 許容または非許容のいずれかの参照型である場合があります。 |
|`where T :` *\<interface name>*|この型引数は、指定されたインターフェイスであるか、そのインターフェイスを実装している必要があります。 複数のインターフェイス制約を指定することができます。 制約のインターフェイスを汎用的にすることもできます。 C# 8.0 以降の null 許容コンテキストでは、`T` は指定したインターフェイスを実装する null 非許容型である必要があります。|
|`where T :` *\<interface name>?*|この型引数は、指定されたインターフェイスであるか、そのインターフェイスを実装している必要があります。 複数のインターフェイス制約を指定することができます。 制約のインターフェイスを汎用的にすることもできます。 C# 8.0 の null 許容コンテキストでは、`T` は null 許容参照型、null 非許容参照型、または値型である場合があります。 `T` は null 許容値型ではない可能性があります。|
|`where T : U`|`T` に指定する型引数は、`U` に指定された引数であるか、その引数から派生している必要があります。 null 許容コンテキストでは、`U` が null 非許容参照型である場合、`T` は null 非許容参照型である必要があります。 `U` が null 許容参照型である場合、`T` は null 許容または null 非許容のいずれかになります。 |

## <a name="why-use-constraints"></a>制約を使用する理由

制約では、型パラメーターの能力と期待を指定します。 これらの制約を宣言することで、制約型の操作とメソッドの呼び出しを使用できるようになります。 お使いのジェネリック クラスまたはメソッドが、単純な割り当てや、<xref:System.Object?displayProperty=nameWithType> でサポートされていない任意のメソッド呼び出しでジェネリック メンバーに対して任意の操作を使用する場合、型パラメーターに制約を適用する必要があります。 たとえば、この基底クラスの制約は、この型のオブジェクト、またはこの型から派生したオブジェクトのみを型引数として使用することをコンパイラに指示しています。 コンパイラがこの保証を獲得したら、その型のメソッドをジェネリック クラスで呼び出すことができるようになります。 基底クラスの制約を適用して `GenericList<T>` クラス (「[ジェネリックの概要](../../../standard/generics/index.md)」を参照) に追加できる機能を説明するコード例を次に示します。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#9)]

この制約ではジェネリック クラスで `Employee.Name` プロパティを使用できるようにします。 制約では、型 `T` のすべての項目が、`Employee` オブジェクトまたは `Employee` から継承するオブジェクトのいずれかになることが保証されることを指定します。

同じ型パラメーターに複数の制約を適用できます。また、制約自体をジェネリック型にすることもできます。次に例を示します。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#10)]

`where T : class` 制約を適用する場合は、型パラメーターに `==` および `!=` 演算子を使用しないでください。これらの演算子でテストされるのは、値の等価性ではなく、参照 ID についてのみです。 これらの演算子が、引数として使用されている型内でオーバーロードされている場合でも、この動作が発生します。 この点を説明するコードを次に示します。<xref:System.String> クラスが `==` 演算子をオーバーロードしている場合でも、出力は false です。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#11)]

コンパイラは `T` がコンパイル時に参照型であることしか認識しておらず、すべての参照型で有効な既定の演算子を使用する必要があります。 値の等価性をテストする必要がある場合は、`where T : IEquatable<T>` または `where T : IComparable<T>` 制約も適用し、ジェネリック クラスの制約に使用されるすべてのクラスでそのインターフェイスを実装することをお勧めします。

## <a name="constraining-multiple-parameters"></a>複数のパラメーターを制約する

複数のパラメーターに制約を適用できます。また、複数の制約を 1 つのパラメーターに適用することができます。次に例を示します。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#12)]

## <a name="unbounded-type-parameters"></a>非バインド型パラメーター

 パブリック クラス `SampleClass<T>{}` の T など、制約がない型パラメーターは、非バインド型パラメーターと呼ばれます。 非バインド型パラメーターには次の規則があります。

- `!=` および `==` 演算子は使用できません。これは、具象型引数によってこれらの演算子がサポートされるという保証がないためです。
- これらの演算子は `System.Object` との間で相互に変換できます。また、任意のインターフェイス型に明示的に変換できます。
- これらは [null](../../language-reference/keywords/null.md) と比較することができます。 非バインド型パラメーターと `null` を比較し、その型引数が値の型の場合、比較結果として常に false が返されます。

## <a name="type-parameters-as-constraints"></a>制約としての型パラメーター

制約としてジェネリック型パラメーターを使用する方法は、独自の型パラメーターがあるメンバー関数が、含まれる型の型パラメーターにそのパラメーターを制約する必要がある場合に便利です。次に例を示します。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#13)]

前の例の `T` は、`Add` メソッドのコンテキストでは型の制約ですが、`List` クラスのコンテキストでは非バインド型パラメーターです。

型パラメーターは、ジェネリック クラス定義の制約としても使用できます。 型パラメーターは、他の型パラメーターと共に山かっこ内で宣言する必要があります。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#14)]

ジェネリック クラスで制約として型パラメーターを使用する方法が便利なのは、限られた場合のみです。コンパイラでは、`System.Object` から派生したことを除き、型パラメーターに関して何も仮定できないためです。 2 つの型パラメーター間に継承関係を適用するシナリオには、ジェネリック クラスの制約として型パラメーターを使用してください。

## <a name="notnull-constraint"></a>NotNull 制約

C# 8.0 以降の null 許容コンテキストでは、`notnull` 制約を使用して、型引数が null 非許容値型または null 非許容参照型である必要があることを指定できます。 `notnull` 制約は、`nullable enable` コンテキストでのみ使用できます。 null 許容が未指定のコンテキストに `notnull` 制約を追加すると、コンパイラにより警告が生成されます。

他の制約とは異なり、型引数が `notnull` 制約に違反すると、そのコードが `nullable enable` コンテキストでコンパイルされるときにコンパイラにより警告が生成されます。 null 許容が未指定のコンテキストでコードがコンパイルされた場合、コンパイラによって警告やエラーは生成されません。

C# 8.0 以降の null 許容コンテキストでは、`class` 制約を使用して、型引数が null 非許容型である必要があることを指定できます。 null 許容コンテキストでは、型パラメーターが null 許容参照型である場合、コンパイラによって警告が生成されます。

## <a name="unmanaged-constraint"></a>アンマネージド制約

C# 7.3 以降、`unmanaged` 制約を指定して、型パラメーターが null 非許容で[アンマネージド型](../../language-reference/builtin-types/unmanaged-types.md)である必要があることを指定できます。 `unmanaged` 制約では、次の例のように、メモリのブロックとして操作できる型を処理する再利用可能なルーチンを記述できます。

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#15)]

ビルトイン型ではない型で `sizeof` 演算子を使用するため、先行するメソッドは `unsafe` コンテキストでコンパイルされる必要があります。 `unmanaged` 制約なしで、`sizeof` 演算子を使用することはできません。

`unmanaged` 制約は `struct` 制約を意味するため、これと組み合わせることはできません。 `struct` 制約は `new()` 制約を意味するため、`unmanaged` 制約を `new()` 制約と組み合わせることもできません。

## <a name="delegate-constraints"></a>制約をデリゲートする

また、C# 7.3 以降、基底クラスの制約として <xref:System.Delegate?displayProperty=nameWithType> または <xref:System.MulticastDelegate?displayProperty=nameWithType> を使用することもできます。 CLR では常にこの制約を許可していますが、C# 言語では許可されていません。 `System.Delegate` 制約では、タイプ セーフな方法でデリゲートを処理するコードを記述できます。 次のコードでは、2 つのデリゲートが同じ型である場合にそれらを組み合わせる拡張メソッドを定義します。

[!code-csharp[using the delegate constraint](snippets/GenericWhereConstraints.cs#16)]

上述のメソッドを使用して、同じ型のデリゲートを組み合わせることができます。

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#17)]

最後の行のコメントを解除した場合、コンパイルされません。 `first` と `test` は両方ともデリゲート型ですが、これらは異なるデリゲート型です。

## <a name="enum-constraints"></a>列挙の制約

C# 7.3 以降、基底クラスの制約として <xref:System.Enum?displayProperty=nameWithType> 型を指定することもできます。 CLR では常にこの制約を許可していますが、C# 言語では許可されていません。 `System.Enum` を使用するジェネリックは、`System.Enum` の静的メソッドの使用から結果をキャッシュするために、タイプ セーフのプログラミングを提供します。 次の例では、列挙型の有効な値をすべて見つけて、それらの値をその文字列表記にマップするディクショナリをビルドします。

[!code-csharp[using the enum constraint](snippets/GenericWhereConstraints.cs#18)]

`Enum.GetValues` と `Enum.GetName` ではリフレクションが使用されます。これは、パフォーマンスに影響を与えます。 リフレクションを必要とする呼び出しを繰り返すのではなく、`EnumNamedValues` を呼び出してキャッシュおよび再利用されるコレクションを作成できます。

次の例で示すように、このメソッドを使用して、列挙を作成し、その値と名前のディクショナリをビルドできます。

[!code-csharp[enum definition](snippets/GenericWhereConstraints.cs#19)]

[!code-csharp[using the enum constrained method](snippets/GenericWhereConstraints.cs#20)]

## <a name="see-also"></a>関連項目

- <xref:System.Collections.Generic>
- [C# プログラミング ガイド](../index.md)
- [ジェネリックの概要](./index.md)
- [ジェネリック クラス](./generic-classes.md)
- [new 制約](../../language-reference/keywords/new-constraint.md)
