---
title: 日付と時刻のデータ
description: .NET Framework Data Provider for SQL Server で日付と時刻の情報を処理するためのデータ型について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.openlocfilehash: 9345e995dcb1179e7d0a86f62737f9fda5889f42
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286495"
---
# <a name="date-and-time-data"></a>日付と時刻のデータ
SQL Server 2008 では、日付と時刻の情報を扱うための新しいデータ型が導入されました。 新しいデータ型には、日付と時刻の別個のデータ型と、範囲、有効桁数、タイム ゾーン処理が向上した拡張データ型が含まれています。 .NET Framework 3.5 Service Pack (SP) 1 以降では、.NET Framework Data Provider for SQL Server (<xref:System.Data.SqlClient>) が SQL Server 2008 データベース エンジンの新機能すべてをサポートします。 SqlClient でこれらの新機能を使用するには、.NET Framework 3.5 SP1 以降をインストールする必要があります。  
  
 SQL Server 2008 より前のバージョンの SQL Server では、日付と時刻に使用できるデータ型には `datetime` と `smalldatetime` の 2 つしかありませんでした。 どちらのデータ型も日付値と時刻値の両方を保持するため、日付と時刻のどちらか一方の値のみを使用するのが困難でした。 さらに、これらのデータ型では、1753 年に英国でグレゴリオ暦が導入された後の日付のみがサポートされます。 もう 1 つの制限事項は、これらの古いデータ型がタイムゾーンに対応していないことです。これにより、複数のタイムゾーンからのデータの操作が困難になります。  
  
 SQL Server のデータ型に関する完全な説明は、SQL Server オンライン ブックに記載されています。 次の表は、バージョン別の日付と時刻のデータに関する初歩的なトピックの一覧です。  
  
 **SQL Server のドキュメント**  
  
1. [日時データの使用](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))  
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>SQL Server 2008 で導入された日付/時刻データ型  
 次の表は、新しい日付と時刻のデータ型の説明です。  
  
|SQL Server のデータ型|説明|  
|--------------------------|-----------------|  
|`date`|データ型 `date` の範囲は 01 年 1 月 1 日から 9999 年 12 月 31 日までで、精度は 1 日です。 既定値は 1900 年 1 月 1 日です。 記憶領域のサイズは 3 バイトです。|  
|`time`|`time` データ型は、24 時間形式で時刻値のみを格納します。 `time` データ型は、00:00:00.0000000 から 23:59:59.9999999 の範囲で、100 ナノ秒の精度です。 既定値は 00:00: 00.0000000 (午前 0 時) です。 `time` データ型はユーザー定義による 1 秒未満の時間の有効桁数をサポートし、記憶領域のサイズは、指定された有効桁数に応じて 3 バイト～ 6 バイトになります。|  
|`datetime2`|`datetime2` データ型では、`date` データ型と `time` データ型の範囲と精度が 1 つのデータ型に結合されます。<br /><br /> 既定値と文字列リテラルの形式は、`date` データ型および `time` データ型で定義されているものと同じです。|  
|`datetimeoffset`|`datetimeoffset` データ型は、`datetime2` のすべての機能に加えて、タイム ゾーン オフセットを持ちます。 タイム ゾーン オフセットは、[+&#124;-] HH:MM として表されます。 HH は、タイム ゾーン オフセットの時間数を表す 00 ～ 14 の 2 桁の数字です。 MM は、タイム ゾーン オフセットの付加的な分数を表す 0 ～ 59 の 2 桁の数字です。 時刻の精度は 100 ナノ秒までサポートされます。 必須の + または - 記号は、ローカル時刻を取得するために、UTC (協定世界時またはグリニッジ標準時) からタイム ゾーン オフセットを加算するか減算するかを示します。|  
  
> [!NOTE]
> `Type System Version` キーワードの使用方法の詳細については、「<xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>」を参照してください。  
  
## <a name="date-format-and-date-order"></a>日付書式と表記順序  
 SQL Server が日付と時刻の値をどのように処理するかは、型システムのバージョンとサーバーのバージョンだけでなく、サーバーの既定の言語と書式設定にも左右されます。 ある言語の日付形式に対して機能する日付文字列は、別の言語および日付形式の設定を使用する接続によってクエリが実行された場合に認識されない可能性があります。  
  
 Transact-SQL SET LANGUAGE ステートメントでは、日付部分の順序を決定する DATEFORMAT を暗黙的に設定します。 接続に対して SET DATEFORMAT Transact-SQL ステートメントを使用して、MDY、DMY、YMD、YDM、MYD、DYM の順序で日付部分を並べ替えることにより、日付値を明確にすることができます。  
  
 接続に対して DATEFORMAT を指定しない場合、SQL Server では接続に関連付けられている既定の言語が使用されます。 たとえば、' 01/02/03' の日付文字列は、米国英語の言語設定のサーバーでは MDY (2003 年 1 月 2 日) として解釈され、英国英語の言語設定のサーバーでは DMY (2003 年 2 月 1 日) として解釈されます。 年は、SQL Server の終了年の規則に従って決定されます。この規則では、世紀の値を割り当てるための終了日が定義されます。 詳しくは、「[two digit year cutoff オプション](/sql/database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option)」をご覧ください。  
  
> [!NOTE]
> YDM 日付書式は、文字列形式から `date`、`time`、`datetime2`、または `datetimeoffset` に変換する場合にはサポートされません。  
  
 SQL Server による日付と時刻のデータの解釈方法について詳しくは、「[日時データの使用](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))」をご覧ください。  
  
