---
title: ストアド プロシージャでのデータの変更
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7d8e9a46-1af6-4a02-bf61-969d77ae07e0
ms.openlocfilehash: 46c92301b717e285c4c18241f84d0069069c7bdc
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70783526"
---
# <a name="modifying-data-with-stored-procedures"></a>ストアド プロシージャでのデータの変更
ストアド プロシージャは、入力パラメーターとしてデータを受け取り、出力パラメーター、結果セット、または戻り値としてデータを返すことができます。 以下のサンプルでは、入力パラメーター、出力パラメーター、および戻り値が ADO.NET によってどのようにやり取りされるかを示したものです。 この例では、主キー列が SQL Server データベースの ID 列であるテーブルに新しいレコードを挿入しています。  
  
> [!NOTE]
> SQL Server のストアド プロシージャで、<xref:System.Data.SqlClient.SqlDataAdapter> を使用してデータを編集または削除する場合、ストアド プロシージャの定義に SET NOCOUNT ON は使用しないでください。 処理された行数がゼロとして返され、`DataAdapter` によってコンカレンシーの競合として解釈されてしまいます。 この場合、<xref:System.Data.DBConcurrencyException> がスローされます。  
  
## <a name="example"></a>例  
 この例では、次のストアド プロシージャを使用して、**Northwind** **Categories** テーブルに新しいカテゴリを挿入します。 このストアド プロシージャは、**CategoryName** 列の値を入力パラメーターとして受け取り、SCOPE_IDENTITY() 関数を使用して ID フィールド **CategoryID** の新しい値を取得し、その値を出力パラメーター内に返します。 RETURN ステートメントは、@@ROWCOUNT 関数を使用して、挿入された行の数を返します。  
  
```sql
CREATE PROCEDURE dbo.InsertCategory  
  @CategoryName nvarchar(15),  
  @Identity int OUT  
AS  
INSERT INTO Categories (CategoryName) VALUES(@CategoryName)  
SET @Identity = SCOPE_IDENTITY()  
RETURN @@ROWCOUNT  
```  
  
 上述の `InsertCategory` ストアド プロシージャを <xref:System.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> の <xref:System.Data.SqlClient.SqlDataAdapter> のソースとして使用する例を次に示します。 `@Identity` 出力パラメーターは、<xref:System.Data.DataSet> の `Update` メソッドが呼び出され、データベースにレコードが挿入された後で <xref:System.Data.SqlClient.SqlDataAdapter> に反映されます。 戻り値も取得されます。  
  
> [!NOTE]
> <xref:System.Data.OleDb.OleDbDataAdapter> を使用するときは、**ReturnValue** の <xref:System.Data.ParameterDirection> を含むパラメーターを、他のパラメーターより先に指定する必要があります。  
  
 [!code-csharp[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.SprocIdentityReturn#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.SprocIdentityReturn/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [ADO.NET でのデータの取得および変更](retrieving-and-modifying-data.md)
- [DataAdapter と DataReader](dataadapters-and-datareaders.md)
- [コマンドの実行](executing-a-command.md)
- [ADO.NET の概要](ado-net-overview.md)
