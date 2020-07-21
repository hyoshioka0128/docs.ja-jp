---
title: where (ジェネリック型制約) - C# リファレンス
ms.date: 04/15/2020
f1_keywords:
- whereconstraint
- whereconstraint_CSharpKeyword
helpviewer_keywords:
- where (generic type constraint) [C#]
ms.openlocfilehash: 406c710cd884363c32b98336717732a09b3d1fc1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84401876"
---
# <a name="where-generic-type-constraint-c-reference"></a>where (ジェネリック型制約) (C# リファレンス)

ジェネリック定義の `where` 句では、型の制約を指定します。この型は、ジェネリック型、メソッド、デリゲート、またはローカル関数における型パラメーターの引数として使用されます。 制約では、インターフェイス (基底クラス) を指定したり、参照、値、またはアンマネージド型となるジェネリック型を要求したりすることができます。 それらにより型引数が処理する必要がある機能が宣言されえます。

たとえば、型パラメーター `T` が <xref:System.IComparable%601> インターフェイスを実装するように、次のように `MyGenericClass` ジェネリック クラスを宣言できます。

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#1)]

> [!NOTE]
> クエリ式での where 句の詳細については、「[where 句](where-clause.md)」を参照してください。

`where` 句には基底クラスの制約を含めることもできます。 基底クラスの制約は、そのジェネリック型の型引数として使用される型が、指定されたクラスを基底クラスとして持つか、その基底クラスであることを示しています。 基底クラスの制約を使用する場合は、型パラメーターに関する制約よりも前に制約を記述する必要があります。 一部の型は、基底クラスの制約として許可されません (<xref:System.Object>、<xref:System.Array>、<xref:System.ValueType>)。 C# 7.3 より前は、<xref:System.Enum>、<xref:System.Delegate>、<xref:System.MulticastDelegate> も基底クラスの制約として許可されていません。 次の例では、この型は基底クラスとして指定できるようになったことを示しています。

[!code-csharp[using an interface constraint](snippets/GenericWhereConstraints.cs#2)]

C# 8.0 以降の null 許容コンテキストでは、基本クラス型の null 許容属性が適用されます。 基底クラスが null 非許容の場合 (たとえば、`Base`)、型引数は null 非許容である必要があります。 基底クラスが null 許容の場合 (`Base?` など)、型引数は null 許容型または null 非許容型のいずれかになります。 基底クラスが null 非許容であるときに、型引数が null 許容の参照型である場合、コンパイラからは警告を発行されます。

`where` 句では、型が `class` または `struct` であることを指定できます。 `struct` 制約では、`System.ValueType` の基底クラスの制約を指定する必要はありません。 `System.ValueType` 型は基底クラスの制約として使用できません。 `class` 制約と `struct` 制約の両方の例を次に示します。

[!code-csharp[using the class and struct constraints](snippets/GenericWhereConstraints.cs#3)]

C# 8.0 以降の null 許容コンテキストでは、`class` 制約には、型が null 非許容の参照型である必要があります。 null 許容の参照型を許可するには、`class?` 制約を使用して、null 許容と null 非許容の参照型の両方を許可します。

`where` 句には、`notnull` 制約を含めることができます。 `notnull` 制約では、型パラメーターを null 非許容型に制限します。 その型には、[値型](../builtin-types/value-types.md)または null 非許容参照型を指定できます。 `notnull` 制約は、C# 8.0 以降の [`nullable enable` コンテキスト](../../nullable-references.md#nullable-contexts)でコンパイルされたコードで使用できます。 他の制約とは異なり、型引数が `notnull` 制約に違反すると、コンパイラによりエラーではなく警告が生成されます。 警告は、`nullable enable` コンテキストでのみ生成されます。

> [!IMPORTANT]
> `notnull` 制約が含まれるジェネリック宣言は、null 許容が未指定のコンテキストで使用できますが、コンパイラではその制約は強制されません。

[!code-csharp[using the nonnull constraint](snippets/GenericWhereConstraints.cs#NotNull)]

`where` 句には、`unmanaged` 制約を含めることもできます。 `unmanaged` 制約では、[アンマネージド型](../builtin-types/unmanaged-types.md)と呼ばれる型に対して型パラメーターを制限します。 `unmanaged` 制約を使用すると、C# でローレベルの相互運用コードを記述しやすくなります。 この制約では、すべてのアンマネージド型にわたって再利用可能なルーチンを可能にします。 `unmanaged` 制約は、`class` や `struct` 制約と組み合わせることはできません。 `unmanaged` 制約は `struct` にする必要がある型を適用します。

[!code-csharp[using the unmanaged constraint](snippets/GenericWhereConstraints.cs#4)]

`where` 句には、コンストラクター制約 `new()` を含めることもできます。 その制約では、`new` 演算子を使用して型パラメーターのインスタンスを作成できるようにします。 [new() 制約](new-constraint.md)に基づいて、コンパイラで、指定されている型引数にはアクセス可能なパラメーターなしのコンストラクターが必要であることが認識されます。 次に例を示します。

[!code-csharp[using the new constraint](snippets/GenericWhereConstraints.cs#5)]

`new()` 制約は `where` 句の最後に示されます。 `new()` 制約は、`struct` や `unmanaged` 制約と組み合わせることはできません。 それらの制約を満たすすべての型には、`new()` 制約を重複させて、アクセス可能なパラメーターなしのコンストラクターが含まれている必要があります。

複数の型パラメーターがある場合には、型パラメーターごとに `where` 句を 1 つずつ使用します。次に例を示します。

[!code-csharp[using multiple where constraints](snippets/GenericWhereConstraints.cs#6)]

次の例に示すように、ジェネリック メソッドの型パラメーターにも制約を適用できます。

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#7)]

デリゲートに対する型パラメーター制約を記述する構文は、メソッドの構文と同じである点に注意してください。

[!code-csharp[where constraints with generic methods](snippets/GenericWhereConstraints.cs#8)]

汎用デリゲートについては、「[汎用デリゲート](../../programming-guide/generics/generic-delegates.md)」を参照してください。

制約の構文と使用方法の詳細については、「[型パラメーターの制約](../../programming-guide/generics/constraints-on-type-parameters.md)」を参照してください。

## <a name="c-language-specification"></a>C# 言語仕様

 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>関連項目

- [C# リファレンス](../index.md)
- [C# プログラミング ガイド](../../programming-guide/index.md)
- [ジェネリックの概要](../../programming-guide/generics/index.md)
- [new 制約](./new-constraint.md)
- [型パラメーターの制約](../../programming-guide/generics/constraints-on-type-parameters.md)
