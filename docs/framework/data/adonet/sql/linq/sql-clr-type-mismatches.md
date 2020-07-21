---
title: SQL と CLR の型の不一致
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 0a90c33f-7ed7-4501-ad5f-6224c5da8e9b
ms.openlocfilehash: 27708f4bb8e191156f578132602570bc4a6337b0
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70781206"
---
# <a name="sql-clr-type-mismatches"></a>SQL と CLR の型の不一致

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] はオブジェクト モデルと SQL Server 間の変換のほとんどを自動化します。 ただし、正確な変換が実行されない場合もあります。 以下のセクションでは、共通言語ランタイム (CLR) の型と SQL Server データベースの型の主な不一致について概要を示します。 特定の型のマッピングと関数の変換については、「[SQL と CLR の型マッピング](sql-clr-type-mapping.md)」と「[データ型と関数](data-types-and-functions.md)」で詳しく説明しています。

## <a name="data-types"></a>データの種類

CLR と SQL Server 間の変換は、クエリがデータベースに送信されるときと、結果がオブジェクト モデルに返されるときに発生します。 たとえば、次の Transact-SQL では 2 つの値の変換が必要です。

```sql
Select DateOfBirth From Customer Where CustomerId = @id
```

SQL Server にクエリを実行する前に、Transact-SQL パラメーターの値を指定する必要があります。 この例では、データベースが値を認識できるように、最初に `id` パラメーターの値を CLR の <xref:System.Int32?displayProperty=nameWithType> 型から SQL Server の `INT` 型に変換します。 次に、結果を取得するために、SQL Server の `DateOfBirth` 列を SQL Server の `DATETIME` 型から、オブジェクト モデルで使用できる CLR の <xref:System.DateTime?displayProperty=nameWithType> 型に変換する必要があります。 この例では、CLR オブジェクト モデルの型と SQL Server データベースの型をそのままマッピングできますが、 これが常に可能であるとは限りません。

### <a name="missing-counterparts"></a>対応する型の欠落

次の型には、対応する適切な型がありません。

- CLR <xref:System> 名前空間の不一致 :

  - **符号なし整数**。 通常、この型はオーバーフローを避けるため、大きいサイズの符号付きの型に変換されます。 リテラルは、値に基づいて、同じサイズまたはより小さいサイズの符号付きの型に変換されます。

  - **[Boolean]** 。 この型は、1 ビット以上の数値型または文字列型に変換できます。 リテラルは、同じ値に評価される式に (たとえば SQL の `1=1` は CLS の `True` に) 変換できます。

  - **TimeSpan**。 この型は、2 つの `DateTime` 値の差分を表します。SQL Server の `timestamp` には相当しません。 CLR の <xref:System.TimeSpan?displayProperty=nameWithType> は、場合によっては SQL Server の `TIME` 型にもマッピングします。 SQL Server の `TIME` 型は、24 時間未満の正の値を表すだけが目的でした。 CLR の <xref:System.TimeSpan> の範囲はこれよりずっと大きくなります。

  > [!NOTE]
  > <xref:System.Data.SqlTypes> にある SQL Server に固有の .NET Framework 型は、この比較には含まれていません。

- SQL Server の不一致 :

  - **固定長文字型**。 Transact-SQL では、Unicode カテゴリと Unicode 以外のカテゴリが区別され、それぞれのカテゴリに 3 つの型 (固定長 `nchar`/`char`、可変長 `nvarchar`/`varchar`、および大きいサイズの `ntext`/`text`) があります。 固定長文字型は、文字を取得するために CLR の <xref:System.Char?displayProperty=nameWithType> 型に変換できますが、この型の変換と動作に正確には対応していません。

  - **ビット**。 `bit` ドメインに格納される値の数は `Nullable<Boolean>` と同じですが、両者の型は異なります。 `Bit` が受け取る値は `1` と `0` であり、`true`/`false` ではありません。また、ブール式に相当する型としては使用できません。

  - **Timestamp**。 CLR の <xref:System.TimeSpan?displayProperty=nameWithType> 型とは異なり、SQL Server の `TIMESTAMP` 型は、各更新に固有のデータベースで生成される 8 バイトの数字を表し、<xref:System.DateTime> の値の差異に基づくものではありません。

  - **Money** および **SmallMoney**。 これらの値は <xref:System.Decimal> に変換できますが、基本的には異なる型であり、サーバーベースの関数や変換では異なる型として扱われます。

