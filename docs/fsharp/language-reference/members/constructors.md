---
title: コンストラクター
description: でF#コンストラクターを定義および使用して、クラスおよび構造体オブジェクトを作成および初期化する方法について説明します。
ms.date: 05/16/2016
ms.openlocfilehash: 6769ec7fc6768090d8ae68e21946a58829b6eea0
ms.sourcegitcommit: 878ca7550b653114c3968ef8906da2b3e60e3c7a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2019
ms.locfileid: "71736848"
---
# <a name="constructors"></a>コンストラクター

この記事では、コンストラクターを定義および使用して、クラスオブジェクトと構造体オブジェクトを作成および初期化する方法について説明します。

## <a name="construction-of-class-objects"></a>クラスオブジェクトの構築

クラス型のオブジェクトにはコンストラクターがあります。 コンストラクターには、次の2種類があります。 1つはプライマリコンストラクターであり、パラメーターは型名の直後にかっこで囲まれています。 `new`キーワードを使用して、その他のオプションの追加コンストラクターを指定します。 このような追加のコンストラクターは、プライマリコンストラクターを呼び出す必要があります。

プライマリコンストラクターには`let` 、 `do`クラス定義の先頭に表示されるバインディングとバインドが含まれています。 バインディング`let`は、クラスのプライベートフィールドおよびメソッドを宣言し`do`ます。バインディングはコードを実行します。 クラスコンストラクター内の`let`バインディングの詳細については、「 [ `let`クラスのバインディング](let-bindings-in-classes.md)」を参照してください。 コンストラクターでの`do`バインディングの詳細については、「 [ `do`クラスのバインディング](do-bindings-in-classes.md)」を参照してください。

呼び出すコンストラクターがプライマリコンストラクターであるか、追加のコンストラクターであるかに関係なく、 `new`式を使用してオブジェクトを作成できます。これには、省略可能`new`なキーワードを指定するかどうかにかかわらず、式を使用します。 オブジェクトをコンストラクター引数と共に初期化するには、引数の順序を指定してコンマで区切り、かっこで囲むか、名前付き引数と値をかっこで囲んで指定します。 また、プロパティ名を使用し、名前付きコンストラクター引数を使用するのと同じように値を割り当てることによって、オブジェクトの構築中にオブジェクトのプロパティを設定することもできます。

次のコードは、コンストラクターとオブジェクトを作成するさまざまな方法を持つクラスを示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3501.fs)]

出力は次のとおりです。

```console
Initialized object that has coordinates (1, 2, 3)
Initialized object that has coordinates (4, 5, 6)
Initialized object that has coordinates (7, 8, 9)
Initialized object that has coordinates (0, 0, 0)
```

## <a name="construction-of-structures"></a>構造体の構築

構造体は、クラスのすべての規則に従います。 したがって、プライマリコンストラクターを持つことができます。また、を使用`new`して追加のコンストラクターを指定することもできます。 ただし、構造体とクラスには1つの重要な違いがあります。構造体には、プライマリコンストラクターが定義されていない場合でも、パラメーターなしのコンストラクター (つまり、引数なし) を含めることができます。 パラメーターなしのコンストラクターは、すべてのフィールドをその型の既定値 (通常は0またはそれと等価) に初期化します。 構造体に対して定義するコンストラクターには、パラメーターなしのコンストラクターと競合しないように、少なくとも1つの引数が必要です。

また、多くの場合、構造体には`val`キーワードを使用して作成されたフィールドがあります。クラスにはこれらのフィールドも含まれます。 `val`キーワードを使用して定義されたフィールドを持つ構造体とクラスは、次のコードに示すように、レコード式を使用して追加のコンストラクターで初期化することもできます。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3502.fs)]

詳細については、次を参照してください。[明示的なフィールド:`val`キーワード](explicit-fields-the-val-keyword.md)します。

## <a name="executing-side-effects-in-constructors"></a>コンストラクターでの副作用の実行

クラスのプライマリコンストラクターは、 `do`バインディングでコードを実行できます。 ただし、 `do`バインドせずに、追加のコンストラクターでコードを実行する必要がある場合はどうすればよいでしょうか。 これを行うには、 `then`キーワードを使用します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3503.fs)]

プライマリコンストラクターの副作用は引き続き実行されます。 したがって、出力は次のようになります。

```console
Created a person object.
Created a person object.
Created an invalid person object.
```

## <a name="self-identifiers-in-constructors"></a>コンストラクター内の自己識別子

他のメンバーでは、各メンバーの定義で現在のオブジェクトの名前を指定します。 コンストラクターのパラメーターの直後に`as`キーワードを使用して、クラス定義の最初の行に自己識別子を配置することもできます。 この構文の例を次に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3504.fs)]

追加のコンストラクターでは、コンストラクターパラメーターの直後に`as`句を配置することで、自己識別子を定義することもできます。 この構文の例を次に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3505.fs)]

オブジェクトを完全に定義する前に使用しようとすると、問題が発生する可能性があります。 したがって、自己識別子を使用すると、コンパイラが警告を出力し、追加のチェックを挿入して、オブジェクトが初期化される前にオブジェクトのメンバーにアクセスしないようにすることができます。 自己識別子は、プライマリコンストラクターのバインディング、 `do`または追加のコンストラクター内の`then`キーワードの後にのみ使用してください。

自己識別子の名前は、で`this`ある必要はありません。 任意の有効な識別子を指定できます。

## <a name="assigning-values-to-properties-at-initialization"></a>初期化時のプロパティへの値の割り当て

コンストラクターの引数リストにフォーム`property = value`の割り当ての一覧を追加することにより、初期化コードでクラスオブジェクトのプロパティに値を割り当てることができます。 これを次のコード例に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3506.fs)]

次のバージョンの前のコードは、通常の引数、省略可能な引数、およびプロパティ設定を1つのコンストラクター呼び出しで組み合わせる方法を示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet3507.fs)]

## <a name="constructors-in-inherited-class"></a>継承されたクラスのコンストラクター

コンストラクターを持つ基底クラスから継承する場合は、inherit 句で引数を指定する必要があります。 詳細については、「[コンストラクターと継承](../inheritance.md#constructors-and-inheritance)」を参照してください。

## <a name="static-constructors-or-type-constructors"></a>静的コンストラクターまたは型コンストラクター

オブジェクトを作成するためのコードを指定する`let`だけ`do`でなく、型を最初に使用して型レベルで初期化を実行する前に実行されるクラス型で静的およびバインディングを作成することもできます。 詳細については、「クラスと[ `do`バインド](do-bindings-in-classes.md) [ `let`のバインド](let-bindings-in-classes.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [メンバー](index.md)
