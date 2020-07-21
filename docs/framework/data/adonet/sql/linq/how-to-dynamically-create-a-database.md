---
title: '方法: データベースを動的に作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fb7f23c4-4572-4c38-9898-a287807d070c
ms.openlocfilehash: 4cadf20cdadb39483f26a29619cae058eac47e50
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793652"
---
# <a name="how-to-dynamically-create-a-database"></a>方法: データベースを動的に作成する
LINQ to SQL では、オブジェクト モデルをリレーショナル データベースに対応付けます。 マッピングを有効化するには、属性ベースの対応付けか、リレーショナル データベースの構造を記述した外部マッピング ファイルを使用します。 いずれの場合も、<xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドを使用してデータベースの新しいインスタンスを作成するために必要な、リレーショナル データベースに関する十分な情報が提供されます。  
  
 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドで作成されるデータベースのレプリカには、オブジェクト モデル内でエンコードされる情報だけが格納されます。 マッピング ファイルおよびオブジェクト モデルの属性では、既存のデータベースの構造のすべてがエンコードされるとは限りません。 ユーザー定義関数、ストアド プロシージャ、トリガー、または CHECK 制約の内容は、マッピング ファイルでは表現されません。 これは多くのデータベースにとって十分な動作です。  
  
 <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドはさまざまなシナリオで使用できますが、特に、Microsoft SQL Server 2008 などの既知のデータ プロバイダーを利用できる場合に適しています。 一般的なシナリオとして、次のようなものが考えられます。  
  
- 顧客のシステムに自動的に自身をインストールするアプリケーションを作成している場合  
  
- オフライン状態を保存するためにローカル データベースを必要とするクライアント アプリケーションを作成している場合  
  
 接続文字列で .mdf ファイルまたは単にカタログ名を使用することにより、SQL Server でも <xref:System.Data.Linq.DataContext.CreateDatabase%2A?displayProperty=nameWithType> メソッドを使用できます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、接続文字列を使用して、作成するデータベースおよびデータベースの作成先となるサーバーを定義します。  
  
> [!NOTE]
> 可能な限り、データベースへの接続には Windows 統合セキュリティを使用してください。これにより、接続文字列にパスワードを含める必要がなくなります。  
  
## <a name="example"></a>例  
 次のコードは、MyDVDs.mdf という名前の新しいデータベースを作成する例です。  
  
 [!code-csharp[DLinqSubmittingChanges#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#5)]
 [!code-vb[DLinqSubmittingChanges#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#5)]  
  
## <a name="example"></a>例  
 次のようにすると、オブジェクト モデルを使用してデータベースを作成できます。  
  
 [!code-csharp[DLinqSubmittingChanges#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#6)]
 [!code-vb[DLinqSubmittingChanges#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#6)]  
  
## <a name="example"></a>例  
 顧客のシステムに自動的に自身をインストールするアプリケーションを作成している場合、新しいデータベースを作成する前に既存のデータベースがあるかどうかを確認して削除します。 <xref:System.Data.Linq.DataContext> クラスには、このプロセスに役立つ <xref:System.Data.Linq.DataContext.DatabaseExists%2A> メソッドと <xref:System.Data.Linq.DataContext.DeleteDatabase%2A> メソッドが用意されています。  
  
 次の例は、これらのメソッドを使用してこの方法を実装する 1 つの方法を示しています。  
  
 [!code-csharp[DLinqSubmittingChanges#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#7)]
 [!code-vb[DLinqSubmittingChanges#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#7)]  
  
## <a name="see-also"></a>関連項目

- [属性ベースの対応付け](attribute-based-mapping.md)
- [外部マップ](external-mapping.md)
- [SQL と CLR の型マッピング](sql-clr-type-mapping.md)
- [背景情報](background-information.md)
- [データの変更と変更の送信](making-and-submitting-data-changes.md)
