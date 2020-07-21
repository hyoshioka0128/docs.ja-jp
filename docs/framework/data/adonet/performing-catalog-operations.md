---
title: カタログ操作の実行
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.openlocfilehash: bedeb4e9c510a3feeedc038e9c4cef6c4721e345
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149246"
---
# <a name="performing-catalog-operations"></a>カタログ操作の実行
データベースまたはカタログを変更するコマンド (CREATE TABLE ステートメント、CREATE PROCEDURE ステートメントなど) を実行するには、適切な SQL ステートメントと **Connection** オブジェクトを使用して、**Command** オブジェクトを作成します。 **Command** オブジェクトの **ExecuteNonQuery** メソッドでコマンドを実行します。  
  
 Microsoft SQL Server データベースにストアド プロシージャを作成するコード サンプルを次に示します。  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim queryString As String = "CREATE PROCEDURE InsertCategory " & _  
    "@CategoryName nchar(15), " & _  
    "@Identity int OUT " & _  
    "AS " & _  
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " & _  
    "SET @Identity = @@Identity " & _  
    "RETURN @@ROWCOUNT"  
  
Dim command As SqlCommand = New SqlCommand(queryString, connection)  
command.ExecuteNonQuery()  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
string queryString = "CREATE PROCEDURE InsertCategory  " +
    "@CategoryName nchar(15), " +  
    "@Identity int OUT " +  
    "AS " +
    "INSERT INTO Categories (CategoryName) VALUES(@CategoryName) " +
    "SET @Identity = @@Identity " +  
    "RETURN @@ROWCOUNT";  
  
SqlCommand command = new SqlCommand(queryString, connection);  
command.ExecuteNonQuery();  
```  
  
## <a name="see-also"></a>関連項目

- [コマンドを使用したデータ変更](using-commands-to-modify-data.md)
- [コマンドおよびパラメーター](commands-and-parameters.md)
- [ADO.NET の概要](ado-net-overview.md)
