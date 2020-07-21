---
title: '方法: グリッド間でサイズ設定プロパティを共有する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Grid control [WPF], sharing sizing data of columns
- sizing data in Grid controls [WPF]
- Grid control [WPF], sharing sizing data of rows
ms.assetid: a0535a6f-ff04-4b25-9912-7dd856e11044
ms.openlocfilehash: d5ab2ac612d55c8cbc34ae6d7d9d63b9f8aa23e7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910586"
---
# <a name="how-to-share-sizing-properties-between-grids"></a>方法: グリッド間でサイズ設定プロパティを共有する
この例からは、サイズ設定の一貫性を維持する目的で <xref:System.Windows.Controls.Grid> 要素間の列と行のサイズ設定データを共有する方法がわかります。  
  
## <a name="example"></a>例  
 次の例では、親 <xref:System.Windows.Controls.DockPanel> の子要素として 2 つの <xref:System.Windows.Controls.Grid> 要素が導入されます。 <xref:System.Windows.Controls.Grid> の <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> 添付プロパティは親 <xref:System.Windows.Controls.DockPanel> で定義されます。  
  
 この例では、2 つの <xref:System.Windows.Controls.Button> 要素を使用してプロパティの値を操作します。各要素は、Boolean プロパティ値の 1 つを表します。 <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A> プロパティ値が `true` に設定されると、<xref:System.Windows.Controls.DefinitionBase.SharedSizeGroup%2A> の各列または行メンバーでは、行または列のコンテンツに関係なく、サイズ設定情報が共有されます。  
  
 [!code-xaml[gridIssharedsizescopeProp#1](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#1)]  
  
 ...  
  
 [!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]  
  
 次のコードビハインド例では、ボタン <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントで発生するメソッドが処理されています。 この例では、これらのメソッドの <xref:System.Windows.Controls.TextBlock> 要素に対する呼び出しの結果を記述しています。この要素は、関連する獲得メソッドを使用して新しいプロパティの値を文字列として出力します。  
  
 [!code-csharp[gridIssharedsizescopeProp#3](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml.cs#3)]
 [!code-vb[gridIssharedsizescopeProp#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/gridIssharedsizescopeProp/VisualBasic/Window1.xaml.vb#3)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Grid>
- <xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A>
- [パネルの概要](panels-overview.md)
