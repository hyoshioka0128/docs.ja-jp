---
title: コマンド ツリーの構造
ms.date: 03/30/2017
ms.assetid: 2215585e-ca47-45f8-98d4-8cb982f8c1d3
ms.openlocfilehash: 8368354049a77a56a5aa54ab500619576f41b0dc
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854264"
---
# <a name="the-shape-of-the-command-trees"></a>コマンド ツリーの構造

SQL 生成モジュールは、指定された入力クエリ コマンド ツリー式に基づいてバックエンドに固有の SQL クエリを生成します。 ここでは、クエリ コマンド ツリーの特性、プロパティ、および構造について説明します。

## <a name="query-command-trees-overview"></a>クエリ コマンド ツリーの概要

クエリ コマンド ツリーは、クエリのオブジェクト モデル表現です。 クエリ コマンド ツリーには、次の 2 つの目的があります。

- Entity Framework に対して指定された入力クエリを表現する。

- プロバイダーに対して提供された出力クエリを表現し、バックエンドに対するクエリを記述する。

クエリ コマンド ツリーでは、入れ子のコレクションおよび型操作、エンティティが特定の型であるかどうかのライク チェック、型に基づくセットのフィルター処理のサポートなど、SQL:1999 準拠のクエリよりも高度なセマンティックがサポートされます。

DBQueryCommandTree.Query プロパティは、クエリのロジックを記述する式ツリーのルートです。 DBQueryCommandTree.Parameters プロパティには、クエリで使用されるパラメーターのリストが格納されます。 式ツリーは、DbExpression オブジェクトから構成されます。

DbExpression オブジェクトは、計算を表します。 Entity Framework では、定数、変数、関数、コンストラクター、およびフィルターや結合のような標準の関係演算子など、クエリ式を構成するための式がいくつか用意されています。 すべての DbExpression オブジェクトには、その式によって生成される結果の型を表す ResultType プロパティがあります。 この型は、TypeUsage として表されます。

## <a name="shapes-of-the-output-query-command-tree"></a>出力クエリ コマンド ツリーの構造

出力クエリ コマンド ツリーは、リレーショナル (SQL) クエリを詳細に表しており、クエリ コマンド ツリーに適用される規則よりもはるかに厳密な規則に従います。 通常、出力クエリ コマンド ツリーの構造は、SQL に簡単に変換することができます。

入力コマンド ツリーは、ナビゲーション プロパティ、エンティティ間のアソシエーション、および継承をサポートする概念モデルに対して表現されます。 出力コマンド ツリーは、ストレージ モデルに対して表現されます。 入力コマンド ツリーでは入れ子になったコレクションを射影することができますが、出力コマンド ツリーではこれはできません。

出力クエリ コマンド ツリーは、利用可能な DbExpression オブジェクトのサブセットを使用して作成されます。また、そのサブセットに含まれる一部の式も、使用法が制限されています。

型の操作、特定の式が特定の型であるかどうかのライク チェック、または型に基づくセットのフィルター処理は、出力コマンド ツリーにはありません。

出力コマンド ツリーでは、ブール値を返す式だけが、射影のために使用されます。また、フィルターや case ステートメントのように述語を必要とする式内の述語のみを対象として使用されます。

出力クエリ コマンド ツリーのルートは、DbProjectExpression オブジェクトです。

### <a name="expression-types-not-present-in-output-query-command-trees"></a>出力クエリ コマンド ツリーに存在しない式の型

次の式の型は出力クエリ コマンド ツリー内では無効であり、プロバイダーによって処理する必要はありません。

- DbDerefExpression

- DbEntityRefExpression

- DbRefKeyExpression

- DbIsOfExpression

- DbOfTypeExpression

- DbRefExpression

- DbRelationshipNavigationExpression

- DbTreatExpression

### <a name="expression-restrictions-and-notes"></a>式の制限および注意事項

式を出力クエリ コマンド ツリー内で使用する場合、多くの式は、その使用方法が制限を受けます。

#### <a name="dbfunctionexpression"></a>DbFunctionExpression

次の種類の関数を渡すことができます。

- Edm 名前空間で認識される正規関数

