---
title: キーワード リファレンス
description: F# 言語のすべてのキーワードに関する情報へのリンクを検索します。
f1_keywords:
- new_FS
- use_FS
- end_FS
- lsl_FS
- exception_FS
- asr_FS
- if_FS
- internal_FS
- default_FS
- in_FS
- lsr_FS
- open_FS
- static_FS
- assert_FS
- match_FS
- land_FS
- with_FS
- inherit_FS
- mutable_FS
- downto_FS
- false_FS
- sig_FS
- and_FS
- true_FS
- namespace_FS
- public_FS
- lxor_FS
- val_FS
- void_FS
- downcast_FS
- function_FS
- while_FS
- for_FS
- class_FS
- done_FS
- to_FS
- module_FS
- let_FS
- delegate_FS
- abstract_FS
- then_FS
- when_FS
- lazy_FS
- try_FS
- inline_FS
- do_FS
- upcast_FS
- begin_FS
- base_FS
- fun_FS
- struct_FS
- as_FS
- extern_FS
- null_FS
- lor_FS
- return_FS
- mod_FS
- private_FS
- of_FS
- or_FS
- member_FS
- type_FS
- rec_FS
- elif_FS
- override_FS
- interface_FS
- yield_FS
- else_FS
- finally_FS
- global_FS
- select_FS
- use!_FS
dev_langs:
- FSharp
ms.date: 11/04/2019
ms.openlocfilehash: 34959f471406643e85990c2c80a38a684759a7f9
ms.sourcegitcommit: b16eacb6f94a5b601882a861ad17cc5470a8d5d5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/27/2020
ms.locfileid: "80352310"
---
# <a name="keyword-reference"></a>キーワード リファレンス

このトピックには、F# のすべての言語キーワードに関する情報へのリンクが含まれています。

## <a name="f-keyword-table"></a>F# キーワード テーブル

次の表は、すべての F# キーワードをアルファベット順に示し、簡単な説明と関連トピックへのリンクを示しています。

