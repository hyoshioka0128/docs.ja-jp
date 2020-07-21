---
title: Oracle スキーマ コレクション
ms.date: 03/30/2017
ms.assetid: 89a75de8-dee8-45e2-a97f-254d7e62e7e1
ms.openlocfilehash: cb91a90ae7323283556954caa401646a2063a37e
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783297"
---
# <a name="oracle-schema-collections"></a>Oracle スキーマ コレクション

Microsoft .NET Framework Data Provider for Oracle は、共通のスキーマ コレクションに加えて次のスキーマ コレクションをサポートしています。

- 列

- Indexes

- IndexColumns

- プロシージャ

- シーケンス

- Synonyms

- [テーブル]

- Users

- Views

- 関数

- パッケージ

- PackageBodies

- 引数

- UniqueKeys

- PrimaryKeys

- ForeignKeys

- ForeignKeyColumns

- ProcedureParameters

## <a name="columns"></a>列

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|テーブル、ビュー、またはクラスターの所有者。|
|TABLE_NAME|String|テーブル、ビュー、またはクラスターの名前。|
|COLUMN_NAME|String|列名。|
|ID|Decimal (10 進数型)|作成された列のシーケンス番号。|
|DATATYPE|String|列のデータ型。|
|LENGTH|Decimal (10 進数型)|列の長さ (バイト単位)。|
|PRECISION|Decimal (10 進数型)|NUMBER データ型の場合は 10 進有効桁数、FLOAT データ型の場合はバイナリ有効桁数、その他のデータ型の場合は NULL になります。|
|SCALE|Decimal (10 進数型)|数値の小数点の右側にある数字。|
|NULLABLE|String|列に NULL を許可するかどうかを指定します。 列に NOT NULL 制約がある場合、または列が PRIMARY KEY の一部である場合、値は N になります。|