### <a name="multiple-mappings"></a>複数のマッピング

SQL Server のデータ型には CLR の 1 つ以上のデータ型にマッピングできるものが多くあります。 また、CLR のデータ型にも SQL Server の 1 つ以上のデータ型にマッピングできるものが多くあります。 マッピングは LINQ to SQL でサポートされている場合がありますが、CLR と SQL Server 間でマッピングされる 2 つの型が有効桁数、範囲、セマンティクスにおいて完全に一致するとは限りません。 これらの要素の一部または全部が異なるマッピングもあります。 さまざまなマッピング パターンで生じる違いの詳細については、「[SQL と CLR の型マッピング](sql-clr-type-mapping.md)」を参照してください。

### <a name="user-defined-types"></a>ユーザー定義型

ユーザー定義の CLR 型は、型システムの差異を埋めるために設計されていますが、 型のバージョン管理に関する興味深い問題が発生しています。 クライアントで使用されるバージョンでの変更が、データベース サーバーに保存されている型での変更に一致しない場合があります。 このような変更が原因で別の型不一致が発生して型のセマンティクスが一致しなくなり、バージョンの差異が表面化する可能性があります。 後続のバージョンで継承階層がリファクタリングされるにつれて、問題はさらに複雑化します。

## <a name="expression-semantics"></a>式のセマンティクス

CLR の型とデータベースの型が 1 対 1 で対応しないという不一致に加えて、式の変換がこの不一致をさらに複雑にしています。 演算子セマンティクス、関数セマンティクス、暗黙の型変換、および優先順位規則について不一致を考慮する必要があります。

ここでは、よく似ている式で起こる不一致について具体的に説明します。 特定の CLR 式にセマンティクス的に同等の SQL 式を生成することが可能な場合があります。 ただし、よく似た 2 つの式のセマンティクスの相違が CLR ユーザーに明らかかどうかは不明なため、セマンティクスの同等性に必要な変更が意図されているかどうかはわかりません。 これが特に重大な問題となるのは、式が一連の値に評価されるときです。 差異が見えるかどうかはデータによっても左右され、コーディングとデバッグの段階で特定することは困難です。

### <a name="null-semantics"></a>null セマンティクス

SQL 式では、ブール式に 3 つの論理値を使用します。 式の結果は true、false、または null です。 これに対し、CLR は null 値に関する比較に、2 つの値によるブール型の結果を指定します。 次のコードがあるとします。

