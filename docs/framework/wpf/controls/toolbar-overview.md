---
title: ToolBar の概要
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], ToolBar
- ToolBar control [WPF]
ms.assetid: a8edb32c-118d-4f31-b6e6-8899082b504b
ms.openlocfilehash: b5498b8b88c7403ffe51256a57544261de3ace08
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186609"
---
# <a name="toolbar-overview"></a>ToolBar の概要
<xref:System.Windows.Controls.ToolBar> コントロールは、コマンドまたはコントロールのグループのコンテナーで、通常、それぞれの機能に関連しています。 <xref:System.Windows.Controls.ToolBar> には通常、コマンドを呼び出すボタンが含まれます。  

<a name="ToolBarControl"></a>
## <a name="toolbar-control"></a>ToolBar コントロール  
 <xref:System.Windows.Controls.ToolBar> コントロールという名前は、ボタンや他のコントロールが 1 つの行または列としてバーのように配置されることに由来します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の <xref:System.Windows.Controls.ToolBar> コントロールでは、サイズ制限のある <xref:System.Windows.Controls.ToolBar> 内に自然に収まらない項目を特別なオーバーフロー領域に配置するオーバーフロー メカニズムが提供されます。 また、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の <xref:System.Windows.Controls.ToolBar> コントロールは通常、関連する <xref:System.Windows.Controls.ToolBarTray> コントロールと共に使用されます。このコントロールでは、特殊なレイアウト動作およびユーザーによるサイズ変更およびツールバーの配置のサポートが提供されます。  
  
<a name="Creating_ToolBars"></a>
## <a name="specifying-the-position-of-toolbars-in-a-toolbartray"></a>ToolBarTray でツールバーの位置を指定する  
 <xref:System.Windows.Controls.ToolBarTray> に <xref:System.Windows.Controls.ToolBar> を配置するには、<xref:System.Windows.Controls.ToolBar.Band%2A> プロパティと <xref:System.Windows.Controls.ToolBar.BandIndex%2A> プロパティを使用します。 <xref:System.Windows.Controls.ToolBar.Band%2A> は、<xref:System.Windows.Controls.ToolBar> がその親の <xref:System.Windows.Controls.ToolBarTray> 内に配置される位置を示します。 <xref:System.Windows.Controls.ToolBar.BandIndex%2A> は、<xref:System.Windows.Controls.ToolBar> がそのバンド内で配置される順序を示します。 次の例では、このプロパティを使用して <xref:System.Windows.Controls.ToolBar> コントロールを <xref:System.Windows.Controls.ToolBarTray> 内に配置する方法を示します。  
  
 [!code-xaml[ToolBarExample#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#2)]  
  
<a name="ToolBars_with_Overflow_Items"></a>
## <a name="toolbars-with-overflow-items"></a>オーバーフロー項目を含むツールバー  
 多くの場合、<xref:System.Windows.Controls.ToolBar> コントロールには、ツールバーのサイズに収まらないほど多くの項目が含まれています。 この場合、<xref:System.Windows.Controls.ToolBar> には、オーバーフロー ボタンが表示されます。 オーバーフロー項目を表示するには、オーバーフロー ボタンをクリックします。項目は、<xref:System.Windows.Controls.ToolBar> の下のポップアップ ウィンドウに表示されます。 次の図は、オーバーフロー項目が含まれる <xref:System.Windows.Controls.ToolBar> を示したものです。  
  
 ![オーバーフロー項目が含まれるツール バーを示すスクリーンショット。](./media/toolbar-overview/toolbar-overflow-items.png)  
  
 <xref:System.Windows.Controls.ToolBar.OverflowMode%2A?displayProperty=nameWithType> 添付プロパティを <xref:System.Windows.Controls.OverflowMode.Always?displayProperty=nameWithType>、<xref:System.Windows.Controls.OverflowMode.Never?displayProperty=nameWithType>、または <xref:System.Windows.Controls.OverflowMode.AsNeeded?displayProperty=nameWithType> に設定することで、いつツールバーにある項目をオーバーフロー パネルに配置するかを指定できます。 次の例では、ツールバーの最後の 4 つのボタンを常にオーバーフロー パネルに配置します。  
  
 [!code-xaml[ToolBarExample#3](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolBarExample/CS/Pane1.xaml#3)]  
  
 <xref:System.Windows.Controls.ToolBar> では、その <xref:System.Windows.Controls.ControlTemplate> で <xref:System.Windows.Controls.Primitives.ToolBarPanel> と <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> を使用します。  <xref:System.Windows.Controls.Primitives.ToolBarPanel> では、ツールバー上の項目のレイアウトが行われます。  <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel> では、<xref:System.Windows.Controls.ToolBar> に収まらない項目のレイアウトが行われます。 <xref:System.Windows.Controls.ToolBar> に対する <xref:System.Windows.Controls.ControlTemplate> の例については、  
  
 「[ToolBar のスタイルとテンプレート](toolbar-styles-and-templates.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.ToolBarPanel>
- <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>
- [ToolBar のコントロールのスタイルを設定する](how-to-style-controls-on-a-toolbar.md)
- [WPF Controls Gallery Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/ControlsAndLayout)
