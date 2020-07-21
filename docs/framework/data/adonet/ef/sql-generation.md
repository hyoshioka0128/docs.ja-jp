---
title: SQL 生成
ms.date: 03/30/2017
ms.assetid: 0e16aa02-d458-4418-a765-58b42aad9315
ms.openlocfilehash: 9c5301d3f4d5bc2e0db4a138c6d8ceb06d3a7845
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70854360"
---
# <a name="sql-generation"></a>SQL 生成
Entity Framework 用のプロバイダーを作成する場合は、Entity Framework のコマンド ツリーを特定のデータベースで認識できる SQL (たとえば、SQL Server の場合は Transact-SQL、Oracle の場合は PL/SQL) に変換する必要があります。 ここでは、Entity Framework プロバイダーのための SQL 生成コンポーネント (SELECT クエリ用) を開発する方法を説明します。 INSERT、UPDATE、および DELETE の各クエリについて詳しくは、「[変更 SQL 生成](modification-sql-generation.md)」をご覧ください。  
  
 このセクションの内容を理解するには、Entity Framework と ADO.NET プロバイダー モデルについての知識が必要です。 また、コマンド ツリーと <xref:System.Data.Common.CommandTrees.DbExpression> について理解している必要もあります。  
  
## <a name="the-role-of-the-sql-generation-module"></a>SQL 生成モジュールの役割  
 Entity Framework プロバイダーの SQL 生成モジュールでは、指定したクエリ コマンド ツリーが、SQL:1999 準拠のデータベースを対象とする 1 つの SQL SELECT ステートメントに変換されます。 生成される SQL 内の入れ子になったクエリは、できるだけ少なくする必要があります。 SQL 生成モジュールによって出力クエリ コマンド ツリーを簡素化する必要はありません。 これは、結合の排除や連続するフィルター ノードの折りたたみなどにより、Entity Framework によって実行される処理です。  
  
 <xref:System.Data.Common.DbProviderServices> クラスは、SQL 生成レイヤーにアクセスしてコマンド ツリーを <xref:System.Data.Common.DbCommand> に変換するための開始点となります。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [コマンド ツリーの構造](the-shape-of-the-command-trees.md)  
  
 [コマンド ツリーからの SQL の生成: ベスト プラクティス](generating-sql-from-command-trees-best-practices.md)  
  
 [サンプル プロバイダーでの SQL 生成](sql-generation-in-the-sample-provider.md)  
  
## <a name="see-also"></a>関連項目

- [Entity Framework データ プロバイダーの作成](writing-an-ef-data-provider.md)
