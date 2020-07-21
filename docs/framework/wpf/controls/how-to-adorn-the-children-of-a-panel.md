---
title: '方法: パネルの子を装飾する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- adorners [WPF], binding to children of Panels
- Panel control [WPF], binding adorners to children
ms.assetid: 4cc9b972-b472-4e5c-bdf3-3702d7fbb1f5
ms.openlocfilehash: 739ccaa0273e66c4650c35217a1156d64336dbbb
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69923526"
---
# <a name="how-to-adorn-the-children-of-a-panel"></a>方法: パネルの子を装飾する
この例では、指定した <xref:System.Windows.Controls.Panel> の子にプログラムで装飾をバインドする方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Panel> の子に装飾をバインドするには、次の手順を行います。  
  
1. 新しい <xref:System.Windows.Documents.AdornerLayer> オブジェクトを宣言し、`static`<xref:System.Windows.Documents.AdornerLayer.GetAdornerLayer%2A> メソッドを呼び出して、子が装飾対象となる要素の装飾層を検出します。  
  
2. 親要素の子を列挙し、<xref:System.Windows.Documents.AdornerLayer.Add%2A> メソッドを呼び出して、装飾を各子要素にバインドします。  
  
 次の例では、SimpleCircleAdorner (上図参照) を *myStackPanel* という名前の <xref:System.Windows.Controls.StackPanel> の子にバインドします。  
  
 [!code-csharp[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/csharp/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/CSharp/Window1.xaml.cs#_adornchildren)]
 [!code-vb[Adorners_SimpleCircleAdorner#_AdornChildren](~/samples/snippets/visualbasic/VS_Snippets_Wpf/Adorners_SimpleCircleAdorner/VisualBasic/Window1.xaml.vb#_adornchildren)]  
  
> [!NOTE]
> [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して、装飾を別の要素にバインドする方法は、現在サポートされていません。  
  
## <a name="see-also"></a>関連項目

- [装飾の概要](adorners-overview.md)