## <a name="datetime-data-types-and-parameters"></a>Date/Time データ型とパラメーター  
 新しい日付型と時刻型をサポートするために、<xref:System.Data.SqlDbType> には、次の列挙値が追加されています。  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

<xref:System.Data.SqlClient.SqlParameter> のデータ型は、前の <xref:System.Data.SqlDbType> 列挙型のいずれかの値を使って指定できます。

> [!NOTE]
> `SqlParameter` の `DbType` プロパティは `SqlDbType.Date` に設定できません。

 <xref:System.Data.SqlClient.SqlParameter> オブジェクトの <xref:System.Data.SqlClient.SqlParameter.DbType%2A> プロパティを特定の `SqlParameter` 列挙値に設定することによって、<xref:System.Data.DbType> の型をジェネリックに指定することもできます。 <xref:System.Data.DbType> データ型と `datetime2` データ型をサポートするために、`datetimeoffset` には、次の列挙値が追加されています。  
  
- DbType.DateTime2  
  
- DbType.DateTimeOffset  
  
 これらの新しい列挙値は、以前のバージョンの .NET Framework に存在した `Date`、`Time`、および `DateTime` の各列挙値を補います。  
  
 パラメーター オブジェクトの .NET Framework データ プロバイダー型は、パラメーター オブジェクトの値の .NET Framework 型か、またはパラメーター オブジェクトの `DbType` から推論されます。 新しい date 型と time 型をサポートするための新しい <xref:System.Data.SqlTypes> データ型は導入されていません。 次の表に、SQL Server 2008 の日付と時刻のデータ型と CLR データ型のマッピングについて説明します。  
  
|SQL Server のデータ型|.NET Framework 型|System.Data.SqlDbType|System.Data.DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|date|System.DateTime|Date|Date|  
|時間|System.TimeSpan|時刻|時刻|  
|datetime2|System.DateTime|DateTime2|DateTime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|datetime|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>SqlParameter プロパティ  
 次の表は、日付と時刻のデータ型に関係する `SqlParameter` プロパティの説明です。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|<xref:System.Data.SqlClient.SqlParameter.IsNullable%2A>|値が null 許容であるかどうかを取得または設定します。 サーバーに NULL パラメーター値を送る場合は、<xref:System.DBNull> (Visual Basic の場合は `null`) ではなく、`Nothing` を指定する必要があります。 データベースの NULL 値の詳細については、「 [Handling Null Values](handling-null-values.md)」を参照してください。|  
