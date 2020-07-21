---
title: 初めての LINQ クエリの作成
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ queries [Visual Basic]
- LINQ [Visual Basic], writing queries
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
ms.openlocfilehash: 9d85f9c0390a659e59e372ad949cffdd17715189
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84413259"
---
# <a name="writing-your-first-linq-query-visual-basic"></a>初めての LINQ クエリの作成 (Visual Basic)
"*クエリ*" は、データ ソースからデータを取得する式です。 クエリは、専用のクエリ言語で表されます。 これまでに、リレーショナル データベース用の SQL や XML 用の XQuery など、各種データ ソースに合わせてさまざまな言語が開発されてきました。 このため、アプリケーション開発者は、サポートするデータ ソースの種類やデータ形式ごとに、新しいクエリ言語を習得する必要がありました。  
  
 統合言語クエリ (LINQ) は、さまざまな種類のデータ ソースやデータ形式のデータを操作するための一貫したモデルを提供することにより、この負担を軽減します。 LINQ クエリでは、操作の対象は常にオブジェクトになります。 共通の基本的なコーディング パターンを使用することで、XML ドキュメント、SQL データベース、ADO.NET データセットおよびエンティティ、.NET Framework のコレクションなど、LINQ プロバイダーを利用できるあらゆるソースまたは形式のデータを照会したり変換したりすることができます。 このドキュメントでは、基本的な LINQ クエリの作成と使用の 3 つのフェーズについて説明しています。  
  
## <a name="three-stages-of-a-query-operation"></a>クエリ操作の 3 つのステージ  
 LINQ クエリ操作はすべて、次の 3 つのアクションで構成されます。  
  
1. データ ソースまたはソースを取得します。  
  
2. クエリを作成します。  
  
3. クエリを実行します。  
  
 LINQ では、クエリの実行とクエリの作成が区別されます。 クエリを作成するだけでは、データは取得されません。 この点については、後で詳しく説明します。  
  
 以下の例は、クエリ操作を構成する 3 つの要素を示しています。 この例では、デモンストレーション用に便利なデータ ソースとして整数の配列を使用しています。 ただし同じ概念は、他のデータ ソースにも当てはまります。  
  
