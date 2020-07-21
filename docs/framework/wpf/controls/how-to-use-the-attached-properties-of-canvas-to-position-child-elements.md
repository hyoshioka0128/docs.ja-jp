---
title: '方法: Canvas の添付プロパティを使用して子要素を配置する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- attached properties [WPF Designer]
- Canvas control [WPF], attached properties
ms.assetid: 48f1d25d-3820-4107-a4cc-d6c1e5664a44
ms.openlocfilehash: 347c8502bd4c5fafcde7a142327f85bfb75b9954
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699072"
---
# <a name="how-to-use-the-attached-properties-of-canvas-to-position-child-elements"></a>方法: Canvas の添付プロパティを使用して子要素を配置する
この例からは、<xref:System.Windows.Controls.Canvas> の添付プロパティを使用し、子要素を配置する方法がわかります。  
  
## <a name="example"></a>例  
 次の例では、親 <xref:System.Windows.Controls.Canvas> の子要素として 4 つの <xref:System.Windows.Controls.Button> 要素が追加されます。 各要素は <xref:System.Windows.Controls.Canvas.Bottom%2A>、<xref:System.Windows.Controls.Canvas.Left%2A>、<xref:System.Windows.Controls.Canvas.Right%2A>、<xref:System.Windows.Controls.Canvas.Top%2A> で表されます。
各 <xref:System.Windows.Controls.Button> は、親 <xref:System.Windows.Controls.Canvas> に相対となる関係で、かつ、割り当てられているプロパティ値に基づいて配置されます。  
  
 [!code-cpp[CanvasAttachedProperties#1](~/samples/snippets/cpp/VS_Snippets_Wpf/CanvasAttachedProperties/CPP/CanvasAttachedProps.cpp#1)]
 [!code-csharp[CanvasAttachedProperties#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasAttachedProperties/CSharp/CanvasAttachedProps.cs#1)]
 [!code-vb[CanvasAttachedProperties#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasAttachedProperties/VisualBasic/CanvasAttachedProps.vb#1)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Canvas>
- <xref:System.Windows.Controls.Canvas.Bottom%2A>
- <xref:System.Windows.Controls.Canvas.Left%2A>
- <xref:System.Windows.Controls.Canvas.Right%2A>
- <xref:System.Windows.Controls.Canvas.Top%2A>
- <xref:System.Windows.Controls.Button>
- [パネルの概要](panels-overview.md)
- [方法トピック](canvas-how-to-topics.md)
- [添付プロパティの概要](../advanced/attached-properties-overview.md)
