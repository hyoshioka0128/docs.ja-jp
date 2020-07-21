---
title: DataGridView コントロールの現在のセルを取得および設定します。
description: Windows フォーム DataGridView コントロールで現在のセルを取得および設定することによって、現在アクティブなセルをプログラムで検出する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataGridView control [Windows Forms], getting current cell
- DataGridView control [Windows Forms], setting current cell
- cells [Windows Forms], getting and setting current
ms.assetid: b0e41e57-493a-4bd0-9376-a6f76723540c
ms.openlocfilehash: 1651ca9c8fa0329f9435a70ce777bce68f15ff63
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622212"
---
# <a name="how-to-get-and-set-the-current-cell-in-the-windows-forms-datagridview-control"></a>方法: Windows フォーム DataGridView コントロールの現在のセルを取得および設定する
との対話で <xref:System.Windows.Forms.DataGridView> は、現在アクティブなセルをプログラムによって検出する必要があります。 また、現在のセルの変更が必要になる場合もあります。 これらのタスクは、プロパティを使用して実行でき <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> ます。  
  
> [!NOTE]
> プロパティがに設定されている行または列の現在のセルを設定することはできません <xref:System.Windows.Forms.DataGridViewBand.Visible%2A> `false` 。  
  
 コントロールの選択モードによっては、現在のセルを変更すると <xref:System.Windows.Forms.DataGridView> 選択範囲が変更される場合があります。 詳細については、「 [Windows フォーム DataGridView コントロールの選択モード](selection-modes-in-the-windows-forms-datagridview-control.md)」を参照してください。  
  
### <a name="to-get-the-current-cell-programmatically"></a>現在のセルをプログラムで取得するには  
  
- <xref:System.Windows.Forms.DataGridView>コントロールのプロパティを使用し <xref:System.Windows.Forms.DataGridView.CurrentCell%2A> ます。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#080](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#080)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#080](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#080)]  
  
### <a name="to-set-the-current-cell-programmatically"></a>現在のセルをプログラムによって設定するには  
  
- <xref:System.Windows.Forms.DataGridView.CurrentCell%2A>コントロールのプロパティを設定 <xref:System.Windows.Forms.DataGridView> します。 次のコード例では、現在のセルは行0、列1に設定されています。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewMisc#085](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/CS/datagridviewmisc.cs#085)]
     [!code-vb[System.Windows.Forms.DataGridViewMisc#085](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewMisc/VB/datagridviewmisc.vb#085)]  
  
## <a name="compiling-the-code"></a>コードのコンパイル  
 この例で必要な要素は次のとおりです。  
  
- <xref:System.Windows.Forms.Button>およびという名前のコントロール `getCurrentCellButton` `setCurrentCellButton` 。 Visual C# では、 <xref:System.Windows.Forms.Control.Click> 各ボタンのイベントを、コード例の関連付けられたイベントハンドラーにアタッチする必要があります。  
  
- `dataGridView1` という名前の <xref:System.Windows.Forms.DataGridView> コントロール。  
  
- <xref:System?displayProperty=nameWithType> アセンブリおよび <xref:System.Windows.Forms?displayProperty=nameWithType> アセンブリへの参照。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.CurrentCell%2A?displayProperty=nameWithType>
- [Windows フォーム DataGridView コントロールでの列、行、およびセルの基本機能](basic-column-row-and-cell-features-wf-datagridview-control.md)
- [Windows フォーム DataGridView コントロールの選択モード](selection-modes-in-the-windows-forms-datagridview-control.md)
