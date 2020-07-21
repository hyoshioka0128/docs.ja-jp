---
title: '方法: LINQ を使用してストアド プロシージャを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- queries [LINQ in Visual Basic], stored procedure calls
- stored procedures sample [Visual Basic]
- stored procedures [LINQ to SQL]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
ms.openlocfilehash: b451642a16f36c4f7fd19c853fdfd2282f5bede5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84405031"
---
# <a name="how-to-call-a-stored-procedure-by-using-linq-visual-basic"></a>方法: LINQ を使用してストアド プロシージャを呼び出す (Visual Basic)
統合言語クエリ (LINQ) を使用すると、ストアド プロシージャなどのデータベース オブジェクトを始めとするデータベース情報に簡単にアクセスできます。  
  
 次の例では、SQL Server データベースのストアド プロシージャを呼び出すアプリケーションを作成する方法を示します。 このサンプルでは、データベース内の 2 つの異なるストアド プロシージャを呼び出す方法を示します。 各プロシージャは、クエリの結果を返します。 プロシージャのうちの 1 つは入力パラメーターを受け取りますが、もう 1 つのプロシージャはパラメーターを受け取りません。  
  
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
  
### <a name="to-add-stored-procedures-to-the-or-designer"></a>ストアド プロシージャを O/R デザイナーに追加するには  
  
1. **[サーバー エクスプローラー]** / **[データベース エクスプローラー]** で、Northwind データベースへの接続を展開します。 **[ストアド プロシージャ]** フォルダーを展開します。  
  
     O/R デザイナーを閉じている場合は、前に追加した northwind.dbml ファイルをダブルクリックして再度開くことができます。  
  
2. **Sales by Year** ストアド プロシージャをクリックし、デザイナーの右ペインにドラッグします。 **Ten Most Expensive Products** ストアド プロシージャをクリックして、デザイナーの右ペインにドラッグします。  
  
3. 変更を保存し、デザイナーを閉じます。  
  
4. プロジェクトを保存します。  
  
### <a name="to-add-code-to-display-the-results-of-the-stored-procedures"></a>ストアド プロシージャの結果を表示するコードを追加するには  
  
1. **[ツールボックス]** から、プロジェクトの既定の Windows フォームである Form1 に <xref:System.Windows.Forms.DataGridView> コントロールをドラッグします。  
  
2. Form1 をダブルクリックして、`Load` イベントにコードを追加します。  
  
3. ストアド プロシージャを O/R デザイナーに追加したときに、<xref:System.Data.Linq.DataContext> オブジェクトがプロジェクトに追加されました。 このオブジェクトには、これらのプロシージャにアクセスするために必要なコードが含まれています。 プロジェクトの <xref:System.Data.Linq.DataContext> オブジェクトの名前は、.dbml ファイルの名前に基づいて付けられます。 このプロジェクトでは、<xref:System.Data.Linq.DataContext> オブジェクトに `northwindDataContext` という名前が付けられています。  
  
     コード内で <xref:System.Data.Linq.DataContext> のインスタンスを作成し、O/R デザイナーによって指定されたストアド プロシージャのメソッドを呼び出すことができます。 <xref:System.Windows.Forms.DataGridView> オブジェクトにバインドするために、ストアド プロシージャの結果に対して <xref:System.Linq.Enumerable.ToList%2A> メソッドを呼び出すことで、クエリの即時実行を強制することが必要な場合があります。  
  
     次のコードを `Load` イベントに追加して、データ コンテキストのメソッドとして公開されているストアド プロシージャのいずれかを呼び出します。  
  
     [!code-vb[VbLINQtoSQLHowTos#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form3.vb#1)]  
    [!code-vb[VbLINQtoSQLHowTos#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbLINQtoSQLHowTos/VB/Form3.vb#2)]  
  
4. F5 キーを押してプロジェクトを実行し、結果を表示します。  
  
## <a name="see-also"></a>関連項目

- [LINQ](index.md)
- [クエリ](../../../language-reference/queries/index.md)
- [LINQ to SQL](../../../../framework/data/adonet/sql/linq/index.md)
- [DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)
- [方法: 更新、挿入、および削除を実行するストアド プロシージャを割り当てる (O/R デザイナー)](/visualstudio/data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer)
