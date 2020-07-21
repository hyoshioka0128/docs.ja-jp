---
title: '方法: データベースに接続する'
description: LINQ to SQL で DataContext を使用してデータベースに接続する方法について説明します。 DataContext を使用してデータベースに接続し、行を取得する方法については、これらの例を参照してください。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c33d74b3-530d-421b-a121-96786dd263a5
ms.openlocfilehash: c3320a598cb8407ab584530c615c2e5ef0de53c8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84286405"
---
# <a name="how-to-connect-to-a-database"></a>方法: データベースに接続する
データベースへの接続、データベースからのオブジェクトの取得、およびデータベースへの変更内容の反映では、<xref:System.Data.Linq.DataContext> を仲介役として使用します。 <xref:System.Data.Linq.DataContext> の使い方は、ADO.NET の <xref:System.Data.SqlClient.SqlConnection> と同じです。 つまり、接続または接続文字列を指定して、<xref:System.Data.Linq.DataContext> を初期化します。 詳しくは、「[DataContext メソッド (O/R デザイナー)](/visualstudio/data-tools/datacontext-methods-o-r-designer)」をご覧ください。  
  
 <xref:System.Data.Linq.DataContext> の役割は、オブジェクトを求める要求を、データベースに対して発行する SQL クエリに変換し、その結果からオブジェクトを組み立てることです。 <xref:System.Data.Linq.DataContext> では、標準クエリ演算子と同じ演算子パターン (`Where` や `Select` など) が実装されており、統合言語クエリ (LINQ) を使用できます。  
  
> [!IMPORTANT]
> セキュリティで保護された接続を確立することは、最も重要です。 詳細については、「[LINQ to SQL のセキュリティ](security-in-linq-to-sql.md)」を参照してください。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Data.Linq.DataContext> を使用して、Northwind サンプル データベースに接続し、市が London である顧客の行を取得しています。  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#1)]
 [!code-vb[DLinqCommunicatingWithDatabase#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#1)]  
  
 各データベース テーブルは `Table` コレクションとして表され、テーブルを識別するエンティティ クラスを使用して <xref:System.Data.Linq.DataContext.GetTable%2A> メソッドでアクセスできます。  
  
## <a name="example"></a>例  
 基本的な <xref:System.Data.Linq.DataContext> クラスおよび <xref:System.Data.Linq.DataContext> メソッドを使用するのではなく、厳密に型指定された <xref:System.Data.Linq.DataContext.GetTable%2A> を宣言するのがベスト プラクティスです。 厳密に型指定された <xref:System.Data.Linq.DataContext> では、次の例のように、すべての `Table` コレクションをそのコンテキストのメンバーとして宣言します。  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#2)]
 [!code-vb[DLinqCommunicatingWithDatabase#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#2)]  
  
 この場合、London の顧客を取得するクエリは、次のように簡単に表せます。  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#5)]
 [!code-vb[DLinqCommunicatingWithDatabase#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [データベースとの通信](communicating-with-the-database.md)
