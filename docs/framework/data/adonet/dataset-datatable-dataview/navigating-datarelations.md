---
title: DataRelation の移動
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e673f4-9b44-45ae-aaea-c504d1cc5d3e
ms.openlocfilehash: 73523297454be37716acedad13498954ef9a89a0
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73040344"
---
# <a name="navigating-datarelations"></a>DataRelation の移動
<xref:System.Data.DataRelation> の主な機能の 1 つは、<xref:System.Data.DataTable> の 1 つの <xref:System.Data.DataSet> から別の  を移動できることです。 これにより、関連付けられた **DataTable** から単一の **DataRow** を指定して、関連するすべての <xref:System.Data.DataRow> オブジェクトを 1 つの **DataTable** に取得できます。 たとえば、顧客のテーブルと注文のテーブル間に **DataRelation** を確立した後、**GetChildRows** を使用して、特定の顧客行に対するすべての注文行を取得できます。  
  
 次のコード例では、**DataSet** の **Customers** テーブルと **Orders** テーブルの間に **DataRelation** を作成し、各顧客に対するすべての注文を返します。  
  
 [!code-csharp[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableRelation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableRelation/VB/source.vb#1)]  
  
 上記の例に基づいて、4 つのテーブルを相互に関連付け、そのテーブルのリレーションシップ間を移動する例を次に示します。 上の例のように、**CustomerID** によって **Customers** テーブルが **Orders** テーブルに関連付けられます。 特定の顧客の注文数とその **OrderID** の値を返すため、**Customers** テーブルの顧客ごとに、**Orders** テーブル内のすべての子の行が特定されます。  
  
 展開された例では、**OrderDetails** テーブルと **Products** テーブルからも値が返されます。 **OrderID** を使用して **Orders** テーブルが **OrderDetails** テーブルに関連付けられ、顧客の注文ごとに、注文された製品と数量が特定されます。 **OrderDetails** テーブルに含まれるのは、注文された製品の **ProductID** だけなので、**ProductName** を返すため、**ProductID** を使用して、**OrderDetails** が **Products** に関連付けられます。 この関係では、**Products** テーブルが親となり、**Order Details** テーブルが子となります。 その結果、**OrderDetails** テーブルの反復処理では、**GetParentRow** を呼び出して、関連付けられた **ProductName** の値を取得します。  
  
 **DataRelation** が **Customers** テーブルと **Orders** テーブルに対して作成されるとき、**createConstraints** フラグに対して値が指定されていないことに注意してください (既定値は **true**)。 これにより、**Orders** テーブルのすべての行に対して、親の **Customers** テーブルに **CustomerID** の値が存在するものと設定されます。 **Customers** テーブルに存在しない **CustomerID** が **Orders** テーブルに存在した場合、<xref:System.Data.ForeignKeyConstraint> では例外がスローされます。  
  
 親の列に含まれていない値が子の列に含まれる場合は、**DataRelation** を追加するときに、**createConstraints** フラグを **false** に設定します。 この例では、**Orders** テーブルと **OrderDetails** テーブルの間の **DataRelation** に対して、**createConstraints** フラグが **false** に設定されています。 このため、このアプリケーションでは、実行時に例外を生成せずに、**OrderDetails** テーブルのすべてのレコードと、**Orders** テーブルのレコードのサブセットだけを、返すことができます。 展開された例では、次の形式で出力が生成されます。  
  
```output  
Customer ID: NORTS  
  Order ID: 10517  
        Order Date: 4/24/1997 12:00:00 AM  
           Product: Filo Mix  
          Quantity: 6  
           Product: Raclette Courdavault  
          Quantity: 4  
           Product: Outback Lager  
          Quantity: 6  
  Order ID: 11057  
        Order Date: 4/29/1998 12:00:00 AM  
           Product: Outback Lager  
          Quantity: 3  
```  
  
 次のコード例はサンプルを拡張したものであり、**OrderDetails** テーブルと **Products** テーブルから値が返され、**Orders** テーブルからはレコードのサブセットだけが返されます。  
  
 [!code-csharp[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/CS/source.cs#1)]
 [!code-vb[DataWorks Data.DataTableNavigation#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks Data.DataTableNavigation/VB/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [DataSet、DataTable、および DataView](index.md)
- [ADO.NET の概要](../ado-net-overview.md)
