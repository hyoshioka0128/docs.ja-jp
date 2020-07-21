---
title: SQL Server でのバルク コピー操作
description: SqlBulkCopy クラスを使用して、大きなファイルを SQL Server データベースのテーブルまたはビューに一括コピーするマネージド コード ソリューションを作成する方法について説明します。
ms.date: 03/30/2017
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
ms.openlocfilehash: 4f877836aa45efe162cce3c42cb5733f86deab2c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286521"
---
# <a name="bulk-copy-operations-in-sql-server"></a>SQL Server でのバルク コピー操作
Microsoft SQL Server には、SQL Server データベースのテーブルまたはビューに大きなファイルを高速で一括コピーするための、**bcp** という一般的なコマンド ライン ユーティリティが用意されています。 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用すると、同様の機能を提供するマネージ コード ソリューションを作成できます。 SQL Server のテーブルにデータを読み込むには、INSERT ステートメントを使用するなどの方法もありますが、<xref:System.Data.SqlClient.SqlBulkCopy> を使用すれば他の方法よりもパフォーマンス面で大幅に有利になります。  
  
 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用すると、SQL Server のテーブルにのみデータを書き込むことができます。 ただし、データ ソースについては SQL Server に限定されているわけではありません。<xref:System.Data.DataTable> インスタンスのデータの読み込み、または、<xref:System.Data.IDataReader> インスタンスによるデータの読み取りであれば、任意のデータ ソースを使用することができます。  
  
 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用すると、次のことを実行できます。  
  
- 単一のバルク コピー操作  
  
- 複数のバルク コピー操作  
  
- トランザクション内でのバルク コピー操作  
  
> [!NOTE]
> <xref:System.Data.SqlClient.SqlBulkCopy> クラスがサポートされていない、バージョン 1.1 以前の .NET Framework では、<xref:System.Data.SqlClient.SqlCommand> オブジェクトを使用して、SQL Server Transact-SQL **BULK INSERT** ステートメントを実行できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [バルク コピー サンプルのセットアップ](bulk-copy-example-setup.md)  
 バルク コピーの例で使用されるテーブルについて説明します。また、AdventureWorks データベースにテーブルを作成する SQL スクリプトを提供します。  
  
 [バルク コピー操作の単一実行](single-bulk-copy-operations.md)  
 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用して、SQL Server のインスタンスにデータをバルク コピーする単一の方法を説明します。また、Transact-SQL ステートメントと <xref:System.Data.SqlClient.SqlCommand> クラスを使用したバルク コピー操作の実行方法も説明します。  
  
 [バルク コピー操作の複数実行](multiple-bulk-copy-operations.md)  
 <xref:System.Data.SqlClient.SqlBulkCopy> クラスを使用して、SQL Server のインスタンスにデータのバルク コピー操作を行う複数の方法を説明します。  
  
 [トランザクションとバルク コピー操作](transaction-and-bulk-copy-operations.md)  
 トランザクション内でのバルク コピー操作の実行方法を説明します。トランザクションのコミットやロールバックの方法も説明します。  
  
## <a name="see-also"></a>関連項目

- [SQL Server と ADO.NET](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
