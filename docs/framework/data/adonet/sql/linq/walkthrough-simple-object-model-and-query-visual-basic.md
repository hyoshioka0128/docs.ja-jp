---
title: 'チュートリアル: 簡単なオブジェクト モデルとクエリ (Visual Basic)'
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: c878e457-f715-46e4-a136-ff14d6c86018
ms.openlocfilehash: c21a187739ba19be2dc8e89b4dddc94ad799f036
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792121"
---
# <a name="walkthrough-simple-object-model-and-query-visual-basic"></a>チュートリアル: 簡単なオブジェクト モデルとクエリ (Visual Basic)

このチュートリアルでは、複雑さを抑えた、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 全体の基本的なシナリオを示します。 サンプルの Northwind データベースにある Customers テーブルのモデル化を行うエンティティ クラスを作成します。 次に、住所がロンドンの顧客を表示するための簡単なクエリを作成します。

このチュートリアルでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の考え方を示すために、コード中心の方法をあえて使用しています。 通常は、オブジェクト リレーショナル デザイナーを使用してオブジェクト モデルを作成できます。

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

このチュートリアルは、Visual Basic 開発設定を使用して記述されています。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、専用フォルダー ("c:\linqtest") を使用してファイルを保持します。 チュートリアルを開始する前に、このフォルダーを作成してください。

- このチュートリアルには、Northwind サンプル データベースが必要です。 開発用コンピューターにこのデータベースがない場合は、Microsoft ダウンロード サイトからダウンロードします。 手順については、「[サンプル データベースのダウンロード](downloading-sample-databases.md)」を参照してください。 データベースをダウンロードしたら、ファイルを c:\linqtest フォルダーにコピーします。

## <a name="overview"></a>概要

このチュートリアルは、主に次の 6 つの手順で構成されています。

- Visual Studio で [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ソリューションを作成します。

- データベース テーブルにクラスを割り当てます。

- クラスに対し、データベース列を表すプロパティを指定します。

- Northwind データベースへの接続を指定します。

- データベースに対して実行する簡単なクエリを作成します。

- クエリを実行して結果を観察する。

## <a name="creating-a-linq-to-sql-solution"></a>LINQ to SQL ソリューションを作成する

最初のタスクに、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] プロジェクトをビルドおよび実行するために必要な参照を含む Visual Studio ソリューションを作成します。

### <a name="to-create-a-linq-to-sql-solution"></a>LINQ to SQL ソリューションを作成するには

1. **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインで、 **[Visual Basic]** をクリックします。

3. **[テンプレート]** ペインの **[コンソール アプリケーション]** をクリックします。

4. **[名前]** ボックスに「**LinqConsoleApp**」と入力します。

5. **[OK]** をクリックします。

## <a name="adding-linq-references-and-directives"></a>LINQ の参照とディレクティブを追加する

このチュートリアルで使用するアセンブリは、既定ではプロジェクトにインストールされていない場合があります。 `System.Data.Linq` がプロジェクトの参照 (**ソリューション エクスプローラー**で **[すべてのファイルを表示]** をクリックし、 **[参照設定]** ノードを展開) に表示されていない場合は、以下の手順に従って追加します。

### <a name="to-add-systemdatalinq"></a>System.Data.Linq を追加するには

1. **ソリューション エクスプローラー**で、 **[参照設定]** を右クリックし、 **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスで、 **[.NET]** をクリックし、System.Data.Linq アセンブリをクリックします。次に、 **[OK]** をクリックします。

     アセンブリがプロジェクトに追加されます。

3. また、 **[参照の追加]** ダイアログ ボックスで、 **[.NET]** をクリックし、System.Windows.Forms までスクロールして、これをクリックします。次に、 **[OK]** をクリックします。

     このチュートリアルで使用するメッセージ ボックスをサポートするアセンブリがプロジェクトに追加されます。

