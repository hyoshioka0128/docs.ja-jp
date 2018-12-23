---
title: 継承 (F#)
description: "'Inherit' キーワードを使用して F# 継承リレーションシップを指定する方法について説明します。"
ms.date: 05/16/2016
ms.openlocfilehash: e4d79244fb9bada5db0c5c4c7179d4bfe6e21f3d
ms.sourcegitcommit: db8b83057d052c1f9f249d128b08d4423af0f7c2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2018
ms.locfileid: "43864470"
---
# <a name="inheritance"></a>継承

継承の使用を「の」リレーションシップをモデル オブジェクト指向プログラミングでは、サブタイプまたはします。

## <a name="specifying-inheritance-relationships"></a>継承リレーションシップの指定

使用して継承リレーションシップを指定する、`inherit`クラス宣言でキーワード。 基本的な構文形式は、次の例に示します。

```fsharp
type MyDerived(...) =
    inherit MyBase(...)
```

クラスは、最大で 1 つ直接基底クラスを持つことができます。 使用して基底クラスを指定しないかどうか、`inherit`キーワード、クラスから暗黙的に継承`System.Object`します。

## <a name="inherited-members"></a>継承されたメンバー

クラスは、別のクラスから継承している場合、メソッドと基底クラスのメンバーは場合、派生クラスの直接のメンバーと同様に、派生クラスのユーザーに公開します。

いずれかの 'let' バインディングとコンス トラクターのパラメーターは、クラスに対してプライベートであるし、そのため、派生クラスからアクセスできません。

キーワード`base`は派生クラスで使用でき、基本クラスのインスタンスを参照します。 これは、自己識別子のように使用されます。

## <a name="virtual-methods-and-overrides"></a>仮想メソッドとオーバーライド

仮想メソッド (およびプロパティ) 動作は少し異なります F# で他の .NET 言語と比較しています。 使用する新しい仮想メンバーを宣言する、`abstract`キーワード。 この操作は、そのメソッドの既定の実装を提供するかどうかに関係なく行います。 したがって、基底クラス仮想メソッドの完全な定義では、このパターンに従います。

```fsharp
abstract member [method-name] : [type]

default [self-identifier].[method-name] [argument-list] = [method-body]
```

この仮想メソッドのオーバーライドを派生クラスでこのパターンに従います。

```fsharp
override [self-identifier].[method-name] [argument-list] = [method-body]
```

基底クラスの既定の実装を省略した場合、基底クラスは抽象クラスになります。

次のコード例は、新しい仮想メソッドの宣言を示しています。`function1`で基底クラスと派生クラスでオーバーライドする方法。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2601.fs)]

## <a name="constructors-and-inheritance"></a>コンストラクターと継承

派生クラスでは、基底クラスのコンス トラクターを呼び出す必要があります。 基底クラスのコンス トラクターの引数、引数のリストに表示、`inherit`句。 使用される値は、派生クラスのコンス トラクターに指定された引数から決定する必要があります。

次のコードは基底クラスと派生クラスでは、派生クラスが継承句の基本クラス コンス トラクターを呼び出します。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2602.fs)]

複数のコンス トラクターの場合、次のコードを使用していることができます。 派生クラスのコンス トラクターの最初の行は、`inherit`句と、フィールドで宣言された明示的なフィールドとして表示されます、`val`キーワード。 詳細については、次を参照してください。[明示的なフィールド:、`val`キーワード](members/explicit-fields-the-val-keyword.md)します。

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

## <a name="alternatives-to-inheritance"></a>継承の代替手段

型の若干の変更が必要な場合は、継承する代わりにオブジェクト式の使用を検討してください。 次の例は、新しい派生型を作成する代わりにオブジェクト式の使用を示しています。

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet2603.fs)]

オブジェクトの式の詳細については、次を参照してください。[オブジェクト式](object-expressions.md)します。

オブジェクト階層を作成するときは、継承ではなくの判別共用体の使用を検討します。 判別共用体は、共通の全体的な型を共有する別のオブジェクトのさまざまなモデルの動作でこともできます。 1 つの判別共用体では、さまざまな派生クラスの他のわずかな違いをする必要がある多くの場合。 判別共用体の詳細については、次を参照してください。[判別共用体](discriminated-unions.md)します。

## <a name="see-also"></a>関連項目

- [オブジェクト式](object-expressions.md)
- [F# 言語リファレンス](index.md)