## <a name="indexes"></a>Indexes

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|インデックスの所有者。|
|INDEX_NAME|String|インデックス名。|
|INDEX_TYPE|String|インデックスの型 (NORMAL、BITMAP、FUNCTION-BASED NORMAL、FUNCTION-BASED BITMAP、または DOMAIN)。|
|TABLE_OWNER|String|インデックス付きオブジェクトの所有者。|
|TABLE_NAME|String|インデックス付きオブジェクト名。|
|TABLE_TYPE|String|インデックス オブジェクトの型 (TABLE、CLUSTER など)。|
|UNIQUENESS|String|インデックスが UNIQUE または NONUNIQUE のどちらであるかを指定します。|
|COMPRESSION|String|インデックスが ENABLED または DISABLED のどちらであるかを指定します。|
|PREFIX_LENGTH|Decimal (10 進数型)|圧縮キーのプレフィックス内の列数。|
|TABLESPACE_NAME|String|インデックスを含むテーブルスペースの名前。|
|INI_TRANS|Decimal (10 進数型)|トランザクションの初期数。|
|MAX_TRANS|Decimal (10 進数型)|トランザクションの最大数。|
|INITIAL_EXTENT|Decimal (10 進数型)|初期エクステントのサイズ。|
|NEXT_EXTENT|Decimal (10 進数型)|セカンダリ エクステントのサイズ。|
|MIN_EXTENTS|Decimal (10 進数型)|セグメント内で許可されているエクステントの最小数。|
|MAX_EXTENTS|Decimal (10 進数型)|セグメント内で許可されているエクステントの最大数。|
|PCT_INCREASE|Decimal (10 進数型)|エクステントのサイズの増加率。|
|PCT_THRESHOLD|Decimal (10 進数型)|インデックスのエントリごとに許可されるブロック領域のしきい値のパーセンテージ。|
|INCLUDE_COLUMN|Decimal (10 進数型)|索引構成表の主キー (オーバーフローなし) のインデックスに含まれる最後の列の列 ID。 この列は、*_TAB_COLUMNS データ辞書ビューの COLUMN_ID 列にマップされます。|
|FREELISTS|Decimal (10 進数型)|このセグメントに割り当てられているプロセスの空きリスト数。|
|FREELIST_GROUPS|Decimal (10 進数型)|このセグメントに割り当てられている空きリスト グループの数。|
|PCT_FREE|Decimal (10 進数型)|ブロックにある空き領域の最小のパーセンテージ。|
|LOGGING|String|ログ情報。|
|BLEVEL|Decimal (10 進数型)|B*-ツリー レベル: ルート ブロックからリーフ ブロックまでのインデックスの深さ。 深さ 0 は、ルート ブロックとリーフ ブロックが同一であることを示します。|
|LEAF_BLOCKS|Decimal (10 進数型)|インデックス内のリーフ ブロックの数。|
|DISTINCT_KEYS|Decimal (10 進数型)|個別にインデックスが付けられた値の数。 UNIQUE および PRIMARY KEY 制約を強制するインデックスの場合、この値はテーブルの行数 (USER_TABLES.NUM_ROWS) と同じです。|
|AVG_LEAF_BLOCKS_PER_KEY|Decimal (10 進数型)|最も近い整数に丸められた、インデックスの個別の値が表示されるリーフ ブロックの平均数。 UNIQUE および PRIMARY KEY 制約を強制するインデックスの場合、この値は常に 1 になります。|
|AVG_DATA_BLOCKS_PER_KEY|Decimal (10 進数型)|最も近い整数に丸められた、インデックス内の個別の値によってポイントされている、テーブル内のデータ ブロックの平均数。 この統計情報は、インデックス列の値を含む行があるデータ ブロックの平均数を示します。|
|CLUSTERING_FACTOR|Decimal (10 進数型)|インデックスの値に基づいて順序付けされている、テーブルの行数を示します。|
|状態|String|分割されていないインデックスが VALID または UNUSABLE のどちらであるかを示します。|
|NUM_ROWS|Decimal (10 進数型)|インデックス内の行数。|
|SAMPLE_SIZE|Decimal (10 進数型)|インデックスの分析に使用されるサンプルのサイズ。|
|LAST_ANALYZED|DateTime|インデックスが最後に分析された日付。|
|DEGREE|String|インデックスがスキャンされるインスタンスごとのスレッド数。|
|INSTANCES|String|インデックスがスキャンされるインスタンス数。|
|PARTITIONED|String|インデックスが分割されているかどうか (YES &#124; NO)。|
|TEMPORARY|String|インデックスが一時テーブルにあるかどうかを示します。|
|GENERATED|String|インデックスの名前がシステム生成かどうか (Y&#124;N)。|
|SECONDARY|String|インデックスが Oracle9i Data Cartridge の ODCIIndexCreate メソッドによって作成されたセカンダリ オブジェクトであるかどうか (Y&#124;N)。|
|BUFFER_POOL|String|インデックス ブロックで使用される既定のバッファー プールの名前。|
|USER_STATS|String|統計情報がユーザーによって直接入力されたものかどうかを示します。|
|DURATION|String|一時テーブルの存続期間を示します。1) SYS$SESSION: 行は、セッションが存続している間、保持されます。2) SYS$TRANSACTION: 行は、COMMIT 後に削除されます。3) 永続テーブルの場合は NULL です。|
|PCT_DIRECT_ACCESS|Decimal (10 進数型)|索引構成表のセカンダリ インデックスでは、VALID であると推測される行のパーセンテージを示します。|
|ITYP_OWNER|String|ドメイン インデックスでは、indextype の所有者を示します。|
|ITYP_NAME|String|ドメイン インデックスでは、indextype の名前を示します。|
|PARAMETERS|String|ドメイン インデックスでは、パラメーターの文字列を示します。|
|GLOBAL_STATS|String|分割されたインデックスでは、統計情報がインデックス全体を分析して収集されたものか (YES)、または基になるインデックスのパーティションおよびサブパーティションから推測されたものであるか (NO) どうかを示します。|
|DOMIDX_STATUS|String|ドメイン インデックスのステータスが反映されます。 NULL: 指定されたインデックスはドメイン インデックスではありません。 VALID: インデックスは有効なドメイン インデックスです。 IDXTYP_INVLD: このドメイン インデックスのインデックス型は無効です。|
|DOMIDX_OPSTATUS|String|ドメイン インデックス上で実行された操作のステータスが反映されます。NULL: 指定されたインデックスはドメイン インデックスではありません。 VALID: 操作がエラーなく実行されました。 FAILED: エラーによって操作が失敗しました。|
|FUNCIDX_STATUS|String|関数ベースのインデックスの状態を示します。NULL: これは関数ベースのインデックスではありません。ENABLED: 関数ベースのインデックスは有効になっています。DISABLED: 関数ベースのインデックスは無効になっています。|
|JOIN_INDEX|String|結合インデックスかどうかを示します。|