4. `Module1` の上に次のディレクティブを追加します。

     [!code-vb[DLinqWalk1VB#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#1)]

## <a name="mapping-a-class-to-a-database-table"></a>データベース テーブルにクラスを対応付ける

この手順では、クラスを作成して、データベース テーブルに対応付けます。 このようなクラスのことを "*エンティティ クラス*" と呼びます。 対応付けは、<xref:System.Data.Linq.Mapping.TableAttribute> 属性を追加するだけで完了します。 <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> プロパティを使用して、データベースのテーブルの名前を指定します。

### <a name="to-create-an-entity-class-and-map-it-to-a-database-table"></a>エンティティ クラスを作成し、データベース テーブルに対応付けるには

- Module1.vb で、`Sub Main` の直前に次のコードを入力または貼り付けます。

     [!code-vb[DLinqWalk1VB#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#2)]

## <a name="designating-properties-on-the-class-to-represent-database-columns"></a>データベース列を表すプロパティをクラスに追加する

この手順では、いくつかのタスクを実行します。

- <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性を使用して、エンティティ クラスの `CustomerID` プロパティおよび `City` プロパティを、データベース テーブルの列を表すものとして指定します。

- `CustomerID` プロパティを、データベースの主キー列を表すものとして指定します。

- プライベートでの格納用として `_CustomerID` フィールドおよび `_City` フィールドを指定します。 これで、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、ビジネス ロジックを含む場合があるパブリック アクセサーを使用せずに、値を直接格納および取得できます。

### <a name="to-represent-characteristics-of-two-database-columns"></a>2 つのデータベース列の特性を指定するには

- Module1.vb で、`End Class` の直前に次のコードを入力または貼り付けます。

     [!code-vb[DLinqWalk1VB#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#3)]

## <a name="specifying-the-connection-to-the-northwind-database"></a>Northwind データベースへの接続を指定する

この手順では、<xref:System.Data.Linq.DataContext> オブジェクトを使用して、コードで作成したデータ構造とデータベース本体との間の接続を確立します。 データベースからのオブジェクトの取得や、変更内容の送信では、<xref:System.Data.Linq.DataContext> を仲介役として使用します。

また、データベースの Customers テーブルに対するクエリ用として、型指定された論理的なテーブルの役割を果たす `Table(Of Customer)` を宣言します。 これらのクエリの作成と実行は後の手順で行います。

### <a name="to-specify-the-database-connection"></a>データベース接続を指定するには

- `Sub Main` メソッドに次のコードを入力または貼り付けます。

     `northwnd.mdf` ファイルは linqtest フォルダーに置かれているものとします。 詳細については、このチュートリアルの「前提条件」を参照してください。

     [!code-vb[DLinqWalk1VB#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1VB/vb/Module1.vb#4)]

## <a name="creating-a-simple-query"></a>簡単なクエリの作成

この手順では、データベースの Customers テーブルから、住所が London の顧客を検索するクエリを作成します。 この手順で作成するクエリ コードは、クエリを指定するだけです。 実行は行いません。 このような方法を "*遅延実行*" といいます。 詳細については、「[LINQ クエリの概要 (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)」を参照してください。

また、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] が生成した SQL コマンドをログに出力します。 <xref:System.Data.Linq.DataContext.Log%2A> を使用したこのログ機能は、デバッグに有効で、データベースに送信されたコマンドが目的のクエリを正確に表しているかどうかを確認するのに役立ちます。

### <a name="to-create-a-simple-query"></a>簡単なクエリを作成するには

- `Sub Main` メソッドの `Table(Of Customer)` 宣言の後に次のコードを入力または貼り付けます。

     [!code-vb[DLinqWalk1AVB#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1AVB/vb/Module1.vb#5)]

## <a name="executing-the-query"></a>クエリの実行

この手順では、実際にクエリを実行します。 ここまでの手順で作成したクエリ式は、結果が必要になるまでは評価されません。 `For Each` の反復処理を開始した時点で、データベースに対して SQL コマンドが実行され、オブジェクトが実体化されます。

### <a name="to-execute-the-query"></a>クエリを実行するには

1. `Sub Main` メソッドの末尾 (クエリ指定の後) に次のコードを入力または貼り付けます。

     [!code-vb[DLinqWalk1AVB#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqWalk1AVB/vb/Module1.vb#6)]

2. F5 キーを押してアプリケーションをデバッグします。

    > [!NOTE]
    > アプリケーションで実行時エラーが発生した場合は、「[チュートリアルによる学習](learning-by-walkthroughs.md)」のトラブルシューティングのセクションを参照してください。

     メッセージ ボックスには 6 人の顧客の一覧が表示されます。 コンソール ウィンドウには生成された SQL コードが表示されます。

3. **[OK]** をクリックしてメッセージ ボックスを閉じます。

     アプリケーションが終了します。

4. **[ファイル]** メニューの **[すべてを保存]** をクリックします。

     引き続き次のチュートリアルに進む場合は、このアプリケーションが必要になります。

## <a name="next-steps"></a>次の手順

「[チュートリアル: リレーションシップ間でクエリを実行する (Visual Basic)](walkthrough-querying-across-relationships-visual-basic.md)」トピックは、このチュートリアルの終了位置から続行します。 「リレーションシップ間でクエリを実行する」のチュートリアルでは、リレーショナル データベースの "*結合*" と同じように、複数のテーブルにまたがったクエリを [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] で行う方法を説明します。

「リレーションシップ間でクエリを実行する」のチュートリアルに進む場合は、必要条件として、ここで完了したチュートリアルのソリューションを保存しておく必要があります。

## <a name="see-also"></a>関連項目

- [チュートリアルによる学習](learning-by-walkthroughs.md)
