---
title: Entity Framework 用の .NET Framework Data Provider for SQL Server (SqlClient) の既知の問題
ms.date: 03/30/2017
ms.assetid: 48fe4912-4d0f-46b6-be96-3a42c54780f6
ms.openlocfilehash: 32a1dd22111498ab5b3b75940f5485b2957367e8
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452501"
---
# <a name="known-issues-in-sqlclient-for-entity-framework"></a>Entity Framework 用の .NET Framework Data Provider for SQL Server (SqlClient) の既知の問題
ここでは、.NET Framework Data Provider for SQL Server (SqlClient) に関連する既知の問題について説明します。  
  
## <a name="trailing-spaces-in-string-functions"></a>文字列関数の末尾のスペース  
 SQL Server では、文字列値の末尾のスペースは無視されます。 そのため、文字列の末尾にスペースを挿入すると、予期できない結果が生じたり、場合によってはエラーが発生することもあります。  
  
 文字列の末尾にスペースを挿入する必要がある場合は、SQL Server で文字列が切り捨てられることがないように、空白文字を挿入することを検討してください。 末尾のスペースが不要である場合は、クエリ パイプラインに渡す前にスペースを削除してください。  
  
## <a name="right-function"></a>RIGHT 関数  
 `RIGHT(nvarchar(max)`, 0`)` または `RIGHT(varchar(max)`, 0`)` に、最初の引数として `null` 以外の値を、2 番目の引数として 0 を渡すと、`empty` 文字列の代わりに `NULL` 値が返されます。  
  
## <a name="cross-and-outer-apply-operators"></a>CROSS APPLY 演算子および OUTER APPLY 演算子  
 CROSS APPLY 演算子および OUTER APPLY 演算子は SQL Server 2005 で導入されました。 場合によっては、クエリ パイプラインにより、CROSS APPLY 演算子または OUTER APPLY 演算子を含む Transact-SQL ステートメントが生成されることがあります。 一部のバックエンド プロバイダー (SQL Server 2005 より古いバージョンの SQL Server など) では、これらの演算子がサポートされていません。したがって、このようなクエリをこれらのバックエンド プロバイダーで実行することはできません。  
  
 CROSS APPLY 演算子または OUTER APPLY 演算子を含むクエリの生成につながる可能性がある一般的なシナリオを次に示します。  
  
- ページングを使用した相関サブクエリ  
  
- 相関サブクエリ全体、またはナビゲーションによって生成されたコレクション全体を対象とした `AnyElement`  
  
- 要素セレクターを受け取るグループ化メソッドを使用する LINQ クエリ  
  
- CROSS APPLY 演算子または OUTER APPLY 演算子が明示的に指定されたクエリ  
  
- REF コンストラクターを引数に取る DEREF コンストラクターを含むクエリ。  
  
## <a name="skip-operator"></a>SKIP 演算子  
 SQL Server 2000 を使用している場合、キー以外の列で ORDER BY と共に SKIP を使用すると、不適切な結果が返される場合があります。 キー以外の列に重複するデータが存在する場合、指定された数を超える行はスキップされます。 これは、SQL Server 2000 での SKIP の変換方法によるものです。 たとえば、次のクエリでは、`E.NonKeyColumn` に重複値が存在する場合、5 行を超える行はスキップされます。  
  
```sql  
SELECT [E] FROM Container.EntitySet AS [E] ORDER BY [E].[NonKeyColumn] DESC SKIP 5L  
```  
  
## <a name="targeting-the-correct-sql-server-version"></a>適切なバージョンの SQL Server を対象としたクエリの実行  
 Entity Framework では、ストレージ モデル (.ssdl) ファイルの Schema 要素の `ProviderManifestToken` 属性で指定されている SQL Server のバージョンに基づいて、実行対象の Transact-SQL クエリが決定されます。 このバージョンは、実際に接続する SQL Server のバージョンとは異なる場合があります。 たとえば、使用している SQL Server のバージョンが 2005 で、`ProviderManifestToken` 属性が 2008 に設定されている場合、生成された Transact-SQL クエリがサーバーで実行されないことがあります。 たとえば、SQL Server 2008 で導入された新しい日時型を使用するクエリは、以前のバージョンの SQL Server では実行されません。 使用している SQL Server のバージョンが 2005 で、`ProviderManifestToken` 属性が 2000 に設定されている場合、生成された Transact-SQL クエリが十分に最適化されなかったり、クエリがサポートされていないことを示す例外が発生することがあります。 詳細については、このトピックの「CROSS APPLY 演算子および OUTER APPLY 演算子」を参照してください。  
  
 データベースの一部の動作は、データベースの互換性レベルの設定に依存します。 使用している SQL Server のバージョンが 2005 で、`ProviderManifestToken` 属性が 2005 に、データベースの互換性レベルが "80" (SQL Server 2000) に設定されている場合、生成された Transact-SQL の実行対象は SQL Server 2005 になりますが、互換性レベルの設定が原因で予期したとおりに実行されないことがあります。 たとえば、ORDER BY リストの列名とセレクターの列名が一致する場合、順序付けが失われることがあります。  
  
## <a name="nested-queries-in-projection"></a>投影内の入れ子になったクエリ  
 projection 句内の入れ子になったクエリは、サーバーでデカルト積に変換されないことがあります。 SQL Server などの一部のバックエンド サーバーでは、これにより TempDB テーブルが非常に大きくなることがあります。 サーバーのパフォーマンスが低下する可能性があります。  
  
 projection 句内の入れ子になったクエリの例を次に示します。  
  
```sql  
SELECT c, (SELECT c, (SELECT c FROM AdventureWorksModel.Vendor AS c  ) As Inner2 FROM AdventureWorksModel.JobCandidate AS c  ) As Inner1 FROM AdventureWorksModel.EmployeeDepartmentHistory AS c  
```  
  
## <a name="server-generated-guid-identity-values"></a>サーバー生成の GUID ID 値  
 Entity Framework では、サーバー生成の GUID 型 ID 値がサポートされますが、プロバイダーは、サーバー生成の ID 値を行の挿入後に返す動作をサポートする必要があります。 SQL Server 2005 以降では、SQL Server データベース内のサーバー生成 GUID 型を [OUTPUT 句](/sql/t-sql/queries/output-clause-transact-sql)で返すことができるようになりました。
  
## <a name="see-also"></a>関連項目

- [Entity Framework 用 SqlClient](sqlclient-for-the-entity-framework.md)
- [LINQ to Entities の既知の問題および注意点](./language-reference/known-issues-and-considerations-in-linq-to-entities.md)
