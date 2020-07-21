---
title: ToolTip の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ToolTip control [WPF], about ToolTip control
- controls [WPF], ToolTip
ms.assetid: f06c1603-e9cb-4809-8a62-234607fc52f7
ms.openlocfilehash: 0fec31b28a21c2e17986210c852b3d630087842d
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181946"
---
# <a name="tooltip-overview"></a>ToolTip の概要
ツールヒントは、ユーザーが <xref:System.Windows.Controls.Button> などの要素の上にマウス ポインターを置いたときに表示される小さなポップアップ ウィンドウです。 このトピックでは、ツールヒントを紹介し、ツールヒントの内容を作成およびカスタマイズする方法について説明します。  

<a name="what_is_a_tooltip"></a>
## <a name="what-is-a-tooltip"></a>ツールヒントとは  
 ツールヒントを持つ要素の上にマウス ポインターを置くと、一定の時間、ツールヒントの内容 (たとえば、コントロールの機能を説明するテキスト コンテンツ) を含むウィンドウが表示されます。 コントロールからマウス ポインターを移動すると、ツールヒントの内容がフォーカスを受け取ることができなくなるため、ウィンドウが消えます  
  
 ツールヒントの内容は、1 行または複数行のテキスト、イメージ、図形などのビジュアル コンテンツを含めることができます。 次のプロパティの 1 つをツールヒントの内容に設定することによって、コントロールのツールヒントを定義します。  
  
- <xref:System.Windows.FrameworkContentElement.ToolTip%2A?displayProperty=nameWithType>  
  
- <xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=nameWithType>  
  
 どのプロパティを使用するかは、ツールヒントを定義するコントロールが <xref:System.Windows.FrameworkContentElement> または <xref:System.Windows.FrameworkElement> のどちらのクラスを継承しているかによって異なります。  
  
