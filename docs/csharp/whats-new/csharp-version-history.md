---
title: C# の歴史 - C# ガイド
description: この言語の最初のバージョンがどのようなものであったか、そしてそれ以降どのように進化してきたかについて説明します。
author: erikdietrich
ms.date: 04/08/2020
ms.openlocfilehash: ed9555bcef1c71964937c2bc18fedbc7da94f0db
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81738149"
---
# <a name="the-history-of-c"></a>C\# の歴史

この記事では、C# 言語の各メジャー リリースの履歴について説明します。 C# チームは、引き続き新機能を刷新および追加していきます。 今後のリリースに向けて検討される機能を含め、言語機能ステータスについての詳細は GitHub の [dotnet/roslyn リポジトリ](https://github.com/dotnet/roslyn/blob/master/docs/Language%20Feature%20Status.md)で見つけられます。

> [!IMPORTANT]
> C# 言語の一部の機能は、C# の仕様で定義されている "*標準ライブラリ*" の型とメソッドに依存しています。 .NET プラットフォームでは、さまざまなパッケージでそれらの型とメソッドが提供されています。 一例として、例外処理があります。 すべての `throw` ステートメントまたは式は、スローされたオブジェクトが <xref:System.Exception> から派生していることを確認するために、チェックされます。 同様に、すべての `catch` は、キャッチされた型が <xref:System.Exception> から派生していることを確認するために、チェックされます。 バージョンごとに新しい要件が追加されている場合があります。 古い環境で言語の最新機能を使用するには、特定のライブラリをインストールする必要がある場合があります。 これらの依存関係については、特定のバージョンごとに用意されたページに記載されています。 この依存関係の経緯と詳細については、[言語とライブラリ間の関係](relationships-between-language-and-library.md)に関する記事をご覧ください。

C# のビルド ツールでは、言語の最新のメジャー リリースが言語の既定のバージョンと見なされます。 メジャー リリースの間には、このセクションの他の記事で詳しく説明するポイント リリースが存在することがあります。 ポイント リリースで最新の機能を使用するには、[コンパイラ言語バージョンを構成](../language-reference/configure-language-version.md)し、バージョンを選択する必要があります。 C# 7.0 以降、3 つのポイント リリースがありました。

