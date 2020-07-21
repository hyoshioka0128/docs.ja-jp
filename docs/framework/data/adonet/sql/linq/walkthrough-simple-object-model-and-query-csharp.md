---
title: 'チュートリアル: 簡単なオブジェクト モデルとクエリ (C#)'
description: このチュートリアルに従って、サンプル データベース内のテーブルをモデル化するエンティティ クラスを作成します。 その後、シンプルなクエリを作成して、特定の場所にいる顧客を一覧表示します。
ms.date: 03/30/2017
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
ms.openlocfilehash: 4637fabecc1726d8fec12857a667073912cfbed5
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286302"
---
# <a name="walkthrough-simple-object-model-and-query-c"></a>チュートリアル: 簡単なオブジェクト モデルとクエリ (C#)

このチュートリアルでは、複雑さを抑えた、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 全体の基本的なシナリオを示します。 サンプルの Northwind データベースにある Customers テーブルのモデル化を行うエンティティ クラスを作成します。 次に、住所がロンドンの顧客を表示するための簡単なクエリを作成します。

このチュートリアルでは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の考え方を示すために、コード中心の方法をあえて使用しています。 通常は、オブジェクト リレーショナル デザイナーを使用してオブジェクト モデルを作成できます。

[!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]

このチュートリアルは、Visual C# 開発設定を使用して記述されています。

## <a name="prerequisites"></a>必須コンポーネント

- このチュートリアルでは、専用フォルダー ("c:\linqtest5") を使用してファイルを保持します。 チュートリアルを開始する前に、このフォルダーを作成してください。

- このチュートリアルには、Northwind サンプル データベースが必要です。 開発用コンピューターにこのデータベースがない場合は、Microsoft ダウンロード サイトからダウンロードします。 手順については、「[サンプル データベースのダウンロード](downloading-sample-databases.md)」を参照してください。 データベースをダウンロードしたら、ファイルを c:\linqtest5 フォルダーにコピーします。

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

1. Visual Studio の **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** ペインで、 **[Visual C#]** をクリックします。

3. **[テンプレート]** ペインの **[コンソール アプリケーション]** をクリックします。

4. **[名前]** ボックスに「**LinqConsoleApp**」と入力します。

5. **[場所]** ボックスで、プロジェクト ファイルを格納する場所を確認します。

6. **[OK]** をクリックします。

## <a name="adding-linq-references-and-directives"></a>LINQ の参照とディレクティブを追加する

このチュートリアルで使用するアセンブリは、既定ではプロジェクトにインストールされていない場合があります。 System.Data.Linq がプロジェクトの参照 (**ソリューション エクスプローラー**で **[参照]** ノードを展開) に表示されていない場合は、以下の手順に従って追加します。

### <a name="to-add-systemdatalinq"></a>System.Data.Linq を追加するには

1. **ソリューション エクスプローラー**で、 **[参照設定]** を右クリックし、 **[参照の追加]** をクリックします。

2. **[参照の追加]** ダイアログ ボックスで、 **[.NET]** をクリックし、System.Data.Linq アセンブリをクリックします。次に、 **[OK]** をクリックします。

     アセンブリがプロジェクトに追加されます。

3. **Program.cs** の先頭に、次のディレクティブを追加します。

     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]

## <a name="mapping-a-class-to-a-database-table"></a>データベース テーブルにクラスを対応付ける

この手順では、クラスを作成して、データベース テーブルに対応付けます。 このようなクラスのことを "*エンティティ クラス*" と呼びます。 対応付けは、<xref:System.Data.Linq.Mapping.TableAttribute> 属性を追加するだけで完了します。 <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> プロパティを使用して、データベースのテーブルの名前を指定します。

### <a name="to-create-an-entity-class-and-map-it-to-a-database-table"></a>エンティティ クラスを作成し、データベース テーブルに対応付けるには

- Program.cs の `Program` クラス宣言の直前に次のコードを入力または貼り付けます。

     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]

## <a name="designating-properties-on-the-class-to-represent-database-columns"></a>データベース列を表すプロパティをクラスに追加する

この手順では、いくつかのタスクを実行します。

- <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性を使用して、エンティティ クラスの `CustomerID` プロパティおよび `City` プロパティを、データベース テーブルの列を表すものとして指定します。

