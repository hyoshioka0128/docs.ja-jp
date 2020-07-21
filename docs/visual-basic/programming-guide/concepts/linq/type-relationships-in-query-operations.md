---
title: クエリ操作での型の関係
ms.date: 07/20/2015
helpviewer_keywords:
- variable relationships [LINQ in Visual Basic]
- type information inferred [LINQ in Visual Basic]
- type relationships [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], type relationships
- data sources [LINQ in Visual Basic], type relationships
- LINQ [Visual Basic], type relationships
- inferring type information [LINQ in Visual Basic]
- relationships [LINQ in Visual Basic]
ms.assetid: b5ff4da5-f3fd-4a8e-aaac-1cbf52fa16f6
ms.openlocfilehash: 73a287541ddf115510bf6ab5c830eafac370cc3a
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406730"
---
# <a name="type-relationships-in-query-operations-visual-basic"></a>クエリ操作での型の関係 (Visual Basic)

統合言語クエリ (LINQ) のクエリ操作で使用される変数は厳密に型指定されており、互いに互換性がなければなりません。 厳密な型指定は、データ ソースで使用されるほか、クエリそのものや、クエリの実行でも使用されます。 次の図は、LINQ クエリの説明で用いられる用語を示したものです。 クエリの構成要素について詳しくは、「[基本的なクエリ操作 (Visual Basic)](basic-query-operations.md)」を参照してください。

![要素が強調表示された擬似コード クエリを示すスクリーンショット](./media/type-relationships-in-query-operations/linq-query-description-terms.png)

クエリの範囲変数の型には、データ ソース内の要素の型との互換性が必要です。 クエリ変数の型は、`Select` 句で定義されているシーケンス要素と互換性がある必要があります。 最後に、シーケンス要素の型も、クエリを実行する `For Each` ステートメントで使用されるループ制御変数の型と互換性がある必要があります。 この厳密な型指定によって、コンパイル時に発生する型エラーが特定しやすくなります。

Visual Basic は、ローカル型推論 ("*暗黙の型指定*" とも呼ばれます) を実装することで、厳密な型指定の利便性を高めています。 その機能は、前の例で使用されているほか、LINQ のサンプルやドキュメントの至る所で目にすることができます。 Visual Basic では、単に `As` 句のない `Dim` ステートメントを使用すれば、ローカル型推論が行われます。 次の例の `city` は、文字列として厳密に型指定されます。