<a name="create_tooltip"></a>
## <a name="creating-a-tooltip"></a>ツールヒントの作成  
 次の例では、<xref:System.Windows.Controls.Button> コントロールの <xref:System.Windows.FrameworkElement.ToolTip%2A> プロパティにテキスト文字列を設定することにより、簡単なツールヒントを作成する方法を示します。  
  
 [!code-xaml[GroupBoxSnippet#ToolTipString](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipstring)]  
  
 また、ツールヒントを <xref:System.Windows.Controls.ToolTip> オブジェクトとして定義することもできます。 次の例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用して、<xref:System.Windows.Controls.TextBox> 要素のツールヒントとして <xref:System.Windows.Controls.ToolTip> オブジェクトを指定しています。 この例では、<xref:System.Windows.FrameworkElement.ToolTip%2A?displayProperty=nameWithType> プロパティを設定することにより <xref:System.Windows.Controls.ToolTip> を指定していることに注意してください。  
  
 [!code-xaml[ToolTipSimple#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#tooltip)]  
  
 次の例では、コードを使用して <xref:System.Windows.Controls.ToolTip> オブジェクトを生成します。 この例では、<xref:System.Windows.Controls.ToolTip> (`tt`) を作成し、それを <xref:System.Windows.Controls.Button> に関連付けます。  
  
 [!code-csharp[ToolTipSimple#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml.cs#2)]
 [!code-vb[ToolTipSimple#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ToolTipSimple/VisualBasic/Window1.xaml.vb#2)]  
  
 <xref:System.Windows.Controls.DockPanel> などのレイアウト要素でツールヒントの内容を囲むことにより、<xref:System.Windows.Controls.ToolTip> オブジェクトとして定義されていないツールヒントの内容を作成することもできます。 次の例では、<xref:System.Windows.Controls.DockPanel> コントロールで囲まれたコンテンツを、<xref:System.Windows.Controls.TextBox> の <xref:System.Windows.FrameworkElement.ToolTip%2A> プロパティに設定する方法を示します。  
  
 [!code-xaml[GroupBoxSnippet#ToolTipDockPanel](~/samples/snippets/csharp/VS_Snippets_Wpf/GroupBoxSnippet/CS/Window1.xaml#tooltipdockpanel)]  
  
<a name="Using_the_ToolTip_and_ToolTipService_Properties"></a>
## <a name="using-the-properties-of-the-tooltip-and-tooltipservice-classes"></a>ToolTip クラスおよび ToolTipService クラスのプロパティの使用  
 ビジュアル プロパティを設定し、スタイルを適用して、ツールヒントの内容をカスタマイズできます。 ツールヒントの内容を <xref:System.Windows.Controls.ToolTip> オブジェクトとして定義した場合は、<xref:System.Windows.Controls.ToolTip> オブジェクトのビジュアル プロパティを設定できます。 それ以外の場合は、<xref:System.Windows.Controls.ToolTipService> クラスで同等の添付プロパティを設定する必要があります。  
  
 ツールヒントの内容の位置を指定するために、<xref:System.Windows.Controls.ToolTip> および <xref:System.Windows.Controls.ToolTipService> プロパティを設定する方法の例については、「[ToolTip を配置する](how-to-position-a-tooltip.md)」を参照してください。  
  
<a name="StylingToolTip"></a>
## <a name="styling-a-tooltip"></a>ツールヒントのスタイル設定  
 カスタム <xref:System.Windows.Style> を定義することで、<xref:System.Windows.Controls.ToolTip> のスタイルを設定できます。 次の例では、<xref:System.Windows.Controls.Control.Background%2A>、<xref:System.Windows.Controls.Control.Foreground%2A>、<xref:System.Windows.Controls.Control.FontSize%2A>、<xref:System.Windows.Controls.Control.FontWeight%2A> を設定することによって、<xref:System.Windows.Controls.ToolTip> の配置をオフセットし、その外観を変更する方法を示す、`Simple` という名前の <xref:System.Windows.Style> を定義します。  
  
 [!code-xaml[ToolTipSimple#Style](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipSimple/CSharp/Pane1.xaml#style)]  
  
<a name="UsingtheToolTipServiceTimeIntervalProperties"></a>
## <a name="using-the-time-interval-properties-of-tooltipservice"></a>ToolTipService の時間間隔プロパティの使用  
 <xref:System.Windows.Controls.ToolTipService> クラスでは、ツールヒントの表示時間を設定するために、<xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A>、<xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A>、<xref:System.Windows.Controls.ToolTipService.ShowDuration%2A> プロパティが提供されています。  
  
 <xref:System.Windows.Controls.ToolTipService.InitialShowDelay%2A> プロパティと <xref:System.Windows.Controls.ToolTipService.ShowDuration%2A> プロパティを使用して、<xref:System.Windows.Controls.ToolTip> が表示される前の遅延 (通常は短い時間) を指定します。また、<xref:System.Windows.Controls.ToolTip> を表示し続ける時間も指定できます。 詳細については、[ツールヒントの表示を遅らせる方法](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms747264(v=vs.90))に関するページを参照してください。  
  
 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> プロパティでは、コントロール間でマウス ポインターをすばやく移動するときに、コントロールのツールヒントを初期遅延なしで表示するかどうかを決定します。 <xref:System.Windows.Controls.ToolTipService.BetweenShowDelay%2A> プロパティの詳細については、「[BetweenShowDelay プロパティを使用する](how-to-use-the-betweenshowdelay-property.md)」を参照してください。  
  
 次の例では、ツールヒントのこれらのプロパティを設定する方法を示します。  
  
 [!code-xaml[ToolTipService#ToolTip](~/samples/snippets/csharp/VS_Snippets_Wpf/ToolTipService/CSharp/Pane1.xaml#tooltip)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ToolTipService>
- <xref:System.Windows.Controls.ToolTip>
- <xref:System.Windows.Controls.ToolTipEventArgs>
- <xref:System.Windows.Controls.ToolTipEventHandler>
- [方法トピック](tooltip-how-to-topics.md)
