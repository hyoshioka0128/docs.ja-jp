---
title: DataView のパフォーマンス
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 90820e49-9d46-41f6-9a3d-6c0741bbd8eb
ms.openlocfilehash: 7c81619bf4ac6ed084ea63349345dbf3b7f139b0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79150689"
---
# <a name="dataview-performance"></a>DataView のパフォーマンス
このトピックでは、<xref:System.Data.DataView.Find%2A> クラスの <xref:System.Data.DataView.FindRows%2A> メソッドと <xref:System.Data.DataView> メソッドを使用すること、および、Web アプリケーションで <xref:System.Data.DataView> をキャッシュすることのパフォーマンス上の利点について説明します。  
  
## <a name="find-and-findrows"></a>Find と FindRows  
 <xref:System.Data.DataView> はインデックスを構築します。 インデックスには、テーブル内またはビュー内の 1 つ以上の列から構築されたキーが含まれています。 これらのキーは特定の構造内に格納され、<xref:System.Data.DataView> はその構造を使用して、キー値に関連した 1 つ以上の行を効率よく迅速に検出できます。 フィルター処理や並べ替えなど、インデックスを使用した操作では、大幅なパフォーマンス向上が期待できます。 <xref:System.Data.DataView> のインデックスは、<xref:System.Data.DataView> の作成時に構築されるほか、並べ替えまたはフィルター処理の情報が変更されたときにも構築されます。 <xref:System.Data.DataView> を作成した後で、並べ替えまたはフィルター処理の情報を設定した場合、インデックスが最低でも 2 回 (<xref:System.Data.DataView> の作成時と、並べ替えまたはフィルターのプロパティの変更時) 構築されることになります。 <xref:System.Data.DataView> でのフィルター処理と並べ替えについて詳しくは、「[DataView によるフィルター処理](filtering-with-dataview-linq-to-dataset.md)」および「[DataView による並べ替え](sorting-with-dataview-linq-to-dataset.md)」をご覧ください。  
  
 データ サブセットの動的ビューの作成とは対照的に、データに対する特定のクエリの結果を取得する場合は、<xref:System.Data.DataView.Find%2A> プロパティを設定する代わりに <xref:System.Data.DataView.FindRows%2A> の <xref:System.Data.DataView> メソッドまたは <xref:System.Data.DataView.RowFilter%2A> メソッドを使用します。 <xref:System.Data.DataView.RowFilter%2A> プロパティは、データ連結アプリケーションでの使用に適しています。このアプリケーションでは、連結されたコントロールによってフィルター処理結果が表示されます。 <xref:System.Data.DataView.RowFilter%2A> プロパティを設定すると、データのインデックスが再構築され、アプリケーションのオーバーヘッドが増加してパフォーマンスの低下を招きます。 <xref:System.Data.DataView.Find%2A> メソッドと <xref:System.Data.DataView.FindRows%2A> メソッドでは、現在のインデックスが使用されます。このため、インデックスを再構築する必要はありません。 <xref:System.Data.DataView.Find%2A> または <xref:System.Data.DataView.FindRows%2A> を 1 回だけ呼び出す場合は、既存の <xref:System.Data.DataView> を使用するようにします。 <xref:System.Data.DataView.Find%2A> または <xref:System.Data.DataView.FindRows%2A> を複数回呼び出す場合は、新しい <xref:System.Data.DataView> を作成して検索対象の列のインデックスを再構築した後、<xref:System.Data.DataView.Find%2A> メソッドまたは <xref:System.Data.DataView.FindRows%2A> メソッドを呼び出します。 <xref:System.Data.DataView.Find%2A> メソッドおよび <xref:System.Data.DataView.FindRows%2A> メソッドについて詳しくは、「[行の検索](./dataset-datatable-dataview/finding-rows.md)」をご覧ください。  
  
 次の例では、<xref:System.Data.DataView.Find%2A> メソッドを使用して、姓が "Zhu" である連絡先を検索します。  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryorderbyfind)]
 [!code-vb[DP DataView Samples#LDVFromQueryOrderByFind](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryorderbyfind)]  
  
 次の例では、<xref:System.Data.DataView.FindRows%2A> メソッドを使用して、赤色の製品をすべて検索します。  
  
 [!code-csharp[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#ldvfromqueryfindrows)]
 [!code-vb[DP DataView Samples#LDVFromQueryFindRows](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#ldvfromqueryfindrows)]  
  
## <a name="aspnet"></a>ASP.NET  
 ASP.NET は、メモリ内に作成するときにサーバー リソースを激しく消費するオブジェクトを保存するためのキャッシュ メカニズムを備えています。 こうしたリソースをキャッシュすることで、アプリケーションのパフォーマンスを大幅に向上させることができます。 キャッシュは、<xref:System.Web.Caching.Cache> クラスに実装されています。キャッシュ インスタンスは、アプリケーションごとにプライベートに保たれます。 新しい <xref:System.Data.DataView> オブジェクトの作成はリソースを大量に消費する処理です。Web アプリケーションにこのキャッシュ機能を使用すれば、Web ページが更新されるたびに <xref:System.Data.DataView> を再構築する必要はありません。  
  
 次の例では、ページが更新されたときにデータの並べ替えをし直さなくても済むように、<xref:System.Data.DataView> をキャッシュしています。  
  
```vb  
If (Cache("ordersView") = Nothing) Then  
  
Dim dataSet As New DataSet()  
  
   FillDataSet(dataSet)  
  
   Dim orders As DataTable = dataSet.Tables("SalesOrderHeader")  
  
   Dim query = _  
                    From order In orders.AsEnumerable() _  
                    Where order.Field(Of Boolean)("OnlineOrderFlag") = True _  
                    Order By order.Field(Of Decimal)("TotalDue") _  
                    Select order  
  
   Dim view As DataView = query.AsDataView()  
  
   Cache.Insert("ordersView", view)  
  
End If  
  
Dim ordersView = CType(Cache("ordersView"), DataView)  
  
GridView1.DataSource = ordersView  
GridView1.DataBind()  
```  
  
```csharp  
if (Cache["ordersView"] == null)  
{  
   // Fill the DataSet.
   DataSet dataSet = FillDataSet();  
  
   DataTable orders = dataSet.Tables["SalesOrderHeader"];  
  
   EnumerableRowCollection<DataRow> query =  
                        from order in orders.AsEnumerable()  
                        where order.Field<bool>("OnlineOrderFlag") == true  
                        orderby order.Field<decimal>("TotalDue")  
                        select order;  
  
   DataView view = query.AsDataView();  
   Cache.Insert("ordersView", view);  
}  
  
DataView ordersView = (DataView)Cache["ordersView"];  
  
GridView1.DataSource = ordersView;  
GridView1.DataBind();  
```  
  
## <a name="see-also"></a>関連項目

- [データ バインディングと LINQ to DataSet](data-binding-and-linq-to-dataset.md)
