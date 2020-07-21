---
title: LINQ to SQL オブジェクト モデル
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 81dd0c37-e2a4-4694-83b0-f2e49e693810
ms.openlocfilehash: b73904e2347c501b21b2c5933d0b43c7abafeb7c
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70792313"
---
# <a name="the-linq-to-sql-object-model"></a>LINQ to SQL オブジェクト モデル
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、開発者のプログラミング言語で表されるオブジェクト モデルが、リレーショナル データベースのデータ モデルに対応付けられています。 データ操作はオブジェクト モデルに従って行われます。  
  
 このシナリオでは、データベースに対してデータベース コマンド (`INSERT` など) を実行する必要はありません。 代わりに、オブジェクト モデル内で値を変更し、メソッドを実行します。 データベースに対してクエリを実行したり、変更を送信する必要がある場合、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、要求を正しい SQL コマンドに変換し、そのコマンドをデータベースに送信します。  
  
 ![Linq オブジェクト モデルを示すスクリーンショット。](./media/the-linq-to-sql-object-model/linq-object-model-two-tier.png)  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] オブジェクト モデル内の最も基本的な要素と、リレーショナル データ モデル内の要素との関係を、次の表に示します。  
  
|LINQ to SQL オブジェクト モデル|リレーショナル データ モデル|  
|------------------------------|---------------------------|  
|エンティティ クラス|テーブル|  
|クラス メンバー|Column|  
|関連付け|外部キー リレーションシップ|  
|メソッド|ストアド プロシージャまたは関数|  
  
> [!NOTE]
> 次の説明は、リレーショナル データ モデルと規則に関する基本的な知識があることが前提です。  
  
## <a name="linq-to-sql-entity-classes-and-database-tables"></a>LINQ to SQL エンティティ クラスおよびデータベース テーブル  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、データベース テーブルは "*エンティティ クラス*" によって表されます。 エンティティ クラスは、作成する他のクラスに似ていますが、クラスをデータベース テーブルに関連付ける特別な情報を使用して、クラスに注釈を付ける点が異なります。 次の例に示すように、クラス宣言にカスタム属性 (<xref:System.Data.Linq.Mapping.TableAttribute>) を追加することによって、この注釈を付けます。  
  
### <a name="example"></a>例  
 [!code-csharp[DLinqObjectModel#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#1)]
 [!code-vb[DLinqObjectModel#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#1)]  
  
 テーブルとして宣言されたクラスのインスタンスのみ (つまり、エンティティ クラス)、データベースに保存できます。  
  
 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」のテーブル属性のセクションをご覧ください。  
  
## <a name="linq-to-sql-class-members-and-database-columns"></a>LINQ to SQL クラス メンバーおよびデータベース列  
 クラスとテーブルの関連付けに加えて、フィールドまたはプロパティを設定してデータベース列を表すことができます。 このためには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、次の例に示すように <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性を定義します。  
  
### <a name="example"></a>例  
 [!code-csharp[DLinqObjectModel#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/Program.cs#2)]
 [!code-vb[DLinqObjectModel#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/Module1.vb#2)]  
  
 列に対応付けられたフィールドおよびプロパティのみ、データベースに保持したり、データベースから取得できます。 列として宣言されていないものは、アプリケーション ロジックの一時的な部分と見なされます。  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性にはさまざまなプロパティがあり、これを使用することで、列を表すメンバーをカスタマイズできます (たとえば、主キー列を表すメンバーを指定できます)。 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」の列属性のセクションをご覧ください。  
  
## <a name="linq-to-sql-associations-and-database-foreign-key-relationships"></a>LINQ to SQL の関連付けおよびデータベースの外部キー リレーションシップ  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、<xref:System.Data.Linq.Mapping.AssociationAttribute> 属性を適用することによって、データベースの関連付け (外部キーと主キーのリレーションシップなど) を表します。 次のコード セグメントでは、<xref:System.Data.Linq.Mapping.AssociationAttribute> 属性を持つ `Customer` プロパティが `Order` クラスに含まれています。 このプロパティとその属性が、`Order` クラスおよび `Customer` クラスとのリレーションシップを提供します。  
  
 `Customer` クラスの `Order` プロパティを表示する方法を次の例に示します。  
  
### <a name="example"></a>例  
 [!code-csharp[DLinqObjectModel#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#3)]
 [!code-vb[DLinqObjectModel#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#3)]  
  
 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」の関連付け属性のセクションをご覧ください。  
  
## <a name="linq-to-sql-methods-and-database-stored-procedures"></a>LINQ to SQL メソッドおよびデータベース ストアド プロシージャ  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、ストアド プロシージャとユーザー定義関数をサポートしています。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、これらのデータベース定義の概念をクライアント オブジェクトに対応付けることによって、クライアント コードから厳密に型指定された方法でのアクセスが実現されます。 メソッド シグネチャは、データベース内で定義されているプロシージャおよび関数のシグネチャと可能な限りよく似ています。 IntelliSense を使用して、これらのメソッドを見つけることができます。  
  
 呼び出しによって対応するプロシージャに返される結果セットは、厳密に型指定されたコレクションです。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] は、<xref:System.Data.Linq.Mapping.FunctionAttribute> 属性と <xref:System.Data.Linq.Mapping.ParameterAttribute> 属性を使用して、ストアド プロシージャおよび関数をメソッドに対応付けます。 ストアド プロシージャを表すメソッドは、<xref:System.Data.Linq.Mapping.FunctionAttribute.IsComposable%2A> プロパティによって、ユーザー定義関数を表すメソッドと区別されます。 このプロパティが `false` (既定値) に設定されている場合、メソッドはストアド プロシージャを表します。 `true` に設定されている場合、メソッドはデータベース関数を表します。  
  
> [!NOTE]
> Visual Studio を使用している場合は、オブジェクト リレーショナル デザイナーを使用して、ストアド プロシージャおよびユーザー定義関数に対応付けられるメソッドを作成できます。  
  
### <a name="example"></a>例  
 [!code-csharp[DLinqObjectModel#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqObjectModel/cs/northwind.cs#4)]
 [!code-vb[DLinqObjectModel#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqObjectModel/vb/northwind.vb#4)]  
  
 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」の関数属性、ストアド プロシージャ属性、パラメーター属性の各セクション、および「[ストアド プロシージャ](stored-procedures.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- [属性ベースの対応付け](attribute-based-mapping.md)
- [背景情報](background-information.md)
