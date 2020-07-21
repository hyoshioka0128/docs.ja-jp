---
title: ContextMenu の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ContextMenu
- ContextMenu controls [WPF], about ContextMenu controls
ms.assetid: 16909c42-799a-4561-91e0-7d69dcfeea91
ms.openlocfilehash: 4d2d8db0f614b5240705146dbe91432b96b46dd6
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185909"
---
# <a name="contextmenu-overview"></a>ContextMenu の概要
<xref:System.Windows.Controls.ContextMenu> クラスは、コンテキスト固有の <xref:System.Windows.Controls.Menu> を使用して機能を公開する要素を表します。 通常、ユーザーはマウス ボタンを右クリックすることによって、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] に <xref:System.Windows.Controls.ContextMenu> を表示します。 このトピックでは、<xref:System.Windows.Controls.ContextMenu> 要素について説明し、この要素を [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] とコードで使用する例を示します。  

<a name="contextmenu_control"></a>
## <a name="contextmenu-control"></a>ContextMenu コントロール  
 <xref:System.Windows.Controls.ContextMenu> は特定のコントロールに結び付けられています。 <xref:System.Windows.Controls.ContextMenu> 要素を使用すると、<xref:System.Windows.Controls.Button> などの特定のコントロールに関連付けられているコマンドやオプションを指定する項目の一覧をユーザーに提供できます。 ユーザーがコントロールを右クリックすると、メニューが表示されます。 通常、<xref:System.Windows.Controls.MenuItem> をクリックすると、サブメニューが開かれるか、またはアプリケーションによってコマンドが実行されます。  
  
<a name="creating_contextmenus"></a>
## <a name="creating-contextmenus"></a>ContextMenu の作成  
 次の例では、サブメニューのある <xref:System.Windows.Controls.ContextMenu> を作成する方法を示します。 <xref:System.Windows.Controls.ContextMenu> コントロールは、ボタン コントロールに結び付けられます。  
  
 [!code-xaml[ContextMenu#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml#1)]  
  
 [!code-csharp[ContextMenu#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenu/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ContextMenu#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ContextMenu/VisualBasic/Pane1.xaml.vb#2)]  
  
<a name="applying_styles_to_contextmenu"></a>
## <a name="applying-styles-to-a-contextmenu"></a>ContextMenu へのスタイルの適用  
 <xref:System.Windows.Style> コントロールを使用すると、カスタム コントロールを作成しなくても、<xref:System.Windows.Controls.ContextMenu> の外観と動作を大幅に変更できます。 視覚プロパティの設定に加えて、コントロールの一部にスタイルを適用することもできます。 たとえば、プロパティを使用してコントロールの一部の動作を変更したり、<xref:System.Windows.Controls.ContextMenu> に対するパーツの追加やレイアウトの変更を行ったりできます。 次の例では、<xref:System.Windows.Controls.ContextMenu> コントロールにスタイルを追加する方法をいくつか示します。  
  
 最初の例では、`SimpleSysResources` という名前のスタイルを定義し、スタイルで現在のシステム設定を使用する方法を示します。 この例では、<xref:System.Windows.Controls.ContextMenu> の <xref:System.Windows.Controls.Control.Background%2A> の色として <xref:System.Windows.SystemColors.MenuHighlightBrushKey%2A> を割り当て、<xref:System.Windows.Controls.Control.Foreground%2A> の色として <xref:System.Windows.SystemColors.MenuTextBrushKey%2A> を割り当てます。  
  
```xaml  
<Style x:Key="SimpleSysResources" TargetType="{x:Type MenuItem}">  
  <Setter Property = "Background" Value=
    "{DynamicResource {x:Static SystemColors.MenuHighlightBrushKey}}"/>  
  <Setter Property = "Foreground" Value=
    "{DynamicResource {x:Static SystemColors.MenuTextBrushKey}}"/>  
</Style>  
```  
  
 次の例では、<xref:System.Windows.Trigger> 要素を使用して、<xref:System.Windows.Controls.ContextMenu> で発生するイベントに応じて、<xref:System.Windows.Controls.Menu> の外観を変更します。 ユーザーがメニューの上にマウスを移動すると、<xref:System.Windows.Controls.ContextMenu> 項目の外観が変わります。  
  
```xaml  
<Style x:Key="Triggers" TargetType="{x:Type MenuItem}">  
  <Style.Triggers>  
    <Trigger Property="MenuItem.IsMouseOver" Value="true">  
      <Setter Property = "FontSize" Value="16"/>  
      <Setter Property = "FontStyle" Value="Italic"/>  
      <Setter Property = "Foreground" Value="Red"/>  
    </Trigger>  
  </Style.Triggers>  
</Style>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.Style>
- <xref:System.Windows.Controls.Menu>
- <xref:System.Windows.Controls.MenuItem>
- [ContextMenu](contextmenu.md)
- [ContextMenu のスタイルとテンプレート](contextmenu-styles-and-templates.md)
- [WPF Controls Gallery Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/ControlsAndLayout)
