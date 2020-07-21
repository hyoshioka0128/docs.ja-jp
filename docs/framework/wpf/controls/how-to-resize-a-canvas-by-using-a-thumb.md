---
title: '方法: つまみを使用したキャンバスのサイズ変更'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- resizing Canvas control [WPF]
- controls [WPF], Thumb
- controls [WPF], Canvas
- Thumb control [WPF]
- Canvas control [WPF]
ms.assetid: 7dc9f435-726c-4d4d-be41-eb24cfe17bef
ms.openlocfilehash: 84f5ac2b53124b7f4d7c15741e94b40e7ee81526
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77124300"
---
# <a name="how-to-resize-a-canvas-by-using-a-thumb"></a>方法: つまみを使用したキャンバスのサイズ変更
この例は、<xref:System.Windows.Controls.Primitives.Thumb> コントロールを使用して <xref:System.Windows.Controls.Canvas> コントロールのサイズを変更する方法を示しています。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Primitives.Thumb> コントロールには、<xref:System.Windows.Controls.Primitives.Thumb> の <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>、<xref:System.Windows.Controls.Primitives.Thumb.DragDelta>、および <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> イベントを監視することにより、コントロールの移動またはサイズ変更に使用できるドラッグ機能が用意されています。  
  
 ユーザーがドラッグ操作を始めるには、マウス ポインターが <xref:System.Windows.Controls.Primitives.Thumb> コントロールに置かれているときに、左マウス ボタンを押します。 マウスの左ボタンが押されている間は、ドラッグ操作が続行されます。 ドラッグ操作中に、<xref:System.Windows.Controls.Primitives.Thumb.DragDelta> が複数回発生する可能性があります。 それが発生するたびに、<xref:System.Windows.Controls.Primitives.DragDeltaEventArgs> クラスからはマウス位置の変化に対応した位置の変化が提供されます。 ユーザーがマウスの左ボタンを放すと、ドラッグ操作は終了します。 ドラッグ操作からは、新しい座標のみが提供されます。<xref:System.Windows.Controls.Primitives.Thumb> の位置が自動的に変更されることはありません。  
  
 次の例は、<xref:System.Windows.Controls.Canvas> コントロールの子要素である <xref:System.Windows.Controls.Primitives.Thumb> コントロールを示しています。 <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> イベントのイベント ハンドラーには、<xref:System.Windows.Controls.Primitives.Thumb> を移動して <xref:System.Windows.Controls.Canvas> のサイズを変更するロジックが用意されています。 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> および <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> イベントのイベント ハンドラーを使用すると、ドラッグ操作中に <xref:System.Windows.Controls.Primitives.Thumb> の色を変更できます。 次の例では、<xref:System.Windows.Controls.Primitives.Thumb> を定義します。  
  
 [!code-xaml[Thumb#thumb](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml#thumb)]  
  
 マウスの動きに応じて <xref:System.Windows.Controls.Primitives.Thumb> を移動し、<xref:System.Windows.Controls.Canvas> のサイズを変更する <xref:System.Windows.Controls.Primitives.Thumb.DragDelta> イベント ハンドラーの例を次に示します。  
  
 [!code-csharp[Thumb#2](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#2)]  
  
 <xref:System.Windows.Controls.Primitives.Thumb.DragStarted> イベント ハンドラーの例を次に示します。  
  
 [!code-csharp[Thumb#DragStartedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragstartedhandler)]
 [!code-vb[Thumb#DragStartedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragstartedhandler)]  
  
 <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted> イベント ハンドラーの例を次に示します。  
  
 [!code-csharp[Thumb#DragCompletedHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/Thumb/CSharp/Pane1.xaml.cs#dragcompletedhandler)]
 [!code-vb[Thumb#DragCompletedHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Thumb/VisualBasic/Pane1.xaml.vb#dragcompletedhandler)]  
  
 サンプル全体については、[Thumb のドラッグ機能のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Drag%20and%20Drop/DragDropThumbOps)を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.Thumb>
- <xref:System.Windows.Controls.Primitives.Thumb.DragStarted>
- <xref:System.Windows.Controls.Primitives.Thumb.DragDelta>
- <xref:System.Windows.Controls.Primitives.Thumb.DragCompleted>
