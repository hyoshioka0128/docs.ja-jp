---
title: DataView の DataRowView コレクションの照会
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: b9070a12-1094-44d6-bb87-a23b50bcb0af
ms.openlocfilehash: 17fab6e4c178eee6b5135045fb953267db810898
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70794456"
---
# <a name="querying-the-datarowview-collection-in-a-dataview"></a>DataView の DataRowView コレクションの照会
<xref:System.Data.DataView> は、<xref:System.Data.DataRowView> オブジェクトの列挙可能なコレクションを公開します。 <xref:System.Data.DataRowView> は、<xref:System.Data.DataRow> のカスタマイズされたビューを表し、<xref:System.Data.DataRow> の特定のバージョンをコントロールに表示します。 <xref:System.Data.DataRow> などのコントロールを通じて、<xref:System.Windows.Forms.DataGridView> のバージョンを 1 つだけ表示できます。 <xref:System.Data.DataRow> が <xref:System.Data.DataRowView> の <xref:System.Data.DataRowView.Row%2A> プロパティを使用して公開している <xref:System.Data.DataRowView> にアクセスできます。 <xref:System.Data.DataRowView> を使用して値を表示している場合は、<xref:System.Data.DataView.RowStateFilter%2A> プロパティによって、基になる <xref:System.Data.DataRow> から公開される行バージョンが決まります。 <xref:System.Data.DataRow> を使用してさまざまな行バージョンにアクセスする方法については、「[行の状態とバージョン](./dataset-datatable-dataview/row-states-and-row-versions.md)」をご覧ください。 <xref:System.Data.DataView> によって公開される <xref:System.Data.DataRowView> オブジェクトのコレクションは列挙可能であるため、LINQ to DataSet を使用してクエリできます。  
  
 次の例では、`Product` テーブルに対して赤色の製品を照会し、そのクエリに基づくテーブルを作成します。 このテーブルから <xref:System.Data.DataView> を作成し、<xref:System.Data.DataView.RowStateFilter%2A> プロパティに、削除行と変更行を条件とするフィルターを設定します。 次に <xref:System.Data.DataView> を LINQ クエリのソースとして使用し、変更済みおよび削除済みの <xref:System.Data.DataRowView> オブジェクトを <xref:System.Windows.Forms.DataGridView> コントロールにバインドします。  
  
 [!code-csharp[DP DataView Samples#QueryDataView2](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview2)]
 [!code-vb[DP DataView Samples#QueryDataView2](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview2)]  
  
 次の例では、<xref:System.Windows.Forms.DataGridView> コントロールにバインドされたビューから製品のテーブルを作成します。 <xref:System.Data.DataView> に対して赤色の製品を照会し、並べ替えた結果を <xref:System.Windows.Forms.DataGridView> コントロールにバインドしています。  
  
 [!code-csharp[DP DataView Samples#QueryDataView1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataView Samples/CS/Form1.cs#querydataview1)]
 [!code-vb[DP DataView Samples#QueryDataView1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataView Samples/VB/Form1.vb#querydataview1)]  
  
## <a name="see-also"></a>関連項目

- [データ バインディングと LINQ to DataSet](data-binding-and-linq-to-dataset.md)