[!code-csharp[DLinqMismatch#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#2)]
[!code-vb[DLinqMismatch#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#2)]

```sql
-- Assume col1 and col2 are integer columns with null values.
-- Assume that ANSI null behavior has not been explicitly
--  turned off.
Select …
From …
Where col1 = col2
-- Evaluates to null, not true and the corresponding row is not
--   selected.
-- To obtain matching behavior (i -> col1, j -> col2) change
--   the query to the following:
Select …
From …
Where
    col1 = col2
or (col1 is null and col2 is null)
-- (Visual Basic 'Nothing'.)
```

同様の問題は、結果が 2 つの値のいずれかになることが前提とされているときにも起こります。

[!code-csharp[DLinqMismatch#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#3)]
[!code-vb[DLinqMismatch#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#3)]

```sql
-- Assume col1 and col2 are nullable columns.
-- Assume that ANSI null behavior has not been explicitly
--   turned off.
Select …
From …
Where
    col1 = col2
or col1 != col2
-- Visual Basic: col1 <> col2.

-- Excludes the case where the boolean expression evaluates
--   to null. Therefore the where clause does not always
--   evaluate to true.
```

この例では、生成される SQL の動作は同等ですが、意図したとおりに正確に変換されない可能性があります。

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、C# の `null` または Visual Basic `nothing` の比較セマンティクスが SQL に強制されません。 比較演算子は、対応する SQL の演算子に構文上は変換されます。 セマンティクスには、サーバーまたは接続の設定で定義された SQL セマンティクスが反映されます。 既定の SQL Server 設定では、2 つの null 値は一致しないと見なされます (この設定を変更するとセマンティクスを変更できます)。 いずれにしても、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ではクエリの変換時にサーバーの設定は考慮されません。

リテラルの `null` (`nothing`) による比較は適切な SQL バージョンの (`is null` または `is not null`) に変換されます。

`null` (`nothing`) の値の照合順序は SQL Server で定義され、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では変更されません。

### <a name="type-conversion-and-promotion"></a>型変換と上位変換

SQL では、式における暗黙の型変換が豊富にサポートされています。 同じような式でも、C# では明示的なキャストが必要です。 次に例を示します。

- `Nvarchar` 型と `DateTime` 型は、SQL では明示的にキャストせずに比較できますが、C# では明示的に変換する必要があります。

- `Decimal` は、SQL では暗黙に `DateTime` に変換されます。 C# では、暗黙の変換は行われません。

同様に、型の基本セットが異なるため、Transact-SQL の型の優先順位は C# の優先順位と異なります。 実際に、両者の優先順位のリストには明白なサブセットやスーパーセットの関係は成り立ちません。 たとえば、`nvarchar` を `varchar` と比較すると、`varchar` 式が `nvarchar` に暗黙的に変換されます。 これに相当する上位変換は CLR にはありません。

単純なケースでは、これらの違いによって、CLR 式には SQL 式では冗長となるキャストがあります。 さらに重要なことは、SQL 式が評価される過程で中間結果として、正確に対応するものが C# に存在しない型に上位変換される (またはその逆) 可能性があることです。 このような式のテスト、デバッグ、および検証には多大な労力を要します。

### <a name="collation"></a>照合順序

Transact-SQL では、明示的な照合順序が文字列型の注釈としてサポートされます。 この照合順序に従って、特定の比較の有効性が決定されます。 たとえば、明示的な照合順序の異なる 2 つの列を比較するとエラーになります。 CTS の文字列型はこれよりも単純なため、このようなエラーは起こりません。 次に例を示します。

```sql
create table T2 (
    Col1 nvarchar(10),
    Col2      nvarchar(10) collate Latin_general_ci_as
)
```

[!code-csharp[DLinqMismatch#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#4)]
[!code-vb[DLinqMismatch#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#4)]

```sql
Select …
From …
Where Col1 = Col2
-- Error, collation conflict.
```

ここでは、collation サブ句で、代用できない "*制限がある型*" を作成しています。

同様に、並べ替え順序も型システムによって顕著に異なります。 この相違は、結果の並べ替えに影響します。 <xref:System.Guid> は、すべての 16 バイトを辞書の編集順序 (`IComparable()`) で並べ替えますが、T-SQL は、node(10-15)、clock-seq(8-9)、time-high(6-7)、time-mid(4-5)、time-low(0-3) の順序で GUID を比較します。 この順序は、NT 生成の GUID がこのようなオクテット順になった SQL 7.0 で採用されました。 この方法により、同じノード クラスターで生成された GUID がタイムスタンプに従って順番に並ぶことが保証されていました。 また、この方法はインデックスの作成にも便利でした (挿入時にランダムな入出力の代わりに追加が発生します)。 この順番はプライバシーを考慮して後に Windows で暗号化されましたが、SQL では互換性を維持する必要があります。 この問題を回避するには、<xref:System.Guid> ではなく <xref:System.Data.SqlTypes.SqlGuid> を使用します。

### <a name="operator-and-function-differences"></a>演算子と関数の相違

基本的には対応する関係にある演算子と関数にも、若干のセマンティクスの違いがあります。 次に例を示します。

- C# の論理演算子 `&&` と `||` については、オペランドの辞書編集上の順序に基づいてショート サーキットのセマンティクスが指定されます。 一方 SQL では、セットベースのクエリの対象となるため、実行の順序を決定する際の自由度が高くなります。 次に、これの具体例をいくつか示します。

  - セマンティクスが等価になるように変換するには、SQL の "`CASE` … `WHEN` … `THEN`" 構造でオペランドの実行順序が変更されないようにする必要があります。

  - C# の式が最初のオペランドの評価結果に基づく 2 番目のオペランドの評価に依存している場合は、`AND`/`OR` 演算子へのルーズな変換によって予期しないエラーが発生する可能性があります。

- `Round()` 関数のセマンティクスは、.NET Framework と T-SQL で異なります。

- 文字列のインデックスは、CLR では 0 から始まりますが、SQL では 1 から始まります。 したがって、インデックスのある関数にはインデックスの変換が必要です。

- CLR では、浮動小数点数に剰余演算子 (%) がサポートされていますが、SQL ではサポートされていません。

- `Like` 演算子は、暗黙的な変換に基づいて自動的にオーバーロードされます。 `Like` は文字列型を操作するために定義された演算子ですが、数値型または `DateTime` 型に `Like` が使用される場合にはこれらの非文字列型からも暗黙の変換が許されます。 CTS には、これに相当する暗黙の変換はありません。 したがって、オーバーロードを追加する必要があります。

    > [!NOTE]
    > この `Like` 演算子の動作は C# のみに当てはまります。Visual Basic の `Like` キーワードは以前と変わりません。

- SQL では常にオーバーフローがチェックされますが、C# ではこのチェックを明示的に指定して折り返しを回避する必要があります (Visual Basic では不要です)。 たとえば、整数の列 C1、C2、および C3 があり、C1+C2 が C3 (Update T Set C3 = C1 + C2) に保存されるとします。

    ```sql
    create table T3 (
        Col1      integer,
        Col2      integer
    )
    insert into T3 (col1, col2) values (2147483647, 5)
    -- Valid values: max integer value and 5.
    select * from T3 where col1 + col2 < 0
    -- Produces arithmetic overflow error.
    ```

[!code-csharp[DLinqMismatch#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#5)]
[!code-vb[DLinqMismatch#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#5)]

- SQL では対称的な算術型丸めが実行されますが、.NET Framework では銀行型丸めが使用されます。 詳細については、サポート技術情報の文書「丸めを行うカスタム プロシージャを実装する方法」(196652) を参照してください。

- 既定で、共通ロケールの SQL で文字や文字列を比較する場合に大文字と小文字は区別されません。 Visual Basic と C# では、大文字と小文字は区別されます。 たとえば、`s` が `food` の場合、`s == "Food"` (Visual Basic では `s = "Food"`) と `s == "Food"` の結果は異なります。

    ```sql
    -- Assume default US-English locale (case insensitive).
    create table T4 (
        Col1      nvarchar (256)
    )
    insert into T4 values (‘Food’)
    insert into T4 values (‘FOOD’)
    select * from T4 where Col1 = ‘food’
    -- Both the rows are returned because of case-insensitive matching.
    ```

[!code-csharp[DLinqMismatch#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#6)]
[!code-vb[DLinqMismatch#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#6)]

- SQL で固定長の文字型引数に適用される演算子や関数と、CLR の <xref:System.String?displayProperty=nameWithType> に適用される同じ演算子や関数とでは、セマンティクスに顕著な違いがあります。 これも、型の説明で指摘したように、対応する型の欠落の問題が波及したものと解釈できます。

    ```sql
    create table T4 (
        Col1      nchar(4)
    )
    Insert into T5(Col1) values ('21');
    Insert into T5(Col1) values ('1021');
    Select * from T5 where Col1 like '%1'
    -- Only the second row with Col1 = '1021' is returned.
    -- Not the first row!
    ```

     [!code-csharp[DLinqMismatch#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#7)]
     [!code-vb[DLinqMismatch#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#7)]

     同様の問題は、文字列の連結でも見られます。

    ```sql
    create table T6 (
        Col1      nchar(4)
        Col2       nchar(4)
    )
    Insert into T6 values ('a', 'b');
    Select Col1+Col2 from T6
    -- Returns concatenation of padded strings "a   b   " and not "ab".
    ```

概して、CLR 式には複雑な変換が必要になる場合があり、SQL 機能を表現するには演算子や関数の追加が必要になる可能性があります。

### <a name="type-casting"></a>型キャスト

C# と SQL では、明示的な型キャスト (`Cast` および `Convert`) を使って、式の既定のセマンティクスをオーバーライドできます。 ただし、型システムの境界を越えてこの機能を提供するとジレンマが生じます。 特定のセマンティクスを提供する SQL のキャストは、それに相当する C# のキャストに簡単には変換できません。 反対に、C# のキャストを SQL の同等のキャストに直接変換することはできません。型の不一致、対応する型の欠落、および型の優先順位の相違があるためです。 型システムの不一致の露出と式の有意性の喪失は、トレードオフの関係にあります。

また、型のキャストは、どちらのドメインでも式の検証には不要かもしれませんが、既定以外のマッピングを式に正しく適用するために必要になる場合があります。

```sql
-- Example from "Non-default Mapping" section extended
create table T5 (
    Col1      nvarchar(10),
    Col2      nvarchar(10)
)
Insert into T5(col1, col2) values (‘3’, ‘2’);
```

[!code-csharp[DLinqMismatch#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#8)]
[!code-vb[DLinqMismatch#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#8)]

```sql
Select *
From T5
Where Col1 + Col2 > 4
-- "Col1 + Col2" expr evaluates to '32'
```

## <a name="performance-issues"></a>パフォーマンスの問題

SQL Server と CLR の型の相違が原因となり、CLR と SQL Server の型システムの境界を越えるときにパフォーマンスが低下する可能性があります。 次のような状況でパフォーマンスに影響が現れます。

- 論理積/和演算子の評価順序の強制

- 述語の評価順序を強制する SQL を生成すると、SQL オプティマイザーの機能が制限されます。

- 型変換は、CLR コンパイラで導入される場合も、オブジェクト リレーショナル クエリ実装で導入される場合も、インデックスの使用を抑制することがあります。

     たとえば、オブジェクトに適用された

    ```sql
    -- Table DDL
    create table T5 (
        Col1      varchar(100)
    )
    ```

     [!code-csharp[DLinqMismatch#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#9)]
     [!code-vb[DLinqMismatch#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#9)]

     式 `(s = SOME_STRING_CONSTANT)` を変換するとします。

    ```sql
    -- Corresponding part of SQL where clause
    Where …
    Col1 = SOME_STRING_CONSTANT
    -- This expression is of the form <varchar> = <nvarchar>.
    -- Hence SQL introduces a conversion from varchar to nvarchar,
    --   resulting in
    Where …
    Convert(nvarchar(100), Col1) = SOME_STRING_CONSTANT
    -- Cannot use the index for column Col1 for some implementations.
    ```

SQL Server と CLR の型システムの境界を越えるときは、セマンティクスの相違に加えて、パフォーマンスへの影響も考慮することが重要です。 データセットが大きい場合、このようなパフォーマンスの問題が、アプリケーションの展開が可能かどうかを左右することがあります。

## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
