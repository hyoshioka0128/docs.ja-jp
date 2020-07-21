---
title: DataRelation の追加
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a4a564fb-c1c4-4135-b6c2-b030e51195e4
ms.openlocfilehash: 8157d296636d0f8661a35af35de561f5cc49c30b
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784811"
---
# <a name="adding-datarelations"></a>DataRelation の追加
複数の <xref:System.Data.DataSet> オブジェクトを含む <xref:System.Data.DataTable> では、<xref:System.Data.DataRelation> オブジェクトを使用して 1 つのテーブルを別のテーブルに関連付けたり、テーブル間を移動したり、関連付けたテーブルから子または親の行を戻したりできます。  
  
 **DataRelation** の作成に必要な引数は、作成する **DataRelation** の名前、およびそのリレーションシップで親子の列となる列への 1 つ以上の <xref:System.Data.DataColumn> 参照の配列です。 **DataRelation** を作成した後は、それを使用して、テーブル間の移動や値の取得を行うことができます。  
  
 <xref:System.Data.DataSet> に **DataRelation** を追加すると、既定では、<xref:System.Data.UniqueConstraint> が親テーブルに、<xref:System.Data.ForeignKeyConstraint> が子テーブルに追加されます。 これらの既定の制約について詳しくは、「[DataTable の制約](datatable-constraints.md)」をご覧ください。  
  
 次のコード例では、<xref:System.Data.DataSet> の 2 つの <xref:System.Data.DataTable> オブジェクトを使用して、**DataRelation** を作成します。 各 <xref:System.Data.DataTable> にある **CustID** という名前の列は、2 つの <xref:System.Data.DataTable> オブジェクト間のリンクとして機能します。 例では、単一の **DataRelation** が <xref:System.Data.DataSet> の **Relations** コレクションに追加されます。 例の最初の引数では、作成する **DataRelation** の名前が指定されています。 2 番目の引数では親の **DataColumn** が設定され、3 番目の引数では子の **DataColumn** が設定されます。  
  
```vb  
customerOrders.Relations.Add("CustOrders", _  
  customerOrders.Tables("Customers").Columns("CustID"), _  
  customerOrders.Tables("Orders").Columns("CustID"))  
```  
  
```csharp  
customerOrders.Relations.Add("CustOrders",  
  customerOrders.Tables["Customers"].Columns["CustID"],  
  customerOrders.Tables["Orders"].Columns["CustID"]);  
```  
  
 **DataRelation** には、**Nested** プロパティもあります。それを **true** に設定すると、<xref:System.Data.DataSet.WriteXml%2A> を使用して XML 要素として書き込んだときに、子テーブルの行が、親テーブルの関連付けられた行の中に入れ子になります。 詳しくは、「[DataSet での XML の使用](using-xml-in-a-dataset.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