> [!NOTE]
> [プロジェクト デザイナー (Visual Basic) の [コンパイル] ページ](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)で、 **[Option infer]** が **[On]** に設定されていることを確認します。  
  
 [!code-vb[VbLINQFirstQuery#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#1)]  
  
 Output:  
  
 `0 2 4 6`  
  
## <a name="the-data-source"></a>データ ソース  
 前の例では、データ ソースが配列であるため、暗黙的にジェネリック <xref:System.Collections.Generic.IEnumerable%601> インターフェイスがサポートされます。 配列を LINQ クエリのデータ ソースとして使用できるのは、そのためです。 <xref:System.Collections.Generic.IEnumerable%601> をサポートする型や、ジェネリック <xref:System.Linq.IQueryable%601> などの派生インターフェイスは、*クエリ可能型*と呼ばれます。  
  
 配列は、暗黙的なクエリ可能型として、変更や特別な処理を行わなくても、LINQ データ ソースとして使用できます。 同じことは、ジェネリックである <xref:System.Collections.Generic.List%601> や <xref:System.Collections.Generic.Dictionary%602>、その他 .NET Framework クラス ライブラリのクラスなど、<xref:System.Collections.Generic.IEnumerable%601> をサポートするすべてのコレクション型に言えます。  
  
 ソース データにまだ <xref:System.Collections.Generic.IEnumerable%601> が実装されていない場合、そのデータ ソースに "*標準クエリ演算子*" の機能を実装するためには、LINQ プロバイダーが必要となります。 たとえば、[!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] は、XML ドキュメントを、クエリ可能な <xref:System.Xml.Linq.XElement> 型に読み込む処理を担います (以下の例を参照)。 標準クエリ演算子について詳しくは、「[標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)」を参照してください。  
  
 [!code-vb[VbLINQFirstQuery#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#2)]  
  
 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] では、まず、デザイン時に手動で、または Visual Studioで [Visual Studio の LINQ to SQL ツール](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)を使用して、オブジェクト リレーショナル マッピングを作成します。 オブジェクトに対するクエリを記述すると、実行時には、[!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)] によってデータベースとの通信が処理されます。 次の例の `customers` は、データベース内の特定のテーブルを表し、<xref:System.Data.Linq.Table%601> はジェネリックの <xref:System.Linq.IQueryable%601> をサポートします。  
  
```vb  
' Create a data source from a SQL table.  
Dim db As New DataContext("C:\Northwind\Northwnd.mdf")  
Dim customers As Table(Of Customer) = db.GetTable(Of Customer)  
```  
  
 それぞれの種類のデータ ソースを作成する方法の詳細については、対応する LINQ プロバイダーのドキュメントを参照してください。 (該当するプロバイダーの一覧については、[LINQ (統合言語クエリ)](index.md) に関するページを参照してください)。基本的な規則は単純です。LINQ データ ソースは、ジェネリック <xref:System.Collections.Generic.IEnumerable%601> インターフェイスか、これを継承するインターフェイスをサポートする任意のオブジェクトです。  
  
> [!NOTE]
> 非ジェネリック <xref:System.Collections.IEnumerable> インターフェイスをサポートする <xref:System.Collections.ArrayList> などの型も、LINQ データ ソースとして使用できます。 <xref:System.Collections.ArrayList> の使用例については、「[方法: LINQ を使用して ArrayList を照会する (Visual Basic)](how-to-query-an-arraylist-with-linq.md)」を参照してください。  
  
## <a name="the-query"></a>クエリ  
 クエリには、データ ソースまたはソースから取得したい情報を指定します。 また、どのように情報を並べ替え、グループ化、または構造化して返されるようにするかをオプションで指定することもできます。 Visual Basic 言語には、クエリの作成に対応するために、新しいクエリ構文が導入されています。  
  
 次の例のクエリを実行すると、整数の配列 `numbers` からすべての偶数が返されます。  
  
 [!code-vb[VbLINQFirstQuery#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#1)]  
  
 このクエリ式には、`From`、`Where`、`Select` の 3 つの句が含まれています。 クエリ式の各句の具体的な関数と目的は、「[基本的なクエリ操作 (Visual Basic)](basic-query-operations.md)」で説明しています。 詳細については、「[クエリ](../../../language-reference/queries/index.md)」を参照してください。 LINQ では多くの場合、クエリの定義はまず変数に格納され、その後実行されます。 前の例の `evensQuery` のように、クエリ変数はクエリ可能型であることが必要です。 `evensQuery` の型は `IEnumerable(Of Integer)` で、コンパイラによってローカル型推論を使用して割り当てられます。  
  
 クエリ変数自体は何も処理を行わず、データを返さないという点に注意してください。 あくまでクエリの定義が格納されるだけです。 前の例で、クエリを実行するのは `For Each` ループです。  
  
## <a name="query-execution"></a>クエリの実行  
 クエリの実行とクエリの作成は分離しています。 クエリを作成することによってクエリは定義されますが、その実行をトリガーするのは別のメカニズムになります。 クエリは、定義後すぐに実行 ("*即時実行*)" することも、定義を保存しておき、後でクエリを実行 ("*遅延実行*") することもできます。  
  
### <a name="deferred-execution"></a>遅延実行  
 一般的な LINQ クエリは、前の例のようなものです。前の例には `evensQuery` が定義されています。 クエリは作成されても、すぐには実行されません。 その代わりに、クエリ変数 `evensQuery` にクエリの定義が格納されます。 通常は、一連の値を返す `For Each` ループを使用するか、標準クエリ演算子 (`Count`、`Max` など) を適用することによって、クエリを後から実行することになります。 この処理を "*遅延実行*" と呼びます。  
  
 [!code-vb[VbLINQFirstQuery#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#7)]  
  
 一連の値を得るには、`For Each` ループの反復変数 (前の例では `number`) を使用して、取得したデータにアクセスします。 クエリ変数 `evensQuery` が保持するのはクエリの結果ではなくクエリの定義であるため、繰り返しクエリ変数を使用することで、必要に応じて何度でもクエリを実行できます。 たとえばアプリケーションに使用しているデータベースが、別のアプリケーションによって絶えず更新されているとします。 データベースからデータを取得するクエリを作成しておき、`For Each` ループを使用して繰り返しクエリを実行すれば、毎回最新のデータを取得できます。  
  
 以下の例は、遅延実行の動作を示したものです。 まず、前の例のように `evensQuery2` を定義し、`For Each` ループで実行した後、データ ソース `numbers` 内のいくつかの要素に変更を加えています。 その後、2 つ目の `For Each` ループで `evensQuery2` を再実行します。 `For Each` ループでクエリを再実行するときは、`numbers` 内の新しい値が使用されるため、2 回目は異なる結果が得られます。  
  
 [!code-vb[VbLINQFirstQuery#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#3)]  
  
 Output:  
  
 `Evens in original array:`  
  
 `0  2  4  6`  
  
 `Evens in changed array:`  
  
 `0  10  2  22  8`  
  
### <a name="immediate-execution"></a>即時実行  
 クエリの遅延実行では、クエリの定義がクエリ変数に格納され、後から実行されます。 即時実行では、クエリがその定義時に実行されます。 クエリ結果の個々の要素にアクセスする必要があるメソッドを適用したときに、実行がトリガーされます。 即時実行は多くの場合、単一の値を返すいずれかの標準クエリ演算子を使用することで強制的に発生します。 たとえば、`Count`、`Max`、`Average`、`First` が該当します。 これらの標準クエリ演算子では、シングルトンの結果を算出して返すために、適用された時点ですぐにクエリが実行されます。 単一の値を返す標準クエリ演算子の詳細については、「[集計操作](aggregation-operations.md)」、「[要素の操作](element-operations.md)」、「[量指定子操作](quantifier-operations.md)」を参照してください。  
  
 次のクエリからは、整数の配列に格納されている偶数の数が返されます。 クエリの定義は保存されません。`numEvens` は単純な `Integer` です。  
  
 [!code-vb[VbLINQFirstQuery#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#4)]  
  
 同じ結果は、`Aggregate` メソッドを使用して取得することもできます。  
  
 [!code-vb[VbLINQFirstQuery#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#5)]  
  
 次のコードに示すとおり、クエリ (即時) またはクエリ変数 (遅延) の `ToList` メソッドまたは `ToArray` メソッドを呼び出すことによって、クエリの実行を強制することもできます。  
  
 [!code-vb[VbLINQFirstQuery#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQFirstQuery/VB/Class1.vb#6)]  
  
 前の例で、`evensQuery3` はクエリ変数ですが、`evensList` はリストで、`evensArray` は配列です。  
  
 `ToList` または `ToArray` を使用して即時実行を強制する手法は、クエリを直ちに実行してその結果を単一のコレクション オブジェクトにキャッシュしておくようなシナリオで特に便利です。 これらのメソッドの詳細については、「[データ型の変換](converting-data-types.md)」を参照してください。  
  
 また、`IEnumerable` メソッド (<xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A> メソッドなど) を使用してクエリの実行を生じさせることもできます。  
  
## <a name="see-also"></a>関連項目

- [Visual Basic の LINQ の概要](getting-started-with-linq.md)
- [ローカル型の推論](../../language-features/variables/local-type-inference.md)
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [Visual Basic における LINQ の概要](../../language-features/linq/introduction-to-linq.md)
- [LINQ](../../language-features/linq/index.md)
- [クエリ](../../../language-reference/queries/index.md)
