---
title: コマンドおよびパラメーター
description: 各 .NET Framework データ プロバイダーの Command オブジェクトを使用してコマンドを実行し、データ ソースからの結果を返す方法について説明します。
ms.date: 03/30/2017
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.openlocfilehash: c0baec4d6c3984cb50178c3aa7f9ed3878055bb6
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287143"
---
# <a name="commands-and-parameters"></a>コマンドおよびパラメーター
データ ソースへの接続を確立した後、<xref:System.Data.Common.DbCommand> オブジェクトを使用してコマンドを実行し、データ ソースから結果を返すことができます。 コマンドは、使用している .NET Framework データ プロバイダーのいずれかのコマンド コンストラクターで作成できます。 コンストラクターには、データ ソースで実行する SQL ステートメント、<xref:System.Data.Common.DbConnection> オブジェクト、<xref:System.Data.Common.DbTransaction> オブジェクトなど、オプションの引数を渡すことができます。 これらのオブジェクトをコマンドのプロパティとして構成することもできます。 また、<xref:System.Data.Common.DbConnection.CreateCommand%2A> オブジェクトの `DbConnection` メソッドを使用して、特定の接続用のコマンドを作成することもできます。 コマンドによって実行される SQL ステートメントは、<xref:System.Data.Common.DbCommand.CommandText%2A> プロパティを使って構成できます。  
  
 .NET Framework に含まれている各 .NET Framework データ プロバイダーは、`Command` オブジェクトを持ちます。 .NET Framework Data Provider for OLE DB には <xref:System.Data.OleDb.OleDbCommand> オブジェクト、.NET Framework Data Provider for SQL Server には <xref:System.Data.SqlClient.SqlCommand> オブジェクト、.NET Framework Data Provider for ODBC には <xref:System.Data.Odbc.OdbcCommand> オブジェクト、.NET Framework Data Provider for Oracle には <xref:System.Data.OracleClient.OracleCommand> があります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [コマンドの実行](executing-a-command.md)  
 ADO.NET の `Command` オブジェクトと、それを使用してデータ ソースに対してクエリやコマンドを実行する方法について説明します。  
  
 [パラメーターおよびパラメーター データ型の構成](configuring-parameters-and-parameter-data-types.md)  
 `Command` のパラメーターの使用 (方向、データ型、パラメーター構文など) について説明します。  
  
 [CommandBuilder でのコマンドの生成](generating-commands-with-commandbuilders.md)  
 `DataAdapter` に単一テーブルを対象とする SELECT コマンドが割り当てられているときに、コマンド ビルダーを使用して INSERT、UPDATE、DELETE の各コマンドを自動的に生成する方法について説明します。  
  
 [データベースからの単一の値の取得](obtaining-a-single-value-from-a-database.md)  
 `ExecuteScalar` オブジェクトの `Command` メソッドを使用してデータベース クエリから単一の値を返す方法について説明します。  
  
 [コマンドを使用したデータ変更](using-commands-to-modify-data.md)  
 データ プロバイダーを使用して、ストアド プロシージャまたはデータ定義言語 (DDL) のステートメントを実行する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [DataSet、DataTable、および DataView](./dataset-datatable-dataview/index.md)
- [データ ソースへの接続](connecting-to-a-data-source.md)
- [ADO.NET の概要](ado-net-overview.md)
