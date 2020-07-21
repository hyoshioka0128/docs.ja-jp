---
title: 'チュートリアル: DataGrid コントロールで SQL Server データベースのデータを表示する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGrid [WPF], displaying data from SQL Server
- controls [WPF], DataGrid
ms.assetid: 6810b048-0a23-4f86-bfa5-97f92b3cfab4
ms.openlocfilehash: 1398d8408a0b85d6603d638312e92ba35c5e77d3
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84591034"
---
# <a name="walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control"></a>チュートリアル: DataGrid コントロールで SQL Server データベースのデータを表示する

このチュートリアルでは、SQL Server データベースからデータを取得し、そのデータを <xref:System.Windows.Controls.DataGrid> コントロールに表示します。 ADO.NET Entity Framework を使用して、データを表すエンティティ クラスを作成し、LINQ を使用して、指定されたデータをエンティティ クラスから取得するクエリを記述します。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- AdventureWorks サンプル データベースが添付された、SQL Server または SQL Server Express の実行中のインスタンスへのアクセス権。 AdventureWorks データベースは [GitHub](https://github.com/Microsoft/sql-server-samples/releases) からダウンロードできます。

## <a name="create-entity-classes"></a>エンティティ クラスを作成する

1. Visual Basic または C# で新しい WPF アプリケーション プロジェクトを作成し、`DataGridSQLExample` という名前を付けます。

2. ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加]** をポイントし、 **[新しい項目]** を選択します。

     [新しい項目の追加] ダイアログ ボックスが表示されます。

3. [インストール済みのテンプレート] ペインで **[データ]** を選択し、テンプレート一覧で **[ADO.NET Entity Data Model]** を選択します。

     ![ADO.NET Entity Data Model 項目テンプレート](../../wcf/feature-details/media/ado-net-entity-data-model-item-template.png)

4. ファイルに `AdventureWorksModel.edmx` と名前を付け、 **[追加]** をクリックします。

     Entity Data Model ウィザードが表示されます。

5. [モデルのコンテンツの選択] 画面で、 **[データベースから EF Designer]** をクリックし、 **[次へ]** をクリックします。

6. [データ接続の選択] 画面で、AdventureWorksLT2008 データベースへの接続を指定します。 詳細については、「[[データ接続の選択] ダイアログ ボックス](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb399244(v=vs.100))」を参照してください。

    名前が `AdventureWorksLT2008Entities` であり、 **[エンティティ接続設定に名前を付けて App.Config に保存]** チェック ボックスがオンであることを確認してから、 **[次へ]** をクリックします。

7. [データベース オブジェクトの選択] 画面で、[テーブル] ノードを展開し、**Product** および **ProductCategory** テーブルを選択します。

     すべてのテーブルのエンティティ クラスを生成できます。ただし、この例では、これら 2 つのテーブルからのみデータを取得します。

     ![テーブルから Product および ProductCategory を選択する](./media/datagrid-sql-ef-step4.png "DataGrid_SQL_EF_Step4")

8. **[完了]** をクリックします。

     Entity Designer に Product および ProductCategory エンティティが表示されます。

     ![Product および ProductCategory エンティティ モデル](./media/datagrid-sql-ef-step5.png "DataGrid_SQL_EF_Step5")

## <a name="retrieve-and-present-the-data"></a>データの取得と表示

1. MainWindow.xaml ファイルを開きます。

2. <xref:System.Windows.Window> の <xref:System.Windows.FrameworkElement.Width%2A> プロパティを 450 に設定します。

3. XAML エディターで、`<Grid>` タグと `</Grid>` タグの間に次の <xref:System.Windows.Controls.DataGrid> タグを追加して、`dataGrid1` という名前の <xref:System.Windows.Controls.DataGrid> を追加します。

     [!code-xaml[DataGrid_SQL_EF_Walkthrough#3](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml#3)]

     ![DataGrid が表示されたウィンドウ](./media/datagrid-sql-ef-step6.png "DataGrid_SQL_EF_Step6")

4. <xref:System.Windows.Window>を選択します。

5. プロパティ ウィンドウまたは XAML エディターを使用して、<xref:System.Windows.FrameworkElement.Loaded> イベントの `Window_Loaded` という名前の <xref:System.Windows.Window> のイベント ハンドラーを作成します。 詳細については、[方法: 単純なイベント ハンドラーを作成する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/bb675300(v=vs.100))」を参照してください。

     MainWindow.xaml の XAML を次に示します。

    > [!NOTE]
    > Visual Basic を使用する場合は、MainWindow.xaml の最初の行の `x:Class="DataGridSQLExample.MainWindow"` を `x:Class="MainWindow"` に置き換えます。

     [!code-xaml[DataGrid_SQL_EF_Walkthrough#1](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml#1)]

6. <xref:System.Windows.Window> の分離コード ファイル (MainWindow.xaml.vb または MainWindow.xaml.cs) を開きます。

7. 次のコードを追加して、結合されたテーブルから特定の値のみを取得し、<xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティをクエリの結果に設定します。

     [!code-csharp[DataGrid_SQL_EF_Walkthrough#2](~/samples/snippets/csharp/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/CS/MainWindow.xaml.cs#2)]
     [!code-vb[DataGrid_SQL_EF_Walkthrough#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataGrid_SQL_EF_Walkthrough/VB/MainWindow.xaml.vb#2)]

8. 例を実行します。

     データを表示する <xref:System.Windows.Controls.DataGrid> が表示されます。

     ![SQL Database のデータが表示された DataGrid](./media/datagrid-sql-ef-step7.png "DataGrid_SQL_EF_Step7")

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataGrid>
