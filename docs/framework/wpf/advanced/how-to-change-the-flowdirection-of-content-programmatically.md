---
title: '方法: プログラムによってコンテンツの FlowDirection を変更する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- FlowDirection property [WPF], changing programmatically
- documents [WPF], changing FlowDirection property programmatically
ms.assetid: 02f5a8ba-f8c0-4e5a-84b9-4c5bf12922a2
ms.openlocfilehash: ec159ed0efce8b5514788331e8715a55e7a8a638
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776559"
---
# <a name="how-to-change-the-flowdirection-of-content-programmatically"></a>方法: プログラムによってコンテンツの FlowDirection を変更する
この例では、<xref:System.Windows.Controls.FlowDocumentReader> の <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティをプログラムで変更する方法を示します。  
  
## <a name="example"></a>例  
 2 つの <xref:System.Windows.Controls.Button> 要素が作成され、それぞれが <xref:System.Windows.FlowDirection> の使用できる値の 1 つを表します。 ボタンがクリックされると、関連付けられているプロパティ値が `tf1` という名前の <xref:System.Windows.Controls.FlowDocumentReader> のコンテンツに適用されます。  プロパティ値は、`txt1` という名前の <xref:System.Windows.Controls.TextBlock> にも書き込まれます。  
  
 [!code-xaml[FlowDirectionSnippets#_FlowDirectionXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml#_flowdirectionxaml)]  
  
## <a name="example"></a>例  
 上で定義されているボタン クリックに関連付けられているイベントは、C# 分離コード ファイルで処理されます。  
  
 [!code-csharp[FlowDirectionSnippets#_FlowDirection](~/samples/snippets/csharp/VS_Snippets_Wpf/FlowDirectionSnippets/CSharp/Window1.xaml.cs#_flowdirection)]
 [!code-vb[FlowDirectionSnippets#_FlowDirection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FlowDirectionSnippets/VisualBasic/Window1.xaml.vb#_flowdirection)]