## <a name="indexcolumns"></a>IndexColumns

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|INDEX_OWNER|String|インデックスの所有者。|
|INDEX_NAME|String|インデックス名。|
|TABLE_OWNER|String|テーブルまたはクラスターの所有者。|
|TABLE_NAME|String|テーブルまたはクラスターの名前。|
|COLUMN_NAME|String|オブジェクト型列の列名または属性。|
|COLUMN_POSITION|Decimal (10 進数型)|インデックス内の列または属性の位置。|
|COLUMN_LENGTH|Decimal (10 進数型)|インデックスが付けられた列の長さ。|
|CHAR_LENGTH|Decimal (10 進数型)|列の最大コードポイント長。|
|DESCEND|String|列が降順で並べ替えられるかどうかを示します。|

## <a name="procedures"></a>プロシージャ

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者。|
|OBJECT_NAME|String|オブジェクト名。|
|SUBOBJECT_NAME|String|サブオブジェクト名 (partition など)。|
|OBJECT_ID|Decimal (10 進数型)|オブジェクトの辞書オブジェクト数。|
|DATA_OBJECT_ID|Decimal (10 進数型)|オブジェクトを含むセグメントの辞書オブジェクト数。|
|LAST_DDL_TIME|DateTime|DDL コマンド (許可および取り消しを含む) の実行結果として、最後に変更されたオブジェクトのタイムスタンプ。|
|TIMESTAMP|String|オブジェクト (文字データ) の指定に対するタイムスタンプ。|
|状態|String|オブジェクトのステータス (VALID、INVALID、または N/A)。|
|TEMPORARY|String|オブジェクトが一時的かどうかを示します (現在のセッションでは、オブジェクト自体に置かれたデータだけが表示される)。|
|GENERATED|String|このオブジェクトの名前がシステムによって生成されたかどうかを示します  (Y &#124; N)。|
|SECONDARY|String|Oracle9i Data Cartridge の ODCIIndexCreate メソッドによって作成されたセカンダリ オブジェクトかどうかを示します (Y &#124; N)。|
|CREATED|DateTime|オブジェクトが作成された日付。|

## <a name="sequences"></a>シーケンス

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|SEQUENCE_OWNER|String|シーケンスの所有者の名前。|
|SEQUENCE_NAME|String|シーケンス名。|
|MIN_VALUE|Decimal (10 進数型)|シーケンスの最小値。|
|MAX_VALUE|Decimal (10 進数型)|シーケンスの最大値。|
|INCREMENT_BY|Decimal (10 進数型)|シーケンスがインクリメントされる値。|
|CYCLE_FLAG|String|限界に到達するとシーケンスはラップされるかを示します。|
|ORDER_FLAG|String|順に生成されたシーケンス番号。|
|CACHE_SIZE|Decimal (10 進数型)|キャッシュするシーケンス番号の数。|
|LAST_NUMBER|Decimal (10 進数型)|ディスクに書き込まれた最後のシーケンス番号。 シーケンスでキャッシュが使用される場合、ディスクに書き込まれた数はシーケンスのキャッシュに置かれた最後の番号になります。 この番号は多くの場合、使用された最後のシーケンス番号より大きくなります。|

## <a name="synonyms"></a>Synonyms

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|シノニムの所有者。|
|SYNONYM_NAME|String|シノニムの名前。|
|TABLE_OWNER|String|シノニムが参照するオブジェクトの所有者。|
|TABLE_NAME|String|シノニムが参照するオブジェクトの名前。|
|DB_LINK|String|参照されるデータベース リンクの名前 (参照される場合)。|

## <a name="tables"></a>[テーブル]

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|テーブルの所有者。|
|TABLE_NAME|String|テーブルの名前。|
|TYPE|String|テーブルの型。|

## <a name="users"></a>Users

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|NAME|String|ユーザー名。|
|ID|Decimal (10 進数型)|ユーザーの ID 番号。|
|CREATEDATE|DateTime|ユーザーの作成日。|

## <a name="views"></a>Views

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|ビューの所有者。|
|VIEW_NAME|String|ビューの名前。|
|TEXT_LENGTH|Decimal (10 進数型)|ビュー テキストの長さ。|
|TEXT|String|ビュー テキスト。|
|TYPE_TEXT_LENGTH|Decimal (10 進数型)|型指定されたビューの TYPE 句の長さ。|
|TYPE_TEXT|String|型指定されたビューの TYPE 句。|
|OID_TEXT_LENGTH|Decimal (10 進数型)|型指定されたビューの WITH OID 句の長さ。|
|OID_TEXT|String|型指定されたビューの WITH OID 句。|
|VIEW_TYPE_OWNER|String|ビューが型指定されたビューである場合の、ビューの型の所有者。|
|VIEW_TYPE|String|ビューが型指定されたビューである場合の、ビューの型。|
|SUPERVIEW_NAME|String|スーパービューの名前。|

## <a name="functions"></a>関数

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者。|
|OBJECT_NAME|String|オブジェクト名。|
|SUBOBJECT_NAME|String|サブオブジェクト名 (partition など)。|
|OBJECT_ID|Decimal (10 進数型)|オブジェクトの辞書オブジェクト数。|
|DATA_OBJECT_ID|Decimal (10 進数型)|オブジェクトを含むセグメントの辞書オブジェクト数。|
|OBJECT_TYPE|String|オブジェクトの型。|
|CREATED|DateTime|オブジェクトが作成された日付。|
|LAST_DDL_TIME|DateTime|DDL コマンド (許可および取り消しを含む) の実行結果として、最後に変更されたオブジェクトのタイムスタンプ。|
|TIMESTAMP|String|オブジェクト (文字データ) の指定に対するタイムスタンプ。|
|状態|String|オブジェクトのステータス (VALID、INVALID、または N/A)。|
|TEMPORARY|String|オブジェクトが一時的かどうかを示します (現在のセッションでは、オブジェクト自体に置かれたデータだけが表示される)。|
|GENERATED|String|このオブジェクトの名前がシステムによって生成されたかどうかを示します  (Y &#124; N)。|
|SECONDARY|String|Oracle9i Data Cartridge の ODCIIndexCreate メソッドによって作成されたセカンダリ オブジェクトかどうかを示します (Y &#124; N)。|

## <a name="packages"></a>パッケージ

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者。|
|OBJECT_NAME|String|オブジェクト名。|
|SUBOBJECT_NAME|String|サブオブジェクト名 (partition など)。|
|OBJECT_ID|Decimal (10 進数型)|オブジェクトの辞書オブジェクト数。|
|DATA_OBJECT_ID|Decimal (10 進数型)|オブジェクトを含むセグメントの辞書オブジェクト数。|
|LAST_DDL_TIME|DateTime|DDL コマンド (許可および取り消しを含む) の実行結果として、最後に変更されたオブジェクトのタイムスタンプ。|
|TIMESTAMP|String|オブジェクト (文字データ) の指定に対するタイムスタンプ。|
|状態|String|オブジェクトのステータス (VALID、INVALID、または N/A)。|
|TEMPORARY|String|オブジェクトが一時的かどうかを示します (現在のセッションでは、オブジェクト自体に置かれたデータだけが表示される)。|
|GENERATED|String|このオブジェクトの名前がシステムによって生成されたかどうかを示します  (Y &#124; N)。|
|SECONDARY|String|Oracle9i Data Cartridge の ODCIIndexCreate メソッドによって作成されたセカンダリ オブジェクトかどうかを示します (Y &#124; N)。|
|CREATED|DateTime|オブジェクトが作成された日付。|

## <a name="packagebodies"></a>PackageBodies

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者。|
|OBJECT_NAME|String|オブジェクト名。|
|SUBOBJECT_NAME|String|サブオブジェクト名 (partition など)。|
|OBJECT_ID|Decimal (10 進数型)|オブジェクトの辞書オブジェクト数。|
|DATA_OBJECT_ID|Decimal (10 進数型)|オブジェクトを含むセグメントの辞書オブジェクト数。|
|LAST_DDL_TIME|DateTime|DDL コマンド (許可および取り消しを含む) の実行結果として、最後に変更されたオブジェクトのタイムスタンプ。|
|TIMESTAMP|String|オブジェクト (文字データ) の指定に対するタイムスタンプ。|
|状態|String|オブジェクトのステータス (VALID、INVALID、または N/A)。|
|TEMPORARY|String|オブジェクトが一時的かどうかを示します (現在のセッションでは、オブジェクト自体に置かれたデータだけが表示される)。|
|GENERATED|String|このオブジェクトの名前がシステムによって生成されたかどうかを示します  (Y &#124; N)。|
|SECONDARY|String|Oracle9i Data Cartridge の ODCIIndexCreate メソッドによって作成されたセカンダリ オブジェクトかどうかを示します (Y &#124; N)。|
|CREATED|DateTime|オブジェクトが作成された日付。|

## <a name="arguments"></a>引数

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者の名前。|
|PACKAGE_NAME|String|パッケージ名。|
|OBJECT_NAME|String|プロシージャまたは関数の名前。|
|ARGUMENT_NAME|String|引数の名前。|
|POSITION|Decimal (10 進数型)|引数リスト内の位置。関数の戻り値の場合は NULL。|
|SEQUENCE|Decimal (10 進数型)|入れ子になったすべてのレベルを含む引数シーケンス。|
|DEFAULT_VALUE|String|引数の既定値。|
|DEFAULT_LENGTH|Decimal (10 進数型)|引数の既定値の長さ。|
|IN_OUT|String|引数の方向 (IN、OUT、または IN/OUT)。|
|DATA_LENGTH|Decimal (10 進数型)|列の長さ (バイト単位)。|
|DATA_PRECISION|Decimal (10 進数型)|小数桁数 (NUMBER) またはバイナリ桁数 (FLOAT) の長さ。|
|DATA_SCALE|Decimal (10 進数型)|数値の小数点の右側にある数字。|
|DATA_TYPE|String|引数のデータ型。|

## <a name="uniquekeys"></a>UniqueKeys

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|制約定義の所有者。|
|CONSTRAINT_NAME|String|制約定義の名前。|
|TABLE_NAME|String|制約定義を持つテーブル (またはビュー) に関連付けられた名前。|
|SEARCH_CONDITION|String|CHECK 制約の検索条件のテキスト。|
|R_OWNER|String|参照制約で参照されるテーブルの所有者。|
|R_CONSTRAINT_NAME|String|参照テーブルの UNIQUE 制約の定義の名前。|
|DELETE_RULE|String|参照制約の削除規則 (CASCADE または NO ACTION)。|
|状態|String|制約の強制ステータス (ENABLED または DISABLED)。|
|DEFERRABLE|String|制約を遅延可能にするかどうかを示します。|
|VALIDATED|String|すべてのデータが制約に従うかどうかを示します (VALIDATED または NOT VALIDATED)。|
|GENERATED|String|制約の名前がユーザーとシステムのどちらによって生成されたかを示します。|
|BAD|String|値 YES は、この制約が世紀をあいまいに指定していることを示します。 このあいまいさによるエラーを回避するには、TO_DATE 関数に 4 桁の西暦を使って制約を定義し直します。|
|RELY|String|有効な制約が強制されたものであるかどうかを示します。|
|LAST_CHANGE|DateTime|制約が最後に有効または無効になった日時を示します。|
|INDEX_OWNER|String|インデックスを所有するユーザーの名前。|
|INDEX_NAME|String|インデックス名。|

## <a name="primarykeys"></a>PrimaryKeys

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|制約定義の所有者。|
|CONSTRAINT_NAME|String|制約定義の名前。|
|TABLE_NAME|String|制約定義を持つテーブル (またはビュー) に関連付けられた名前。|
|SEARCH_CONDITION|String|CHECK 制約の検索条件のテキスト。|
|R_OWNER|String|参照制約で参照されるテーブルの所有者。|
|R_CONSTRAINT_NAME|String|参照テーブルの UNIQUE 制約の定義の名前。|
|DELETE_RULE|String|参照制約の削除規則 (CASCADE または NO ACTION)。|
|状態|String|制約の強制ステータス (ENABLED または DISABLED)。|
|DEFERRABLE|String|制約を遅延可能にするかどうかを示します。|
|VALIDATED|String|すべてのデータが制約に従うかどうかを示します (VALIDATED または NOT VALIDATED)。|
|GENERATED|String|制約の名前がユーザーとシステムのどちらによって生成されたかを示します。|
|BAD|String|値 YES は、この制約が世紀をあいまいに指定していることを示します。 このあいまいさによるエラーを回避するには、TO_DATE 関数に 4 桁の西暦を使って制約を定義し直します。|
|RELY|String|有効な制約が強制されたものであるかどうかを示します。|
|LAST_CHANGE|DateTime|制約が最後に有効または無効になった日時を示します。|
|INDEX_OWNER|String|インデックスを所有するユーザーの名前。|
|INDEX_NAME|String|インデックス名。|

## <a name="foreignkeys"></a>ForeignKeys

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|PRIMARY_KEY_CONSTRAINT_NAME|String|制約定義の名前。|
|PRIMARY_KEY_OWNER|String|制約定義の所有者。|
|PRIMARY_KEY_TABLE_NAME|String|制約定義を持つテーブル (またはビュー) に関連付けられた名前。|
|FOREIGN_KEY_OWNER|String|制約定義の所有者。|
|FOREIGN_KEY_CONSTRAINT_NAME|String|制約定義の名前。|
|FOREIGN_KEY_TABLE_NAME|String|制約定義を持つテーブル (またはビュー) に関連付けられた名前。|
|SEARCH_CONDITION|String|CHECK 制約の検索条件のテキスト。|
|R_OWNER|String|参照制約で参照されるテーブルの所有者。|
|R_CONSTRAINT_NAME|String|参照テーブルの UNIQUE 制約の定義の名前。|
|DELETE_RULE|String|参照制約の削除規則 (CASCADE または NO ACTION)。|
|状態|String|制約の強制ステータス (ENABLED または DISABLED)。|
|VALIDATED|String|すべてのデータが制約に従うかどうかを示します (VALIDATED または NOT VALIDATED)。|
|GENERATED|String|制約の名前がユーザーとシステムのどちらによって生成されたかを示します。|
|RELY|String|有効な制約が強制されたものであるかどうかを示します。|
|LAST_CHANGE|DateTime|制約が最後に有効または無効になった日時を示します。|
|INDEX_OWNER|String|インデックスを所有するユーザーの名前。|
|INDEX_NAME|String|インデックス名。|

## <a name="foreignkeycolumns"></a>ForeignKeyColumns

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|制約定義の所有者。|
|CONSTRAINT_NAME|String|制約定義の名前。|
|TABLE_NAME|String|制約定義を持つテーブル名。|
|COLUMN_NAME|String|制約定義で指定されているオブジェクト型列の列名または属性名。|
|POSITION|Decimal (10 進数型)|オブジェクトの定義内の列または属性の元の位置。|

## <a name="procedureparameters"></a>ProcedureParameters

|ColumnName|DataType|説明|
|----------------|--------------|-----------------|
|OWNER|String|オブジェクトの所有者。|
|OBJECT_NAME|String|プロシージャまたは関数の名前。|
|PACKAGE_NAME|String|プロシージャまたは関数の名前。|
|OBJECT_ID|Decimal (10 進数型)|オブジェクトのオブジェクト番号。|
|OVERLOAD|String|オーバーロードの一意識別子。|
|ARGUMENT_NAME|String|引数の名前。|
|POSITION|Decimal (10 進数型)|引数リスト内の位置。関数の戻り値の場合は NULL。|
|SEQUENCE|Decimal (10 進数型)|入れ子になったすべてのレベルを含む引数シーケンス。|
|DATA_LEVEL|Decimal (10 進数型)|複合型の引数の入れ子の深さ。|
|DATA_TYPE|String|引数のデータ型。|
|DEFAULT_VALUE|String|引数の既定値。|
|DEFAULT_LENGTH|Decimal (10 進数型)|引数の既定値の長さ。|
|IN_OUT|String|引数の方向 (IN、OUT、または IN/OUT)。|
|DATA_LENGTH|Decimal (10 進数型)|列の長さ (バイト単位)。|
|DATA_PRECISION|Decimal (10 進数型)|小数桁数 (NUMBER) またはバイナリ桁数 (FLOAT) の長さ。|
|DATA_SCALE|Decimal (10 進数型)|数値の小数点の右側にある数字。|
|RADIX|Decimal (10 進数型)|数値の引数の基数。|
|CHARACTER_SET_NAME|String|引数の文字セットの名前。|
|TYPE_OWNER|String|引数の型の所有者。|
|TYPE_NAME|String|引数の型の名前。 パッケージ ローカル型である (パッケージ指定で宣言されている) 場合、この列にはパッケージ名が表示されます。|
|TYPE_SUBNAME|String|パッケージ ローカル型にのみ関係します。 TYPE_NAME 列で特定されたパッケージで宣言された型の名前が表示されます。|
|TYPE_LINK|String|TYPE_NAME 列で特定されたパッケージがリモート パッケージである場合は、パッケージ ローカル型のみに関係します。 この列には、リモート パッケージの参照に使用されるデータベース リンクが表示されます。|
|PLS_TYPE|String|数値引数の場合、引数の PL/SQL 型の名前を示します。 その他の場合は NULL が返されます。|
|CHAR_LENGTH|Decimal (10 進数型)|文字列データ型の文字数制限。|
|CHAR_USED|String|文字列のバイト数制限 (B) または文字数制限 (C) が正式であるかどうかを示します。|

## <a name="see-also"></a>関連項目

- [ADO.NET の概要](ado-net-overview.md)
