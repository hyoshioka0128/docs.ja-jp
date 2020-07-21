---
title: アーキテクチャとデザイン
ms.date: 03/30/2017
ms.assetid: bd738d39-00e2-4bab-b387-90aac1a014bd
ms.openlocfilehash: 35fbc39db23a2b08ab926e122d2f1eb1806a369b
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040022"
---
# <a name="architecture-and-design"></a>アーキテクチャとデザイン

[サンプル プロバイダー](https://code.msdn.microsoft.com/windowsdesktop/Entity-Framework-Sample-6a9801d0)の SQL 生成モジュールは、コマンド ツリーを表す式ツリー上のビジターとして実装されます。 生成は、式ツリーを介した単一のパスで行われます。

ツリーのノードはボトムアップ方式で処理されます。 まず、中間構造として SqlSelectStatement または SqlBuilder が生成され、いずれでも ISqlFragment が実装されています。 次に、文字列である SQL ステートメントがその構造から生成されます。 中間構造には 2 つの理由があります。

- 論理上、SQL SELECT ステートメントは順序を無視して挿入されます。 FROM 句に参加するノードは、WHERE 句、GROUP BY 句、および ORDER BY 句に参加するノードの前にアクセスされます。

- 別名の名前を変更するには、名前の変更中に競合が発生しないように、使用されているすべての別名を識別する必要があります。 SqlBuilder で名前変更の選択を遅らせるには、Symbol オブジェクトを使用して、名前変更の候補となる列を表します。

![図](./media/de1ca705-4f7c-4d2d-ace5-afefc6d3cefa.gif "de1ca705-4f7c-4d2d-ace5-afefc6d3cefa")

最初のフェーズでは、式ツリーにアクセスしている間、式が SqlSelectStatement にグループ化され、結合がフラット化され、結合の別名がフラット化されます。 この段階では、Symbol オブジェクトは、名前変更が可能な列または入力の別名を表します。

2 番目のフェーズでは、実際の文字列を生成している間、別名の名前が変更されます。

## <a name="data-structures"></a>データ構造

ここでは、SQL ステートメントを作成するために使用する[サンプル プロバイダー](https://code.msdn.microsoft.com/windowsdesktop/Entity-Framework-Sample-6a9801d0)で使用されている型について説明します。

### <a name="isqlfragment"></a>ISqlFragment

このセクションでは、ISqlFragment インターフェイスを実装するクラスについて説明します。このインターフェイスは、2 つの目的を達成します。

- すべてのビジター メソッドに共通する戻り値の型です。

- 最終的な SQL 文字列を作成するためのメソッドを指定します。

```csharp
internal interface ISqlFragment {
   void WriteSql(SqlWriter writer, SqlGenerator sqlGenerator);
}
```

#### <a name="sqlbuilder"></a>SqlBuilder

SqlBuilder は、StringBuilder と同様に、最終的な SQL 文字列の収集デバイスです。 これは、最終的な SQL を構成する文字列、および文字列に変換できる ISqlFragment で構成されます。

```csharp
internal sealed class SqlBuilder : ISqlFragment {
   public void Append(object s)
   public void AppendLine()
   public bool IsEmpty
}
```

#### <a name="sqlselectstatement"></a>SqlSelectStatement

SqlSelectStatement では、次のような正規の SQL SELECT ステートメントの形式が表されます: "SELECT …  FROM ...  WHERE … GROUP BY …  ORDER BY"。

各 SQL 句は StringBuilder によって表されます。 また、Distinct が指定されているかどうか、およびステートメントが最上位かどうかを追跡します。 ステートメントが最上位ではなく、ステートメントに TOP 句も含まれていない場合は、ORDER BY 句は省略されます。

FromExtents には、SELECT ステートメントの入力のリストが格納されます。 通常、これに含まれる要素は 1 つだけです。 結合のための SELECT ステートメントには、一時的に、複数の要素が含まれる場合があります。

SELECT ステートメントが結合ノードによって作成されると、SqlSelectStatement は、AllJoinExtents の結合でフラット化されたすべてのエクステントのリストを保持します。 OuterExtents は SqlSelectStatement の外部参照を表し、入力の別名の名前変更に使用されます。

```csharp
internal sealed class SqlSelectStatement : ISqlFragment {
   internal bool IsDistinct { get, set };
   internal bool IsTopMost

   internal List<Symbol> AllJoinExtents { get, set };
   internal List<Symbol> FromExtents { get};
   internal Dictionary<Symbol, bool> OuterExtents { get};

   internal TopClause Top { get, set };

   internal SqlBuilder Select {get};
   internal SqlBuilder From
   internal SqlBuilder Where
   internal SqlBuilder GroupBy
   public SqlBuilder OrderBy
}
```

#### <a name="topclause"></a>TopClause

TopClause は SqlSelectStatement の TOP 式を表します。 TopCount プロパティは、選択する必要がある TOP 行の数を示します。  WithTies が true の場合、TopClause は DbLimitExpression から作成されています。

```csharp
class TopClause : ISqlFragment {
   internal bool WithTies {get}
   internal ISqlFragment TopCount {get}
   internal TopClause(ISqlFragment topCount, bool withTies)
   internal TopClause(int topCount, bool withTies)
}
```

### <a name="symbols"></a>シンボル

Symbol 関連のクラスおよびシンボル テーブルは、入力の別名の名前変更、結合の別名のフラット化、および列の別名の名前変更を実行します。

Symbol クラスは、エクステント、入れ子になった SELECT ステートメント、または列を表します。 Symbol クラスは、使用後に名前を変更できるように、実際の別名の代わりに使用されます。また、Symbol クラスが表す成果物の追加情報も伝達します (型も同様です)。

```csharp
class Symbol : ISqlFragment {
   internal Dictionary<string, Symbol> Columns {get}
   internal bool NeedsRenaming {get, set}
   internal bool IsUnnest {get, set}   //not used

   public string Name{get}
   public string NewName {get,set}
   internal TypeUsage Type {get, set}

   public Symbol(string name, TypeUsage type)
}
```

Name には、表されるエクステント、入れ子になった SELECT ステートメント、または列の元の別名が格納されます。

NewName には、SQL SELECT ステートメントで使用される別名が格納されます。 最初は Name に設定され、最終的な文字列クエリを生成する際に必要な場合のみ、名前が変更されます。

Type は、エクステントおよび入れ子になった SELECT ステートメントを表すシンボルの場合のみ有効です。

#### <a name="symbolpair"></a>SymbolPair

SymbolPair クラスは、レコードのフラット化に対処します。

プロパティ式 D(v, "j3.j2.j1.a.x") を考えてみます。この式では、v は VarRef、j1、j2、j3 は結合、a はエクステント、x は列です。

これは、最終的に {j'}.{x'} に変換する必要があります。 ソース フィールドが表す最も外側の SqlStatement は、結合式 (j2 など) を表します。つまり、これは常に Join シンボルです。 列フィールドは、非結合シンボルで停止するまで、ある結合シンボルから次の結合シンボルに移動します。 これは、DbPropertyExpression にアクセスすると返されますが、SqlBuilder に追加されることはありません。

```csharp
class SymbolPair : ISqlFragment {
   public Symbol Source;
   public Symbol Column;
   public SymbolPair(Symbol source, Symbol column)
}
```

#### <a name="joinsymbol"></a>JoinSymbol

Join シンボルは、結合または結合入力を含む入れ子になった SELECT ステートメントを表す Symbol です。

```csharp
internal sealed class JoinSymbol : Symbol {
   internal List<Symbol> ColumnList {get, set}
   internal List<Symbol> ExtentList {get}
   internal List<Symbol> FlattenedExtentList {get, set}
   internal Dictionary<string, Symbol> NameToExtent {get}
   internal bool IsNestedJoin {get, set}

   public JoinSymbol(string name, TypeUsage type, List<Symbol> extents)
}
```

このシンボルが SQL SELECT ステートメントを表す場合、ColumnList は SELECT 句内の列のリストを表します。 ExtentList は、SELECT 句内のエクステントのリストです。 結合により最上位で複数のエクステントがフラット化された場合、FlattenedExtentList はそのエクステントを追跡し、エクステントの別名が正しく変更されたことを確認します。

NameToExtent は、ExtentList 内のすべてのエクステントをディクショナリとして使用します。 IsNestedJoin は、JoinSymbol が通常の結合シンボルか、対応する SqlSelectStatement を持つ結合シンボルかを判断するために使用します。

すべてのリストは、正確に設定されると、参照または列挙に使用されます。

#### <a name="symboltable"></a>SymbolTable

SymbolTable は、変数名を Symbol に解決するために使用されます。 SymbolTable は、各スコープの新しいエントリを持つスタックとして実装されます。 Lookup は、エントリが見つかるまでスタックの最上位から最下位まで検索します。

```csharp
internal sealed class SymbolTable {
   internal void EnterScope()
   internal void ExitScope()
   internal void Add(string name, Symbol value)
   internal Symbol Lookup(string name)
}
```

SQL 生成モジュールのインスタンス 1 つにつき、SymbolTable は 1 つしかありません。 各リレーショナル ノードでは、スコープへの出入りが行われます。 前のスコープ内のすべてのシンボルは、同じ名前の他のシンボルによって非表示になっている場合を除いて、後のスコープに表示されます。

### <a name="global-state-for-the-visitor"></a>ビジターのグローバル状態

別名と列の名前変更を支援するために、クエリ ツリーを最初に通過する際に使用されたすべての列名 (AllColumnNames) とすべてのエクステントの別名 (AllExtentNames) のリストを保持します。  シンボル テーブルは、変数名を Symbol に解決します。 IsVarRefSingle は、検証目的でのみ使用されるため、必ずしも必要ではありません。

CurrentSelectStatement および IsParentAJoin を介して使用される 2 つのスタックは、親ノードから子ノードに "parameters" を渡すために使用されます。これは、ビジター パターンによってパラメーターを渡すことができないためです。

```csharp
internal Dictionary<string, int> AllExtentNames {get}
internal Dictionary<string, int> AllColumnNames {get}
SymbolTable symbolTable = new SymbolTable();
bool isVarRefSingle = false;

Stack<SqlSelectStatement> selectStatementStack;
private SqlSelectStatement CurrentSelectStatement{get}

Stack<bool> isParentAJoinStack;
private bool IsParentAJoin{get}
```

## <a name="common-scenarios"></a>一般的なシナリオ

このセクションでは、一般的なプロバイダー シナリオについて説明します。

### <a name="grouping-expression-nodes-into-sql-statements"></a>SQL ステートメントへの式ノードのグループ化

ボトムアップ方式でツリーにアクセスしたときに最初のリレーショナル ノード (通常は DbScanExpression エクステント) が見つかった場合に SqlSelectStatement が作成されます。 入れ子になったクエリをできるだけ少なくして SQL SELECT ステートメントを生成するには、その SqlSelectStatement でできるだけ多くの親ノードを集計します。

特定の (リレーショナル) ノードを現在の SqlSelectStatement (入力にアクセスしたときに返される SqlSelectStatement) に追加できるかどうか、または新しいステートメントを開始する必要があるかどうかの決定は、IsCompatible メソッドによって計算され、SqlSelectStatement に既に含まれるノードに依存します。これは、指定されたノードの下にあったノードによって異なります。

通常、連結が検討されているノードが空ではない句の後に SQL ステートメントの句が評価される場合、そのノードを現在のステートメントに追加することはできません。 たとえば、次のノードが Filter の場合、そのノードを現在の SqlSelectStatement に組み込むことができるのは、次の条件に当てはまる場合のみです。

- SELECT リストが空の場合。 SELECT リストが空ではない場合、SELECT リストはフィルターの前のノードによって生成されているため、述語はその SELECT リストによって生成された列を参照できます。

- GROUPBY が空の場合。 GROUPBY が空ではない場合、フィルターを追加すると、グループ化の前にフィルター処理することになりますが、これは正しい処理ではありません。

- TOP 句が空の場合。 TOP 句が空ではない場合、フィルターを追加すると、TOP を実行する前にフィルター処理することになりますが、これは正しい処理ではありません。

これは、DbConstantExpression や算術式のような非リレーショナル ノードには当てはまりません。非リレーショナル ノードは、常に既存の SqlSelectStatement に含まれているためです。

また、結合ツリーのルート (結合の親を持たない結合ノード) が見つかると、新しい SqlSelectStatement が開始されます。 左辺スパイン結合の子はすべて、その SqlSelectStatement に集計されます。

新しい SqlSelectStatement が開始され、現在の SqlSelectStatement が入力に追加されるたびに、投影列 (SELECT 句) が存在しない場合はこの列を追加することによって、現在の SqlSelectStatement を完了することが必要になる場合があります。 これを行うには、AddDefaultColumns メソッドを使用します。このメソッドは、SqlSelectStatement の FromExtents を参照し、FromExtents が表すエクステントのリストによってスコープに取り込まれるすべての列を、投影された列のリストに追加します。 これが実行されるのは、その時点で、他のノードが参照している列が不明なためです。 これは、後で使用できる列のみを投影するように最適化できます。

### <a name="join-flattening"></a>結合のフラット化

IsParentAJoin プロパティは、特定の結合をフラット化できるかどうかを判断するのに役立ちます。 特に、IsParentAJoin は、結合の左側の子、および結合への即時入力となる各 DbScanExpression に対してのみ `true` を返します。この場合、その子ノードでは、後で親で使用されるのと同じ SqlSelectStatement が再利用されます。 詳細については、「結合式」を参照してください。

### <a name="input-alias-redirecting"></a>入力の別名のリダイレクト

入力の別名のリダイレクトは、シンボル テーブルによって行われます。

入力の別名のリダイレクトを説明するには、「[コマンド ツリーからの SQL の生成: ベスト プラクティス](generating-sql-from-command-trees-best-practices.md)」の最初の例を参照してください。  この例では、"a" を投影の "b" にリダイレクトする必要がありました。

SqlSelectStatement オブジェクトが作成されると、ノードへの入力であるエクステントが SqlSelectStatement の From プロパティに配置されます。 Symbol (\<symbol_b>) は、入力バインディング名 ("b") に基づいて作成され、エクステントおよび "AS  " + \<symbol_b> が From 句に追加されることを表します。  シンボルは FromExtents プロパティにも追加されます。

シンボルはシンボル テーブルにも追加され、入力バインディング名がシンボルにリンクされます ("b", \<symbol_b>)。

後続のノードが SqlSelectStatement を再利用する場合、シンボル テーブルにエントリが追加され、その入力バインディング名がそのシンボルにリンクされます。 この例では、入力バインディング名が "a" の DbProjectExpression により、SqlSelectStatement を再利用して ("a", \< symbol_b>) が表に追加されます。

SqlSelectStatement を再利用しているノードの入力バインディング名を式で参照すると、その参照は、シンボル テーブルを使用して、リダイレクトされた正しいシンボルに解決されます。 "a" を表す DbVariableReferenceExpression にアクセスしているときに "a.x" から "a" に解決されると、Symbol \<symbol_b> に解決されます。

### <a name="join-alias-flattening"></a>結合の別名のフラット化

結合の別名のフラット化は、「DbPropertyExpression」で説明されているように、DbPropertyExpression にアクセスするときに行われます。

### <a name="column-name-and-extent-alias-renaming"></a>列名およびエクステントの別名の名前変更

列名とエクステントの別名の名前変更に関する問題を解決するには、「SQL 生成の 2 番目のフェーズ: 文字列コマンドの生成」で説明されている、生成の 2 番目のフェーズで別名に置換されるシンボルを使用します。

## <a name="first-phase-of-the-sql-generation-visiting-the-expression-tree"></a>SQL 生成の最初のフェーズ: 式ツリーへのアクセス

このセクションでは、SQL 生成の最初のフェーズについて説明します。このフェーズでは、クエリを表す式にアクセスするときに、中間構造 SqlSelectStatement または SqlBuilder が生成されます。

このセクションでは、さまざまな式ノード カテゴリにアクセスする際の原則、および特定の式の型にアクセスする際の詳細について説明します。

### <a name="relational-non-join-nodes"></a>リレーショナル (非結合) ノード

非結合ノードをサポートする式の型を次に示します。

- DbDistinctExpression

- DbFilterExpression

- DbGroupByExpression

- DbLimitExpression

- DbProjectExpression

- DbSkipExpression

- DbSortExpression

これらのノードへのアクセスは、次のパターンに従います。

1. リレーショナル入力にアクセスし、結果の SqlSelectStatement を取得します。 リレーショナル ノードへの入力は次のいずれかになります。

    - エクステントを含むリレーショナル ノード (DbScanExpression など)。 このようなノードにアクセスすると、SqlSelectStatement が返されます。

    - 集合演算式 (UNION ALL など)。 結果は、角かっこで囲み、新しい SqlSelectStatement の FROM 句に配置する必要があります。

2. 入力によって生成された SqlSelectStatement に現在のノードを追加できるかどうかを確認します。 これについては、「SQL ステートメントへの式ノードのグループ化」で説明しています。 追加できない場合は、次の操作を行います。

    - 現在の SqlSelectStatement オブジェクトを表示します。

    - 新しい SqlSelectStatement オブジェクトを作成し、表示された SqlSelectStatement を新しい SqlSelectStatement オブジェクトの FROM として追加します。

    - スタックの先頭に新しいオブジェクトを配置します。

3. 入力式バインディングを入力から正しいシンボルにリダイレクトします。 この情報は、SqlSelectStatement オブジェクトに保持されます。

4. 新しい SymbolTable スコープを追加します。

5. 式の非入力部分 (投影や述語など) にアクセスします。

6. グローバル スタックに追加されたすべてのオブジェクトを表示します。

 SQL で DbSkipExpression に相当するものはありません。 論理上、次のように変換されます。

```sql
SELECT Y.x1, Y.x2, ..., Y.xn
FROM (
   SELECT X.x1, X.x2, ..., X.xn, row_number() OVER (ORDER BY sk1, sk2, ...) AS [row_number]
   FROM input as X
   ) as Y
WHERE Y.[row_number] > count
ORDER BY sk1, sk2, ...
```

### <a name="join-expressions"></a>結合式

次の式は結合式と見なされ、VisitJoinExpression メソッドによって一般的な方法で処理されます。

- DbApplyExpression

- DbJoinExpression

- DbCrossJoinExpression

アクセスする手順を次に示します。

まず、子にアクセスする前に、IsParentAJoin を呼び出し、結合ノードが左スパインに沿った結合の子であるかどうかを確認します。 false が返された場合は、新しい SqlSelectStatement が開始されます。 その意味で、結合にアクセスする方法はその他のノードとは異なります。これは、親 (結合ノード) によって、子が使用する可能性のある SqlSelectStatement が作成されるためです。

次に、入力を 1 つずつ処理します。 入力ごとに、次の手順を実行します。

1. 入力にアクセスします。

2. ProcessJoinInputResult を呼び出して、入力にアクセスした結果の後処理を実行します。ProcessJoinInputResult は、結合式の子にアクセスした後にシンボル テーブルを保持し、場合によっては、子によって生成された SqlSelectStatement を終了します。 子の結果は次のいずれかになります。

    - 親が追加される SqlSelectStatement とは別の SqlSelectStatement。 この場合、既定の列を追加して完了する必要があります。 入力が Join だった場合、新しい結合シンボルを作成する必要があります。 それ以外の場合は、標準のシンボルを作成します。

    - エクステント (DbScanExpression など)。この場合、エクステントは親の SqlSelectStatement の入力のリストに追加されます。

    - SqlSelectStatement 以外。この場合、角かっこで囲まれています。

    - 親が追加されるのと同じ SqlSelectStatement。 この場合、FromExtents リスト内のシンボルは、すべてのシンボルを表す新しい 1 つの JoinSymbol に置き換える必要があります。

    - 最初の 3 つの場合、AS 句を追加してシンボル テーブルを更新するために AddFromSymbol が呼び出されます。

その後、結合条件がある場合は、その条件にアクセスします。

### <a name="set-operations"></a>セット操作

集合演算 DbUnionAllExpression、DbExceptExpression、および DbIntersectExpression は、VisitSetOpExpression メソッドによって処理されます。 次の構造の SqlBuilder が作成されます。

```xml
<leftSqlSelectStatement> <setOp> <rightSqlSelectStatement>
```

この場合、\<leftSqlSelectStatement> および \<rightSqlSelectStatement> は、各入力にアクセスすることで取得される SqlSelectStatement を表し、\<setOp> は対応する演算 (UNION ALL など) を表します。

### <a name="dbscanexpression"></a>DbScanExpression

(別の結合の左側の子である結合への入力として) 結合コンテキストにアクセスすると、DbScanExpression は対応するターゲット (定義クエリ、テーブル、またはビュー) のターゲット SQL と共に SqlBuilder を返します。 それ以外の場合は、対応するターゲットに対応するように設定された FROM フィールドを使用して新しい SqlSelectStatement が作成されます。

### <a name="dbvariablereferenceexpression"></a>DbVariableReferenceExpression

DbVariableReferenceExpression にアクセスすると、シンボル テーブル内の参照に基づいてその変数参照式に対応する Symbol が返されます。

### <a name="dbpropertyexpression"></a>DbPropertyExpression

結合の別名のフラット化は、DbPropertyExpression にアクセスするときに識別および処理されます。

Instance プロパティは最初にアクセスされると、結果は Symbol、JoinSymbol、または SymbolPair になります。 この 3 つのケースを処理する方法を次に示します。

- JoinSymbol が返された場合、その NameToExtent プロパティには、必要なプロパティのシンボルが格納されます。 結合シンボルが入れ子になった結合を表す場合、新しい Symbol のペアが結合シンボルと共に返され、インスタンスの別名として使用されるシンボルと、さらに解決するために実際のプロパティを表すシンボルを追跡します。

- SymbolPair が返され、その Column 部分が結合シンボルである場合、結合シンボルが再び返されますが、現在のプロパティ式で表されるプロパティを指すように列プロパティが更新されます。 それ以外の場合は、別名として SymbolPair ソース、および列として現在のプロパティのシンボルを含む SqlBuilder が返されます。

- Symbol が返された場合、Visit メソッドは、別名としてそのインスタンス、および列名としてプロパティ名を含む SqlBuilder メソッドを返します。

### <a name="dbnewinstanceexpression"></a>DbNewInstanceExpression

DbProjectExpression の Projection プロパティとして使用する場合、DbNewInstanceExpression は、投影された列を表すためにコンマで区切った引数のリストを生成します。

DbNewInstanceExpression が、コレクションの戻り値の型を格納しており、引数として指定される式の新しいコレクションを定義している場合、次の 3 つのケースは個別に処理されます。

- DbNewInstanceExpression に唯一の引数として DbElementExpression が使用されている場合、次のように変換されます。

```sql
NewInstance(Element(X)) =>  SELECT TOP 1 …FROM X
```

DbNewInstanceExpression に引数がない (空のテーブルを表す) 場合、DbNewInstanceExpression は次のように変換されます。

```sql
SELECT CAST(NULL AS <primitiveType>) as X
FROM (SELECT 1) AS Y WHERE 1=0
```

それ以外の場合、DbNewInstanceExpression は引数の全体結合ラダーを作成します。

```sql
SELECT <visit-result-arg1> as X
UNION ALL SELECT <visit-result-arg2> as X
UNION ALL …
UNION ALL SELECT <visit-result-argN> as X
```

### <a name="dbfunctionexpression"></a>DbFunctionExpression

正規関数と組み込み関数は同じように処理されます。そのため、これらの関数に特別な処理 (TRIM(string) の LTRIM(RTRIM(string)) へのマップなど) が必要な場合は、適切なハンドラーが呼び出されます。 それ以外の場合、これらの関数は FunctionName(arg1, arg2, ..., argn) に変換されます。

特別な処理が必要な関数、およびその関数の適切なハンドラーを追跡するには、ディクショナリを使用します。

ユーザー定義関数は、NamespaceName.FunctionName(arg1, arg2, ..., argn) に変換されます。

### <a name="dbelementexpression"></a>DbElementExpression

DbElementExpression にアクセスするメソッドは、スカラー サブクエリを表すために使用されると DbElementExpression にアクセスする場合にのみ呼び出されます。 したがって、DbElementExpression は、完全な SqlSelectStatement に変換され、その周囲に角かっこを追加します。

### <a name="dbquantifierexpression"></a>DbQuantifierExpression

式の型 (Any または All) に応じて、DbQuantifierExpression は次のように変換されます。

```sql
Any(input, x) => Exists(Filter(input,x))
All(input, x) => Not Exists(Filter(input, not(x))
```

### <a name="dbnotexpression"></a>DbNotExpression

場合によっては、入力式を使用して DbNotExpression の変換を折りたたむことができます。 次に例を示します。

```sql
Not(IsNull(a)) =>  "a IS NOT NULL"
Not(All(input, x) => Not (Not Exists(Filter(input, not(x))) => Exists(Filter(input, not(x))
```

2 番目の折りたたみが行われるのは、All 型の DbQuantifierExpression を変換するときにプロバイダーによって非効率が生じたためです。 したがって、Entity Framework は単純化を実行できませんでした。

### <a name="dbisemptyexpression"></a>DbIsEmptyExpression

DbIsEmptyExpression は次のように変換されます。

```sql
IsEmpty(input) = Not Exists(input)
```

## <a name="second-phase-of-sql-generation-generating-the-string-command"></a>SQL 生成の 2 番目のフェーズ: 文字列コマンドの生成

文字列 SQL コマンドを生成すると、SqlSelectStatement によって、シンボルの実際の別名が生成されます。これにより、列名とエクステントの別名の名前変更に関する問題が解決されます。

エクステントの別名の名前変更は、SqlSelectStatement オブジェクトを文字列に書き込むときに行われます。 まず、外部エクステントで使用されるすべての別名のリストを作成します。 FromExtents (または null 以外の場合は AllJoinExtents) 内の各シンボルは、外部エクステントのいずれかと衝突する場合に名前が変更されます。 名前の変更が必要な場合は、AllExtentNames で収集されたエクステントと競合することはありません。

列の名前変更は、Symbol オブジェクトを文字列に書き込むときに行われます。 最初のフェーズの AddDefaultColumns は、特定の列のシンボルの名前を変更する必要があるかどうかを判断します。 2 番目のフェーズでは、生成された名前が AllColumnNames で使用される名前と競合しないことを確認するために、名前の変更のみが行われます。

エクステントの別名と列の両方について一意の名前を生成するには、\<existing_name>_n を使用します。n はまだ使用されていない最小の別名です。 すべての別名のグローバル リストを使用すると、連鎖名前変更の必要性が高くなります。

## <a name="see-also"></a>関連項目

- [サンプル プロバイダーでの SQL 生成](sql-generation-in-the-sample-provider.md)
