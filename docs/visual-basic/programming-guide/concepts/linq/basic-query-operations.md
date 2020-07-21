---
title: クエリの基本操作
ms.date: 07/20/2015
helpviewer_keywords:
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
ms.openlocfilehash: 92ac5beb70526795eb140bd794e47981cebfea93
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410917"
---
# <a name="basic-query-operations-visual-basic"></a>基本的なクエリ操作 (Visual Basic)
このトピックでは、Visual Basic における統合言語クエリ (LINQ) 式と、クエリで実行されるいくつかの一般的な操作について簡単に紹介します。 詳細については、次のトピックを参照してください。  
  
 [Visual Basic における LINQ の概要](../../language-features/linq/introduction-to-linq.md)  
  
 [クエリ](../../../language-reference/queries/index.md)  
  
 [チュートリアル: Visual Basic でのクエリの作成](walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>データ ソースを指定する (From)  
 LINQ クエリで最初に行う手順は、照会するデータ ソースの指定です。 そのためクエリでは、`From` 句が必ず先頭に来ます。 クエリ演算子は、ソースの種類に基づいて結果を選択し、整形します。  
  
 [!code-vb[VbLINQBasicOps#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#1)]  
  
 `From` 句は、データ ソース (`customers`) と "*範囲変数*" (`cust`) を指定するものです。 範囲変数はループの反復変数に似ていますが、クエリ式では実際の反復処理が実行されない点は除きます。 クエリは多くの場合、`For Each` ループを使用して実行され、範囲変数は、クエリが実行されたとき、`customers` に含まれる連続する各要素への参照として機能します。 `cust` の型はコンパイラで推論できるため、明示的に指定する必要はありません。 明示的な型指定を使用して記述されたクエリと使用せずに記述されたクエリの例については、「[クエリ操作での型の関係 (Visual Basic)](type-relationships-in-query-operations.md)」を参照してください。  
  
 Visual Basic での `From` 句の使い方について詳しくは、「[From 句](../../../language-reference/queries/from-clause.md)」を参照してください。  
  
## <a name="filtering-data-where"></a>データをフィルター処理する (Where)  
 最も一般的なクエリ操作は、ブール式の形式でフィルターを適用することです。 その場合、クエリからは、式が true となる要素のみが返されます。 フィルター処理は、`Where` 句を使用して実行されます。 データ ソース内のどの要素を結果のシーケンスに含めるかをフィルターで指定します。 次の例では、住所がロンドンにある顧客だけが結果に含まれます。  
  
 [!code-vb[VbLINQBasicOps#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#2)]  
  
 `Where` 句では、`And` や `Or` といった論理演算子を使用して、複数のフィルター式を結合することができます。 たとえばロンドン在住で、なおかつ名前が Devon である顧客のみを取得するには、次のコードを使用します。  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"
```  
  
 ロンドンまたはパリ在住の顧客を取得するには、次のコードを使用します。  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"
```  
  
 Visual Basic での `Where` 句の使い方について詳しくは、「[Where 句](../../../language-reference/queries/where-clause.md)」を参照してください。  
  
## <a name="ordering-data-order-by"></a>データを並べ替える (Order By)  
 返されたデータを特定の順序で並べ替えると都合がよい場合は少なくありません。 `Order By` 句を使用すると、返されたシーケンス内の要素が、指定された 1 つまたは複数のフィールドを基準に並べ替えられます。 たとえば、次のクエリは `Name` プロパティに基づいて結果を並べ替えます。 `Name` は文字列であるため、返されるデータはアルファベット順 (A から Z) に並べ替えられます。  
  
 [!code-vb[VbLINQBasicOps#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#3)]  
  
 結果を逆の順序 (Z から A) で並び替えるには、`Order By...Descending` 句を使用します。 `Ascending` も `Descending` も指定されなかった場合は、既定で `Ascending` が使用されます。  
  
 Visual Basic での `Order By` 句の使い方について詳しくは、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。  
  
## <a name="selecting-data-select"></a>データを選択する (Select)  
 `Select` 句は、返された要素の形式と内容を指定します。 たとえば、`Customer` オブジェクト全体、1 つの `Customer` プロパティのみ、プロパティのサブセット、各種データ ソースのプロパティの組み合わせ、計算に基づくなんらかの新しい結果型のいずれで結果が構成されるかを指定できます。 `Select` 句でソース要素のコピー以外のものを生成する場合、その操作は*投影*と呼ばれます。  
  
 `Customer` オブジェクト全体から成るコレクションを取得するには、範囲変数自体を選択します。  
  
 [!code-vb[VbLINQBasicOps#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#4)]  
  
 `Customer` インスタンスがフィールドを多数含んだ大きなオブジェクトで、取得したいのはその名前だけである場合は、次の例のように `cust.Name` を選択できます。 それに伴い、結果の型が `Customer` オブジェクトのコレクションから文字列のコレクションに変化したことは、ローカル型推論によって認識されます。  
  
 [!code-vb[VbLINQBasicOps#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#5)]  
  
 データ ソースから複数のフィールドを選択したい場合、次の 2 つの選択肢があります。  
  
- `Select` 句で、結果に含めたいフィールドを指定します。 それらのフィールドをプロパティとして持つ匿名型がコンパイラによって定義されます。 詳細については、「[匿名型](../../language-features/objects-and-classes/anonymous-types.md)」を参照してください。  
  
     以下の例で返される要素は匿名型のインスタンスであるため、コード内の他の場所では、型を名前で参照することができません。 コンパイラによって指定された型名には、通常の Visual Basic コードでは無効な文字が含まれます。 次の例で、`londonCusts4` としてクエリから返されるコレクション内の要素は匿名型のインスタンスです。  
  
     [!code-vb[VbLINQBasicOps#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#6)]  
  
     \- または -  
  
- 結果に含めたい特定のフィールドを含む名前付きの型を定義し、その型のインスタンスを `Select` 句で作成して初期化します。 この方法を使用するのは、結果が返されるコレクションの外で個々の結果を使用しなければならない場合や、それらをパラメーターとしてメソッド呼び出しに渡す必要がある場合のみです。 次の例では、`londonCusts5` の型が IEnumerable(Of NamePhone) になります。  
  
     [!code-vb[VbLINQBasicOps#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#7)]  
  
     [!code-vb[VbLINQBasicOps#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#8)]  
  
 Visual Basic での `Select` 句の使い方について詳しくは、「[Select 句](../../../language-reference/queries/select-clause.md)」を参照してください。  
  
## <a name="joining-data-join-and-group-join"></a>データを結合する (Join と Group Join)  
 `From` 句では、いくつかの方法で複数のデータ ソースを結合することができます。 たとえば次のコードでは、2 つのデータ ソースを使用し、その両方のプロパティを結果の中で暗黙的に結合しています。 このクエリでは、姓が母音で始まる学生が選択されます。  
  
 [!code-vb[VbLINQBasicOps#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#9)]  
  
> [!NOTE]
> このコードは、「[方法: 項目のリストを作成する](how-to-create-a-list-of-items.md)」で作成した学生のリストを使用して実行できます。  
  
 `Join` キーワードは、SQL の `INNER JOIN` に相当します。 2 つのコレクションの要素間の一致するキーの値に基づいて 2 つのコレクションを結合します。 このクエリは、一致するキー値を持つコレクション要素の全部または一部を返します。 たとえば、前の暗黙的結合のアクションを再現するコードを次に示します。  
  
 [!code-vb[VbLINQBasicOps#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#10)]  
  
 SQL の `LEFT JOIN` のように、複数のコレクションを結合して 1 つの階層コレクションにするには、`Group Join` を使用します。 詳細については、「[Join 句](../../../language-reference/queries/join-clause.md)」および「[Group Join 句](../../../language-reference/queries/group-join-clause.md)」を参照してください。  
  
## <a name="grouping-data-group-by"></a>データをグループ化する (Group By)  
 `Group By` 句を追加すれば、クエリの結果に含まれる要素を、その要素の 1 つ以上のフィールドに従ってグループ化することができます。 たとえば、次のコードは、学生を学年ごとにグループ化するものです。  
  
 [!code-vb[VbLINQBasicOps#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#11)]  
  
 「[方法: 項目のリストを作成する](how-to-create-a-list-of-items.md)」で作成した学生のリストを使用してこのコードを実行した場合、`For Each` ステートメントから次の出力が返されます。  
  
 年:Junior  
  
 Tucker, Michael  
  
 Garcia, Hugo  
  
 Garcia, Debra  
  
 Tucker, Lance  
  
 年:Senior  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, Hanying  
  
 Adams, Terry  
  
 年:Freshman  
  
 Mortensen, Sven  
  
 Garcia, Cesar  
  
 次のコードでは、先ほどの例を応用し、学生をまず学年で並べ替えた後、各学年の学生を姓で並べ替えています。  
  
 [!code-vb[VbLINQBasicOps#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQBasicOps/VB/Class1.vb#12)]  
  
 `Group By` の詳細については、「[Group By 句](../../../language-reference/queries/group-by-clause.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Collections.Generic.IEnumerable%601>
- [Visual Basic の LINQ の概要](getting-started-with-linq.md)
- [クエリ](../../../language-reference/queries/index.md)
- [標準クエリ演算子の概要 (Visual Basic)](standard-query-operators-overview.md)
- [LINQ](../../language-features/linq/index.md)