- [C# 7.3](csharp-7-3.md):
  - C# 7.3 は [Visual Studio 2017 バージョン 15.7](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) および [.NET Core 2.1 SDK](../../core/whats-new/dotnet-core-2-1.md) 以降で利用可能です。
- [C# 7.2](csharp-7-2.md):
  - C# 7.2 は [Visual Studio 2017 バージョン 15.5](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) および [.NET Core 2.0 SDK](../../core/whats-new/dotnet-core-2-0.md) 以降で利用可能です。
- [C# 7.1](csharp-7-1.md):
  - C# 7.1 は [Visual Studio 2017 バージョン 15.3](https://visualstudio.microsoft.com/vs/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link) および [.NET Core 2.0 SDK](../../core/whats-new/dotnet-core-2-0.md) 以降で利用可能です。

## <a name="c-version-10"></a>C# バージョン 1.0

振り返ってみると、Visual Studio .NET 2002 でリリースされた C# バージョン 1.0 は Java に似ていました。 [ECMA で掲げられた設計目標の一環](https://feeldotneteasy.blogspot.com/2011/01/c-design-goals.html)として、C# は "シンプルかつモダンな汎用オブジェクト指向言語" を目指していました。  当時、Java に似ていることは、初期の設計目標を達成したことを意味していました。

しかし、今 C# 1.0 を振り返ってみると、少し混乱するかもしれません。 現在では当たり前となっている組み込みの非同期機能や、ジェネリック関連の優れた機能の一部は備わっていませんでした。 実際、ジェネリック全体がなかったのです。  そして [LINQ](../linq/index.md) も、 まだ使用できませんでした。 このような追加機能が登場するまでにはまだ数年かかります。

C# バージョン 1.0 は、現在のバージョンと比べると、機能がはぎ取られたように見えます。 気がつくと冗長なコードを記述している場合があるでしょう。 しかしそれでも、千里の道も一歩からです。 C# バージョン 1.0 は、Windows プラットフォームにおける Java の実行可能な代替手段でした。

C# 1.0 の主な機能:

- [クラス](../programming-guide/classes-and-structs/classes.md)
- [構造体](../language-reference/builtin-types/struct.md)
- [インターフェイス](../programming-guide/interfaces/index.md)
- [イベント](../events-overview.md)
- [プロパティ](../properties.md)
- [デリゲート](../delegates-overview.md)
- [式](../programming-guide/statements-expressions-operators/expressions.md)
- [ステートメント](../programming-guide/statements-expressions-operators/statements.md)
- [属性](../programming-guide/concepts/attributes/index.md)

## <a name="c-version-12"></a>C# バージョン 1.2

Visual Studio .NET 2003 に付属の C# バージョン 1.2。 言語に対する細かな機能強化がいくつか含まれています。 最も重要な点は、このバージョン以降、<xref:System.Collections.IEnumerator> によって <xref:System.IDisposable> が実装された場合、`foreach` ループ内で生成されたコードでは、その <xref:System.Collections.IEnumerator> 上で <xref:System.IDisposable.Dispose%2A> が呼び出されているということです。

## <a name="c-version-20"></a>C# バージョン 2.0

ここから面白くなり始めます。 Visual Studio 2005 と共に 2005 年にリリースされた C# 2.0 の主な機能をいくつか見てみましょう。

- [ジェネリック](../programming-guide/generics/index.md)
- [部分型](../programming-guide/classes-and-structs/partial-classes-and-methods.md#partial-classes)
- [匿名メソッド](../language-reference/operators/delegate-operator.md)
- [null 許容値型](../language-reference/builtin-types/nullable-value-types.md)
- [反復子](../programming-guide/concepts/iterators.md)
- [共変性と反変性](../programming-guide/concepts/covariance-contravariance/index.md)

その他の C# 2.0 機能では既存の機能に新たな能力を追加しました。

- ゲッター/セッター別のアクセシビリティ
- メソッド グループの変換 (デリゲート)
- 静的クラス
- デリゲート推論

C# は汎用的なオブジェクト指向 (OO) 言語として始まったかもしれませんが、C# バージョン 2.0 ではそれが急速に変化しました。 マイクロソフトが本腰を入れると、いくつかの開発者の重大な問題点を追究しました。 そしてその問題点を著しく追究しました。

ジェネリックでは、型とメソッドがタイプ セーフを維持しながら任意の型に対して操作を行えます。 たとえば、<xref:System.Collections.Generic.List%601> があると、`List<string>` または `List<int>` を使用し、これらの文字列または整数に対してタイプ セーフ操作を実行しながら、これらを反復処理することができます。 ジェネリックの使用は、すべての操作で `ArrayList` から派生する `ListInt` を作成する方法や、`Object` からキャストする方法よりも優れています。

C# バージョン 2.0 で、反復子が導入されました。 手短に言うと、反復子を使用すると、`List` 内のすべての項目 (またはその他の列挙可能な型) を `foreach` ループで確認することができます。 反復子を言語のファーストクラスの部分として持つことで、言語の読みやすさと、ユーザーのコードについて推論する能力が劇的に高まりました。

それでもまだ、C# は Java にほんの少し後れを取り続けていました。 Java は、ジェネリックと反復子が含まれたバージョンを既にリリースしていました。 しかし間もなく、2 つの言語は別々の進化を続けていくことになります。

## <a name="c-version-30"></a>C# バージョン 3.0

C# バージョン 3.0 は、Visual Studio 2008 と共に 2007 年後半に登場しましたが、すべての言語機能が搭載されたのは、実際には .NET Framework バージョン 3.5 からでした。 このバージョンは、C# の成長において大きな変化を遂げました。 このバージョンで、C# は真に強力なプログラミング言語としての地位を確立しました。 このバージョンでの主な機能をいくつか見てみましょう。

- [自動実装プロパティ](../programming-guide/classes-and-structs/auto-implemented-properties.md)
- [匿名型](../programming-guide/classes-and-structs/anonymous-types.md)
- [クエリ式](../linq/query-expression-basics.md)
- [ラムダ式](../programming-guide/statements-expressions-operators/lambda-expressions.md)
- [式ツリー](../expression-trees.md)
- [拡張メソッド](../programming-guide/classes-and-structs/extension-methods.md)
- [暗黙的に型指定されるローカル変数](../language-reference/keywords/var.md)
- [部分メソッド](../language-reference/keywords/partial-method.md)
- [オブジェクト初期化子とコレクション初期化子](../programming-guide/classes-and-structs/object-and-collection-initializers.md)

今になって考えると、これらの機能の多くは必然で切り離せないものに思えます。 これらすべてが戦略的に組み合わさっています。 一般的には、C# のこのバージョンでの目玉機能はクエリ式 (統合言語クエリ (LINQ) とも呼ばれる) だったと考えられています。

もう少し異なる見解では、式ツリー、ラムダ式、匿名型が、LINQ が構築される基になっていると分析しています。 しかし、いずれにしても、C# 3.0 は革新的な概念を提示しました。 C# 3.0 から、C# をオブジェクト指向と関数型言語のハイブリッドに変換するための下準備が始まりました。

いろいろありますが、特に、今では記述できるようになった SQL スタイル、コレクションに対して操作を実行する宣言型クエリなどがあります。 `for` ループを記述して整数のリストの平均を計算する代わりに、今では単純に `list.Average()` でこれを行うことができます。 クエリ式と拡張メソッドの組み合わせにより、整数のリストが非常にスマートになったように見えるようになりました。

ユーザーが概念を真に理解して統合するには時間がかかりましたが、徐々にそうなりました。 そして数年後の現在、コードはもっと簡潔、シンプルかつ機能的になりました。

## <a name="c-version-40"></a>C# バージョン 4.0

Visual Studio 2010 でリリースされた C# バージョン 4.0 は、バージョン 3.0 の革新的なステータスに応えるための困難な時期だったと言えるでしょう。 バージョン 3.0 で C# は Java の影から脱却して、主要な言語となったのです。 この言語は急速に洗練されました。

次のバージョンでは、いくつかの興味深い新機能が導入されました。

- [動的バインディング](../language-reference/builtin-types/reference-types.md)
- [名前付き/省略可能な引数](../programming-guide/classes-and-structs/named-and-optional-arguments.md)
- [ジェネリックの共変と反変](../../standard/generics/covariance-and-contravariance.md)
- [埋め込まれた相互運用機能型](../../framework/interop/type-equivalence-and-embedded-interop-types.md)

埋め込まれた相互運用機能型は、展開の問題を緩和しました。 ジェネリックの共変性と反変性は、ジェネリックを使用する権限を強化しますが、少々アカデミックで、最も高く評価されているのは、おそらくフレームワークとライブラリの作成者からでしょう。 名前付きパラメーターと省略可能なパラメーターは、多くのメソッドのオーバーロードを排除して、利便性を高めることができます。 しかし、これらの機能はいずれもパラダイムを変えるほどのものではありませんでした。

主要な機能は、`dynamic` キーワードの導入でした。 C# バージョン 4.0 で導入された `dynamic` キーワードにより、コンパイル時の型指定でコンパイラをオーバーライドできるようになりました。 dynamic キーワードを使用することで、JavaScript のような動的に型指定された言語と同様のコンストラクトを作成することができます。 `dynamic x = "a string"` を作成してから、それに 6 を追加して、実行時までそのままにして次に発生する必要のあることを整理することができます。

動的バインドには潜在的なエラーの可能性がありますが、同時に、この言語が持つ大きな力にもなっています。

## <a name="c-version-50"></a>C# バージョン 5.0

Visual Studio 2012 でリリースされた C# バージョン 5.0 は、この言語の専心的なバージョンでした。 このバージョンに対するほぼすべての努力が、非同期プログラミングの `async` および `await` モデルというもう一つの革新的な言語の概念に注がれました。  主要な機能の一覧を次に示します。

- [非同期メンバー](../async.md)
- [呼び出し元情報属性](../language-reference/attributes/caller-information.md)

### <a name="see-also"></a>関連項目

- [コード プロジェクト:C# 5.0 の呼び出し元情報属性](https://www.codeproject.com/Tips/606379/Caller-Info-Attributes-in-Csharp)

呼び出し元情報属性を使用すると、さまざまな定型リフレクション コードを使用しなくても、実行しているコンテキストに関する情報を簡単に取得できます。 診断とログ記録のタスクでは、さまざまな用途があります。

しかしこのリリースの真の主役は、`async` と `await` です。 2012 年にこれらの機能が登場したとき、C# はファーストクラスの一部として非同期を言語に採用したことで再び流れを変えました。 これまでに、長時間実行される操作とコールバックの Web の実装に対処したことがあれば、おそらくこの言語機能を気に入っているでしょう。

## <a name="c-version-60"></a>C# バージョン 6.0

C# バージョン 3.0 と 5.0 では、主要な新機能がオブジェクト指向言語に追加されました。 Visual Studio 2015 と共にリリースされたバージョン 6.0 では、主要な目玉機能を投入する代わりに、C# プログラミングをより生産的にする多くの小さな機能をリリースしました。 その一部を次に示します。

- [静的インポート](./csharp-6.md#using-static)
- [例外フィルター](./csharp-6.md#exception-filters)
- [自動プロパティ初期化子](./csharp-6.md#auto-property-initializers)
- [式形式のメンバー](./csharp-6.md#expression-bodied-function-members)
- [Null 伝達子](./csharp-6.md#null-conditional-operators)
- [文字列補間](./csharp-6.md#string-interpolation)
- [nameof 演算子](./csharp-6.md#the-nameof-expression)
- [インデックス初期化子](csharp-6.md#extension-add-methods-in-collection-initializers)

その他に次の新機能があります。

- Catch/Finally ブロックでの Await
- ゲッターのみのプロパティの既定値

これらの機能は、単独でも興味深い機能ですが、 全体として見てみると、興味深いパターンが見えます。 このバージョンで、コードをより簡潔で読みやすくするため、C# から定型表現が排除されました。 そのため、クリーンで単純なコードが好きな人に、この言語バージョンは大当たりしました。

マイクロソフトはこのバージョンとともにもう 1 つ別のことを行いましたが、それ自体が従来の言語機能ではありませんでした。 [サービスとしてのコンパイラ Roslyn](https://github.com/dotnet/roslyn) をリリースしたのです。 C# コンパイラは現在、C# で記述され、プログラミングのための取り組みの一環として、コンパイラを使用することができます。

## <a name="c-version-70"></a>C# バージョン 7.0

C# バージョン 7.0 は、Visual Studio 2017 でリリースされました。 このバージョンには、C# 6.0 から続くいくつかの革新的で優れた機能がありますが、サービスとしてのコンパイラはありません。 新機能の一部を次に示します。

- [out 変数](./csharp-7.md#out-variables)
- [タプルと分解](./csharp-7.md#tuples)
- [パターン マッチング](./csharp-7.md#pattern-matching)
- [ローカル関数](./csharp-7.md#local-functions)
- [拡張された式形式のメンバー](./csharp-7.md#more-expression-bodied-members)
- [ref ローカル変数と戻り値](./csharp-7.md#ref-locals-and-returns)

その他の機能:

- [破棄](./csharp-7.md#discards)
- [バイナリ リテラルと桁区切り文字](./csharp-7.md#numeric-literal-syntax-improvements)
- [throw 式](./csharp-7.md#throw-expressions)

これらすべての機能が素晴らしい新機能を開発者に提供し、これまでよりもさらにクリーンなコードを記述する機会を提供します。 ハイライトは、`out` キーワードで使用するために変数の宣言を凝縮することと、タプルを通じて複数の戻り値を許可することです。

しかし C# はさらに広範に使用されています。 .NET Core は現在、任意のオペレーティング システムを対象としており、クラウドと移植性をしっかりと見据えています。  この言語の設計者たちは、新機能を考え出すことに加え、こうした新たな能力についても多くの思考と時間を費やしています。

## <a name="c-version-71"></a>C# バージョン 7.1

C# は、C#7.1 で "*ポイント リリース*" のリリースを開始しました。 このバージョンでは、[言語バージョン選択](../language-reference/configure-language-version.md)構成要素、3 つの新しい言語機能、新しいコンパイラ動作が追加されます。

このリリースの新しい言語機能は次のとおりです。

- [`async` `Main`メソッド](./csharp-7-1.md#async-main)
  - アプリケーションのエントリ ポイントに `async` 修飾子を設定できます。
- [`default` リテラル式](./csharp-7-1.md#default-literal-expressions)
  - ターゲットの種類を推論できるとき、既定の値式で既定のリテラル式を使用できます。
- [推論されたタプル要素の名前](./csharp-7-1.md#inferred-tuple-element-names)
  - タプル要素の名前は、多くの場合、タプル初期化から推論できます。
- [ジェネリック型パラメーターのパターン マッチ](./csharp-7-1.md#pattern-matching-on-generic-type-parameters)
  - 型がジェネリック型パラメーターである変数にパターン マッチ式を使用できます。

最後に、コンパイラには、[参照アセンブリ生成](./csharp-7-1.md#reference-assembly-generation)を制御する 2 つのオプション、`-refout` と `-refonly` があります。

## <a name="c-version-72"></a>C# バージョン 7.2

C# 7.2 では、いくつかの小規模な言語機能が追加されました。

- [安全で効率的なコードを記述するための手法](./csharp-7-2.md#safe-efficient-code-enhancements)
  - 参照セマンティクスを使用したさまざまな値の型の使用を有効にする、構文の機能強化の組み合わせ。
- [末尾以外の名前付き引数](./csharp-7-2.md#non-trailing-named-arguments)
  - 名前付き引数の後ろに位置引数を続けることができます。
- [数値リテラルでの先頭のアンダースコア (_)](./csharp-7-2.md#leading-underscores-in-numeric-literals)
  - 数値リテラルの印刷桁の前に先頭のアンダースコア(_) を含めることができるようになりました。
- [`private protected` アクセス修飾子](./csharp-7-2.md#private-protected-access-modifier)
  - `private protected` アクセス修飾子によって、同じアセンブリ内の派生クラスのアクセスが有効になります。
- [条件付きの `ref` 式](./csharp-7-2.md#conditional-ref-expressions)
  - 条件式 (`?:`) の結果を参照にすることができるようになりました。

## <a name="c-version-73"></a>C# バージョン 7.3

C# 7.3 リリースには 2 つの主要なテーマがあります。 1 つ目のテーマは、アンセーフ コードと同様のパフォーマンスをセーフ コードで確保するための機能の提供です。 2 つ目のテーマは、既存の機能のインクリメンタルな改善の提供です。 また、新しいコンパイラ オプションがこのリリースで追加されました。

次の新機能は、セーフ コードのパフォーマンス向上のテーマをサポートします。

- [ピン留めを使用せずに fixed フィールドにアクセスできます。](csharp-7-3.md#indexing-fixed-fields-does-not-require-pinning)
- [`ref` ローカル変数を再割り当てできます。](csharp-7-3.md#ref-local-variables-may-be-reassigned)
- [`stackalloc` 配列で初期化子を使用できます。](csharp-7-3.md#stackalloc-arrays-support-initializers)
- [パターンをサポートする型と共に `fixed` ステートメントを使用できます。](csharp-7-3.md#more-types-support-the-fixed-statement)
- [追加のジェネリック制約を使用できます。](csharp-7-3.md#enhanced-generic-constraints)

既存の機能が次のように強化されました。

- [タプル型を使用して `==` と `!=` をテストできます。](csharp-7-3.md#tuples-support--and-)
- [式の変数をより多くの場所で使用できます。](csharp-7-3.md#extend-expression-variables-in-initializers)
- [自動実装プロパティのバッキング フィールドに属性をアタッチできます。](csharp-7-3.md#attach-attributes-to-the-backing-fields-for-auto-implemented-properties)
- [引数が `in` によって異なる場合のメソッド解決が改善されました。](csharp-7-3.md#in-method-overload-resolution-tiebreaker)
- [オーバーロードの解決のあいまいなケースが削減されました。](csharp-7-3.md#improved-overload-candidates)

新しいコンパイラ オプションは次のとおりです。

- [`-publicsign`: オープン ソース ソフトウェア (OSS) のアセンブリの署名を可能にします。](csharp-7-3.md#public-or-open-source-signing)
- [`-pathmap`: ソース ディレクトリのマッピングを提供します。](csharp-7-3.md#pathmap)

## <a name="c-version-80"></a>C# バージョン 8.0

C# 8.0 は、特に C# .NET Core をターゲットとする最初のメジャー リリースです。 新しい CLR 機能に依存する機能と、.NET Core にのみ追加されたライブラリの型に依存する機能があります。 C# 8.0 では、C# 言語に次の機能と機能強化が追加されています。

- [読み取り専用メンバー](./csharp-8.md#readonly-members)
- [既定のインターフェイス メソッド](./csharp-8.md#default-interface-methods)
- [パターン マッチングの拡張機能](./csharp-8.md#more-patterns-in-more-places):
  - [switch 式](./csharp-8.md#switch-expressions)
  - [プロパティのパターン](./csharp-8.md#property-patterns)
  - [タプル パターン](./csharp-8.md#tuple-patterns)
  - [位置指定パターン](./csharp-8.md#positional-patterns)
- [using 宣言](./csharp-8.md#using-declarations)
- [静的ローカル関数](./csharp-8.md#static-local-functions)
- [破棄可能な ref 構造体](./csharp-8.md#disposable-ref-structs)
- [Null 許容参照型](../language-reference/builtin-types/nullable-reference-types.md)
- [非同期ストリーム](./csharp-8.md#asynchronous-streams)
- [インデックスと範囲](./csharp-8.md#indices-and-ranges)
- [null 合体割り当て](./csharp-8.md#null-coalescing-assignment)
- [構築されたアンマネージド型](./csharp-8.md#unmanaged-constructed-types)
- [入れ子になった式の stackalloc](./csharp-8.md#stackalloc-in-nested-expressions)
- [verbatim 補間文字列の拡張](./csharp-8.md#enhancement-of-interpolated-verbatim-strings)

既定のインターフェイス メンバーには、CLR の拡張機能が必要です。 これらの機能は、CLR for .NET Core 3.0 で追加されました。 範囲とインデックス、および非同期ストリームには、.NET Core 3.0 ライブラリの新しい型が必要です。 null 許容参照型は、コンパイラに実装されていますが、引数と戻り値の null 状態に関するセマンティック情報を提供する注釈がライブラリに付けられている場合に非常に役立ちます。 このような注釈は .NET Core ライブラリに追加されています。

_記事_は、[_NDepend ブログで元々公開されていたものです_](https://blog.ndepend.com/c-versions-look-language-history/) _(提供: Erik Dietrich および Patrick Smacchia)。_