[!code-vb[VbLINQTypeRels#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#1)]

> [!NOTE]
> ローカル型推論が機能するのは、`Option Infer` が `On` に設定されているときだけです。 詳細については、「[Option Infer ステートメント](../../../language-reference/statements/option-infer-statement.md)」を参照してください。

ただし、クエリでローカル型推論を使用した場合でも、データ ソース内の変数、クエリ変数、クエリの実行ループの間に存在する型の関係は同じです。 こうした型の関係についての基本的な知識は、LINQ クエリを記述するときや、ドキュメント内のサンプルまたはコード例を扱うときに役立ちます。

データ ソースから返された型と一致しない範囲変数には、明示的な型の指定が必要になる場合もあります。 範囲変数の型は、`As` 句を使用して指定できます。 ただし、変換が[縮小変換](../../language-features/data-types/widening-and-narrowing-conversions.md)で、なおかつ `Option Strict` が `On` に設定されているとエラーになります。 したがって変換は、データ ソースから取得された値に対して実行することをお勧めします。 <xref:System.Linq.Enumerable.Cast%2A> メソッドを使用すると、データ ソースから取得された値を、明示的な範囲変数の型に変換することができます。 また、`Select` 句で選択した値を、範囲変数の型とは異なる明示的な型にキャストすることもできます。 以上の点については、次のコードで説明しています。

[!code-vb[VbLINQTypeRels#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#4)]

## <a name="queries-that-return-entire-elements-of-the-source-data"></a>ソース データの要素全体を返すクエリ

次の例は、ソース データから選択された要素のシーケンスを返す LINQ クエリ操作を示しています。 ソース (`names`) には、文字列の配列が格納されます。アルファベットの M で始まる文字列を含んだシーケンスがクエリの出力となります。

[!code-vb[VbLINQTypeRels#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#2)]

次のコードに相当しますが、こちらの方がはるかに短く、記述しやすくなっています。 Visual Basic では、クエリにローカル型推論を使うのが、推奨されるスタイルです。

[!code-vb[VbLINQTypeRels#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQTypeRels/VB/Class1.vb#3)]

型の指定が暗黙的であれ明示的であれ、前出のコード例には、どちらも次の関係が存在します。

1. データ ソース (`names`) に含まれる要素の型は、クエリの範囲変数 (`name`) の型です。

2. 選択したオブジェクト (`name`) の型によって、クエリ変数 (`mNames`) の型が決まります。 ここでは `name` が文字列であるため、クエリ変数は Visual Basic の IEnumerable(Of String) となります。

3. `mNames` で定義されたクエリは、`For Each` ループで実行されます。 このループによって、クエリの実行結果が反復処理されます。 `mNames` は、実行されたときに文字列のシーケンスを返すため、ループの反復変数 (`nm`) も文字列になります。

## <a name="queries-that-return-one-field-from-selected-elements"></a>選択された要素から 1 つのフィールドを返すクエリ

次の例は、データ ソースから選択された各要素の一部分のみを含んだシーケンスを返す [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] クエリ操作を示しています。 このクエリは、`Customer` オブジェクトのコレクションをそのデータ ソースとして受け取って、`Name` プロパティのみを結果に投影します。 顧客名は文字列なので、クエリは出力として文字列のシーケンスを作成します。

```vb
' Method GetTable returns a table of Customer objects.
Dim customers = db.GetTable(Of Customer)()
Dim custNames = From cust In customers
                Where cust.City = "London"
                Select cust.Name

For Each custName In custNames
    Console.WriteLine(custName)
Next
```

単純な方の例と同様、変数間の関係は次のようになります。

1. データ ソース (`customers`) に含まれる要素の型は、クエリの範囲変数 (`cust`) の型です。 この例では、`Customer` 型が該当します。

2. `Select` ステートメントから返されるのは、オブジェクト全体ではなく、各 `Customer` オブジェクトの `Name` プロパティです。 `Name` は文字列であるため、この場合もクエリ変数 (`custNames`) は IEnumerable(Of String) であって、`Customer` ではありません。

3. `custNames` は文字列のシーケンスを表すので、`For Each` ループの反復変数 (`custName`) も文字列である必要があります。

ローカル型推論がなければ、前出の例は、もっと書きづらく、また理解しにくいものになるでしょう。その例を次に示します。

```vb
' Method GetTable returns a table of Customer objects.
 Dim customers As Table(Of Customer) = db.GetTable(Of Customer)()
 Dim custNames As IEnumerable(Of String) =
     From cust As Customer In customers
     Where cust.City = "London"
     Select cust.Name

 For Each custName As String In custNames
     Console.WriteLine(custName)
 Next
```

## <a name="queries-that-require-anonymous-types"></a>匿名型を必要とするクエリ

次に示したのは、より複雑な状況の例です。 前の例では、すべての変数に対して明示的に型を指定するのは、容易ではありませんでした。 この例では、それが不可能となります。 このクエリの `Select` 句は、データ ソースから `Customer` 要素全体を選択したり、各要素から 1 つのフィールドだけを選択したりするのではなく、元の `Customer` オブジェクトから `Name` と `City` の 2 つのプロパティを返します。 `Select` 句に対する応答として、それら 2 つのプロパティを含んだ匿名型がコンパイラによって定義されます。 `For Each` ループで `nameCityQuery` を実行した結果は、新しい匿名型のインスタンスのコレクションです。 匿名型には有効な名前がないため、`nameCityQuery` と `custInfo` の型を明示的に指定することができません。 つまり、匿名型では、`IEnumerable(Of String)` の `String` の代わりに使用できる型名がないのです。 詳細については、「[匿名型](../../language-features/objects-and-classes/anonymous-types.md)」を参照してください。

```vb
' Method GetTable returns a table of Customer objects.
Dim customers = db.GetTable(Of Customer)()
Dim nameCityQuery = From cust In customers
                    Where cust.City = "London"
                    Select cust.Name, cust.City

For Each custInfo In nameCityQuery
    Console.WriteLine(custInfo.Name)
Next
```

前の例のすべての変数に型を指定することはできませんが、その関係は変わりません。

1. この場合も、データ ソースに含まれる要素の型は、クエリの範囲変数の型です。 この例の `cust` は、`Customer` のインスタンスです。

2. `Select` ステートメントによって匿名型が生成されるため、クエリ変数 (`nameCityQuery`) は、匿名型として暗黙的に型指定する必要があります。 匿名型は、有効な名前を持たないため、明示的に指定することはできません。

3. `For Each` ループにおける反復変数の型は、手順 2. で作成した匿名型です。 この型には有効な名前がないため、ループの反復変数の型は、必然的に暗黙的に指定されます。

## <a name="see-also"></a>関連項目

- [Visual Basic の LINQ の概要](getting-started-with-linq.md)
- [匿名型](../../language-features/objects-and-classes/anonymous-types.md)
- [ローカル型の推論](../../language-features/variables/local-type-inference.md)
- [Visual Basic における LINQ の概要](../../language-features/linq/introduction-to-linq.md)
- [LINQ](../../language-features/linq/index.md)
- [クエリ](../../../language-reference/queries/index.md)