- `CustomerID` プロパティを、データベースの主キー列を表すものとして指定します。

- プライベートでの格納用として `_CustomerID` フィールドおよび `_City` フィールドを指定します。 これで、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、ビジネス ロジックを含む場合があるパブリック アクセサーを使用せずに、値を直接格納および取得できます。

### <a name="to-represent-characteristics-of-two-database-columns"></a>2 つのデータベース列の特性を指定するには

- Program.cs の `Customer` クラスの中かっこ内に次のコードを入力または貼り付けます。

     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]

## <a name="specifying-the-connection-to-the-northwind-database"></a>Northwind データベースへの接続を指定する

この手順では、<xref:System.Data.Linq.DataContext> オブジェクトを使用して、コードで作成したデータ構造とデータベース本体との間の接続を確立します。 データベースからのオブジェクトの取得や、変更内容の送信では、<xref:System.Data.Linq.DataContext> を仲介役として使用します。

また、データベースの Customers テーブルに対するクエリ用として、型指定された論理的なテーブルの役割を果たす `Table<Customer>` を宣言します。 これらのクエリの作成と実行は後の手順で行います。

### <a name="to-specify-the-database-connection"></a>データベース接続を指定するには

- `Main` メソッドに次のコードを入力または貼り付けます。

     `northwnd.mdf` ファイルは、linqtest5 フォルダーにあるものとします。 詳細については、このチュートリアルの「前提条件」を参照してください。

     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]

## <a name="creating-a-simple-query"></a>簡単なクエリの作成

この手順では、データベースの Customers テーブルから、住所が London の顧客を検索するクエリを作成します。 この手順で作成するクエリ コードは、クエリを指定するだけです。 実行は行いません。 このような方法を "*遅延実行*" といいます。 詳細については、「[LINQ クエリの概要 (C#)](../../../../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md)」を参照してください。

また、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] が生成した SQL コマンドをログに出力します。 <xref:System.Data.Linq.DataContext.Log%2A> を使用したこのログ機能は、デバッグに有効で、データベースに送信されたコマンドが目的のクエリを正確に表しているかどうかを確認するのに役立ちます。

### <a name="to-create-a-simple-query"></a>簡単なクエリを作成するには

- `Main` メソッドの `Table<Customer>` 宣言の後に次のコードを入力または貼り付けます。

     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]

## <a name="executing-the-query"></a>クエリの実行

この手順では、実際にクエリを実行します。 ここまでの手順で作成したクエリ式は、結果が必要になるまでは評価されません。 `foreach` の反復処理を開始した時点で、データベースに対して SQL コマンドが実行され、オブジェクトが実体化されます。

### <a name="to-execute-the-query"></a>クエリを実行するには

1. `Main` メソッドの末尾 (クエリ指定の後) に次のコードを入力または貼り付けます。

     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]

2. F5 キーを押してアプリケーションをデバッグします。

    > [!NOTE]
    > アプリケーションで実行時エラーが発生した場合は、「[チュートリアルによる学習](learning-by-walkthroughs.md)」のトラブルシューティングのセクションを参照してください。

     クエリの結果は、以下のようにコンソール ウィンドウに表示されます。

     `ID=AROUT, City=London`

     `ID=BSBEV, City=London`

     `ID=CONSH, City=London`

     `ID=EASTC, City=London`

     `ID=NORTS, City=London`

     `ID=SEVES, City=London`

3. コンソール ウィンドウで Enter キーを押してアプリケーションを終了します。

## <a name="next-steps"></a>次の手順

「[チュートリアル: リレーションシップ間でクエリを実行する (C#)](walkthrough-querying-across-relationships-csharp.md)」トピックは、このチュートリアルの終了位置から続行します。 「リレーションシップ間でクエリを実行する」のチュートリアルでは、リレーショナル データベースの "*結合*" と同じように、複数のテーブルにまたがったクエリを [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] で行う方法を説明します。

「リレーションシップ間でクエリを実行する」のチュートリアルに進む場合は、必要条件として、ここで完了したチュートリアルのソリューションを保存しておく必要があります。

## <a name="see-also"></a>関連項目

- [チュートリアルによる学習](learning-by-walkthroughs.md)
