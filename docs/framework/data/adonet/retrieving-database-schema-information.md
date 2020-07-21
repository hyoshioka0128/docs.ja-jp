---
title: データベース スキーマ情報の取得
ms.date: 03/30/2017
ms.assetid: 79038d52-f122-4fd4-9bfb-aaa22d6a114b
ms.openlocfilehash: 26b234e35a0d0849914d87b61f4e8c8a87599448
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70782729"
---
# <a name="retrieving-database-schema-information"></a>データベース スキーマ情報の取得
データベースからのスキーマ情報の取得は、スキーマの検出プロセスによって行われます。 スキーマの検出により、アプリケーションでは、特定のデータベースのデータベース スキーマ ("*メタデータ*" とも呼ばれます) に関する情報を検索して返すように、マネージド プロバイダーに要求できます。 テーブル、列、ストアド プロシージャなどの各種のデータベース スキーマ要素は、スキーマ コレクションを通じて公開されます。 各スキーマ コレクションには、使用されているプロバイダーに固有の各種のスキーマ情報が含まれています。  
  
 各 .NET Framework マネージド プロバイダーでは、**Connection** クラスの **GetSchema** メソッドが実装されていて、**GetSchema** メソッドから返されるスキーマ情報は、<xref:System.Data.DataTable> という形式になります。 **GetSchema** メソッドはオーバーロードされたメソッドであり、オプションのパラメーターで、取得するスキーマ コレクションを指定し、返される情報の量を制限することができます。  
  
 OLE DB、ODBC、Oracle、SqlClient 用の .NET Framework データ プロバイダーで提供されている **GetSchemaTable** メソッドでは、**DataReader** の列のメタデータを表す DataTable が返されます。  
  
 .NET Framework Data Provider for OLE DB では、<xref:System.Data.OleDb.OleDbConnection.GetOleDbSchemaTable%2A> オブジェクトの <xref:System.Data.OleDb.OleDbConnection> メソッドを使ってスキーマ情報を公開します。 **GetOleDbSchemaTable** は、引数として、返すスキーマ情報を識別する <xref:System.Data.OleDb.OleDbSchemaGuid> と、返された列に対する制限の配列を受け取ります。 **GetOleDbSchemaTable** では、要求したスキーマ情報が格納されている <xref:System.Data.DataTable> が返されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [GetSchema およびスキーマ コレクション](getschema-and-schema-collections.md)  
 **GetSchema** メソッドと、このメソッドを使ってデータベースからスキーマ情報を取得して制限する方法について説明します。  
  
 スキーマの制限  
 **GetSchema** で使用できるスキーマの制限について説明します。  
  
 [共通のスキーマ コレクション](common-schema-collections.md)  
 すべての .NET Framework マネージド プロバイダーでサポートされる共通のスキーマ コレクションについて説明します。  
  
 [SQL Server スキーマ コレクション](sql-server-schema-collections.md)  
 .NET Framework Provider for SQL Server でサポートされるスキーマ コレクションについて説明します。  
  
 [Oracle スキーマ コレクション](oracle-schema-collections.md)  
 .NET Framework Provider for Oracle でサポートされるスキーマ コレクションについて説明します。  
  
 [ODBC スキーマ コレクション](odbc-schema-collections.md)  
 ODBC ドライバーのスキーマ コレクションについて説明します。  
  
 [OLE DB スキーマ コレクション](ole-db-schema-collections.md)  
 OLE DB プロバイダーのスキーマ コレクションについて説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.Data.Common.DbConnection.GetSchema%2A>  
 <xref:System.Data.Common.DbConnection> クラスの **GetSchema** メソッドについて説明します。  
  
 <xref:System.Data.Odbc.OdbcConnection.GetSchema%2A>  
 <xref:System.Data.Odbc.OdbcConnection> クラスの **GetSchema** メソッドについて説明します。  
  
 <xref:System.Data.OleDb.OleDbConnection.GetSchema%2A>  
 <xref:System.Data.OleDb.OleDbConnection> クラスの **GetSchema** メソッドについて説明します。  
  
 <xref:System.Data.OracleClient.OracleConnection.GetSchema%2A>  
 <xref:System.Data.OracleClient.OracleConnection> クラスの **GetSchema** メソッドについて説明します。  
  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>  
 <xref:System.Data.SqlClient.SqlConnection> クラスの **GetSchema** メソッドについて説明します。  
  
 <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
 <xref:System.Data.Common.DbDataReader> クラスの **GetSchemaTable** メソッドについて説明します。  
  
 <xref:System.Data.Odbc.OdbcDataReader.GetSchemaTable%2A>  
 <xref:System.Data.Odbc.OdbcDataReader> クラスの **GetSchemaTable** メソッドについて説明します。  
  
 <xref:System.Data.OleDb.OleDbDataReader.GetSchemaTable%2A>  
 <xref:System.Data.OleDb.OleDbDataReader> クラスの **GetSchemaTable** メソッドについて説明します。  
  
 <xref:System.Data.OracleClient.OracleDataReader.GetSchemaTable%2A>  
 <xref:System.Data.OracleClient.OracleDataReader> クラスの **GetSchemaTable** メソッドについて説明します。  
  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
 <xref:System.Data.SqlClient.SqlDataReader> クラスの **GetSchemaTable** メソッドについて説明します。  
  
## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [ADO.NET の概要](ado-net-overview.md)
