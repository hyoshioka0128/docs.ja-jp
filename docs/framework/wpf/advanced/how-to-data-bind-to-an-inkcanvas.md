---
title: '方法: InkCanvas にデータをバインドする'
ms.date: 03/30/2017
helpviewer_keywords:
- InkCanvas [WPF], binding data to
- binding data [WPF], to InkCanvas
ms.assetid: 8d6b4d9e-ea7f-4412-ba83-3feccec5a515
ms.openlocfilehash: 5d3fc0ed7b6176d7bc68bf20af42c311b5563908
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776468"
---
# <a name="how-to-data-bind-to-an-inkcanvas"></a>方法: InkCanvas にデータをバインドする
## <a name="example"></a>例  
 次の例は、<xref:System.Windows.Controls.InkCanvas> の <xref:System.Windows.Controls.InkCanvas.Strokes%2A> プロパティを別の <xref:System.Windows.Controls.InkCanvas> にバインドする方法を示しています。  
  
 [!code-xaml[InkCanvasBindingSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#2)]  
  
 次の例は、<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> プロパティをデータ ソースにバインドする方法を示しています。  
  
 [!code-xaml[InkCanvasBindingSnippet#3](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#3)]  
[!code-xaml[InkCanvasBindingSnippet#4](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window2.xaml#4)]  
  
 次の例では、XAML で 2 つの <xref:System.Windows.Controls.InkCanvas> オブジェクトを宣言し、それらと他のデータ ソースの間でデータ バインドを確立しています。  `ic` と呼ばれる最初の <xref:System.Windows.Controls.InkCanvas> は、2 つのデータ ソースにバインドされます。  `ic` の <xref:System.Windows.Controls.InkCanvas.EditingMode%2A> と <xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A> プロパティは、XAML で定義されている配列にバインドされる <xref:System.Windows.Controls.ListBox> オブジェクトにバインドされます。  2 番目の <xref:System.Windows.Controls.InkCanvas> の <xref:System.Windows.Controls.InkCanvas.EditingMode%2A>、<xref:System.Windows.Controls.InkCanvas.DefaultDrawingAttributes%2A>、<xref:System.Windows.Controls.InkCanvas.Strokes%2A> プロパティは、最初の <xref:System.Windows.Controls.InkCanvas>、`ic` にバインドされます。  
  
 [!code-xaml[InkCanvasBindingSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/InkCanvasBindingSnippet/CS/Window1.xaml#1)]
