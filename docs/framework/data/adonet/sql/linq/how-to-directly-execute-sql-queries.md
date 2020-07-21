---
title: '方法: SQL クエリを直接実行する'
description: ExecuteQuery を使用してクエリを実行し、LINQ to SQL クエリでは不十分な場合は、その結果を直接オブジェクトに変換する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e491b9bf-741a-4296-9f51-76c25ddf6a82
ms.openlocfilehash: 59bd404e41f6be1181d6a625c31ee23358db0df3
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286366"
---
# <a name="how-to-directly-execute-sql-queries"></a>方法: SQL クエリを直接実行する
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、作成したクエリをパラメーター化された SQL クエリ (テキスト形式) に変換し、それを SQL Server に送って処理します。  
  
 アプリケーションでローカルに使用できるさまざまなメソッドの中には、SQL では実行できないものもあります。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、このようなローカル メソッドを、SQL 環境内で使用できる同等の操作や関数に変換しようとします。 .NET Framework の組み込み型に対するほとんどのメソッドと演算子には、SQL コマンドに直接対応する変換が用意されています。 使用可能な関数から生成できるものもあります。 生成できないものについては、ランタイム例外が発生します。 詳しくは、「[SQL と CLR の型マッピング](sql-clr-type-mapping.md)」をご覧ください。  
  
 特殊なタスクに対して [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] クエリでは不十分な場合は、<xref:System.Data.Linq.DataContext.ExecuteQuery%2A> メソッドを使用して SQL クエリを実行し、そのクエリの結果をオブジェクトに直接変換できます。  
  
## <a name="example"></a>例  
 次の例では、`Customer` クラスのデータが 2 つのテーブル (customer1 および customer2) にわたって格納されているものとします。 クエリは `Customer` オブジェクトのシーケンスを返します。  
  
 [!code-csharp[DLinqQuerying#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#4)]
 [!code-vb[DLinqQuerying#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#4)]  
  
 表形式の結果の列名がエンティティ クラスの列のプロパティと一致する限り、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] によって SQL クエリからオブジェクトが作成されます。  
  
## <a name="example"></a>例  
 <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> メソッドは、パラメーターの使用にも対応しています。 パラメーター化されたクエリを実行するには、次のようなコードを使用します。  
  
 [!code-csharp[DLinqQuerying#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#5)]
 [!code-vb[DLinqQuerying#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#5)]  
  
 クエリ テキスト内では、`Console.WriteLine()` および `String.Format()` で使用するのと同じ中かっこ表記を使用して、パラメーターを表現します。 実際には、指定したクエリ文字列について `String.Format()` が呼び出され、中かっこで囲まれたパラメーターは、生成された @p0、@p1、...、@p(n) のようなパラメーター名に置き換えられます。  
  
## <a name="see-also"></a>関連項目

- [背景情報](background-information.md)
- [データベースに対するクエリの実行](querying-the-database.md)
