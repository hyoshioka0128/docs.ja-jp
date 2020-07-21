---
title: '方法: TextWrapping プロパティをプログラムにより変更する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], changing TextWrapping property programmatically
- TextWrapping property [WPF], changing programmatically
ms.assetid: 30d25554-4c82-4df9-a8d6-35683a4a13bb
ms.openlocfilehash: 21ca31d24121492fe6927cd533d5b3c0785b5a28
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776663"
---
# <a name="how-to-change-the-textwrapping-property-programmatically"></a>方法: TextWrapping プロパティをプログラムにより変更する
## <a name="example"></a>例  
 次のコード例では、<xref:System.Windows.Controls.TextBlock.TextWrapping%2A> プロパティの値をプログラムで変更する方法を示しています。  
  
 3 つの <xref:System.Windows.Controls.Button> 要素は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.Controls.StackPanel> 要素に配置されます。 <xref:System.Windows.Controls.Button> の各 <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントは、そのコードのイベント ハンドラーに対応します。 イベント ハンドラーは、ボタンがクリックされると `txt2` に適用される、<xref:System.Windows.Controls.TextBlock.TextWrapping%2A> 値と同じ名前を使用します。 また、([!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] にはない <xref:System.Windows.Controls.TextBlock> である) `txt1` のテキストが更新され、プロパティが変わったことが反映されます。  
  
 [!code-xaml[TextWrapProperty#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml#1)]  
  
 [!code-csharp[TextWrapProperty#2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextWrapProperty/CSharp/Window1.xaml.cs#2)]
 [!code-vb[TextWrapProperty#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextWrapProperty/VisualBasic/Pane1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.TextBlock.TextWrapping%2A>
- <xref:System.Windows.TextWrapping>
