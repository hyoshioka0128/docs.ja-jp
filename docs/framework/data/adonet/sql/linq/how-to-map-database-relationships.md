---
title: '方法: データベース リレーションシップを割り当てる'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 538def39-8399-46fb-b02d-60ede4e050af
ms.openlocfilehash: c89fb3e11ae8e0f8ea37727446cdf65db9499a1d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79148375"
---
# <a name="how-to-map-database-relationships"></a>方法: データベース リレーションシップを割り当てる
データ リレーションシップが常に同じ場合は、これをエンティティ クラス内のプロパティ参照としてエンコードできます。 たとえば、Northwind サンプル データベースでは、通常は顧客が注文を発注するため、モデルには、顧客と注文のリレーションシップが常に存在します。  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、そのようなリレーションシップを表すのに役立つ <xref:System.Data.Linq.Mapping.AssociationAttribute> 属性が定義されています。 この属性を、<xref:System.Data.Linq.EntitySet%601> 型および <xref:System.Data.Linq.EntityRef%601> 型と共に使用することで、データベース内の外部キー リレーションシップが表されます。 詳しくは、「[属性ベースの対応付け](attribute-based-mapping.md)」の関連付け属性のセクションをご覧ください。  
  
> [!NOTE]
> AssociationAttribute プロパティ値と ColumnAttribute Storage プロパティ値では大文字と小文字が区別されます。 たとえば、AssociationAttribute.Storage  プロパティの属性に使用されている値は、コード内の別の場所で使用されている対応するプロパティ名と、大文字と小文字が一致するようにしてください。 これは、Visual Basic など、通常は大文字と小文字が区別されない言語を含むすべての .NET プログラミング言語に適用されます。 Storage プロパティの詳細については、「<xref:System.Data.Linq.Mapping.DataAttribute.Storage%2A?displayProperty=nameWithType>」を参照してください。  
  
 ほとんどのリレーションシップは、このトピックの例のように、一対多のリレーションシップです。 次に示すように、一対一および多対多のリレーションシップも表すことができます。  
  
- 一対一: 両側で <xref:System.Data.Linq.EntitySet%601> を指定することによって、この種類のリレーションシップを表します。  
  
     たとえば、顧客のセキュリティ コードが `Customer` テーブルにはなく、承認されたユーザーのみがアクセスできるように作成された、`Customer`-`SecurityCode` リレーションシップがその例です。  
  
- 多対多: 多対多リレーションシップでは、リンク テーブル ("*結合*" テーブルともいいます) の主キーは、多くの場合、他の 2 つのテーブルの外部キーが結合して作成されます。  
  
     たとえば、リンク テーブル `Employee` を使用して作成される -`Project``EmployeeProject` という多対多リレーションシップがあるとします。 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] では、このようなリレーションシップを、`Employee`、`Project`、および `EmployeeProject` という 3 つのクラスを使用してモデル化する必要があります。 この場合、`Employee` と `Project` の間のリレーションシップを変更すると、主キーの `EmployeeProject` の更新が必要であるように見える可能性がありす。 ただし、この状態は、既存の `EmployeeProject` の削除、および新しい `EmployeeProject` の作成として適切にモデル化されます。  
  
    > [!NOTE]
    > リレーショナル データベース内のリレーションシップは、通常、他のテーブルの主キーを参照する外部キー値としてモデル化されます。 それらの間を移動するには、リレーショナル "*結合*" 演算を使用して、2 つのテーブルを明示的に関連付けます。  
    >
    >  これに対し、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] 内のオブジェクトは、"*ドット*" 表記を使用してナビゲートするプロパティ参照または参照のコレクションを使用して、互いを参照します。  
  
## <a name="example"></a>例  
 次の一対多の例では、`Customer` クラスは、顧客とその注文のリレーションシップを宣言するプロパティを持ちます。  `Orders` プロパティは <xref:System.Data.Linq.EntitySet%601> 型です。 この型は、このリレーションシップが一対多 (1 人の顧客対多くの注文) であることを意味します。 <xref:System.Data.Linq.Mapping.AssociationAttribute.OtherKey%2A> プロパティを使用して、この関連付けを実現する方法を記述します。つまり、これと比較する、関連クラス内のプロパティの名前を指定します。 この例では、データベース "*結合*" でその列の値が比較されるときに、`CustomerID` プロパティが比較されます。  
  
> [!NOTE]
> Visual Studio を使用している場合は、オブジェクト リレーショナル デザイナーを使用して、クラス間の関連付けを作成できます。  
  
 [!code-csharp[DlinqCustomize#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#3)]
 [!code-vb[DlinqCustomize#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#3)]  
  
## <a name="example"></a>例  
 逆の場合も可能です。 `Customer` クラスを使用して顧客と注文の関連付けを記述するのではなく、`Order` クラスを使用できます。 `Order` クラスは、<xref:System.Data.Linq.EntityRef%601> 型を使用して、次のコード例に示すように、顧客へのリレーションシップを記述できます。  
  
> [!NOTE]
> <xref:System.Data.Linq.EntityRef%601> クラスでは、"*遅延読み込み*" がサポートされています。 詳細については、「[遅延読み込みと即時読み込み](deferred-versus-immediate-loading.md)」を "*参照してください*"。  
  
 [!code-csharp[DLinqCustomize#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#5)]
 [!code-vb[DLinqCustomize#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#5)]  
  
## <a name="see-also"></a>関連項目

- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
