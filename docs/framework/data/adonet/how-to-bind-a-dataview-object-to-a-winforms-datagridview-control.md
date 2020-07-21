---
title: '方法: DataView オブジェクトを Windows フォーム DataGridView コントロールにバインドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2b73d60a-6049-446a-85a7-3e5a68b183e2
ms.openlocfilehash: 3a3089073cdc5afb4ee51caca9114b401c740b45
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2019
ms.locfileid: "70795007"
---
# <a name="how-to-bind-a-dataview-object-to-a-windows-forms-datagridview-control"></a>方法: DataView オブジェクトを Windows フォーム DataGridView コントロールにバインドする
<xref:System.Windows.Forms.DataGridView> コントロールには、データを表形式で表示するための強力で柔軟な機能が用意されています。 <xref:System.Windows.Forms.DataGridView> コントロールは、標準 Windows フォーム データ バインディング モデルをサポートするため、<xref:System.Data.DataView> およびその他の各種のデータ ソースにバインドします。 ただし、ほとんどの状況では、データ ソースとの対話の詳細を管理する <xref:System.Windows.Forms.BindingSource> コンポーネントにバインドします。  
  
 <xref:System.Windows.Forms.DataGridView> コントロールについて詳しくは、「[DataGridView コントロールの概要](../../winforms/controls/datagridview-control-overview-windows-forms.md)」をご覧ください。  
  
### <a name="to-connect-a-datagridview-control-to-a-dataview"></a>DataGridView コントロールを DataView に接続するには  
  
1. データベースからデータを取得する操作の詳細を処理するメソッドを実装します。 次のコード例では、`GetData` コンポーネントを初期化する <xref:System.Data.SqlClient.SqlDataAdapter> メソッドを実装し、これを使用して <xref:System.Data.DataSet> に値を設定します。 `connectionString` 変数は、使用しているデータベースに合った値に設定してください。 AdventureWorks SQL Server サンプル データベースがインストールされているサーバーにアクセスする必要があります。  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1getdata)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1GetData](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1getdata)]  
  
2. フォームの <xref:System.Windows.Forms.Form.Load> イベント ハンドラーで、<xref:System.Windows.Forms.DataGridView> コントロールを <xref:System.Windows.Forms.BindingSource> コンポーネントにバインドし、`GetData` メソッドを呼び出してデータベースからデータを取得します。 <xref:System.Data.DataView> は、Contact <xref:System.Data.DataTable> に対する LINQ to DataSet クエリから作成された後、<xref:System.Windows.Forms.BindingSource> コンポーネントにバインドされます。  
  
     [!code-csharp[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/CS/Form1.cs#ldvsample1formload)]
     [!code-vb[DP DataViewWinForms Sample#LDVSample1FormLoad](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP DataViewWinForms Sample/VB/Form1.vb#ldvsample1formload)]  
  
## <a name="see-also"></a>関連項目

- [データ バインディングと LINQ to DataSet](data-binding-and-linq-to-dataset.md)
