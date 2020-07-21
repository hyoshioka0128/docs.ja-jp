---
title: 部分メソッドによるビジネス ロジックの追加
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 3a73991e-fd4e-4610-93fb-7ced4dc6b7f9
ms.openlocfilehash: 251d7a05971ff7940f85ec9d555d26f2e57067c3
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2019
ms.locfileid: "70248137"
---
# <a name="adding-business-logic-by-using-partial-methods"></a>部分メソッドによるビジネス ロジックの追加
生成された Visual Basic および C# のコードは、"*部分メソッド*" を使用して [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] プロジェクトでカスタマイズできます。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] から生成されるコードでは、シグネチャが部分メソッドの一部として定義されています。 このメソッドを実装する場合に、独自の部分メソッドを追加できます。 独自の実装を追加しない場合は、コンパイラで部分メソッドのシグネチャが破棄され、既定のメソッドが [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] で呼び出されます。  
  
> [!NOTE]
> Visual Studio を使用している場合は、オブジェクト リレーショナル デザイナーを使用して、妥当性検査やその他のカスタマイズをエンティティ クラスに追加できます。  
  
 たとえば、Northwind サンプル データベースの `Customer` クラスに対する既定の対応付けには次の部分メソッドが含まれます。  
  
 [!code-csharp[DLinqOverrideDefault#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#2)]
 [!code-vb[DLinqOverrideDefault#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#2)]  
  
 次のようなコードを独自の部分 `Customer` クラスに追加することで、独自のメソッドを実装できます。  
  
 [!code-csharp[DLinqOverrideDefault#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/Program.cs#3)]
 [!code-vb[DLinqOverrideDefault#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/Module1.vb#3)]  
  
 この方法は、`Insert`、`Update`、`Delete` の既定のメソッドをオーバーライドし、オブジェクトのライフサイクル イベントの発生時にプロパティを検証するために、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] で一般的に使用されます。  
  
 詳細については、「[部分メソッド](../../../../../visual-basic/programming-guide/language-features/procedures/partial-methods.md)」(Visual Basic) または「[partial (メソッド) (C# リファレンス)](../../../../../csharp/language-reference/keywords/partial-method.md)」(C#) を参照してください。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、SQLMetal などのコード生成ツールによって定義される `ExampleClass` を最初に示し、次に 2 つのメソッドの 1 つだけを実装できることを示します。  
  
### <a name="code"></a>コード  
 [!code-csharp[DLinqSubmittingChanges#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#4)]
 [!code-vb[DLinqSubmittingChanges#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#4)]  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例では、`Shipper` エンティティと `Order` エンティティのリレーションシップを使用します。 メソッドには部分メソッドの `InsertShipper` と `DeleteShipper` が含まれています。 これらのメソッドは、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の対応付けによって提供される既定の部分メソッドをオーバーライドします。  
  
### <a name="code"></a>コード  
 [!code-csharp[DLinqOverrideDefault#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqOverrideDefault/cs/northwind.cs#1)]
 [!code-vb[DLinqOverrideDefault#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqOverrideDefault/vb/northwind.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [データの変更と変更の送信](making-and-submitting-data-changes.md)
- [挿入、更新、および削除の各操作のカスタマイズ](customizing-insert-update-and-delete-operations.md)