|<xref:System.Data.SqlClient.SqlParameter.Precision%2A>|その値の最大桁数を取得または設定します。 この設定は日付と時刻のデータ型では無視されます。|  
|<xref:System.Data.SqlClient.SqlParameter.Scale%2A>|小数点以下の桁数を取得または設定します。これは `Time`、`DateTime2`、`DateTimeOffset` の時刻部分の値の処理で使用されます。 既定値は 0 で、これは実際のスケールが値から推論され、サーバーに送信されることを意味します。|  
|<xref:System.Data.SqlClient.SqlParameter.Size%2A>|日付と時刻のデータ型では無視されます。|  
|<xref:System.Data.SqlClient.SqlParameter.Value%2A>|パラメーター値を取得または設定します。|  
|<xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>|パラメーター値を取得または設定します。|  
  
> [!NOTE]
> 時刻の値が 0 と 24 の間にない場合は、<xref:System.ArgumentException> がスローされます。  
  
### <a name="creating-parameters"></a>パラメーターの作成  
 <xref:System.Data.SqlClient.SqlParameter> オブジェクトは、そのコンストラクターを使って作成できるほか、<xref:System.Data.SqlClient.SqlCommand> の <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> メソッドを呼び出して、`Add`<xref:System.Data.SqlClient.SqlParameterCollection> コレクションにそれを追加することによって作成することもできます。 `Add` メソッドは、入力としてコンストラクター引数または既存のパラメーター オブジェクトを受け取ります。  
  
 このトピックの次のセクションでは、日付と時刻のパラメーターを指定する方法の例を示します。 パラメーターの使用に関するその他の例については、「[パラメーターおよびパラメーター データ型の構成](../configuring-parameters-and-parameter-data-types.md)」および「[DataAdapter パラメーター](../dataadapter-parameters.md)」をご覧ください。  
  
### <a name="date-example"></a>Date の例  
 次のコード フラグメントは、`date` パラメーターの指定方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Date"  
parameter.SqlDbType = SqlDbType.Date  
parameter.Value = "2007/12/1"  
```  
  
### <a name="time-example"></a>Time の例  
 次のコード フラグメントは、`time` パラメーターの指定方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Time"  
parameter.SqlDbType = SqlDbType.Time  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Datetime2 の例  
 次のコード フラグメントは、`datetime2` パラメーターの日付と時刻の指定方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@Datetime2"  
parameter.SqlDbType = SqlDbType.DateTime2  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>DateTimeOffSet の例  
 次のコード フラグメントは、`DateTimeOffSet` パラメーターの日付と時刻、およびタイム ゾーン オフセット 0 を指定する方法を示しています。  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
```vb  
Dim parameter As New SqlParameter()  
parameter.ParameterName = "@DateTimeOffSet"  
parameter.SqlDbType = SqlDbType.DateTimeOffSet  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>AddWithValue  
 次のコード フラグメントに示すように、<xref:System.Data.SqlClient.SqlCommand> の `AddWithValue` メソッドを使用してパラメーターを指定することもできます。 ただし、`AddWithValue` メソッドでは、パラメーターの <xref:System.Data.SqlClient.SqlParameter.DbType%2A> または <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> を指定することはできません。  
  
```csharp  
command.Parameters.AddWithValue(
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
```vb  
command.Parameters.AddWithValue( _  
    "@date", DateTimeOffset.Parse("16660902"))  
