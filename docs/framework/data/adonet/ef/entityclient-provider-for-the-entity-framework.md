---
title: Entity Framework 用の EntityClient プロバイダー
ms.date: 03/30/2017
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
ms.openlocfilehash: e3a87d4a936e5bdf633e1f997f66dd98add2a9cb
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854702"
---
# <a name="entityclient-provider-for-the-entity-framework"></a>Entity Framework 用の EntityClient プロバイダー
EntityClient プロバイダーは、概念モデルで記述されているデータにアクセスするために Entity Framework アプリケーションで使用するデータ プロバイダーです。 概念モデルについては、「[モデリングとマッピング](modeling-and-mapping.md)」をご覧ください。 EntityClient は、他の .NET Framework データ プロバイダーを使用してデータ ソースにアクセスします。 たとえば、EntityClient は、SQL Server データベースにアクセスするときは .NET Framework Data Provider for SQL Server (SqlClient) を使用します。 SqlClient プロバイダーについては、「[Entity Framework 用 SqlClient](sqlclient-for-the-entity-framework.md)」をご覧ください。 EntityClient プロバイダーは <xref:System.Data.EntityClient> 名前空間で実装されます。  
  
## <a name="managing-connections"></a>接続の管理  
 Entity Framework は、基になるデータ プロバイダーとリレーショナル データベースへの <xref:System.Data.EntityClient.EntityConnection> を提供することにより、ストレージ固有の ADO.NET データ プロバイダーを基にして構築されます。 <xref:System.Data.EntityClient.EntityConnection> オブジェクトを構築するには、必要なモデルとマッピング、さらにストレージ固有のデータ プロバイダー名と接続文字列を含んだ一連のメタデータを参照する必要があります。 <xref:System.Data.EntityClient.EntityConnection> を確立すると、概念モデルから生成されたクラスを使用してエンティティにアクセスできます。  
  
 app.config ファイルの接続文字列を指定できます。  
  
 <xref:System.Data.EntityClient> には、<xref:System.Data.EntityClient.EntityConnectionStringBuilder> クラスも含まれています。 このクラスを使用すると、開発者はこのクラスのプロパティおよびメソッドを使用することによって、正しい構文の接続文字列をプログラムで作成し、既存の接続文字列の解析や再作成を行うことができます。 詳細については、「[方法: EntityConnection の接続文字列を作成する](how-to-build-an-entityconnection-connection-string.md)」をご覧ください。  
  
## <a name="creating-queries"></a>クエリの作成  
 [!INCLUDE[esql](../../../../../includes/esql-md.md)] 言語は、エンティティの概念スキーマを直接操作し、継承やリレーションシップなどの Entity Data Model 概念をサポートする、ストレージの影響を受けない SQL の言語です。 エンティティ モデルに対して [!INCLUDE[esql](../../../../../includes/esql-md.md)] コマンドを実行するには、<xref:System.Data.EntityClient.EntityCommand> クラスを使用します。 <xref:System.Data.EntityClient.EntityCommand> オブジェクトを構築する場合は、ストアド プロシージャ名またはクエリ テキストを指定できます。 Entity Framework では、ストレージ固有のデータ プロバイダーとの連携により、汎用的な [!INCLUDE[esql](../../../../../includes/esql-md.md)] がストレージ固有のクエリに変換されます。 [!INCLUDE[esql](../../../../../includes/esql-md.md)] のクエリの記述について詳しくは、「[Entity SQL 言語](./language-reference/entity-sql-language.md)」をご覧ください。  
  
 次の例では、<xref:System.Data.EntityClient.EntityCommand> オブジェクトを作成し、[!INCLUDE[esql](../../../../../includes/esql-md.md)] クエリのテキストを <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> プロパティに割り当てます。 この [!INCLUDE[esql](../../../../../includes/esql-md.md)] クエリでは、表示価格で並べ替えた製品を概念モデルに要求します。 次のコードでは、ストレージ モデルが認識されません。  
  
 ```csharp
EntityCommand cmd = conn.CreateCommand();
cmd.CommandText = @"SELECT VALUE p
  FROM AdventureWorksEntities.Product AS p
  ORDER BY p.ListPrice";
```
  
## <a name="executing-queries"></a>クエリの実行  
 クエリを実行すると、そのクエリが解析され、正規コマンド ツリーに変換されます。 すべての後続の処理は、コマンド ツリーで行われます。 コマンド ツリーは、<xref:System.Data.EntityClient> と、<xref:System.Data.SqlClient> などの基になる .NET Framework データ プロバイダーとの間の通信手段です。  
  
 概念モデルに対する <xref:System.Data.EntityClient.EntityDataReader> の実行結果は、<xref:System.Data.EntityClient.EntityCommand> によって公開されます。 <xref:System.Data.EntityClient.EntityDataReader> を返すコマンドを実行するには、<xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A> を呼び出します。 <xref:System.Data.EntityClient.EntityDataReader> は、構造化されたさまざまな結果を記述するための <xref:System.Data.IExtendedDataRecord> を実装します。  
  
## <a name="managing-transactions"></a>トランザクションの管理  
 Entity Framework では、自動トランザクションと明示的トランザクションという 2 つの使用方法があります。 自動トランザクションでは <xref:System.Transactions> 名前空間を使用し、明示的トランザクションでは <xref:System.Data.EntityClient.EntityTransaction> クラスを使用します。  
  
 概念モデルによって公開されたデータを更新するには、「[方法: Entity Framework のトランザクションを管理する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb738523(v=vs.100))」をご覧ください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [方法: EntityConnection の接続文字列を作成する](how-to-build-an-entityconnection-connection-string.md)  
  
 [方法: PrimitiveType の結果を返すクエリを実行する](how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [方法: StructuralType の結果を返すクエリを実行する](how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [方法: RefType の結果を返すクエリを実行する](how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [方法: 複合型を返すクエリを実行する](how-to-execute-a-query-that-returns-complex-types.md)  
  
 [方法: 入れ子になったコレクションを返すクエリを実行する](how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [方法: EntityCommand を使用してパラメーター化 Entity SQL クエリを実行する](how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [方法: EntityCommand を使用してパラメーター化されたストアド プロシージャを実行する](how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [方法: ポリモーフィック クエリを実行する](how-to-execute-a-polymorphic-query.md)  
  
 [方法: Navigate 演算子でリレーションシップをナビゲートする](how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="see-also"></a>関連項目

- [接続とトランザクションの管理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [ADO.NET Entity Framework](index.md)
- [言語リファレンス](./language-reference/index.md)
