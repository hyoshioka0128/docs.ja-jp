---
title: '方法: データベース データ型を指定する'
ms.date: 03/30/2017
ms.assetid: 2228fdad-7e6a-4b1b-b4d1-79d0198b7c28
ms.openlocfilehash: 09ca8dc6fa440138523bcd2905335a04517dd806
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70793271"
---
# <a name="how-to-specify-database-data-types"></a>方法: データベース データ型を指定する
T-SQL テーブル宣言の列を定義する正確なテキストを指定するには、[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] の <xref:System.Data.Linq.Mapping.ColumnAttribute> 属性の <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> プロパティを使用します。  
  
 <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> プロパティは、<xref:System.Data.Linq.DataContext.CreateDatabase%2A> を使用してデータベースのインスタンスを作成することを予定している場合のみ指定する必要があります。  
  
 コード例については、「<xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A>」を参照してください。  
  
### <a name="to-specify-text-to-define-a-data-type-in-a-t-sql-table"></a>データ型を T-SQL テーブルに定義するテキストを指定するには  
  
1. <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> 属性に <xref:System.Data.Linq.Mapping.ColumnAttribute> プロパティを追加します。  
  
2. <xref:System.Data.Linq.Mapping.ColumnAttribute.DbType%2A> プロパティの値を T-SQL で使用される正確なテキストに設定します。  
  
## <a name="see-also"></a>関連項目

- [LINQ to SQL オブジェクト モデル](the-linq-to-sql-object-model.md)
- [方法: コード エディターを使用してエンティティ クラスをカスタマイズする](how-to-customize-entity-classes-by-using-the-code-editor.md)