- BuiltInAttribute で認識される組み込み関数 (ストア関数)

- ユーザー定義関数

正規関数は Entity Framework の一部として指定されています (詳細については、「[正規関数](./language-reference/canonical-functions.md)」を参照)。プロバイダーは、これらの指定に基づいて、正規関数の実装を提供する必要があります。 ストア関数は、対応するプロバイダー マニフェスト内の仕様に基づいています。 ユーザー定義の関数は、SSDL 内の仕様に基づいています。

また、NiladicFunction 属性を持つ関数は引数を持たないため、末尾のかっこを省略して変換する必要があります。  つまり、 *\<functionName>()* ではなく *\<functionName>* のようにします。

#### <a name="dbnewinstanceexpression"></a>DbNewInstanceExpression

DbNewInstanceExpression は、次の 2 つのケースでのみ使用できます。

- DbProjectExpression の Projection プロパティとして使用する場合。  使用時には、次の制限が適用されます。

  - 結果型は行型である必要があります。

  - それぞれの引数は、プリミティブ型の結果を生成する式です。 通常、それぞれの引数は、スカラー式 (たとえば、DbVariableReferenceExpression に対する PropertyExpression)、関数呼び出し、または DbVariableReferenceExpression に対する DbPropertyExpression や関数呼び出しの算術演算です。 ただし、スカラー サブクエリを表す式は、DbNewInstanceExpression の引数リスト内にも使用できます。 スカラー サブクエリを表す式は、DbElementExpression オブジェクト ルートを含むプリミティブ型の 1 行および 1 列のみを返すサブクエリを表す式ツリーです。

- 戻り値の型がコレクション型の場合。この場合は、引数として提供される式の新しいコレクションを定義します。

#### <a name="dbvariablereferenceexpression"></a>DbVariableReferenceExpression

DbVariableReferenceExpression は、DbPropertyExpression ノードの子である必要があります。

#### <a name="dbgroupbyexpression"></a>DbGroupByExpression

DbGroupByExpression の Aggregates プロパティは、DbFunctionAggregate 型の要素のみを持つことができます。 それ以外の集計型はありません。

#### <a name="dblimitexpression"></a>DbLimitExpression

Limit プロパティには、DbConstantExpression または DbParameterReferenceExpression のみを設定できます。 また、.NET Framework Version 3.5 では、WithTies プロパティは常に false です。

#### <a name="dbscanexpression"></a>DbScanExpression

出力コマンド ツリー内で使用した場合、DbScanExpression は、EntitySetBase::Target によって表されるテーブル、ビュー、またはストア クエリに対するスキャンを効果的に表します。

ターゲットの "Defining Query" メタデータ プロパティが null 以外の場合、このプロパティはクエリを表します。クエリのクエリ テキストは、ストア スキーマ定義に指定されたプロバイダーの特定の言語 (またはダイアレクト) でメタデータ プロパティ内に提供されます。

ターゲットの "Defining Query" メタデータ プロパティが null の場合、ターゲットは、テーブルまたはビューを表します。 スキーマ プレフィックスは、null 以外の場合は "Schema" メタデータ プロパティに含まれています。null の場合は、エンティティ コンテナー名が使用されます。  テーブル名またはビュー名は、"Table" メタデータ プロパティに含まれています (このプロパティが null 以外の場合)。このプロパティが null の場合は、エンティティ セット ベースの Name プロパティに含まれています。

これらのプロパティはすべて、ストア スキーマ定義ファイル (SSDL) 内の対応する EntitySet の定義に基づいています。

### <a name="using-primitive-types"></a>プリミティブ型の使用

プリミティブ型を出力コマンド ツリー内で参照する場合、通常は概念モデルのプリミティブ型で参照します。 ただし、一部の式に対しては、対応するストア プリミティブ型がプロバイダーで必要となります。 このような式の例としては、DbCastExpression があります。また、null を対応する型にキャストする必要がある場合は、DbNullExpression も同様です。 こうした式では、プロバイダーは、プリミティブ型の種類およびファセットに基づいて、プロバイダー型へマッピングする必要があります。

## <a name="see-also"></a>関連項目

- [SQL 生成](sql-generation.md)
