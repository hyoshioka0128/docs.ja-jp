---
title: SQL Server データ型のマッピング
description: SQL Server と .NET Framework の異なる型システム間のマッピングについて説明します。 この記事では、ADO.NET でシステムがやり取りする方法をまとめています。
ms.date: 03/30/2017
ms.assetid: fafdc31a-f435-4cd3-883f-1dfadd971277
ms.openlocfilehash: 83be217a69f912047360cd097db702e4a95a6512
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286586"
---
# <a name="sql-server-data-type-mappings"></a>SQL Server データ型のマッピング
SQL Server と .NET Framework は異なる型システムを使用しています。 たとえば、.NET Framework の <xref:System.Decimal> 構造体の最大小数点以下桁数は 28 ですが、SQL Server の decimal データ型と numeric データ型の最大小数点以下桁数は 38 です。 データを読み書きするときにデータの整合性を保つために、<xref:System.Data.SqlClient.SqlDataReader> では、.NET Framework の型を返すアクセサー メソッドと共に、<xref:System.Data.SqlTypes> のオブジェクトを返す SQL Server 固有の型指定されたアクセサー メソッドを公開しています。 SQL Server の型と .NET Framework の型は、両方とも <xref:System.Data.DbType> および <xref:System.Data.SqlDbType> クラスの列挙によって表されます。これらは <xref:System.Data.SqlClient.SqlParameter> データ型を指定するときに使用できます。  
  
 推論される .NET Framework 型、<xref:System.Data.DbType> 列挙型と <xref:System.Data.SqlDbType> 列挙型、<xref:System.Data.SqlClient.SqlDataReader> のアクセサー メソッドを、次の表に示します。  
  
