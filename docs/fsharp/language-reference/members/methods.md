---
title: メソッド
description: F# メソッドが、オブジェクトと型の機能と動作を公開および実装するために使用される型に関連付けられた関数である方法について説明します。
ms.date: 11/04/2019
ms.openlocfilehash: 6f5ae76ea450b07763eb58d0c95b18b30f634551
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "79401065"
---
# <a name="methods"></a>メソッド

*メソッド*は、型に関連付けられている関数です。 オブジェクト指向プログラミングでは、メソッドを使用してオブジェクトと型の機能と動作を公開および実装します。

## <a name="syntax"></a>構文

```fsharp
// Instance method definition.
[ attributes ]
member [inline] self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Static method definition.
[ attributes ]
static member [inline] method-name parameter-list [ : return-type ] =
    method-body

// Abstract method declaration or virtual dispatch slot.
[ attributes ]
abstract member method-name : type-signature

// Virtual method declaration and default implementation.
[ attributes ]
abstract member method-name : type-signature
[ attributes ]
default self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Override of inherited virtual method.
[ attributes ]
override self-identifier.method-name parameter-list [ : return-type ] =
    method-body

// Optional and DefaultParameterValue attributes on input parameters
[ attributes ]
[ modifier ] member [inline] self-identifier.method-name ([<Optional; DefaultParameterValue( default-value )>] input) [ : return-type ]
```

## <a name="remarks"></a>解説

前の構文では、メソッドの宣言と定義のさまざまな形式を確認できます。 長いメソッドボディでは、改行は等号 (=) に続き、メソッド本体全体がインデントされます。

属性は、任意のメソッド宣言に適用できます。 これらは、メソッド定義の構文の前に、通常は別の行にリストされます。 詳細については、「[属性](../attributes.md)」を参照してください。

メソッドは、`inline`にマークできます。 `inline` の詳細については、「[Inline Functions](../functions/inline-functions.md)」(インライン関数) を参照してください。

非インライン メソッドは、型内で再帰的に使用できます。キーワードを明示的に使用する`rec`必要はありません。

## <a name="instance-methods"></a>インスタンス メソッド

インスタンス メソッドは`member`、キーワードと*自己識別子*を使用して宣言され、その後にピリオド (.) とメソッド名とパラメーターが続きます。 `let`バインディングの場合と同様に、*パラメーター・リスト*もパターンにすることができます。 通常、メソッド パラメーターは、他の .NET Framework 言語で作成された場合に F# でメソッドが表示される方法である、組の形式でかっこで囲みます。 ただし、カリー化された形式 (スペースで区切られたパラメーター) も一般的であり、他のパターンもサポートされています。

非抽象インスタンス メソッドの定義と使用方法を次の例に示します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3401.fs)]

インスタンス メソッド内では、let バインディングを使用して定義されたフィールドにアクセスするために、自己識別子を使用しないでください。 他のメンバーやプロパティにアクセスする場合は、自己識別子を使用します。

## <a name="static-methods"></a>静的メソッド

このキーワード`static`は、メソッドをインスタンスなしで呼び出すことができるように指定し、オブジェクト インスタンスに関連付けられていないことを指定するために使用されます。 それ以外の場合、メソッドはインスタンス メソッドです。

次のセクションの例では、キーワードで宣言された`let`フィールド、キーワードで宣言された`member`プロパティ メンバー、およびキーワードで宣言された静的`static`メソッドを示します。

次の例は、静的メソッドの定義と使用方法を示しています。 これらのメソッド定義が前のセクションの`SomeType`クラスに含まれると仮定します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3402.fs)]

## <a name="abstract-and-virtual-methods"></a>抽象メソッドと仮想メソッド

