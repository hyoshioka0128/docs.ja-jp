---
title: DbConnection、DbCommand、および DbException
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 58aab611-7e6f-4749-b983-28ab7ae87dbe
ms.openlocfilehash: 09526f111adeecb817ce4c4e587ca3713e0d8cde
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785193"
---
# <a name="dbconnection-dbcommand-and-dbexception"></a>DbConnection、DbCommand、および DbException
<xref:System.Data.Common.DbProviderFactory> および <xref:System.Data.Common.DbConnection> を作成すると、コマンドおよびデータ リーダーを使用してデータ ソースからデータを取得できます。  
  
## <a name="retrieving-data-example"></a>データの取得例  
 次のコード例は、`DbConnection` オブジェクトを引数として受け取ります。 <xref:System.Data.Common.DbCommand> に SQL SELECT ステートメントを設定することによって、Categories テーブルからデータを検索するための <xref:System.Data.Common.DbCommand.CommandText%2A> を作成します。 このコードを実行するには、データ ソースに Categories テーブルが存在する必要があります。 接続を開いた後、<xref:System.Data.Common.DbDataReader> を使用してデータが取得されます。  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommandData#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommandData/VB/source.vb#1)]  
  
## <a name="executing-a-command-example"></a>コマンド実行例  
 次のコード例は、`DbConnection` オブジェクトを引数として受け取ります。 `DbConnection` が有効である場合、接続が開かれ、<xref:System.Data.Common.DbCommand> が作成されて実行されます。 <xref:System.Data.Common.DbCommand.CommandText%2A> には、Northwind データベースの Categories テーブルへの挿入操作を実行する SQL INSERT ステートメントが設定されています。 このコードを実行するには、データ ソースに Northwind データベースが存在すること、および、指定されたプロバイダーの有効な SQL 構文が INSERT ステートメントに使用されていることが必要です。 データ ソースで発生したエラーは <xref:System.Data.Common.DbException> コード ブロックで処理され、それ以外のすべての例外は <xref:System.Exception> ブロックで処理されます。  
  
 [!code-csharp[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbCommand#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbCommand/VB/source.vb#1)]  
  
## <a name="handling-data-errors-with-dbexception"></a>DbException でのデータ エラーの処理  
 <xref:System.Data.Common.DbException> クラスは、データ ソースでスローされるすべての例外の基本クラスです。 このクラスを例外処理コードに使用することで、プロバイダーに固有の例外クラスを参照することなく、各種のプロバイダーによってスローされる例外を処理できます。 次のコード フラグメントでは、<xref:System.Data.Common.DbException> の各プロパティ (<xref:System.Exception.GetType%2A>、<xref:System.Exception.Source%2A>、<xref:System.Runtime.InteropServices.ExternalException.ErrorCode%2A>、および <xref:System.Exception.Message%2A>) を使って、データ ソースから返されたエラー情報を表示しています。 出力結果には、エラーの種類、エラーの発生元 (プロバイダー名)、エラー コード、および、エラーに関連付けられたメッセージが表示されます。  
  
```vb  
Try  
    ' Do work here.  
Catch ex As DbException  
    ' Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType())  
    Console.WriteLine("Source: {0}", ex.Source)  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode)  
    Console.WriteLine("Message: {0}", ex.Message)  
Finally  
    ' Perform cleanup here.  
End Try  
```  
  
```csharp  
try  
{  
    // Do work here.  
}  
catch (DbException ex)  
{  
    // Display information about the exception.  
    Console.WriteLine("GetType: {0}", ex.GetType());  
    Console.WriteLine("Source: {0}", ex.Source);  
    Console.WriteLine("ErrorCode: {0}", ex.ErrorCode);  
    Console.WriteLine("Message: {0}", ex.Message);  
}  
finally  
{  
    // Perform cleanup here.  
}  
```  
  
## <a name="see-also"></a>関連項目

- [DbProviderFactories](dbproviderfactories.md)
- [DbProviderFactory の取得](obtaining-a-dbproviderfactory.md)
- [DbDataAdapter を使用したデータの変更](modifying-data-with-a-dbdataadapter.md)
- [ADO.NET の概要](ado-net-overview.md)
