---
title: SQL と CLR の型マッピング
ms.date: 07/23/2018
ms.assetid: 4ed76327-54a7-414b-82a9-7579bfcec04b
ms.openlocfilehash: 336732e0fe7ca8955702d325309db6a8e61b1722
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174538"
---
# <a name="sql-clr-type-mapping"></a>SQL と CLR の型マッピング
LINQ to SQL では、リレーショナル データベースのデータ モデルが、任意のプログラミング言語で表されるオブジェクト モデルに対応付けられています。 アプリケーションが実行されると、LINQ to SQL は、オブジェクト モデルの統合言語クエリを SQL に変換し、それをデータベースに送信して実行します。 データベースから結果が返されると、LINQ to SQL はその結果をプログラミング言語で操作できるオブジェクトに変換し直します。  
  
 オブジェクト モデルとデータベースの間でデータを変換するには、"*型マッピング*" を定義する必要があります。 LINQ to SQL は型マッピングを使用して、共通言語ランタイム (CLR) のそれぞれの型を SQL Server の特定の型に対応付けます。 型マッピングおよびその他のマッピング情報 (データベース構造やテーブルのリレーションシップなど) は、オブジェクト モデル内で属性ベースの対応付けを使用して定義できます。 また、オブジェクト モデルの外部で外部マッピング ファイルを使用して指定することもできます。 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」および「[外部マップ](external-mapping.md)」をご覧ください。  
  
 このトピックでは、以下の点について説明します。  
  
