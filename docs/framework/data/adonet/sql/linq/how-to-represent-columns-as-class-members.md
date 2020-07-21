---
title: '方法: クラス メンバーとして列を表す'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 7ab28021-4d15-4d9c-bf2e-6ccc0daa7d1a
ms.openlocfilehash: 515a8477b3a9c72934e0ad11d7b1bf599e8b16a2
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793505"
---
# <a name="how-to-represent-columns-as-class-members"></a>方法: クラス メンバーとして列を表す
フィールドまたはプロパティをデータベース列に関連付けるには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性を使用します。  
  
### <a name="to-map-a-field-or-property-to-a-database-column"></a>フィールドまたはプロパティをデータベース列に対応付けるには  
  
- プロパティまたはフィールドの宣言に <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性を追加します。  
  
## <a name="example"></a>例  
 次の例では、`CustomerID` クラス内の `Customer` フィールドを `CustomerID` データベース テーブル内の `Customers` 列に対応付けます。  
  
 [!code-csharp[DLinqCustomize#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCustomize/cs/Program.cs#2)]
 [!code-vb[DLinqCustomize#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCustomize/vb/Module1.vb#2)]  
  
 名前が推論できる場合は、<xref:System.Data.Linq.Mapping.DataAttribute.Name%2A> プロパティを指定する必要はありません。 名前を指定しない場合は、プロパティまたはフィールドと同じ名前であると見なされます。  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
