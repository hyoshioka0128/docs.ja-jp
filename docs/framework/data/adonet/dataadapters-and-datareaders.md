---
title: DataAdapter と DataReader
description: データベースからデータを取得する ADO.NET DataReader と、データソースからデータを取得してデータセットを設定する DataAdapter について説明します。
ms.date: 03/30/2017
ms.assetid: cc952ca2-ec19-46ab-9189-15174b52cb74
ms.openlocfilehash: 17463d65266baa53521bed9603c8abd96923277b
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286974"
---
# <a name="dataadapters-and-datareaders"></a>DataAdapter と DataReader
ADO.NET の **DataReader** を使用すると、データベースから前方への読み取り専用のストリームを取得できます。 結果はクエリを実行すると返され、**DataReader** の **Read** メソッドを使用して要求するまで、クライアントのネットワーク バッファーに格納されます。 **DataReader** を使用すると、アプリケーションのパフォーマンスが向上します。これは、使用可能になったデータをすぐに取得するためと、一度に 1 つの行しかメモリに格納しない (既定の設定) ことによってシステムのオーバーヘッドが軽減されるためです。  
  
 <xref:System.Data.Common.DataAdapter> は、データ ソースからデータを取得し、1 つの <xref:System.Data.DataSet> 内でテーブルを設定するために使用されます。 また、`DataAdapter` は、`DataSet` に対して加えられた変更をデータ ソースに反映させます。 `DataAdapter` は .NET Framework データ プロバイダーの `Connection` オブジェクトを使用してデータ ソースに接続し、`Command` オブジェクトを使用してデータ ソースからデータを取得し、変更をデータ ソースに反映させます。  
  
 .NET Framework に含まれている各 .NET Framework データ プロバイダーには、<xref:System.Data.Common.DbDataReader> および <xref:System.Data.Common.DbDataAdapter> オブジェクトがあります。.NET Framework Data Provider for OLE DB には <xref:System.Data.OleDb.OleDbDataReader> および <xref:System.Data.OleDb.OleDbDataAdapter> オブジェクトがあります。.NET Framework Data Provider for SQL Server には <xref:System.Data.SqlClient.SqlDataReader> および <xref:System.Data.SqlClient.SqlDataAdapter> オブジェクトがあります。.NET Framework Data Provider for ODBC には、<xref:System.Data.Odbc.OdbcDataReader> および <xref:System.Data.Odbc.OdbcDataAdapter> オブジェクトがあります。.NET Framework Data Provider for Oracle には、<xref:System.Data.OracleClient.OracleDataReader> および <xref:System.Data.OracleClient.OracleDataAdapter> オブジェクトがあります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataReader によるデータの取得](retrieving-data-using-a-datareader.md)  
 ADO.NET の **DataReader** オブジェクトと、それを使用してデータ ソースから結果ストリームを返す方法について説明します。  
  
 [DataAdapter からの DataSet の読み込み](populating-a-dataset-from-a-dataadapter.md)  
 `DataSet` を使用して `DataAdapter` にテーブル、列、および行を設定する方法について説明します。  
  
 [DataAdapter パラメーター](dataadapter-parameters.md)  
 `DataAdapter` のコマンド プロパティのパラメーターを使用する方法と、`DataSet` の列の内容をコマンド パラメーターに割り当てる方法について説明します。  
  
 [DataSet への既存の制約の追加](adding-existing-constraints-to-a-dataset.md)  
 既存の制約を `DataSet` に追加する方法について説明します。  
  
 [DataAdapter DataTable と DataColumn のマップ](dataadapter-datatable-and-datacolumn-mappings.md)  
 `DataTableMappings` の `ColumnMappings` および `DataAdapter` を設定する方法について説明します。  
  
 [クエリ結果のページング](paging-through-a-query-result.md)  
 クエリの結果をデータ ページとして表示する例を示します。  
  
 [DataAdapter によるデータ ソースの更新](updating-data-sources-with-dataadapters.md)  
 `DataAdapter` を使用して `DataSet` の変更内容を解決してデータベースに戻す方法について説明します。  
  
 [DataAdapter のイベント処理](handling-dataadapter-events.md)  
 `DataAdapter` のイベントおよびその使用方法について説明します。  
  
 [DataAdapter を使用したバッチ操作の実行](performing-batch-operations-using-dataadapters.md)  
 `DataSet` から更新を適用する際に、SQL Server へのラウンド トリップ回数を減らすことにより、アプリケーションのパフォーマンスを向上させる方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [データ ソースへの接続](connecting-to-a-data-source.md)
- [コマンドおよびパラメーター](commands-and-parameters.md)
- [トランザクションとコンカレンシー](transactions-and-concurrency.md)
- [DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)
- [ADO.NET の概要](ado-net-overview.md)
