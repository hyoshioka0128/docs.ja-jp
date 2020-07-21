---
title: サンプル プロバイダーでの SQL 生成
ms.date: 03/30/2017
ms.assetid: e70f553d-4622-4627-928e-1aa2ee605d8e
ms.openlocfilehash: a59f1fecf85d63208c3388204c962b5838902ba7
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854321"
---
# <a name="sql-generation-in-the-sample-provider"></a>サンプル プロバイダーでの SQL 生成
[Entity Framework Sample Provider](https://code.msdn.microsoft.com/windowsdesktop/Entity-Framework-Sample-6a9801d0) では、Entity Framework をサポートする ADO.NET データ プロバイダーの新しいコンポーネントが示されています。  これは、SQL Server 2005 データベースで動作し、System.Data.SqlClient ADO.NET 2.0 データ プロバイダーのラッパーとして実装されます。  
  
 サンプル プロバイダーの SQL 生成モジュール (DmlSqlGenerator.cs ファイルを除き、SQL Generation フォルダーにあります) では、入力として DbQueryCommandTree を使用し、単一の SQL SELECT ステートメントを生成します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 ここでは、次のトピックについて説明します。  
  
 [アーキテクチャとデザイン](architecture-and-design.md)  
  
 [チュートリアル: SQL 生成](walkthrough-sql-generation.md)  
  
## <a name="see-also"></a>関連項目

- [SQL 生成](sql-generation.md)