|Keyword|Link|説明|
|-------|----|-----------|
|`abstract`|[メンバー](./members/index.md)<br /><br />[抽象クラス](abstract-classes.md)|メソッドが宣言されている型に実装がないか、仮想で既定の実装を持つメソッドを示します。|
|`and`|[`let`バインド](./functions/let-bindings.md)<br /><br />[レコード](records.md)<br /><br />[メンバー](./members/index.md)<br /><br />[制約](./generics/constraints.md)|相互に再帰的なバインディングとレコード、プロパティ宣言、およびジェネリック パラメーターに対する複数の制約で使用されます。|
|`as`|[クラス](classes.md)<br /><br />[パターン マッチ](Pattern-Matching.md)|現在のクラス オブジェクトにオブジェクト名を付けるために使用します。 また、パターンマッチ内のパターン全体に名前を付けるためにも使用されます。|
|`assert`|[アサーション](assertions.md)|デバッグ中にコードを検証するために使用します。|
|`base`|[クラス](classes.md)<br /><br />[継承](inheritance.md)|基本クラス オブジェクトの名前として使用されます。|
|`begin`|[冗語構文](verbose-syntax.md)|詳細な構文では、コード ブロックの開始を示します。|
|`class`|[クラス](classes.md)|詳細な構文では、クラス定義の開始を示します。|
|`default`|[メンバー](./members/index.md)|抽象メソッドの実装を示します。仮想メソッドを作成するために抽象メソッド宣言と一緒に使用されます。|
|`delegate`|[デリゲート](delegates.md)|デリゲートを宣言するために使用します。|
|`do`|[do 束縛](./functions/do-bindings.md)<br /><br />[ループ: `for...to` 式](loops-for-to-expression.md)<br /><br />[ループ: `for...in` 式](loops-for-in-expression.md)<br /><br />[ループ: `while...do` 式](loops-while-do-expression.md)|ループ構造で使用されるか、命令型コードを実行します。|
|`done`|[冗語構文](verbose-syntax.md)|詳細な構文では、ループ式のコード ブロックの末尾を示します。|
|`downcast`|[キャストと変換](casting-and-conversions.md)|継承チェーンの下位にある型に変換するために使用します。|
|`downto`|[ループ: `for...to` 式](loops-for-to-expression.md)|`for`逆にカウントするときに使用される式。|
|`elif`|[条件式:`if...then...else`](conditional-expressions-if-then-else.md)|条件付き分岐で使用されます。 の短い形式`else if`.|
|`else`|[条件式:`if...then...else`](conditional-expressions-if-then-else.md)|条件付き分岐で使用されます。|
|`end`|[構造体](structures.md)<br /><br />[判別共用体](discriminated-unions.md)<br /><br />[レコード](records.md)<br /><br />[型拡張](type-extensions.md)<br /><br />[冗語構文](verbose-syntax.md)|型定義および型拡張では、メンバー定義のセクションの末尾を示します。<br /><br />詳細な構文では、キーワードで始まるコード ブロックの末尾を指定するために使用します`begin`。|
|`exception`|[例外処理](./exception-handling/index.md)<br /><br />[例外の種類](./exception-handling/exception-types.md)|例外の種類を宣言するために使用します。|
|`extern`|[外部関数](./functions/external-functions.md)|宣言されたプログラム要素が別のバイナリまたはアセンブリで定義されていることを示します。|
|`false`|[プリミティブ型](basic-types.md)|ブール型リテラルとして使用されます。|
|`finally`|[例外: `try...finally` 式](./exception-handling/the-try-finally-expression.md)|例外が発生`try`したかどうかに関係なく実行されるコード ブロックを導入するために、共に使用します。|
|`fixed`|[固定](fixed.md)|ガベージ コレクションを回避するために、スタック上のポインターを "ピン留め" するために使用します。|
|`for`|[ループ: `for...to` 式](loops-for-to-expression.md)<br /><br />[ループ: for...in 式](loops-for-in-expression.md)|ループ構造で使用されます。|
|`fun`|[ラムダ式:`fun`キーワード](./functions/lambda-expressions-the-fun-keyword.md)|ラムダ式で使用されます。|
|`function`|[match 式](match-expressions.md)<br /><br />[ラムダ式: 楽しいキーワード](./functions/lambda-expressions-the-fun-keyword.md)|キーワードの短い代替として使用`fun`され、単`match`一の引数でパターン一致を持つラムダ式の式。|
|`global`|[名前空間](namespaces.md)|最上位の .NET 名前空間を参照するために使用します。|
|`if`|[条件式:`if...then...else`](conditional-expressions-if-then-else.md)|条件付き分岐構造で使用されます。|
|`in`|[ループ: for...in 式](loops-for-in-expression.md)<br /><br />[冗語構文](verbose-syntax.md)|シーケンス式、および詳細構文で、式とバインディングを分離するために使用されます。|
|`inherit`|[継承](inheritance.md)|基本クラスまたは基本インターフェイスを指定するために使用します。|
|`inline`|[関数](./functions/index.md)<br /><br />[インライン関数](./functions/inline-functions.md)|呼び出し元のコードに直接統合する関数を示すために使用されます。|
|`interface`|[インターフェイス](interfaces.md)|インターフェイスの宣言と実装に使用します。|
|`internal`|[アクセス制御](access-control.md)|メンバーがアセンブリ内で可視であり、その外部には表示されないことを指定するために使用します。|
|`lazy`|[遅延式](lazy-expressions.md)|結果が必要な場合にのみ実行される式を指定するために使用します。|
|`let`|[`let`バインド](./functions/let-bindings.md)|名前を値または関数に関連付けるか、バインドするために使用します。|
|`let!`|[非同期ワークフロー](asynchronous-workflows.md)<br /><br />[コンピュテーション式](computation-expressions.md)|非同期の計算の結果に名前をバインドする非同期ワークフローで使用されるか、その他の計算式で、計算タイプである結果に名前をバインドするために使用されます。|
|`match`|[match 式](match-expressions.md)|値をパターンと比較して分岐するために使用します。|
|`match!`|[コンピュテーション式](computation-expressions.md#match)|計算式の呼び出しとその結果に対するパターン一致をインライン化するために使用されます。|
|`member`|[メンバー](./members/index.md)|オブジェクト型でプロパティまたはメソッドを宣言するために使用します。|
|`module`|[モジュール](modules.md)|名前を関連する型、値、および関数のグループに関連付け、他のコードから論理的に分離するために使用します。|
|`mutable`|[let 束縛](./functions/let-bindings.md)|変数、つまり変更可能な値を宣言するために使用します。|
|`namespace`|[名前空間](namespaces.md)|名前を関連する型とモジュールのグループに関連付け、他のコードから論理的に分離するために使用します。|
|`new`|[コンストラクター](./members/constructors.md)<br /><br />[制約](./generics/constraints.md)|オブジェクトを作成または作成できるコンストラクターを宣言、定義、または呼び出すために使用します。<br /><br />ジェネリック パラメーター制約で使用して、型に特定のコンストラクターが必要であることを示します。|
|`not`|[シンボルと演算子のリファレンス](./symbol-and-operator-reference/index.md)<br /><br />[制約](./generics/constraints.md)|実際にはキーワードではありません。 ただし、`not struct`組み合わせてジェネリック パラメーター制約として使用されます。|
|`null`|[null 値](./values/null-values.md)<br /><br />[制約](./generics/constraints.md)|オブジェクトがないことを示します。<br /><br />ジェネリック パラメーター制約でも使用されます。|
|`of`|[判別共用体](discriminated-unions.md)<br /><br />[デリゲート](delegates.md)<br /><br />[例外の種類](./exception-handling/exception-types.md)|値のカテゴリの種類を示すために、およびデリゲート宣言と例外宣言で、判別共用体で使用されます。|
|`open`|[インポート宣言: `open` キーワード](import-declarations-the-open-keyword.md)|名前空間またはモジュールの内容を修飾なしで利用できるようにするために使用します。|
|`or`|[シンボルと演算子のリファレンス](./symbol-and-operator-reference/index.md)<br /><br />[制約](./generics/constraints.md)|ブール`or`演算子としてブール条件で使用されます。 `||` と同等です。<br /><br />メンバー制約でも使用されます。|
|`override`|[メンバー](./members/index.md)|基本バージョンとは異なる抽象メソッドまたは仮想メソッドのバージョンを実装するために使用します。|
|`private`|[アクセス制御](access-control.md)|メンバーへのアクセスを、同じ型またはモジュール内のコードに制限します。|
|`public`|[アクセス制御](access-control.md)|型の外部からメンバーにアクセスできるようにします。|
|`rec`|[関数](./functions/index.md)|関数が再帰的であることを示すために使用されます。|
|`return`|[非同期ワークフロー](Asynchronous-Workflows.md)<br /><br />[コンピュテーション式](computation-expressions.md)|計算式の結果として指定する値を示すために使用されます。|
|`return!`|[コンピュテーション式](computation-expressions.md)<br /><br />[非同期ワークフロー](asynchronous-workflows.md)|評価された場合に、含まれている計算式の結果を提供する計算式を示すために使用されます。|
|`select`|[クエリ式](query-expressions.md)|抽出するフィールドまたは列を指定するために、クエリ式で使用されます。 これはコンテキストキーワードであり、実際には予約語ではなく、適切なコンテキストのキーワードとしてのみ機能することに注意してください。|
|`static`|[メンバー](./members/index.md)|型のインスタンスなしで呼び出すことができるメソッドまたはプロパティ、または型のすべてのインスタンス間で共有される値のメンバーを示すために使用します。|
|`struct`|[構造体](structures.md)<br /><br /> [タプル](tuples.md)<br/><br/>[制約](./generics/constraints.md)|構造体型を宣言するために使用します。<br /><br/>構造体の組を指定するために使用します。<br/><br />ジェネリック パラメーター制約でも使用されます。<br /><br />モジュール定義での OCaml 互換性のために使用されます。|
|`then`|[条件式:`if...then...else`](conditional-expressions-if-then-else.md)<br /><br />[コンストラクター](./members/constructors.md)|条件式で使用されます。<br /><br />また、オブジェクト構築後に副作用を実行するために使用されます。|
|`to`|[ループ: `for...to` 式](loops-for-to-expression.md)|範囲を`for`示すためにループで使用されます。|
|`true`|[プリミティブ型](basic-types.md)|ブール型リテラルとして使用されます。|
|`try`|[例外: try...with 式](./exception-handling/the-try-with-expression.md)<br /><br />[例外: try...finally 式](./exception-handling/the-try-finally-expression.md)|例外を生成する可能性のあるコード ブロックを導入するために使用します。 または と`with`一`finally`緒に使用します。|
|`type`|[F# の型](fsharp-types.md)<br /><br />[クラス](classes.md)<br /><br />[レコード](records.md)<br /><br />[構造体](structures.md)<br /><br />[列挙](enumerations.md)<br /><br />[判別共用体](discriminated-unions.md)<br /><br />[型略称](type-abbreviations.md)<br /><br />[測定単位](units-of-measure.md)|クラス、レコード、構造体、判別共用体、列挙型、測定単位、または型の省略形を宣言するために使用します。|
|`upcast`|[キャストと変換](casting-and-conversions.md)|継承チェーンの上位の型に変換するために使用します。|
|`use`|[リソースの管理: `use` キーワード](resource-management-the-use-keyword.md)|リソースを`let`解放するために呼び出`Dispose`す必要がある値の代わりに使用されます。|
|`use!`|[コンピュテーション式](computation-expressions.md)<br /><br />[非同期ワークフロー](asynchronous-workflows.md)|リソースを`let!`解放するために呼び出す必要`Dispose`がある値の非同期ワークフローやその他の計算式の代わりに使用されます。|
|`val`|[明示的なフィールド:`val`キーワード](./members/explicit-fields-the-val-keyword.md)<br /><br />[シグネチャ](signature-files.md)<br /><br />[メンバー](./members/index.md)|限られた状況で、値を示すためにシグネチャで使用するか、型でメンバーを宣言します。|
|`void`|[プリミティブ型](basic-types.md)|.NET`void`の種類を示します。 他の .NET 言語と相互運用するときに使用されます。|
|`when`|[制約](./generics/constraints.md)|パターン一致のブール条件 (*ガード時*) に使用され、ジェネリック型パラメーターの制約句を導入します。|
|`while`|[ループ: `while...do` 式](loops-while-do-expression.md)|ループ構造を導入します。|
|`with`|[match 式](match-expressions.md)<br /><br />[オブジェクト式](object-expressions.md)<br /><br />[レコード式のコピーと更新](copy-and-update-record-expressions.md)<br /><br />[型拡張](type-extensions.md)<br /><br />[例外: `try...with` 式](./exception-handling/the-try-with-expression.md)|パターンマッチング式で`match`キーワードと一緒に使用されます。 また、オブジェクト式、レコード コピー式、および型拡張でメンバー定義を導入し、例外ハンドラーを導入するために使用します。|
|`yield`|[リスト](lists.md)、[配列](arrays.md)、[シーケンス](sequences.md)|シーケンスの値を生成するために、リスト、配列、またはシーケンス式で使用されます。 ほとんどの状況では暗黙的であるため、通常は省略できます。|
|`yield!`|[コンピュテーション式](computation-expressions.md)<br /><br />[非同期ワークフロー](asynchronous-workflows.md)|指定された計算式の結果を、含む計算式の結果のコレクションに追加するために、計算式で使用されます。|

次のトークンは、OCaml 言語のキーワードであるため、F# で予約されています。

- `asr`
- `land`
- `lor`
- `lsl`
- `lsr`
- `lxor`
- `mod`
- `sig`

コンパイラー・オプション`--mlcompatibility`を使用する場合、上記のキーワードを ID として使用できます。

次のトークンは、F# 言語の将来の拡張のためにキーワードとして予約されています。

- `atomic`
- `break`
- `checked`
- `component`
- `const`
- `constraint`
- `constructor`
- `continue`
- `eager`
- `event`
- `external`
- `functor`
- `include`
- `method`
- `mixin`
- `object`
- `parallel`
- `process`
- `protected`
- `pure`
- `sealed`
- `tailcall`
- `trait`
- `virtual`
- `volatile`

## <a name="see-also"></a>関連項目

- [F# 言語リファレンス](index.md)
- [シンボルと演算子のリファレンス](./symbol-and-operator-reference/index.md)
- [コンパイラ オプション](compiler-options.md)
