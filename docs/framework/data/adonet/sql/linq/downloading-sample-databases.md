---
title: ADO.NET コード サンプル用のサンプル SQL Server データベースを入手する
description: ADO.NET のドキュメントのコード サンプルで使用されているサンプル SQL Server データベースと、SQL Server および管理ツールをダウンロードします。
ms.date: 01/11/2019
ms.assetid: ef9d69a1-9461-43fe-94bb-7c836754bcb5
ms.openlocfilehash: 3449f502834f449f5023bd52457d45ffaf9b0fa1
ms.sourcegitcommit: d9470d8b2278b33108332c05224d86049cb9484b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81607985"
---
# <a name="get-the-sample-databases-for-adonet-code-samples"></a>ADO.NET コード サンプル用のサンプル データベースを入手する

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] のドキュメントに含まれる多数のサンプルとチュートリアルでは、サンプル SQL Server データベースと SQL Server Express が使用されています。 これらの製品は、Microsoft から無料でダウンロードできます。

## <a name="get-the-northwind-sample-database-for-sql-server"></a>SQL Server 用の Northwind サンプル データベースを入手する

SQL Server 用の Northwind サンプル データベースを作成して読み込むには、次の GitHub リポジトリからスクリプト `instnwnd.sql` をダウンロードします。

[Microsoft SQL Server 用の Northwind および pubs サンプル データベース](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs)

Northwind データベースを使用するには、先に、ダウンロードした `instnwnd.sql` スクリプト ファイルを実行し、[SQL Server Management Studio](#get_ssms) または同様のツールを使用して、SQL Server のインスタンスにデータベースを再作成する必要があります。 リポジトリにある Readme ファイルの手順に従ってください。

> [!TIP]
> Microsoft Access 用の Northwind データベースを探している場合は、「[Microsoft Access 用の Northwind サンプル データベースを入手する](#northwind_access)」をご覧ください。

## <a name="get-the-northwind-sample-database-for-microsoft-access"></a><a name="northwind_access"></a> Microsoft Access 用の Northwind サンプル データベースを入手する

Microsoft Access 用の Northwind サンプル データベースは、Microsoft ダウンロード センターでは入手できません。 Access 内から直接 Northwind をインストールするには、次のようにします。

1. Access を開きます。

1. **[Search for Online Templates]\(オンライン テンプレートの検索\)** ボックスに「**Northwind**」と入力し、**Enter** キーを押します。

1. 結果画面で、**Northwind** を選択します。 新しいウィンドウが開き、Northwind データベースの説明が表示されます。

1. 新しいウィンドウで、 **[ファイル名]** テキスト ボックスに、Northwind データベースの自分のコピーのファイル名を入力します。

1. **[作成]** を選択します。 Access で Northwind データベースがダウンロードされて、ファイルが準備されます。

1. この処理が完了すると、データベースのようこそ画面が開きます。

## <a name="get-the-adventureworks-sample-database-for-sql-server"></a>SQL Server 用の AdventureWorks サンプル データベースを入手する

次の GitHub リポジトリから SQL Server 用の AdventureWorks サンプル データベースをダウンロードします。

[AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)

データベース バックアップ (\*.bak) ファイルの 1 つをダウンロードした後、SQL Server Management Studio (SSMS) を使用して、SQL Server のインスタンスにバックアップを復元します。 「[SQL Server Management Studio を入手する](#get_ssms)」をご覧ください。

## <a name="get-sql-server-management-studio"></a><a name="get_ssms"></a> SQL Server Management Studio を入手する
ダウンロードしたデータベースを表示または変更する場合は、SQL Server Management Studio (SSMS) を使用できます。 次のページから SSMS をダウンロードします。

[SQL Server Management Studio (SSMS) のダウンロード](/sql/ssms/download-sql-server-management-studio-ssms)

Visual Studio 統合開発環境 (IDE) でデータベースを表示して管理することもできます。 [Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019) で、**SQL Server オブジェクト エクスプローラー**からデータベースに接続するか、**サーバー エクスプローラー**でデータベースへのデータ接続を作成します。 これらのエクスプローラー ペインは、 **[表示]** メニューから開きます。

## <a name="get-sql-server-express"></a><a name="get_sql"></a> SQL Server Express を入手する

SQL Server Express は、アプリケーションと共に再頒布できる SQL Server の無料のエントリ レベル エディションです。 次のページから SQL Server Express をダウンロードします。
  
[SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)

[Visual Studio](https://www.visualstudio.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2019) を使用している場合は、Visual Studio の無料の Community エディションおよび Professional 以上のエディションに、SQL Server Express LocalDB が含まれています。  

## <a name="see-also"></a>関連項目

- [はじめに](getting-started.md)
