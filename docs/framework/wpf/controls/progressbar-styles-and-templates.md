---
title: ProgressBar のスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- parts [WPF], ProgressBar
- ProgressBar [WPF], styles and templates
- styles [WPF], ProgressBar
- ControlTemplate [WPF], ProgressBar
- templates [WPF], ProgressBar
- states [WPF], ProgressBar
ms.assetid: 935aa600-16e6-4947-a905-37a189a583dd
ms.openlocfilehash: 6551701e86dd6abcd42f143f146c7bdadfeabbcf
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283447"
---
# <a name="progressbar-styles-and-templates"></a>ProgressBar のスタイルとテンプレート
このトピックでは、<xref:System.Windows.Controls.ProgressBar> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためにテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」をご覧ください。  
  
## <a name="progressbar-parts"></a>ProgressBar のパーツ  
 次の表は、<xref:System.Windows.Controls.ProgressBar> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_Indicator|<xref:System.Windows.FrameworkElement>|進行状況を示すオブジェクト。|  
|PART_Track|<xref:System.Windows.FrameworkElement>|進行状況インジケーターのパスを定義するオブジェクト。|  
|PART_GlowRect|<xref:System.Windows.FrameworkElement>|進行状況バーを装飾するオブジェクト。|  
  
## <a name="progressbar-states"></a>ProgressBar の状態  
 次の表は、<xref:System.Windows.Controls.ProgressBar> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|----------------------|---------------------------|-----------------|  
|Determinate|CommonStates|<xref:System.Windows.Controls.ProgressBar> で、進行状況を <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> プロパティに基づいて報告します。|  
|Indeterminate|CommonStates|<xref:System.Windows.Controls.ProgressBar> 繰り返しパターンを使用して一般的な進行状況を報告します。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがある `true` です。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがない `true` です。|  
  
## <a name="progressbar-controltemplate-example"></a>ProgressBar の ControlTemplate の例  
 次の例は、<xref:System.Windows.Controls.ProgressBar> コントロールの <xref:System.Windows.Controls.ControlTemplate> を定義する方法を示しています。  
  
 [!code-xaml[ControlTemplateExamples#ProgressBar](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/progressbar.xaml#progressbar)]  
  
 前の例では、次のリソースの 1 つ以上を使用します。  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 完全なサンプルについては、[Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [コントロールのスタイルとテンプレート](control-styles-and-templates.md)
- [コントロールのカスタマイズ](control-customization.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)