キーワード`abstract`は、メソッドに仮想ディスパッチ スロットがあり、クラスに定義がない可能性があることを示します。 *仮想ディスパッチ・スロット*は、内部保守の関数の表の中の項目で、実行時にオブジェクト指向型の仮想関数呼び出しを検索するために使用されます。 仮想ディスパッチ機構は、オブジェクト指向プログラミングの重要な特徴である*ポリモーフィズム*を実装するメカニズムです。 定義のない抽象メソッドが少なくとも 1 つあるクラスは*抽象クラス*です。 抽象クラスの詳細については、「[抽象クラス](../abstract-classes.md)」を参照してください。

抽象メソッドの宣言には、メソッド本体は含まれません。 代わりに、メソッドの名前の後にコロン (:)メソッドの型シグネチャ。 メソッドの型シグネチャは、パラメーター名を除いて、Visual Studio コード エディターでメソッド名の上にマウス ポインターを置いたときに IntelliSense によって表示されるシグネチャと同じです。 対話的に作業しているときは、型シグネチャもインタプリタの fsi.exe によって表示されます。 メソッドの型シグネチャは、パラメーターの型を一覧表示し、その後に戻り値の型を適切な区切り記号で示します。 カリー化されたパラメーターは で`->`区切られ、組のパラメーターは`*`で区切られます。 戻り値は、常に、引数から記号`->`によって区切られます。 かっこを使用すると、関数型がパラメーターの場合など、複雑なパラメーターをグループ化したり、組が 2 つのパラメーターとしてではなく単一のパラメーターとして扱われるように指定したりできます。

また、抽象メソッドに定義をクラスに追加し、キーワードを`default`使用して抽象メソッドの既定の定義を指定することもできます。 同じクラスの定義を持つ抽象メソッドは、他の .NET Framework 言語の仮想メソッドと同じです。 定義が存在するかどうかにかかわらず、キーワードは`abstract`クラスの仮想関数テーブルに新しいディスパッチ スロットを作成します。

基本クラスが抽象メソッドを実装しているかどうかに関係なく、派生クラスは抽象メソッドの実装を提供できます。 派生クラスで抽象メソッドを実装するには、または`override``default`キーワードを使用する以外は、派生クラスで同じ名前とシグネチャを持つメソッドを定義し、メソッド本体を提供します。 キーワードとは`override`全`default`く同じ意味です。 新`override`しいメソッドが基本クラスの実装をオーバーライドする場合に使用します。元`default`の抽象宣言と同じクラスで実装を作成する場合に使用します。 基本クラスで`abstract`抽象として宣言されたメソッドを実装するメソッドでは、キーワードを使用しないでください。

次の例は、.NET `Rotate` Framework 仮想メソッドと同等の既定の実装を持つ抽象メソッドを示しています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3403.fs)]

基本クラスのメソッドをオーバーライドする派生クラスの例を次に示します。 この場合、オーバーライドはメソッドが何も実行しないように動作を変更します。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3404.fs)]

## <a name="overloaded-methods"></a>オーバーロードされたメソッド

オーバーロードされたメソッドは、特定の型で同じ名前を持ち、引数が異なるメソッドです。 F# では、通常、オーバーロードされたメソッドの代わりに省略可能な引数が使用されます。 ただし、オーバーロードされたメソッドは、引数がカリー化された形式ではなく、組形式である場合、言語で許可されます。

## <a name="optional-arguments"></a>省略可能な引数

F# 4.1 以降では、メソッドの既定のパラメーター値を持つ省略可能な引数を持つことができます。  これは、C# コードとの相互運用を容易にするためです。  次の例は、構文を示しています。

```fsharp
// A class with a method M, which takes in an optional integer argument.
type C() =
    _.M([<Optional; DefaultParameterValue(12)>] i) = i + 1
```

渡される値は入力タイプと`DefaultParameterValue`一致する必要があります。  上記のサンプルでは`int`、.  非整数値を渡そうとする`DefaultParameterValue`と、コンパイル エラーが発生します。

## <a name="example-properties-and-methods"></a>例: プロパティとメソッド

次の例には、フィールド、プライベート関数、プロパティ、および静的メソッドの例を含む型が含まれています。

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-1/snippet3406.fs)]

## <a name="see-also"></a>関連項目

- [メンバー](index.md)
