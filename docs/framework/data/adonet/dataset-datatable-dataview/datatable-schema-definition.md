---
title: DataTable スキーマの定義
ms.date: 03/30/2017
ms.assetid: efbcdda4-f5a9-421d-8be2-4c194c74552f
ms.openlocfilehash: d18af8001fd24f3b21c3e7fd13f9dabb2587b322
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70786389"
---
# <a name="datatable-schema-definition"></a>DataTable スキーマの定義
テーブルのスキーマ (構造) は、列と制約で表されます。 <xref:System.Data.DataTable> のスキーマは、<xref:System.Data.DataColumn>、<xref:System.Data.ForeignKeyConstraint>、<xref:System.Data.UniqueConstraint> の各オブジェクトを使用して定義します。 テーブルの列は、データ ソースの列に割り当てたり、式で算出された値を格納したり、格納されている値を自動的にインクリメントしたり、主キー値を格納したりできます。  
  
 テーブルの列、リレーション、および制約を名前で参照する場合は、大文字と小文字が区別されます。 複数の列、リレーション、または制約の名前が同じであっても、大文字と小文字が異なっていれば、1 つのテーブルで使用できます。 たとえば、**Col1** と **col1** を同時に使用できます。 この場合、列を名前で参照するときは、列名の大文字と小文字を正確に指定する必要があります。正確に指定しない場合は、例外がスローされます。 たとえば、テーブル **myTable** に列 **Col1** と列 **col1** がある場合、**Col1** は名前 **myTable.Columns["Col1"]** で参照され、**col1** は名前 **myTable.Columns["col1"]** で参照されます。 いずれかの列を **myTable.Columns["COL1"]** という名前で参照しようとすると、例外が生成されます。  
  
 大文字と小文字の区別の規則は、特定の名前の列、リレーション、または制約が 1 つしかない場合には適用されません。 つまり、特定の列、リレーション、または制約オブジェクトと名前が一致する列、リレーション、または制約オブジェクトがテーブルに存在しない場合は、大文字と小文字を区別せずにそのオブジェクトを名前で参照することができます。このとき、例外はスローされません。 たとえば、テーブルに **Col1** が 1 つしかない場合は、**my.Columns["COL1"]** を使用してこの列を参照できます。  
  
> [!NOTE]
> したがって、この動作は **DataTable** の <xref:System.Data.DataTable.CaseSensitive%2A> プロパティの影響を受けません。 **CaseSensitive** プロパティは、テーブルのデータに適用され、並べ替え、検索、フィルター処理、制約の適用などに影響を及ぼします。このプロパティは、テーブルの列、リレーション、および制約の参照には適用されません。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [DataTable への列の追加](adding-columns-to-a-datatable.md)  
 **DataColumn** オブジェクトを使用して、テーブルの列を定義する方法について説明します。  
  
 [式列の作成](creating-expression-columns.md)  
 列の **Expression** プロパティを使用して、同じ行にある他の列の値を基に値を計算する方法について説明します。  
  
 [AutoIncrement 列の作成](creating-autoincrement-columns.md)  
 数値を自動的にインクリメントして行ごとに一意の列値が割り当てられるように列を設定する方法について説明します。  
  
 [主キーの定義](defining-primary-keys.md)  
 1 つ以上の **DataColumn** オブジェクトからテーブルの主キーを指定する方法について説明します。  
  
 [DataTable の制約](datatable-constraints.md)  
 テーブルの列の外部キー制約と UNIQUE 制約を定義する方法について説明します。  
  
## <a name="see-also"></a>関連項目

- [DataTables](datatables.md)
- [ADO.NET の概要](../ado-net-overview.md)
