---
title: '方法: GridSplitter を表示されるようにする'
ms.date: 03/30/2017
helpviewer_keywords:
- GridSplitter control [WPF], ensuring visibility of
ms.assetid: 0a62a964-89c8-48f0-9023-5df721a8cf47
ms.openlocfilehash: 2085ac5cec206d8692a1267acf132688f0aa9082
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64663316"
---
# <a name="how-to-make-sure-that-a-gridsplitter-is-visible"></a>方法: GridSplitter を表示されるようにする
この例では、<xref:System.Windows.Controls.Grid> 内の他のコントロールによって <xref:System.Windows.Controls.GridSplitter> コントロールが非表示にされていないことを確認する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Grid> コントロールの <xref:System.Windows.Controls.Panel.Children%2A> は、マークアップまたはコードで定義されている順序で表示されます。 <xref:System.Windows.Controls.GridSplitter> コントロールは、<xref:System.Windows.Controls.Panel.Children%2A> コレクション内の最後の要素として定義されていない場合、またはより高い <xref:System.Windows.Controls.Panel.ZIndexProperty> が他のコントロールに指定されている場合に、他のコントロールによって非表示にすることができます。  
  
 <xref:System.Windows.Controls.GridSplitter> コントロールが非表示にされないようにするには、次のいずれかの操作を行います。  
  
- <xref:System.Windows.Controls.GridSplitter> コントロールが <xref:System.Windows.Controls.Grid> に追加された最後の <xref:System.Windows.Controls.Panel.Children%2A> であることを確認します。 次の例では、<xref:System.Windows.Controls.Grid> の <xref:System.Windows.Controls.Panel.Children%2A> コレクション内の最後の要素として <xref:System.Windows.Controls.GridSplitter> が示されています。  
  
 [!code-xaml[GridSplitterSnips#GridSplitterLastChild](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterlastchild)]  
  
- <xref:System.Windows.Controls.GridSplitter> の <xref:System.Windows.Controls.Panel.ZIndexProperty> を、非表示にされないよう、コントロールよりも高く設定します。 次の例では、<xref:System.Windows.Controls.Button> コントロールよりも高い <xref:System.Windows.Controls.Panel.ZIndexProperty> が <xref:System.Windows.Controls.GridSplitter> コントロールに設定されています。  
  
 [!code-xaml[GridSplitterSnips#GridSplitterZIndex](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplitterzindex)]  
  
- <xref:System.Windows.Controls.GridSplitter> が表示されるようにするため、<xref:System.Windows.Controls.GridSplitter> が非表示にされないようにコントロールに余白を設定します。 次の例では、<xref:System.Windows.Controls.GridSplitter> がオーバーレイされて非表示にされないように、コントロールに余白が設定されています。  
  
 [!code-xaml[GridSplitterSnips#GridSplitterMargin](~/samples/snippets/csharp/VS_Snippets_Wpf/GridSplitterSnips/CSharp/Window1.xaml#gridsplittermargin)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GridSplitter>
- [方法トピック](gridsplitter-how-to-topics.md)
