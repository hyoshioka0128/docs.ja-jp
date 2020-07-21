---
title: '方法: LINQ を使用してクエリ結果をフィルター処理する'
ms.date: 07/20/2015
helpviewer_keywords:
- filtering [Visual Basic]
- filtering data [LINQ in Visual Basic]
- filtering [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], filtering results
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
- filtering data [Visual Basic]
ms.assetid: ef103092-9bed-4134-97f4-2db696e83c12
ms.openlocfilehash: 4d91783429f24abfe4149217542f8f7a6073bfef
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404992"
---
# <a name="how-to-filter-query-results-by-using-linq-visual-basic"></a>方法: LINQ を使用してクエリ結果をフィルター処理する (Visual Basic)

統合言語クエリ (LINQ) を使用すると、データベース情報に簡単にアクセスしてクエリを実行できます。

次の例は、SQL Server データベースに対してクエリを実行し、`Where` 句を使用して特定の値で結果をフィルター処理する新しいアプリケーションの作成方法を示しています。 詳細については、「[Where 句](../../../language-reference/queries/where-clause.md)」を参照してください。

このトピックの例では、Northwind サンプル データベースを使用します。 開発用コンピューターにこのデータベースがない場合は、Microsoft ダウンロード センターからダウンロードできます。 手順については、「[サンプル データベースのダウンロード](../../../../framework/data/adonet/sql/linq/downloading-sample-databases.md)」を参照してください。

[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]

## <a name="to-create-a-connection-to-a-database"></a>データベースへの接続を作成するには

1. Visual Studio で、 **[表示]** メニューの **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** をクリックして、 **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** を開きます。

2. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で **[データ接続]** を右クリックし、 **[接続の追加]** をクリックします。

3. Northwind サンプル データベースへの有効な接続を指定します。

## <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>LINQ to SQL ファイルを含むプロジェクトを追加するには

1. Visual Studio で、 **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 プロジェクト タイプとして Visual Basic **[Windows フォーム アプリケーション]** を選択します。

2. **[プロジェクト]** メニューの **[新しい項目の追加]** をクリックします。 **[LINQ to SQL クラス]** 項目テンプレートを選択します。

3. そのファイルに `northwind.dbml` という名前を付けます。 **[追加]** をクリックします。 オブジェクト リレーショナル デザイナー (O/R デザイナー) が northwind.dbml ファイル用に開きます。

## <a name="to-add-tables-to-query-to-the-or-designer"></a>O/R デザイナーにクエリを実行するテーブルを追加するには

1. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で、Northwind データベースへの接続を展開します。 **[テーブル]** フォルダーを展開します。

     O/R デザイナーを閉じている場合は、前に追加した northwind.dbml ファイルをダブルクリックして再度開くことができます。

2. Customers テーブルをクリックし、デザイナーの左ペインにドラッグします。 Orders テーブルをクリックし、デザイナーの左ペインにドラッグします。

     デザイナーによって、プロジェクトの新しい `Customer` と `Order` オブジェクトが作成されます。 デザイナーによってテーブル間のリレーションシップが自動的に検出され、関連するオブジェクトの子プロパティが作成されることに注目してください。 たとえば、IntelliSense では、`Customer` オブジェクトに、その顧客に関連するすべての注文の `Orders` プロパティがあることを示します。

3. 変更を保存し、デザイナーを閉じます。

4. プロジェクトを保存します。

## <a name="to-add-code-to-query-the-database-and-display-the-results"></a>データベースに対してクエリを実行し、結果を表示するコードを追加するには

1. **[ツールボックス]** から、プロジェクトの既定の Windows フォームである Form1 に <xref:System.Windows.Forms.DataGridView> コントロールをドラッグします。

2. Form1 をダブルクリックして、コードをフォームの `Load` イベントに追加します。

3. テーブルを O/R デザイナーに追加したときに、<xref:System.Data.Linq.DataContext> オブジェクトがプロジェクトに追加されました。 このオブジェクトには、各テーブルの個々のオブジェクトとコレクションに加え、それらのテーブルにアクセスするために必要なコードが含まれます。 プロジェクトの <xref:System.Data.Linq.DataContext> オブジェクトの名前は、.dbml ファイルの名前に基づいて付けられます。 このプロジェクトでは、<xref:System.Data.Linq.DataContext> オブジェクトに `northwindDataContext` という名前が付けられています。

    コードで <xref:System.Data.Linq.DataContext> のインスタンスを作成し、O/R デザイナーによって指定されたテーブルに対してクエリを実行できます。

    次のコードを `Load` イベントに追加し、データ コンテキストのプロパティとして公開されているテーブルに対してクエリを実行します。 クエリでは結果がフィルター処理され、`London` にある顧客のみが返されます。

    [!code-vb[VbLINQToSQLHowTos#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form5.vb#11)]

4. F5 キーを押してプロジェクトを実行し、結果を表示します。

5. 他にも、次のようなフィルターをいくつか試すことができます。

    [!code-vb[VbLINQToSQLHowTos#12](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form5.vb#12)]

## <a name="see-also"></a>関連項目

- [LINQ](index.md)
- [クエリ](../../../language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
