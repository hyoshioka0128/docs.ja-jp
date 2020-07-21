---
title: '方法: LINQ を使用したクエリ結果内の最小値と最大値の検索'
ms.date: 07/20/2015
helpviewer_keywords:
- max operator [LINQ in Visual Basic]
- aggregate operator [LINQ in Visual Basic]
- aggregate queries
- minimum values [LINQ in Visual Basic]
- min operator [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], minimum and maximum values
- Max property
- maximum values [LINQ in Visual Basic]
- Aggregate clause [Visual Basic]
- queries [LINQ in Visual Basic], aggregate queries
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 238b763b-7dcd-4b14-8050-b65500a4f71c
ms.openlocfilehash: a148d8b726da78261eda152fcaafdd64ea01bb24
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404979"
---
# <a name="how-to-find-the-minimum-or-maximum-value-in-a-query-result-by-using-linq-visual-basic"></a>方法: LINQ を使用したクエリ結果内の最小値と最大値の検索 (Visual Basic)
統合言語クエリ (LINQ) を使用すると、データベース情報に簡単にアクセスしてクエリを実行できます。  
  
 次の例は、SQL Server データベースに対してクエリを実行する新しいアプリケーションを作成する方法を示しています。 このサンプルでは、`Aggregate` 句と `Group By` 句を使用して、結果の最小値と最大値を特定します。 詳細については、「[Aggregate 句](../../../language-reference/queries/aggregate-clause.md)」および「[Group By 句](../../../language-reference/queries/group-by-clause.md)」を参照してください。  
  
 このトピックの例では、Northwind サンプル データベースを使用します。 開発用コンピューターにこのデータベースがない場合は、Microsoft ダウンロード センターからダウンロードできます。 手順については、「[サンプル データベースのダウンロード](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)」を参照してください。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
## <a name="create-a-connection-to-a-database"></a>データベースへの接続を作成する  
  
1. Visual Studio で、 **[表示]** メニューの **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** をクリックして、 **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** を開きます。  
  
2. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で **[データ接続]** を右クリックし、 **[接続の追加]** をクリックします。  
  
3. Northwind サンプル データベースへの有効な接続を指定します。  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL ファイルを含むプロジェクトを追加するには  
  
1. Visual Studio で、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 プロジェクト タイプとして Visual Basic **[Windows フォーム アプリケーション]** を選択します。  
  
2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。 **[LINQ to SQL クラス]** 項目テンプレートを選択します。  
  
3. そのファイルに `northwind.dbml` という名前を付けます。 **[追加]** をクリックします。 オブジェクト リレーショナル デザイナー (O/R デザイナー) が northwind.dbml ファイルを対象にして開きます。  
  
## <a name="add-tables-to-query-to-the-or-designer"></a>O/R デザイナーに対してクエリを実行するテーブルを追加する  
  
1. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で、Northwind データベースへの接続を展開します。 **[テーブル]** フォルダーを展開します。  
  
     O/R デザイナーを閉じている場合は、前に追加した northwind.dbml ファイルをダブルクリックして再度開くことができます。  
  
2. Customers テーブルをクリックし、デザイナーの左ペインにドラッグします。 Orders テーブルをクリックし、デザイナーの左ペインにドラッグします。  
  
     デザイナーによって、プロジェクトの新しい `Customer` と `Order` オブジェクトが作成されます。 デザイナーがテーブル間のリレーションシップを自動的に検出し、関連するオブジェクトの子プロパティを作成することに注意してください。 たとえば、IntelliSense は、`Customer` オブジェクトに、その顧客に関連するすべての注文のための `Orders` プロパティがあることを示します。  
  
3. 変更を保存し、デザイナーを閉じます。  
  
4. プロジェクトを保存します。  
  
## <a name="add-code-to-query-the-database-and-display-the-results"></a>データベースに対してクエリを実行し、結果を表示するコードを追加する  
  
1. **[ツールボックス]** から、プロジェクトの既定の Windows フォームである Form1 に <xref:System.Windows.Forms.DataGridView> コントロールをドラッグします。  
  
2. Form1 をダブルクリックして、フォームの `Load` イベントにコードを追加します。  
  
3. テーブルを O/R デザイナーに追加したときに、<xref:System.Data.Linq.DataContext> オブジェクトがプロジェクトに追加されました。 このオブジェクトには、各テーブルの個々のオブジェクトとコレクションに加えて、それらのテーブルにアクセスするために必要なコードが含まれます。 プロジェクトの <xref:System.Data.Linq.DataContext> オブジェクトには、.dbml ファイルの名前に基づいて名前が付けられます。 このプロジェクトでは、<xref:System.Data.Linq.DataContext> オブジェクトに `northwindDataContext` という名前が付けられています。  
  
     コード内で <xref:System.Data.Linq.DataContext> のインスタンスを作成し、O/R デザイナーによって指定されたテーブルに対してクエリを実行できます。  
  
     `Load` イベントに次のコードを追加します。 このコードは、データ コンテキストのプロパティとして公開されているテーブルに対してクエリを実行し、結果の最小値と最大値を特定します。 このサンプルでは、`Aggregate` 句を使用して 1 つの結果に対してクエリを実行し、`Group By` 句を使用してグループ化された結果の平均を表示します。  
  
     [!code-vb[VbLINQToSQLHowTos#14](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form7.vb#14)]  
  
4. **F5** キーを押してプロジェクトを実行し、結果を表示します。  
  
## <a name="see-also"></a>関連項目

- [LINQ](index.md)
- [クエリ](../../../language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
