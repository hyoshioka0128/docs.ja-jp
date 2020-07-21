---
title: '方法: 要素に装飾をバインドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- UIElements [WPF], binding adorners to
- adorners [WPF], binding to specified UIElements
ms.assetid: b2101611-a0ee-4137-bdb8-9b3673d2e6b9
ms.openlocfilehash: e8c7eb929042bfe1455bfc9bf459fc466de5c397
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923493"
---
# <a name="how-to-bind-an-adorner-to-an-element"></a>方法: 要素に装飾をバインドする
この例では、指定した <xref:System.Windows.UIElement> にプログラムで装飾をバインドする方法を示します。  
  
## <a name="example"></a>例  
 特定の <xref:System.Windows.UIElement> に装飾をバインドするには、次の手順を行います。  
  
1. `static` メソッド <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> を呼び出して、装飾対象となる <xref:System.Windows.UIElement> の <xref:System.Windows.Documents.AdornerLayer> オブジェクトを取得します。 <xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> は、指定した **UIElement** を起点としてビジュアル ツリーを上に探索し、最初に見つかった装飾層を返します。 (装飾層が見つからない場合、メソッドにより null が返されます)。  
  
2. <xref:System.Windows.Documents.AdornerLayer.Add%2A> メソッドを呼び出して、対象の **UIElement** に装飾をバインドします。  
  
 次の例では、SimpleCircleAdorner (上図参照) を *myTextBox* という名前の <xref:System.Windows.Controls.TextBox> にバインドします。  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornsingleelement)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornSingleElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornsingleelement)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して、装飾を別の要素にバインドする方法は、現在サポートされていません。  
  
## <a name="see-also"></a>関連項目

- [装飾の概要](adorners-overview.md)
