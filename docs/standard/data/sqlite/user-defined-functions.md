---
title: ユーザー定義関数
ms.date: 12/13/2019
description: ユーザー定義のスカラー関数と集計関数を作成する方法について説明します。
ms.openlocfilehash: 9ee3fbac73215353c8dc82199203b0d25e580cdb
ms.sourcegitcommit: 30a558d23e3ac5a52071121a52c305c85fe15726
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75450412"
---
# <a name="user-defined-functions"></a>ユーザー定義関数

ほとんどのデータベースには、独自の関数の定義に使用できる SQL 手続き型言語が用意されています。 ただし、SQLite はアプリのインプロセスで実行されます。 新しい SQL 言語を習得する代わりに、アプリのプログラミング言語を使用するだけで済みます。

## <a name="scalar-functions"></a>スカラー関数

スカラー関数では、クエリ内の行ごとに 1 つのスカラー値が返されます。 <xref:Microsoft.Data.Sqlite.SqliteConnection.CreateFunction%2A> を使用して、新しいスカラー関数を定義し、組み込みの関数をオーバーライドします。

`func` 引数でサポートされているパラメーターと戻り値の型の一覧については、「[データ型](types.md)」を参照してください。

`state` 引数を指定すると、その値が関数のすべての呼び出しに渡されます。 クロージャを避ける場合は、これを使用します。

関数が決定的である場合、クエリのコンパイル時に SQLite で追加の最適化を使用できるようにするには、`isDeterministic` を指定します。

次の例では、円柱の半径を計算するスカラー関数を追加する方法を示します。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/ScalarFunctionSample/Program.cs?name=snippet_CreateFunction)]

## <a name="operators"></a>演算子

次の SQLite 演算子は、対応するスカラー関数によって実装されます。 これらのスカラー関数をアプリで定義すると、これらの演算子の動作がオーバーライドされます。

| 演算子          | 関数      |
| ----------------- | ------------- |
| X GLOB Y          | glob(Y, X)    |
| X LIKE Y          | like(Y, X)    |
| X LIKE Y ESCAPE Z | like(Y, X, Z) |
| X MATCH Y         | match(Y, X)   |
| X REGEXP Y        | regexp(Y, X)  |

次の例では、regexp 関数を定義して、それに対応する演算子を使用できるようにする方法を示します。 SQLite には、regexp 関数の既定の実装は含まれていません。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/RegularExpressionSample/Program.cs?name=snippet_Regex)]

## <a name="aggregate-functions"></a>集計関数

集計関数では、クエリ内のすべての行に対して 1 つの集計値が返されます。 集計関数は <xref:Microsoft.Data.Sqlite.SqliteConnection.CreateAggregate%2A> を使用して定義およびオーバーライドします。

`seed` 引数は、コンテキストの初期状態を指定します。 これは、クロージャを避ける場合にも使用します。

`func` 引数は、行ごとに 1 回だけ呼び出します。 コンテキストを使用して、最終的な結果を累積します。 コンテキストを返します。 このパターンでは、コンテキストを値の型または変更不可にすることができます。

`resultSelector` が指定されていない場合、コンテキストの最終的な状態が結果として使用されます。 これにより、sum や count などの関数の定義を単純化でき、行ごとに数値をインクリメントして返すだけで済むようになります。

すべての行を反復処理した後でコンテキストから最終的な結果を計算するには、`resultSelector` を指定します。

`resultSelector` の `func` 引数と戻り値の型でサポートされているパラメーターの型の一覧については、「[データ型](types.md)」を参照してください。

関数が決定的である場合、クエリのコンパイル時に SQLite で追加の最適化を使用できるようにするには、`isDeterministic` を指定します。

次の例では、列の標準偏差を計算する集計関数を定義します。

[!code-csharp[](../../../../samples/snippets/standard/data/sqlite/AggregateFunctionSample/Program.cs?name=snippet_CreateAggregate)]

## <a name="errors"></a>エラー

ユーザー定義関数で例外がスローされた場合、メッセージが SQLite に返されます。 SQLite によってエラーが生成され、Microsoft.Data.Sqlite によって SqliteException がスローされます。 詳細については、「[データベース エラー](database-errors.md)」を参照してください。

既定では、エラーの SQLite エラー コードは SQLITE_ERROR (または 1) になります。 ただしこれは、目的の <xref:Microsoft.Data.Sqlite.SqliteException.SqliteErrorCode> を指定して関数内で <xref:Microsoft.Data.Sqlite.SqliteException> をスローすることによって変更できます。

## <a name="debugging"></a>デバッグ

SQLite では、実装が直接呼び出されます。 これにより、SQLite でクエリが評価されている間にトリガーされるブレークポイントを追加できます。 ユーザー定義関数の作成に役立つ、.NET の一連のデバッグ機能を利用できます。

## <a name="see-also"></a>関連項目

* [データ型](types.md)
* [SQLite コア関数](https://www.sqlite.org/lang_corefunc.html)
* [SQLite 集計関数](https://www.sqlite.org/lang_aggfunc.html)
