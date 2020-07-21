---
title: 継承
description: "'inherit' キーワードを使用して F# 継承関係を指定する方法について説明します。"
ms.date: 05/16/2016
ms.openlocfilehash: 5ab891a93528427a66e4eb8f7bfeccbf6e4d2c7e
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401131"
---
# <a name="inheritance"></a>継承

継承は、オブジェクト指向プログラミングにおける "is-a" 関係 (サブタイプ) をモデル化するために使用されます。

## <a name="specifying-inheritance-relationships"></a>継承関係の指定

継承関係を指定するには、クラス`inherit`宣言でキーワードを使用します。 基本的な構文形式を次の例に示します。

```fsharp
type MyDerived(...) =
    inherit MyBase(...)
```

クラスは、1 つの直接基本クラスを 1 つでも持つことができます。 `inherit`キーワードを使用して基本クラスを指定しない場合、そのクラスは暗黙的に . `System.Object`

## <a name="inherited-members"></a>継承メンバー

クラスが別のクラスから継承する場合、基本クラスのメソッドとメンバーは、派生クラスの直接メンバーであるかのように、派生クラスのユーザーが使用できます。

let バインディングとコンストラクター パラメーターはクラスに対してプライベートであるため、派生クラスからはアクセスできません。

キーワード`base`は派生クラスで使用でき、基本クラスのインスタンスを参照します。 これは自己識別子のように使用されます。

## <a name="virtual-methods-and-overrides"></a>仮想メソッドとオーバーライド

F# では、他の .NET 言語と比較して、仮想メソッド (およびプロパティ) の動作が若干異なります。 新しい仮想メンバーを宣言するには、 キーワード`abstract`を使用します。 この方法の既定の実装を提供するかどうかに関係なく、これを行います。 したがって、基本クラスの仮想メソッドの完全な定義は、次のパターンに従います。

```fsharp
abstract member [method-name] : [type]

default [self-identifier].[method-name] [argument-list] = [method-body]
```

派生クラスでは、この仮想メソッドのオーバーライドは次のパターンに従います。

```fsharp
override [self-identifier].[method-name] [argument-list] = [method-body]
```

基本クラスの既定の実装を省略すると、基本クラスは抽象クラスになります。

次のコード例は、基本クラスでの新しい仮想`function1`メソッドの宣言と、それを派生クラスでオーバーライドする方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2601.fs)]

## <a name="constructors-and-inheritance"></a>コンストラクターと継承

基本クラスのコンストラクターは、派生クラスで呼び出す必要があります。 基本クラスのコンストラクターの引数は、句の引数リストに`inherit`表示されます。 使用される値は、派生クラスのコンストラクターに渡される引数から決定する必要があります。

次のコードは、派生クラスが inherit 句の基本クラス コンストラクターを呼び出す、基本クラスと派生クラスを示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2602.fs)]

複数のコンストラクターの場合は、次のコードを使用できます。 派生クラスのコンストラクターの最初の行は`inherit`句で、フィールドは`val`キーワードで宣言された明示的なフィールドとして表示されます。 詳細については、「[明示的なフィールド: キーワード`val`](./members/explicit-fields-the-val-keyword.md)」を参照してください。

```fsharp
type BaseClass =
    val string1 : string
    new (str) = { string1 = str }
    new () = { string1 = "" }

type DerivedClass =
    inherit BaseClass

    val string2 : string
    new (str1, str2) = { inherit BaseClass(str1); string2 = str2 }
    new (str2) = { inherit BaseClass(); string2 = str2 }

let obj1 = DerivedClass("A", "B")
let obj2 = DerivedClass("A")
```

## <a name="alternatives-to-inheritance"></a>継承の代替方法

型のマイナーな変更が必要な場合は、継承の代わりにオブジェクト式を使用することを検討してください。 次の例は、新しい派生型を作成する代わりにオブジェクト式を使用する方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet2603.fs)]

オブジェクト式の詳細については、「[オブジェクト](object-expressions.md)式」を参照してください。

オブジェクト階層を作成する場合は、継承ではなく判別共用体を使用することを検討してください。 判別共用体は、共通の全体的なタイプを共有するさまざまなオブジェクトの様々な動作をモデル化することもできます。 単一の判別共用体は、多くの場合、互いに小さなバリエーションである派生クラスの数を必要としなくなります。 判別共用体の詳細については、「[判別共用体](discriminated-unions.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [オブジェクト式](object-expressions.md)
- [F# 言語リファレンス](index.md)
