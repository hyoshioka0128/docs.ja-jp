---
title: '方法: LINQ を使用してクエリ結果を並べ替える'
ms.date: 07/20/2015
helpviewer_keywords:
- sorting query results, multiple columns
- sorting data [Visual Basic]
- sorting data [LINQ in Visual Basic]
- sorting query results [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], sorting results
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 07a4584d-9fd8-4a1d-b7d9-ccf2efa5c84e
ms.openlocfilehash: c1bc6ab863f9de118d59e102d3d5d251d326f497
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404940"
---
# <a name="how-to-sort-query-results-by-using-linq-visual-basic"></a>方法: LINQ を使用してクエリ結果を並べ替える (Visual Basic)
統合言語クエリ (LINQ) を使用すると、データベース情報に簡単にアクセスしてクエリを実行できます。  
  
 次の例は、SQL Server データベースに対してクエリを実行し、`Order By` 句を使用して複数のフィールドで結果を並べ替える新しいアプリケーションの作成方法を示しています。 各フィールドの並べ替え順序は、昇順または降順にすることができます。 詳細については、「[Order By 句](../../../language-reference/queries/order-by-clause.md)」を参照してください。  
  
 このトピックの例では、Northwind サンプル データベースを使用します。 開発用コンピューターにこのデータベースがない場合は、Microsoft ダウンロード センターからダウンロードできます。 手順については、「[サンプル データベースのダウンロード](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)」を参照してください。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>データベースへの接続を作成するには  
  
1. Visual Studio で、 **[表示]** メニューの **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** をクリックして、 **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** を開きます。  
  
2. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で **[データ接続]** を右クリックし、 **[接続の追加]** をクリックします。  
  
3. Northwind サンプル データベースへの有効な接続を指定します。  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL ファイルを含むプロジェクトを追加するには  
  
1. Visual Studio で、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 プロジェクト タイプとして Visual Basic **[Windows フォーム アプリケーション]** を選択します。  
  
2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。 **[LINQ to SQL クラス]** 項目テンプレートを選択します。  
  
3. そのファイルに `northwind.dbml` という名前を付けます。 **[追加]** をクリックします。 オブジェクト リレーショナル デザイナー (O/R デザイナー) が northwind.dbml ファイル用に開きます。  
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>O/R デザイナーにクエリを実行する対象のテーブルを追加するには  
  
1. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で、Northwind データベースへの接続を展開します。 **[テーブル]** フォルダーを展開します。  
  
     O/R デザイナーを閉じている場合は、前に追加した northwind.dbml ファイルをダブルクリックして再度開くことができます。  
  
2. Customers テーブルをクリックし、デザイナーの左ペインにドラッグします。 Orders テーブルをクリックし、デザイナーの左ペインにドラッグします。  
  
     デザイナーによって、プロジェクトの新しい `Customer` と `Order` オブジェクトが作成されます。 デザイナーがテーブル間のリレーションシップを自動的に検出し、関連するオブジェクトの子プロパティを作成することに注意してください。 たとえば、IntelliSense は、`Customer` オブジェクトに、その顧客に関連するすべての注文のための `Orders` プロパティがあることを示します。  
  
3. 変更を保存し、デザイナーを閉じます。  
  
4. プロジェクトを保存します。  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>データベースに対してクエリを実行し、結果を表示するコードを追加するには  
  
1. **[ツールボックス]** から、プロジェクトの既定の Windows フォームである Form1 に <xref:System.Windows.Forms.DataGridView> コントロールをドラッグします。  
  
2. Form1 をダブルクリックして、フォームの `Load` イベントにコードを追加します。  
  
3. テーブルを O/R デザイナーに追加したときに、デザイナーによって <xref:System.Data.Linq.DataContext> オブジェクトがプロジェクトに追加されました。 このオブジェクトには、これらのテーブルにアクセスするため、および各テーブルの個々のオブジェクトとコレクションにアクセスするために必要なコードが含まれています。 プロジェクトの <xref:System.Data.Linq.DataContext> オブジェクトの名前は、.dbml ファイルの名前に基づいて付けられます。 このプロジェクトでは、<xref:System.Data.Linq.DataContext> オブジェクトに `northwindDataContext` という名前が付けられています。  
  
     コード内で <xref:System.Data.Linq.DataContext> のインスタンスを作成し、O/R デザイナーによって指定されたテーブルに対してクエリを実行できます。  
  
     データ コンテキストのプロパティとして公開されているテーブルに対してクエリを実行し、その結果を並べ替えるために、次のコードを `Load` イベントに追加します。 このクエリでは、顧客の注文数の降順で結果が並べ替えられます。 顧客の注文数が同じ場合は、会社名の昇順 (既定) で並べ替えられます。  
  
     [!code-vb[VbLINQToSQLHowTos#10](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form4.vb#10)]  
  
4. F5 キーを押してプロジェクトを実行し、結果を表示します。  
  
## <a name="see-also"></a>関連項目

- [LINQ](index.md)
- [クエリ](../../../language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
