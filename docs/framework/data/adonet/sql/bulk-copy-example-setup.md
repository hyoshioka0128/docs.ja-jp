---
title: バルク コピー サンプルのセットアップ
ms.date: 03/30/2017
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.openlocfilehash: 80350d112da03c00e422432ce271ca5ea3ac58ab
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79148843"
---
# <a name="bulk-copy-example-setup"></a>バルク コピー サンプルのセットアップ
<xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用すると、SQL Server のテーブルにのみデータを書き込むことができます。 このトピック内のコード サンプルには、SQL Server のサンプル データベース **AdventureWorks** が使用されています。 既存のテーブルの改変を防ぐため、コード サンプルでは、別途作成したテーブルにデータを書き込みます。このテーブルを最初に作成しておく必要があります。  
  
 **BulkCopyDemoMatchingColumns** テーブルと **BulkCopyDemoDifferentColumns** テーブルは、どちらも **AdventureWorks** の **Production.Products** テーブルに基づいています。 コード サンプルではこれらのテーブルを使用し、**Production.Products** テーブルからこれらのサンプル テーブルのいずれかにデータを追加します。 **BulkCopyDemoDifferentColumns** テーブルは、ソース データからコピー先のテーブルに列をマップする方法を例示するサンプルに使用されます。**BulkCopyDemoMatchingColumns** は他のサンプルの大部分に使用されます。  
  
 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用して複数のテーブルに書き込む方法を説明するコード サンプルもあります。 これらのサンプルでは、**BulkCopyDemoOrderHeader** テーブルと **BulkCopyDemoOrderDetail** テーブルはコピー先のテーブルとして使用されます。 これらのテーブルは、**AdventureWorks** の **Sales.SalesOrderHeader** テーブルと **Sales.SalesOrderDetail** テーブルに基づいたテーブルです。  
  
> [!NOTE]
> **SqlBulkCopy** コード サンプルでは、**SqlBulkCopy** だけを使用した構文について説明します。 コピー元およびコピー先のテーブルが同一の SQL Server インスタンス内に存在する場合、Transact-SQL `INSERT … SELECT` ステートメントを使用すれば簡単かつ高速にデータをコピーすることができます。  
  
## <a name="table-setup"></a>テーブルのセットアップ  
 コード サンプルを正しく動作させるために必要なテーブルを作成するには、SQL Server データベースで次の Transact-SQL ステートメントを実行する必要があります。  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="see-also"></a>関連項目

- [SQL Server でのバルク コピー操作](bulk-copy-operations-in-sql-server.md)
- [ADO.NET の概要](../ado-net-overview.md)