|SQL Server データベース エンジンの型|.NET Framework 型|SqlDbType 列挙|SqlDataReader SqlTypes の型指定されたアクセサー|DbType 列挙|SqlDataReader DbType の型指定されたアクセサー|  
|-------------------------------------|-------------------------|---------------------------|-------------------------------------------|------------------------|-----------------------------------------|  
|bigint|Int64|<xref:System.Data.SqlDbType.BigInt>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt64%2A>|<xref:System.Data.DbType.Int64>|<xref:System.Data.SqlClient.SqlDataReader.GetInt64%2A>|  
|バイナリ|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|bit|ブール型|<xref:System.Data.SqlDbType.Bit>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBoolean%2A>|<xref:System.Data.DbType.Boolean>|<xref:System.Data.SqlClient.SqlDataReader.GetBoolean%2A>|  
|char|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.Char>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.AnsiStringFixedLength>、<br /><br /> <xref:System.Data.DbType.String>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|date <sup>1</sup><br /><br /> (SQL Server 2008 以降)|DateTime|<xref:System.Data.SqlDbType.Date> <sup>1</sup>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.Date> <sup>1</sup>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime|DateTime|<xref:System.Data.SqlDbType.DateTime>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.DateTime>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetime2<br /><br /> (SQL Server 2008 以降)|DateTime|<xref:System.Data.SqlDbType.DateTime2>|None|<xref:System.Data.DbType.DateTime2>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|datetimeoffset<br /><br /> (SQL Server 2008 以降)|DateTimeOffset|<xref:System.Data.SqlDbType.DateTimeOffset>|none|<xref:System.Data.DbType.DateTimeOffset>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|  
|decimal|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|FILESTREAM 属性 (varbinary(max))|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBytes%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|float|Double|<xref:System.Data.SqlDbType.Float>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDouble%2A>|<xref:System.Data.DbType.Double>|<xref:System.Data.SqlClient.SqlDataReader.GetDouble%2A>|  
|イメージ|Byte[]|<xref:System.Data.SqlDbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|int|Int32|<xref:System.Data.SqlDbType.Int>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt32%2A>|<xref:System.Data.DbType.Int32>|<xref:System.Data.SqlClient.SqlDataReader.GetInt32%2A>|  
|money|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Money>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NChar>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.StringFixedLength>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|ntext|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NText>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|数値|Decimal (10 進数型)|<xref:System.Data.SqlDbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDecimal%2A>|<xref:System.Data.DbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|nvarchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.NVarChar>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|実数|Single|<xref:System.Data.SqlDbType.Real>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlSingle%2A>|<xref:System.Data.DbType.Single>|<xref:System.Data.SqlClient.SqlDataReader.GetFloat%2A>|  
|rowversion|Byte[]|<xref:System.Data.SqlDbType.Timestamp>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|smalldatetime|DateTime|<xref:System.Data.SqlDbType.DateTime>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlDateTime%2A>|<xref:System.Data.DbType.DateTime>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|smallint|Int16|<xref:System.Data.SqlDbType.SmallInt>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlInt16%2A>|<xref:System.Data.DbType.Int16>|<xref:System.Data.SqlClient.SqlDataReader.GetInt16%2A>|  
|smallmoney|Decimal (10 進数型)|<xref:System.Data.SqlDbType.SmallMoney>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlMoney%2A>|<xref:System.Data.DbType.Decimal>|<xref:System.Data.SqlClient.SqlDataReader.GetDecimal%2A>|  
|sql_variant|Object <sup>2</sup>|<xref:System.Data.SqlDbType.Variant>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A> <sup>2</sup>|<xref:System.Data.DbType.Object>|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A> <sup>2</sup>|  
|テキスト|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.Text>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.String>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|時間<br /><br /> (SQL Server 2008 以降)|TimeSpan|<xref:System.Data.SqlDbType.Time>|none|<xref:System.Data.DbType.Time>|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|  
|タイムスタンプ|Byte[]|<xref:System.Data.SqlDbType.Timestamp>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|tinyint|Byte|<xref:System.Data.SqlDbType.TinyInt>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlByte%2A>|<xref:System.Data.DbType.Byte>|<xref:System.Data.SqlClient.SqlDataReader.GetByte%2A>|  
|uniqueidentifier|GUID|<xref:System.Data.SqlDbType.UniqueIdentifier>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlGuid%2A>|<xref:System.Data.DbType.Guid>|<xref:System.Data.SqlClient.SqlDataReader.GetGuid%2A>|  
|varbinary|Byte[]|<xref:System.Data.SqlDbType.VarBinary>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlBinary%2A>|<xref:System.Data.DbType.Binary>|<xref:System.Data.SqlClient.SqlDataReader.GetBytes%2A>|  
|varchar|String<br /><br /> Char[]|<xref:System.Data.SqlDbType.VarChar>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|<xref:System.Data.DbType.AnsiString>、<xref:System.Data.DbType.String>|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A><br /><br /> <xref:System.Data.SqlClient.SqlDataReader.GetChars%2A>|  
|xml|Xml|<xref:System.Data.SqlDbType.Xml>|<xref:System.Data.SqlClient.SqlDataReader.GetSqlXml%2A>|<xref:System.Data.DbType.Xml>|none|  
  
<sup>1</sup> `SqlParameter` の `DbType` プロパティを `SqlDbType.Date` に設定することはできません。  
<sup>2</sup> `sql_variant` の基になる型がわかっている場合は、特定の型指定されたアクセサーを使用してください。  
  
## <a name="sql-server-documentation"></a>SQL Server ドキュメント

SQL Server のデータ型について詳しくは、「[データ型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)」をご覧ください。
  
## <a name="see-also"></a>関連項目

- [SQL Server データ型と ADO.NET](./sql/sql-server-data-types.md)
- [SQL Server のバイナリ データと大きな値のデータ](./sql/sql-server-binary-and-large-value-data.md)
- [ADO.NET でのデータ型のマッピング](data-type-mappings-in-ado-net.md)
- [パラメーターおよびパラメーター データ型の構成](configuring-parameters-and-parameter-data-types.md)
- [ADO.NET の概要](ado-net-overview.md)