- [既定の型マッピング](#DefaultTypeMapping)  
  
- [型マッピングと実行時動作の関係](#BehaviorMatrix)  
  
- [CLR と SQL の実行時の動作の違い](#BehaviorDiffs)  
  
- [Enum 型のマッピング](#EnumMapping)  
  
- [数値のマッピング](#NumericMapping)  
  
- [テキストおよび XML のマッピング](#TextMapping)  
  
- [日付および時刻のマッピング](#DateMapping)  
  
- [バイナリのマッピング](#BinaryMapping)  
  
- [その他のマッピング](#MiscMapping)  
  
<a name="DefaultTypeMapping"></a>
## <a name="default-type-mapping"></a>既定の型マッピング  
 オブジェクト モデルまたは外部マッピング ファイルは、オブジェクト リレーショナル デザイナー (O/R デザイナー) または SQLMetal コマンド ライン ツールを使用して自動的に作成できます。 これらのツールの既定の型マッピングでは、SQL Server データベース内の列にマップするためにどの CLR 型を選択するかが定義されています。 これらのツールの使用方法の詳細については、「[オブジェクト モデルの作成](creating-the-object-model.md)」を参照してください。  
  
 また、<xref:System.Data.Linq.DataContext.CreateDatabase%2A> メソッドを使用して、オブジェクト モデルまたは外部マッピング ファイルのマッピング情報に基づいて SQL Server データベースを作成することもできます。 <xref:System.Data.Linq.DataContext.CreateDatabase%2A> メソッドの既定の型マッピングでは、オブジェクト モデル内の CLR 型にマップするためにどの型の SQL Server 列を作成するかが定義されています。 詳細については、[データベースを動的に作成する](how-to-dynamically-create-a-database.md)」を参照してください。  
  
<a name="BehaviorMatrix"></a>
## <a name="type-mapping-run-time-behavior-matrix"></a>型マッピングと実行時動作の関係  
 次の図は、データがデータベースから取得されるときやデータベースに保存されるときに、特定の型マッピングで行われる実行時の動作を示しています。 シリアル化を除き、LINQ to SQL では、このマトリックスに指定されていない CLR または SQL Server のデータ型のマッピングはサポートされません。 シリアル化のサポートの詳細については、「[バイナリ シリアル化](#BinarySerialization)」を参照してください。  

![SQL Server と SQL CLR のデータ型マッピング テーブル](./media/sql-clr-type-mapping.png)

> [!NOTE]
> 一部の型マッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。  
  
### <a name="custom-type-mapping"></a>カスタム型マッピング  
 LINQ to SQL では、O/R デザイナー、SQLMetal、および <xref:System.Data.Linq.DataContext.CreateDatabase%2A> メソッドで使用される既定の型マッピング以外も使用できます。 DBML ファイルで明示的に指定すると、カスタム型マッピングを作成できます。 次に、その DBML ファイルを使用してオブジェクト モデル コードとマッピング ファイルを作成できます。 詳細については、「[SQL と CLR のカスタム型マッピング](sql-clr-custom-type-mappings.md)」を参照してください。  
  
<a name="BehaviorDiffs"></a>
## <a name="behavior-differences-between-clr-and-sql-execution"></a>CLR と SQL の実行時の動作の違い  
 CLR と SQL Server では有効桁数や実行方法が異なるため、計算を実行する場所によって、得られる結果や動作が異なる場合があります。 LINQ to SQL クエリで実行される計算は、実際は Transact-SQL に変換されてから SQL Server データベースで実行されます。 LINQ to SQL クエリの外部で実行される計算は、CLR のコンテキスト内で実行されます。  
  
 CLR および SQL Server 間での動作の違いの例を次に示します。  
  
- SQL Server では、一部のデータ型が、CLR の対応する型のデータとは異なる順序で並べ替えられます。 たとえば、SQL Server の `UNIQUEIDENTIFIER` 型のデータは、CLR の <xref:System.Guid?displayProperty=nameWithType> 型のデータとは異なる順序で並べ替えられます。  
  
- SQL Server では、一部の文字列比較操作の処理が CLR とは異なります。 SQL Server での文字列比較の動作は、サーバー上の照合順序の設定によって決まります。 詳細については、Microsoft SQL Server オンライン ブックの「[照合順序の使用](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/ms187582(v=sql.105))」を参照してください。  
  
- SQL Server では、マップされている一部の関数で、CLR とは異なる値が返されることがあります。 たとえば、末尾の空白文字のみが異なる 2 つの文字列を等価関数で比較した場合、SQL Server では等しいと見なされるのに対し、CLR では等しくないと見なされます。  
  
<a name="EnumMapping"></a>
## <a name="enum-mapping"></a>Enum 型のマッピング  
 LINQ to SQL では、CLR の <xref:System.Enum?displayProperty=nameWithType> 型の SQL Server 型へのマッピングが 2 種類サポートされています。  
  
- SQL 数値型 (`TINYINT`、`SMALLINT`、`INT`、`BIGINT`) へのマッピング  
  
     CLR <xref:System.Enum?displayProperty=nameWithType> 型を SQL 数値型にマップすると、基になる CLR <xref:System.Enum?displayProperty=nameWithType> の整数値は SQL Server データベース列の値にマップされます。 たとえば、<xref:System.Enum?displayProperty=nameWithType> という名前の `DaysOfWeek` に、基になる整数値が 3 である `Tue` という名前のメンバーが含まれる場合、そのメンバーはデータベース値 3 にマップされます。  
  
- SQL テキスト型 (`CHAR`、`NCHAR`、`VARCHAR`、`NVARCHAR`) へのマッピング  
  
     CLR <xref:System.Enum?displayProperty=nameWithType> 型を SQL テキスト型にマップすると、CLR <xref:System.Enum?displayProperty=nameWithType> のメンバーの名前に SQL データベース値がマップされます。 たとえば、<xref:System.Enum?displayProperty=nameWithType> という名前の `DaysOfWeek` に、基になる整数値が 3 である `Tue` という名前のメンバーが含まれる場合、このメンバーはデータベース値 `Tue` にマップされます。  
  
> [!NOTE]
> SQL のテキスト型を CLR の <xref:System.Enum?displayProperty=nameWithType> にマップする場合は、マップされる SQL 列に <xref:System.Enum> メンバーの名前のみを含めてください。 <xref:System.Enum> 型にマップされる SQL 列では、他の値はサポートされません。  
  
 O/R デザイナーと SQLMetal コマンド ライン ツールでは、SQL の型から CLR の <xref:System.Enum> クラスへの自動的なマッピングはできません。 DBML ファイルを O/R デザイナーと SQLMetal で使用できるようにカスタマイズして、このマッピングを明示的に設定する必要があります。 カスタム型マッピングの詳細については、「[SQL と CLR のカスタム型マッピング](sql-clr-custom-type-mappings.md)」を参照してください。  
  
 列挙を目的とする SQL の列は、他の数値やテキストの列と型が同じであるため、これらのツールはユーザーの意図を認識できず、次の「[数値のマッピング](#NumericMapping)」と「[テキストおよび XML のマッピング](#TextMapping)」のセクションで説明するように既定のマッピングを使用します。 DBML ファイルを使用したコード生成の詳細については、「[LINQ to SQL でのコード生成](code-generation-in-linq-to-sql.md)」を参照してください。  
  
 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドでは、CLR の <xref:System.Enum?displayProperty=nameWithType> 型をマップするために数値型の SQL 列が作成されます。  
  
<a name="NumericMapping"></a>
## <a name="numeric-mapping"></a>数値のマッピング  
 LINQ to SQL では、CLR と SQL Server のさまざまな数値型をマップできます。 次の表に、O/R デザイナーおよび SQLMetal でデータベースに基づいてオブジェクト モデルまたは外部マッピング ファイルを作成するときに選択される CLR 型を示します。  
  
|SQL Server 型|O/R デザイナーおよび SQLMetal で使用される既定の CLR 型マッピング|  
|---------------------|-----------------------------------------------------------------|  
|`BIT`|<xref:System.Boolean?displayProperty=nameWithType>|  
|`TINYINT`|<xref:System.Int16?displayProperty=nameWithType>|  
|`INT`|<xref:System.Int32?displayProperty=nameWithType>|  
|`BIGINT`|<xref:System.Int64?displayProperty=nameWithType>|  
|`SMALLMONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`MONEY`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`DECIMAL`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`NUMERIC`|<xref:System.Decimal?displayProperty=nameWithType>|  
|`REAL/FLOAT(24)`|<xref:System.Single?displayProperty=nameWithType>|  
|`FLOAT/FLOAT(53)`|<xref:System.Double?displayProperty=nameWithType>|  
  
 次の表に、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで使用される既定の型マッピングを示します。既定の型マッピングでは、オブジェクト モデルまたは外部マッピング ファイルで定義された CLR 型にマップするために作成される SQL 列の型が定義されています。  
  
|CLR 型|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> で使用される既定の SQL Server 型|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Boolean?displayProperty=nameWithType>|`BIT`|  
|<xref:System.Byte?displayProperty=nameWithType>|`TINYINT`|  
|<xref:System.Int16?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.Int32?displayProperty=nameWithType>|`INT`|  
|<xref:System.Int64?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.SByte?displayProperty=nameWithType>|`SMALLINT`|  
|<xref:System.UInt16?displayProperty=nameWithType>|`INT`|  
|<xref:System.UInt32?displayProperty=nameWithType>|`BIGINT`|  
|<xref:System.UInt64?displayProperty=nameWithType>|`DECIMAL(20)`|  
|<xref:System.Decimal?displayProperty=nameWithType>|`DECIMAL(29,4)`|  
|<xref:System.Single?displayProperty=nameWithType>|`REAL`|  
|<xref:System.Double?displayProperty=nameWithType>|`FLOAT`|  
  
 これ以外にもさまざまな数値のマッピングを選択できますが、一部のマッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。 詳細については、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」を参照してください。  
  
### <a name="decimal-and-money-types"></a>Decimal 型と Money 型  
 SQL Server の `DECIMAL` 型の既定の有効桁数 (小数点の右側と左側で 18 桁) は、対応する既定の型である CLR の <xref:System.Decimal?displayProperty=nameWithType> 型の有効桁数よりはるかに少なくなっています。 その結果、データベースにデータを保存するときに有効桁数が少なくなることがあります。 一方、SQL Server の `DECIMAL` 型に 29 桁を超える有効桁数が設定されている場合、その逆が発生する可能性があります。 SQL Server の `DECIMAL` 型に CLR の <xref:System.Decimal?displayProperty=nameWithType> より大きい有効桁数の値が設定されていると、データベースからデータを取得するときに有効桁数が少なくなることがあります。  
  
 SQL Server の `MONEY` 型と `SMALLMONEY` 型も、既定で CLR の <xref:System.Decimal?displayProperty=nameWithType> 型に対応付けられます。これらの型も有効桁数がはるかに少ないため、データベースにデータを保存するときにオーバーフローやデータ損失の例外が発生する可能性があります。  
  
<a name="TextMapping"></a>
## <a name="text-and-xml-mapping"></a>テキストおよび XML のマッピング  
 さまざまなテキスト ベースの型および XML 型も、LINQ to SQL を使用してマップすることができます。 次の表に、O/R デザイナーおよび SQLMetal でデータベースに基づいてオブジェクト モデルまたは外部マッピング ファイルを作成するときに選択される CLR 型を示します。  
  
|SQL Server 型|O/R デザイナーおよび SQLMetal で使用される既定の CLR 型マッピング|  
|---------------------|-----------------------------------------------------------------|  
|`CHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`VARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`NVARCHAR`|<xref:System.String?displayProperty=nameWithType>|  
|`TEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`NTEXT`|<xref:System.String?displayProperty=nameWithType>|  
|`XML`|<xref:System.Xml.Linq.XElement?displayProperty=nameWithType>|  
  
 次の表に、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで使用される既定の型マッピングを示します。既定の型マッピングでは、オブジェクト モデルまたは外部マッピング ファイルで定義された CLR 型にマップするために作成される SQL 列の型が定義されています。  
  
|CLR 型|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> で使用される既定の SQL Server 型|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Char?displayProperty=nameWithType>|`NCHAR(1)`|  
|<xref:System.String?displayProperty=nameWithType>|`NVARCHAR(4000)`|  
|<xref:System.Char?displayProperty=nameWithType>[]|`NVARCHAR(4000)`|  
|`Parse()` および `ToString()` を実装するカスタム型|`NVARCHAR(MAX)`|  
  
 これ以外にもさまざまなテキスト ベースおよび XML のマッピングを選択できますが、一部のマッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。 詳細については、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」を参照してください。  
  
### <a name="xml-types"></a>XML 型  
 SQL Server の `XML` データ型は、Microsoft SQL Server 2005 以降で使用できます。 SQL Server の `XML` データ型は、<xref:System.Xml.Linq.XElement>、<xref:System.Xml.Linq.XDocument>、または <xref:System.String> にマップできます。 <xref:System.Xml.Linq.XElement> に読み込むことができない XML フラグメントが列に格納されている場合は、列を <xref:System.String> にマップして、実行時エラーを回避する必要があります。 <xref:System.String> にマップする必要がある XML フラグメントを次に示します。  
  
- XML 要素のシーケンス  
  
- 属性  
  
- パブリック識別子 (PI)  
  
- コメント  
  
 <xref:System.Xml.Linq.XElement> および <xref:System.Xml.Linq.XDocument> は、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」で示したように SQL Server にマップすることができますが、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドには、これらの型に対する既定の SQL Server 型マッピングはありません。  
  
### <a name="custom-types"></a>カスタム型  
 クラスで `Parse()` および `ToString()` が実装されている場合は、そのオブジェクトを SQL の任意のテキスト型 (`CHAR`、`NCHAR`、`VARCHAR`、`NVARCHAR`、`TEXT`、`NTEXT`、`XML`) にマップできます。 オブジェクトをデータベースに格納するには、`ToString()` から返された値をマップ先のデータベース列に送信します。 オブジェクトを再構築するには、データベースから返された文字列に対して `Parse()` を呼び出します。  
  
> [!NOTE]
> LINQ to SQL では、<xref:System.Xml.Serialization.IXmlSerializable?displayProperty=nameWithType> の使用によるシリアル化はサポートされません。  
  
<a name="DateMapping"></a>
## <a name="date-and-time-mapping"></a>日付および時刻のマッピング  
 LINQ to SQL では、SQL Server のさまざまな日付型および時刻型をマップできます。 次の表に、O/R デザイナーおよび SQLMetal でデータベースに基づいてオブジェクト モデルまたは外部マッピング ファイルを作成するときに選択される CLR 型を示します。  
  
|SQL Server 型|O/R デザイナーおよび SQLMetal で使用される既定の CLR 型マッピング|  
|---------------------|-----------------------------------------------------------------|  
|`SMALLDATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIME2`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`DATETIMEOFFSET`|<xref:System.DateTimeOffset?displayProperty=nameWithType>|  
|`DATE`|<xref:System.DateTime?displayProperty=nameWithType>|  
|`TIME`|<xref:System.TimeSpan?displayProperty=nameWithType>|  
  
 次の表に、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで使用される既定の型マッピングを示します。既定の型マッピングでは、オブジェクト モデルまたは外部マッピング ファイルで定義された CLR 型にマップするために作成される SQL 列の型が定義されています。  
  
|CLR 型|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> で使用される既定の SQL Server 型|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.DateTime?displayProperty=nameWithType>|`DATETIME`|  
|<xref:System.DateTimeOffset?displayProperty=nameWithType>|`DATETIMEOFFSET`|  
|<xref:System.TimeSpan?displayProperty=nameWithType>|`TIME`|  
  
 これ以外にもさまざまな日付および時刻のマッピングを選択できますが、一部のマッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。 詳細については、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」を参照してください。  
  
> [!NOTE]
> SQL Server の `DATETIME2` 型、`DATETIMEOFFSET` 型、`DATE` 型、および `TIME` 型は、Microsoft SQL Server 2008 以降で使用できます。 Microsoft .NET Framework version 3.5 SP1 以降の LINQ to SQL では、これらの新しい型へのマッピングがサポートされています。  
  
### <a name="systemdatetime"></a>System.Datetime  
 CLR の <xref:System.DateTime?displayProperty=nameWithType> 型の範囲と有効桁数の値は、`DATETIME` メソッドの既定の型マッピングである SQL Server の <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> 型の範囲と有効桁数より大きな値です。 `DATETIME` の範囲外の日付に関連する例外を回避するには、Microsoft SQL Server 2008 以降で利用できる `DATETIME2` を使用してください。 `DATETIME2`は、CLR の <xref:System.DateTime?displayProperty=nameWithType> の範囲と精度に対応させることができます。  
  
 SQL Server の日付には、CLR で十分にサポートされている機能である <xref:System.TimeZone> の概念がありません。 <xref:System.TimeZone> の値は、元の <xref:System.TimeZone> の情報にかかわらず、<xref:System.DateTimeKind> 変換なしでそのまま保存されます。 <xref:System.DateTime> 値がデータベースから取得される場合、その値は、<xref:System.DateTime> が <xref:System.DateTimeKind> の状態で、そのまま <xref:System.DateTimeKind.Unspecified> に読み込まれます。 サポートされる <xref:System.DateTime?displayProperty=nameWithType> メソッドの詳細については、「[System.DateTime メソッド](system-datetime-methods.md)」を参照してください。  
  
### <a name="systemtimespan"></a>System.TimeSpan  
 Microsoft SQL Server 2008 および .NET Framework 3.5 SP1 では、CLR の <xref:System.TimeSpan?displayProperty=nameWithType> 型を SQL Server の `TIME` 型にマップできます。 ただし、CLR の <xref:System.TimeSpan?displayProperty=nameWithType> でサポートされる範囲と SQL Server `TIME` 型でサポートされる範囲には大きな差があります。 時間を表す 0 より小さい値または 23:59:59.9999999 より大きい値を SQL の `TIME` にマップすると、オーバーフロー例外が発生します。 詳細については、「[System.TimeSpan メソッド](system-timespan-methods.md)」を参照してください。  
  
 Microsoft SQL Server 2000 および SQL Server 2005 では、データベース フィールドを <xref:System.TimeSpan> にマップすることはできません。 ただし、<xref:System.TimeSpan> 値を <xref:System.TimeSpan> 減算から返したり、リテラル変数またはバインド変数として式に取り込んだりできるため、<xref:System.DateTime> の操作はサポートされています。  
  
<a name="BinaryMapping"></a>
## <a name="binary-mapping"></a>バイナリのマッピング  
 SQL Server のさまざまな型を CLR の <xref:System.Data.Linq.Binary?displayProperty=nameWithType> 型にマップすることができます。 次の表に、O/R デザイナーおよび SQLMetal でデータベースに基づいてオブジェクト モデルまたは外部マッピング ファイルを作成するときに、CLR の <xref:System.Data.Linq.Binary?displayProperty=nameWithType> 型が選択される SQL Server 型を示します。  
  
|SQL Server 型|O/R デザイナーおよび SQLMetal で使用される既定の CLR 型マッピング|  
|---------------------|-----------------------------------------------------------------|  
|`BINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(50)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`VARBINARY(MAX)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`FILESTREAM` 属性を持つ `VARBINARY(MAX)`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`IMAGE`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
|`TIMESTAMP`|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|  
  
 次の表に、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで使用される既定の型マッピングを示します。既定の型マッピングでは、オブジェクト モデルまたは外部マッピング ファイルで定義された CLR 型にマップするために作成される SQL 列の型が定義されています。  
  
|CLR 型|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> で使用される既定の SQL Server 型|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Data.Linq.Binary?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Byte?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
|<xref:System.Runtime.Serialization.ISerializable?displayProperty=nameWithType>|`VARBINARY(MAX)`|  
  
 これ以外にもさまざまなバイナリのマッピングを選択できますが、一部のマッピングでは、データベースに対する変換操作中にオーバーフローやデータ損失の例外が発生することがあります。 詳細については、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」を参照してください。  
  
### <a name="sql-server-filestream"></a>SQL Server の FILESTREAM  
 `FILESTREAM` 列の `VARBINARY(MAX)` 属性は、Microsoft SQL Server 2008 以降で使用できます。.NET Framework version 3.5 SP1 以降の LINQ to SQL では、これらの属性にマップすることができます。  
  
 `VARBINARY(MAX)` 属性を持つ `FILESTREAM` 列を <xref:System.Data.Linq.Binary> オブジェクトにマップすることはできますが、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドを使用して `FILESTREAM` 属性を持つ列を自動的に作成することはできません。 `FILESTREAM` について詳しくは、「[FILESTREAM の概要](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/bb933993(v=sql.105))」をご覧ください。  
  
<a name="BinarySerialization"></a>
### <a name="binary-serialization"></a>バイナリ シリアル化  
 クラスが <xref:System.Runtime.Serialization.ISerializable> インターフェイスを実装している場合は、オブジェクトを SQL バイナリ フィールド (`BINARY`、`VARBINARY`、`IMAGE`) にシリアル化できます。 <xref:System.Runtime.Serialization.ISerializable> インターフェイスの実装方法に従って、オブジェクトのシリアル化と逆シリアル化が行われます。 詳しくは、「[バイナリ シリアル化](../../../../../standard/serialization/binary-serialization.md)」をご覧ください。
  
<a name="MiscMapping"></a>
## <a name="miscellaneous-mapping"></a>その他のマッピング  
 ここでは、上記以外のさまざまな型について、既定の型マッピングを示します。 次の表に、O/R デザイナーおよび SQLMetal でデータベースに基づいてオブジェクト モデルまたは外部マッピング ファイルを作成するときに選択される CLR 型を示します。  
  
|SQL Server 型|O/R デザイナーおよび SQLMetal で使用される既定の CLR 型マッピング|  
|---------------------|-----------------------------------------------------------------|  
|`UNIQUEIDENTIFIER`|<xref:System.Guid?displayProperty=nameWithType>|  
|`SQL_VARIANT`|<xref:System.Object?displayProperty=nameWithType>|  
  
 次の表に、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで使用される既定の型マッピングを示します。既定の型マッピングでは、オブジェクト モデルまたは外部マッピング ファイルで定義された CLR 型にマップするために作成される SQL 列の型が定義されています。  
  
|CLR 型|<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> で使用される既定の SQL Server 型|  
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|  
|<xref:System.Guid?displayProperty=nameWithType>|`UNIQUEIDENTIFIER`|  
|<xref:System.Object?displayProperty=nameWithType>|`SQL_VARIANT`|  
  
 LINQ to SQL では、ここに示したその他の型に対する上記以外の型マッピングはサポートされません。  詳細については、「[型マッピングと実行時動作の関係](#BehaviorMatrix)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [属性ベースの対応付け](attribute-based-mapping.md)
- [外部マップ](external-mapping.md)
- [データ型と関数](data-types-and-functions.md)
- [SQL と CLR の型の不一致](sql-clr-type-mismatches.md)
