---
title: LINQ の概要
ms.date: 08/28/2018
helpviewer_keywords:
- queries [LINQ in Visual Basic], about LINQ in Visual Basic queries
- query execution [LINQ in Visual Basic]
- range variables [Visual Basic]
- LINQ [Visual Basic]
- LINQ [Visual Basic], about LINQ in Visual Basic
- query expressions [LINQ in Visual Basic]
- LINQ
- deferred execution
- iteration variables [Visual Basic]
ms.assetid: 3047d86e-0d49-40e2-928b-dc02e46c7984
ms.openlocfilehash: 273c688d7e9d3fb86d4baece75193ce6d112b62f
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404915"
---
# <a name="introduction-to-linq-in-visual-basic"></a>Visual Basic における LINQ の概要
統合言語クエリ (LINQ) は、Visual Basic にクエリ機能を追加します。この単純かつ強力な機能を使用して、あらゆる種類のデータを操作できます。 処理の対象であるデータベースにクエリを送信したり、検索するデータの種類ごとに異なるクエリ構文を使用したりする代わりに、LINQ では、Visual Basic 言語の一部としてのクエリを採用しています。 LINQ では、データの型に関係なく、統一された構文を使用します。  
  
 LINQ を使用すると、SQL Server データベース、XML、インメモリ配列、インメモリ コレクション、ADO.NET データセットなど、LINQ をサポートするリモートまたはローカルのデータ ソースのデータに対してクエリを実行できます。 これらはすべて、共通 Visual Basic 言語要素を使用して実行できます。 クエリは Visual Basic 言語で記述されるので、クエリ結果は、厳密に型指定されたオブジェクトとして返されます。 これらのオブジェクトは IntelliSense をサポートするので、コードの記述時間を短縮でき、さらに、クエリに含まれるエラーを実行時ではなくコンパイル時に把握できます。 LINQ クエリは、結果を絞り込むための追加クエリのソースとして使用できます。 クエリ結果をユーザーが簡単に表示および変更できるように、コントロールにバインディングすることもできます。  
  
 たとえば、次のコード例は、コレクションから顧客リストを返し、住所に基づいて顧客をグループ化する LINQ クエリを示しています。  
  
 [!code-vb[VbVbalrIntroToLINQ#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#1)]  
  
## <a name="running-the-examples"></a>例の実行  
 概要と「[LINQ クエリの構造](#structure-of-a-linq-query)」セクションの例を実行するには、次のコードを含めます。これにより、顧客と注文の一覧が返されます。  
  
 [!code-vb[VbVbalrIntroToLINQ#31](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#31)]  
  
## <a name="linq-providers"></a>LINQ プロバイダー  
 "*LINQ プロバイダー*" は、Visual Basic LINQ クエリを、クエリ対象のデータ ソースにマップします。 LINQ クエリを記述すると、そのクエリは、プロバイダーによって、データ ソースが実行できるコマンドに変換されます。 プロバイダーは、ソースのデータを、クエリ結果を構成するオブジェクトに変換する操作も行います。 最後に、プロバイダーは、データ ソースに更新が送信されるときに、オブジェクトをデータに変換します。  
  
 Visual Basic には、次の LINQ プロバイダーが含まれています。  
  
|プロバイダー|説明|  
|---|---|  
|LINQ to Objects|LINQ to Objects プロバイダーは、インメモリ コレクションとインメモリ配列のクエリを可能にします。 オブジェクトが <xref:System.Collections.IEnumerable> インターフェイスまたは <xref:System.Collections.Generic.IEnumerable%601> インターフェイスをサポートしている場合、LINQ to Objects プロバイダーを使用してクエリを実行できます。<br /><br /> LINQ to Objects プロバイダーを有効にするには、すべての Visual Basic プロジェクトに対して既定でインポートされる <xref:System.Linq> 名前空間をインポートします。<br /><br /> LINQ to Objects プロバイダーの詳細については、「[LINQ to Objects](../../concepts/linq/linq-to-objects.md)」を参照してください。|  
|LINQ to SQL|LINQ to SQL プロバイダーは、SQL Server データベース内のデータのクエリと変更を可能にします。 これにより、アプリケーションのオブジェクト モデルを、データベース内のテーブルとオブジェクトに簡単に対応付けることができます。<br /><br /> Visual Basic では、オブジェクト リレーショナル デザイナー (O/R デザイナー) を用意することで、LINQ to SQL の操作を容易にしています。 このデザイナーを使用して、データベース内のオブジェクトに対応付けられるアプリケーション内のオブジェクト モデルを作成します。 O/R デザイナーは、ストアド プロシージャと関数を <xref:System.Data.Linq.DataContext> オブジェクト (データベースとの通信を管理し、オプティミスティック同時実行制御チェックの状態を保存します) にマップする機能も備えています。<br /><br /> LINQ to SQL プロバイダーの詳細については、「[LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)」を参照してください。 オブジェクト リレーショナル デザイナーの詳細については、「[Visual Studio の LINQ to SQL ツール](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)」を参照してください。|  
|LINQ to XML|LINQ to XML プロバイダーは、XML のクエリと変更を可能にします。 インメモリ XML を変更することや、XML をファイルから読み込んだりファイルに保存したりすることができます。<br /><br /> さらに、LINQ to XML プロバイダーでは、XML リテラルと XML 軸プロパティを使用して、XML を Visual Basic コード内に直接記述できます。 詳細については、「[XML](../xml/index.md)」を参照してください。|  
|LINQ to DataSet|LINQ to DataSet プロバイダーは、ADO.NET データセット内のデータのクエリと更新を可能にします。 データセットを使用するアプリケーションに LINQ を追加することで、データセット内のデータのクエリ、集計、および更新などの機能を単純化すると同時に拡張できます。<br /><br /> 詳細については、「[LINQ to DataSet](../../../../framework/data/adonet/linq-to-dataset.md)」を参照してください。|  
  
## <a name="structure-of-a-linq-query"></a>LINQ クエリの構造  
 LINQ クエリ ("*クエリ式*" とも呼ばれます) は、データ ソースを識別するクエリ句と、クエリの反復変数の組み合わせで構成されます。 クエリ式には、並べ替え、フィルター処理、グループ化、および結合を実行する命令や、ソース データに適用する演算も指定できます。 クエリ式の構文は SQL の構文に似ているので、ほとんどの構文は、改めて覚える必要はありません。  
  
 クエリ式は、`From` 句で始まります。 この句は、クエリのソース データと、ソース データの各要素を個別に参照するために使用される変数を識別します。 これらの変数は、"*範囲変数*" または "*反復変数*" と呼ばれます。 `From` 句は、`Aggregate` クエリ以外のクエリでは必須です。このクエリでは、`From` 句は省略できます。 `From` 句または `Aggregate` 句でクエリのスコープとソースを識別した後、クエリを絞り込むためのクエリ句を自由に組み合わせて記述できます。 クエリ句の詳細については、このトピックの「Visual Basic LINQ クエリ演算子」を参照してください。 たとえば、次のクエリでは、顧客データのソース コレクションを `customers` 変数として識別し、`cust` という名前の反復変数を識別します。  
  
 [!code-vb[VbVbalrIntroToLINQ#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#2)]  
  
 この例はそのままでも有効なクエリですが、結果を絞り込むクエリ句を追加すると、はるかに強力なクエリになります。 たとえば、`Where` 句を追加して、結果を 1 つ以上の値でフィルター処理できます。 クエリ式は、1 行のコードです。追加のクエリ句は、クエリの末尾に単純に追加できます。 クエリを読みやすくするために、行連結文字のアンダースコア (\_) を使用して、複数のテキスト行に分割できます。 次のコード例は、`Where` 句を含むクエリの例を示しています。  
  
 [!code-vb[VbVbalrIntroToLINQ#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#3)]  
  
 別の強力なクエリ句として、`Select` 句があります。この句を使用すると、データ ソースから選択したフィールドだけを返すことができます。 LINQ クエリは、厳密に型指定されたオブジェクトの列挙可能なコレクションを返します。 クエリは、匿名型または名前付きの型のコレクションを返すことができます。 `Select` 句を使用して、データ ソースから単一のフィールドを返すことができます。 これを行った場合、返されるコレクションの型は、その単一のフィールドの型になります。 `Select` 句を使用して、データ ソースから複数のフィールドを返すこともできます。 これを行った場合、返されるコレクションの型は、新しい匿名型になります。 クエリで返されたフィールドを、指定した名前付きの型のフィールドと一致させることもできます。 次のコード例は、データ ソースから選択されたフィールドのデータが設定されたメンバーのコレクションで、匿名型のコレクションを返すクエリ式を示します。  
  
 [!code-vb[VbVbalrIntroToLINQ#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#4)]  
  
 LINQ クエリを使用して、複数のデータ ソースを結合し、単一の結果を返すこともできます。 これは、1 つまたは複数の `From` 句を使用するか、`Join` クエリ句または `Group Join` クエリ句を使用して実行できます。 次のコード例は、顧客データと注文データを結合し、顧客データと注文データが格納された匿名型のコレクションを返すクエリ式を示します。  
  
 [!code-vb[VbVbalrIntroToLINQ#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#5)]  
  
 `Group Join` 句を使用して、顧客オブジェクトのコレクションを格納する階層的なクエリ結果を作成できます。 各顧客オブジェクトには、その顧客のすべての注文のコレクションを含むプロパティがあります。 次のコード例は、顧客データと注文データを階層的な結果として結合し、匿名型のコレクションを返すクエリ式を示します。 このクエリは、顧客の注文データのコレクションを格納する `CustomerOrders` プロパティを含む型を返します。 その顧客のすべての注文の合計を格納する `OrderTotal` プロパティも含まれます (このクエリは、LEFT OUTER JOIN と同等です)。  
  
 [!code-vb[VbVbalrIntroToLINQ#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/class2.vb#6)]  
  
 上記以外にも、強力なクエリ式を作成するために使用できる、さまざまな LINQ クエリ演算子があります。 このトピックの次のセクションで、クエリ式で使用できるさまざまなクエリ句について説明します。 Visual Basic クエリ句の詳細については、「[クエリ](../../../language-reference/queries/index.md)」を参照してください。  
  
## <a name="visual-basic-linq-query-operators"></a>Visual Basic LINQ クエリ演算子  

LINQ クエリをサポートする <xref:System.Linq> 名前空間とその他の名前空間のクラスには、アプリケーションの要件に基づいてクエリの作成と絞り込みを行うために呼び出すことができるメソッドが含まれています。 Visual Basic には、次の一般的なクエリ句のキーワードが含まれます。 Visual Basic クエリ句の詳細については、「[クエリ](../../../language-reference/queries/index.md)」を参照してください。

### <a name="from-clause"></a>From 句

クエリを開始するには、[`From` 句](../../../language-reference/queries/from-clause.md)または `Aggregate` 句のいずれかが必要です。 `From` 句は、クエリのソース コレクションと反復変数を指定します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#7)]

### <a name="select-clause"></a>Select 句

任意。 [`Select` 句](../../../language-reference/queries/select-clause.md)は、クエリの反復変数のセットを宣言します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#8)]

`Select` 句の指定がない場合、クエリの反復変数は、`From` 句または `Aggregate` 句で指定された反復変数で構成されます。

### <a name="where-clause"></a>Where 句

任意。 [`Where` 句](../../../language-reference/queries/where-clause.md)は、クエリのフィルター処理条件を指定します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#9)]

### <a name="order-by-clause"></a>Order By 句

任意。 [`Order By` 句](../../../language-reference/queries/order-by-clause.md)は、クエリ内に列の並べ替え順序を指定します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#10)]

### <a name="join-clause"></a>Join 句

任意。 [`Join` 句](../../../language-reference/queries/join-clause.md)は、2 つのコレクションを単一のコレクションに結合します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#11)]

### <a name="group-by-clause"></a>Group By 句

任意。 [`Group By` 句](../../../language-reference/queries/group-by-clause.md)は、クエリ結果の要素をグループ化します。 これを使用して、グループごとに集計関数を適用できます。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#12)]

### <a name="group-join-clause"></a>Group Join 句

任意。 [`Group Join` 句](../../../language-reference/queries/group-join-clause.md)は、2 つのコレクションを単一の階層コレクションに結合します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#13](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#13)]

### <a name="aggregate-clause"></a>Aggregate 句

クエリを開始するには、[`Aggregate` 句](../../../language-reference/queries/aggregate-clause.md)または `From` 句のいずれかが必要です。 `Aggregate` 句は、1 つ以上の集計関数をコレクションに適用します。 たとえば、次の例で行っているように、`Aggregate` 句を使用して、クエリで返されたすべての要素の合計を計算できます。

 [!code-vb[VbVbalrIntroToLINQ#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#14)]

`Aggregate` 句を使用してクエリを変更することもできます。 たとえば、`Aggregate` 句を使用して、関連するクエリ コレクションに対して計算を実行できます。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#15)]

### <a name="let-clause"></a>Let 句

任意。 [`Let` 句](../../../language-reference/queries/let-clause.md)は、値を計算し、それをクエリ内の新しい変数に代入します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#16](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#16)]

### <a name="distinct-clause"></a>Distinct 句

任意。 `Distinct` 句は、現在の反復変数の値を制限して、クエリ結果内で重複する値を除去します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#17)]

### <a name="skip-clause"></a>Skip 句

任意。 [`Skip` 句](../../../language-reference/queries/skip-clause.md)は、コレクション内の指定された数の要素をバイパスし、残りの要素を返します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#18)]

### <a name="skip-while-clause"></a>Skip While 句

任意。 [`Skip While` 句](../../../language-reference/queries/skip-while-clause.md)は、指定された条件が `true` である限り、コレクションの要素をバイパスし、残りの要素を返します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#19)]

### <a name="take-clause"></a>Take 句

任意。 [`Take` 句](../../../language-reference/queries/take-clause.md)は、コレクションの先頭から、指定された数の連続する要素を返します。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#20)]

### <a name="take-while-clause"></a>Take While 句

任意。 [`Take While` 句](../../../language-reference/queries/take-while-clause.md)は、指定された条件が `true` である限り、コレクションの要素を含むようにし、残りの要素をバイパスします。 次に例を示します。

 [!code-vb[VbVbalrIntroToLINQ#21](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#21)]
  
## <a name="use-additional-linq-query-features"></a>追加の LINQ クエリ機能の使用  
  
LINQ によって提供される列挙可能でクエリ可能な型のメンバーを呼び出すことで、追加の LINQ クエリ機能を使用できます。 これらの追加機能は、クエリ式の結果に対して特定のクエリ演算子を呼び出すことで使用できます。 たとえば、次の例では、<xref:System.Linq.Enumerable.Union%2A?displayProperty=nameWithType> メソッドを使用して、2 つのクエリの結果を、1 つのクエリ結果に結合します。 また、<xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> メソッドを使用して、クエリ結果をジェネリック リストとして返します。
  
 [!code-vb[VbVbalrIntroToLINQ#22](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrIntroToLINQ/VB/Class1.vb#22)]  
  
 その他の LINQ 機能の詳細については、「[標準クエリ演算子の概要](../../concepts/linq/standard-query-operators-overview.md)」を参照してください。  
  
## <a name="connect-to-a-database-by-using-linq-to-sql"></a>LINQ to SQL を使用したデータベースへの接続  
 Visual Basic では、アクセスする SQL Server データベース オブジェクト (テーブル、ビュー、ストアド プロシージャなど) を、LINQ to SQL ファイルを使用して識別します。 LINQ to SQL ファイルには、.dbml という拡張子が付きます。  
  
 SQL Server データベースへの有効な接続が存在する場合は、**LINQ to SQL クラス**項目テンプレートをプロジェクトに追加できます。 これを行うと、オブジェクト リレーショナル デザイナー (O/R デザイナー) が表示されます。 O/R デザイナーを使用して、コード内でアクセスする項目を、**サーバー エクスプローラー**/**データベース エクスプローラー**からデザイナー画面にドラッグできます。 LINQ to SQL ファイルは、<xref:System.Data.Linq.DataContext> オブジェクトをプロジェクトに追加します。 このオブジェクトには、アクセスするテーブルとビューのプロパティおよびコレクションと、呼び出すストアド プロシージャのメソッドが格納されます。 変更を LINQ to SQL (.dbml) ファイルに保存した後、O/R デザイナーで定義された <xref:System.Data.Linq.DataContext> オブジェクトを参照することで、コード内でこれらのオブジェクトにアクセスできます。 プロジェクトの <xref:System.Data.Linq.DataContext> オブジェクトには、LINQ to SQL ファイルの名前に基づいて名前が付けられます。 たとえば、Northwind.dbml という名前の LINQ to SQL ファイルの場合は、<xref:System.Data.Linq.DataContext> という名前の `NorthwindDataContext` オブジェクトが作成されます。  
  
 詳細な手順を示した例については、「[方法: データベースに対してクエリを実行する](how-to-query-a-database-by-using-linq.md)」と「[方法: ストアド プロシージャの呼び出し](how-to-call-a-stored-procedure-by-using-linq.md)」を参照してください。  
  
## <a name="visual-basic-features-that-support-linq"></a>LINQ をサポートする Visual Basic の機能  
 Visual Basic には、LINQ の使用を単純化し、LINQ クエリを実行するために記述する必要があるコードの量を減らすことができる、注目に値する機能が他にもあります。 次に例を示します。  
  
- **匿名型**。クエリ結果に基づいて、新しい型を作成できます。  
  
- **暗黙的に型指定される変数**。型の指定を遅らせ、クエリ結果に基づいてコンパイラで型を推論できます。  
  
- **拡張メソッド**。型自体を変更することなく、独自のメソッドを使用して既存の型を拡張できます。  
  
 詳細については、「[LINQ をサポートする Visual Basic の機能](../../concepts/linq/features-that-support-linq.md)」を参照してください。  
  
## <a name="deferred-and-immediate-query-execution"></a>クエリの遅延実行と即時実行

 クエリの実行とクエリの作成は分離しています。 クエリを作成した後、その実行は、別のメカニズムによってトリガーされます。 クエリは、定義後すぐに実行 ("*即時実行*)" することも、定義を保存しておき、後でクエリを実行 ("*遅延実行*") することもできます。  
  
 既定では、クエリを作成しても、クエリ自体が直ちに実行されることはありません。 代わりに、クエリ結果を参照するために使用される変数にクエリ定義が格納されます。 そのクエリ結果変数が、後でコード内の `For…Next` ループなどでアクセスされると、クエリが実行されます。 この処理を "*遅延実行*" と呼びます。  
  
 クエリは、それを定義したときに実行することもできます。これを "*即時実行*" と呼びます。 即時実行は、クエリ結果の個々の要素にアクセスする必要があるメソッドを適用することで開始できます。 `Count`、`Sum`、`Average`、`Min`、`Max` などの集計関数を含めることで、この結果を得ることができます。 集計関数の詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」を参照してください。  
  
 `ToList` メソッドまたは `ToArray` メソッドを使用することでも、即時実行を開始できます。 これは、クエリを直ちに実行し、結果をキャッシュする場合に役に立ちます。 これらのメソッドの詳細については、「[データ型の変換](../../concepts/linq/converting-data-types.md)」を参照してください。  
  
 クエリの実行の詳細については、「[初めての LINQ クエリの作成](../../concepts/linq/writing-your-first-linq-query.md)」を参照してください。  
  
## <a name="xml-in-visual-basic"></a>Visual Basic における XML  
 Visual Basic における XML の機能には、XML リテラルと XML 軸プロパティがあります。これらを使用して、コード内で XML を簡単に作成、アクセス、照会、および変更できます。 XML リテラルを使用すると、XML をコード内に直接記述できます。 Visual Basic コンパイラは、XML を、最初のクラスのデータ オブジェクトとして処理します。  
  
 次のコード例は、XML 要素を作成し、そのサブ要素と属性にアクセスし、LINQ を使用してその要素の内容を照会する方法を示しています。  
  
 [!code-vb[VbXmlSamples#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbXMLSamples/VB/XMLSamples3.vb#8)]  
  
 詳細については、「[XML](../xml/index.md)」を参照してください。  
  
## <a name="related-resources"></a>関連資料  
  
|トピック|説明|  
|---|---|  
|[XML](../xml/index.md)|Visual Basic における XML の機能について説明します。これらの機能を使用すると、クエリを実行したり、XML を最初のクラスのデータ オブジェクトとして Visual Basic コード内に含めたりすることができます。|  
|[クエリ](../../../language-reference/queries/index.md)|Visual Basic で使用できるクエリ句のリファレンス情報を示します。|  
|[統合言語クエリ (LINQ)](../../concepts/linq/index.md)|LINQ の概要、プログラミング ガイド、およびサンプルを示します。|  
|[LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)|LINQ to SQL の概要、プログラミング ガイド、およびサンプルを示します。|  
|[LINQ to Objects](../../concepts/linq/linq-to-objects.md)|LINQ to Objects の概要、プログラミング ガイド、およびサンプルを示します。|  
|[LINQ to ADO.NET (ポータル ページ)](../../concepts/linq/linq-to-adonet-portal-page.md)|LINQ to ADO.NET の概要、プログラミング ガイド、およびサンプルへのリンクを示します。|  
|[LINQ to XML](../../concepts/linq/linq-to-xml.md)|LINQ to XML の概要、プログラミング ガイド、およびサンプルを示します。|  
  
## <a name="how-to-and-walkthrough-topics"></a>方法とチュートリアルのトピック
 [方法: データベースに対してクエリを実行する](how-to-query-a-database-by-using-linq.md)  
  
 [方法: ストアド プロシージャの呼び出し](how-to-call-a-stored-procedure-by-using-linq.md)  
  
 [方法: データベースのデータの変更](how-to-modify-data-in-a-database-by-using-linq.md)  
  
 [方法: 結合を使用したデータの結合](how-to-combine-data-with-linq-by-using-joins.md)  
  
 [方法: クエリ結果を並べ替える](how-to-sort-query-results-by-using-linq.md)  
  
 [方法: クエリ結果をフィルター処理する](how-to-filter-query-results-by-using-linq.md)  
  
 [方法: データの数、合計、または平均の算出](how-to-count-sum-or-average-data-by-using-linq.md)  
  
 [方法: クエリ結果内の最小値と最大値の検索](how-to-find-the-minimum-or-maximum-value-in-a-query-result.md)  
  
 [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)  
  
## <a name="featured-book-chapters"></a>参考書籍の該当する章  
 「[第 17 章: LINQ](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652502(v=orm.10))」 (『[Programming Visual Basic 2008](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2008/ff652504(v=orm.10))』)  
  
## <a name="see-also"></a>関連項目

- [統合言語クエリ (LINQ)](../../concepts/linq/index.md)
- [Visual Basic における LINQ to XML の概要](../xml/overview-of-linq-to-xml.md)
- [LINQ to DataSet の概要](../../../../framework/data/adonet/linq-to-dataset-overview.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [Visual Studio の LINQ to SQL ツール](/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