```  
  
 `@date` パラメーターは、サーバー上の `date`、`datetime`、または `datetime2` データ型にマッピングできます。 新しい `datetime` データ型を使用する場合は、パラメーターの <xref:System.Data.SqlDbType> プロパティをインスタンスのデータ型に明示的に設定する必要があります。 <xref:System.Data.SqlDbType.Variant> を使用するか、または暗黙的にパラメーター値を指定すると、`datetime` データ型および `smalldatetime` データ型との下位互換性の問題が発生する可能性があります。  
  
 次の表は、どの CLR 型からどの `SqlDbTypes` が推論されるかを示しています。  
  
|CLR 型|推定される SqlDbType|  
|--------------|------------------------|  
|DateTime|SqlDbType.DateTime|  
|TimeSpan|SqlDbType.Time|  
|DateTimeOffset|SqlDbType.DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>日付と時刻データの取得  
 SQL Server 2008 の日付値および時刻値を取得するためのメソッドを次の表に示します。  
  
|SqlClient のメソッド|説明|  
|----------------------|-----------------|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTime%2A>|指定された列の値を <xref:System.DateTime> 構造体として取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|指定された列の値を <xref:System.DateTimeOffset> 構造体として取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|そのフィールドの基になるプロバイダー固有の型である型を返します。 新しい日付と時刻の型に対して `GetFieldType` と同じ型を返します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|指定された列の値を取得します。 新しい日付と時刻の型に対して `GetValue` と同じ型を返します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|指定した配列内の値を取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlString%2A>|列の値を <xref:System.Data.SqlTypes.SqlString> として取得します。 データを `SqlString` として表現できない場合、<xref:System.InvalidCastException> が発生します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|列データをその既定の `SqlDbType` として取得します。 新しい日付と時刻の型に対して `GetValue` と同じ型を返します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|指定した配列内の値を取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetString%2A>|Type System Version が SQL Server 2005 に設定されている場合、列の値を文字列として取得します。 データを文字列として表現できない場合、<xref:System.InvalidCastException> が発生します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|指定された列の値を <xref:System.TimeSpan> 構造体として取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValue%2A>|指定した列の値を、その基になる CLR 型として取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetValues%2A>|配列内の列の値を取得します。|  
|<xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|結果セットのメタデータを記述する <xref:System.Data.DataTable> を返します。|  
  
> [!NOTE]
> 新しい日付と時刻の `SqlDbTypes` は、SQL Server でインプロセスで実行されているコードではサポートされていません。 そのような型の 1 つがサーバーに渡されると、例外が発生します。  
  
## <a name="specifying-date-and-time-values-as-literals"></a>日付値と時刻値のリテラル指定  
 日付と時刻のデータ型は、さまざまなリテラル文字列形式を使用して指定できます。SQL Server は、実行時にそれらを内部の日付/時刻構造体に変換します。 SQL Server では、一重引用符 (') で囲まれた日付と時刻のデータが認識されます。 次の例に、いくつかの形式を示します。  
  
- アルファベットの日付形式 (`'October 15, 2006'` など)。  
  
- 数値の日付形式 (`'10/15/2006'`など)。  
  
- 区切られていない文字列形式 (`'20061015'` など。これは ISO 標準日付形式を使用している場合、2006 年 10 月 15 日と解釈される)。  
  
> [!NOTE]
> すべてのリテラル文字列形式と、日付と時刻のデータ型のその他の機能に関する完全なドキュメントについては、SQL Server オンライン ブックを参照してください。  
  
 時刻の値が 0 と 24 の間にない場合は、<xref:System.ArgumentException> がスローされます。  
  
## <a name="resources-in-sql-server-books-online"></a>SQL Server オンライン ブックの関連トピック  
 SQL Server での日付値と時刻値の使用方法の詳細については、SQL Server オンライン ブックで以下のリソースを参照してください。  
  
|トピック|説明|  
|-----------|-----------------|  
|[日付と時刻のデータ型および関数 (Transact-SQL)](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|Transact-SQL の日付と時刻のデータ型および関数の概要について説明します。|  
|[日時データの使用](https://docs.microsoft.com/previous-versions/sql/sql-server-2008/ms180878(v=sql.100))|日付と時刻のデータ型と関数の情報、および使用例を示します。|  
|[データ型 (Transact-SQL)](/sql/t-sql/data-types/data-types-transact-sql)|SQL Server でのシステム データ型について説明します。|  
  
## <a name="see-also"></a>関連項目

- [SQL Server データ型のマッピング](../sql-server-data-type-mappings.md)
- [パラメーターおよびパラメーター データ型の構成](../configuring-parameters-and-parameter-data-types.md)
- [SQL Server データ型と ADO.NET](sql-server-data-types.md)
- [ADO.NET の概要](../ado-net-overview.md)
