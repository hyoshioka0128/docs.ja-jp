---
title: DataGridView コントロールで選択されたセル、行、および列を取得します。
description: 対応するプロパティを使用して、DataGridView コントロールから選択されたセル、行、または列を取得する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- selection [Windows Forms], DataGridView control [Windows Forms]
- DataGridView control [Windows Forms], getting selection
- getting selection [Windows Forms], DataGridView control [Windows Forms]
ms.assetid: d93c4b5b-498e-49bc-982a-2229d61778e4
ms.openlocfilehash: 32ddae34104d23b8e5fbc0cce7da79f33fcce1d2
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904170"
---
# <a name="how-to-get-the-selected-cells-rows-and-columns-in-the-windows-forms-datagridview-control"></a>方法: Windows フォーム DataGridView コントロールの選択されたセル、行、および列を取得する
コントロールから選択されたセル、行、または列を取得する <xref:System.Windows.Forms.DataGridView> には、対応するプロパティである、、およびを使用し <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> ます。 次の手順では、選択したセルを取得し、そのセルの行インデックスと列インデックスをに表示し <xref:System.Windows.Forms.MessageBox> ます。  
  
### <a name="to-get-the-selected-cells-in-a-datagridview-control"></a>DataGridView コントロール内の選択されたセルを取得するには  
  
- <xref:System.Windows.Forms.DataGridView.SelectedCells%2A> プロパティを使用します。  
  
    > [!NOTE]
    > 多くの <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A> セルが表示されないようにするには、メソッドを使用します。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#10](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#10](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#10)]  
  
### <a name="to-get-the-selected-rows-in-a-datagridview-control"></a>DataGridView コントロールで選択された行を取得するには  
  
- <xref:System.Windows.Forms.DataGridView.SelectedRows%2A> プロパティを使用します。 ユーザーが行を選択できるようにするには、プロパティをまたはに設定する必要があり <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> <xref:System.Windows.Forms.DataGridViewSelectionMode.FullRowSelect> <xref:System.Windows.Forms.DataGridViewSelectionMode.RowHeaderSelect> ます。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#20](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#20](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#20)]  
  
### <a name="to-get-the-selected-columns-in-a-datagridview-control"></a>DataGridView コントロールで選択されている列を取得するには  
  
- <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A> プロパティを使用します。 ユーザーが列を選択できるようにするには、プロパティをまたはに設定する必要があり <xref:System.Windows.Forms.DataGridView.SelectionMode%2A> <xref:System.Windows.Forms.DataGridViewSelectionMode.FullColumnSelect> <xref:System.Windows.Forms.DataGridViewSelectionMode.ColumnHeaderSelect> ます。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSelectedCollections#30](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/CS/DataGridViewSelectedCollections.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSelectedCollections#30](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSelectedCollections/VB/DataGridViewSelectedCollections.vb#30)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System.Windows.Forms.Button>、、およびという名前のコントロール `selectedCellsButton` `selectedRowsButton` 。それぞれに、 `selectedColumnsButton` アタッチされるイベントのハンドラーが <xref:System.Windows.Forms.Control.Click> あります。  
  
- `dataGridView1` という名前の <xref:System.Windows.Forms.DataGridView> コントロール。  
  
- <xref:System?displayProperty=nameWithType>、<xref:System.Windows.Forms?displayProperty=nameWithType>、および <xref:System.Text?displayProperty=nameWithType> の各アセンブリへの参照。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 このトピックで説明するコレクションは、多数のセル、行、または列が選択されている場合は、効率的には実行されません。 大量のデータでこれらのコレクションを使用する方法の詳細については、「 [Windows フォーム DataGridView コントロールのスケーリングに関するベストプラクティス](best-practices-for-scaling-the-windows-forms-datagridview-control.md)」を参照してください。  
  
## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.SelectionMode%2A>
- <xref:System.Windows.Forms.DataGridView.AreAllCellsSelected%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedCells%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedRows%2A>
- <xref:System.Windows.Forms.DataGridView.SelectedColumns%2A>
- [Windows フォーム DataGridView コントロールでの選択およびクリップボードの使用](selection-and-clipboard-use-with-the-windows-forms-datagridview-control.md)
