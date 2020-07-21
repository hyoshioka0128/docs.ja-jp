---
title: RepeatButton のスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- RepeatButton [WPF], styles and templates
- styles [WPF], RepeatButton
- templates [WPF], RepeatButton
- parts [WPF], RepeatButton
- ControlTemplate [WPF], RepeatButton
- states [WPF], RepeatButton
ms.assetid: fd340743-f44f-4990-9077-085301469670
ms.openlocfilehash: 8585e98536fd908daa11f21da395cab44924d612
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283426"
---
# <a name="repeatbutton-styles-and-templates"></a>RepeatButton のスタイルとテンプレート

このトピックでは、<xref:System.Windows.Controls.Primitives.RepeatButton> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためにテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」をご覧ください。

## <a name="repeatbutton-parts"></a>RepeatButton のパーツ

<xref:System.Windows.Controls.Primitives.RepeatButton> コントロールに名前付きパーツはありません。

## <a name="repeatbutton-states"></a>RepeatButton の状態

次の表は、<xref:System.Windows.Controls.Primitives.RepeatButton> コントロールの表示状態の一覧を示します。

|VisualState 名|VisualStateGroup 名|説明|
|-|-|-|
|標準|CommonStates|既定の状態です。|
|MouseOver|CommonStates|マウス ポインターがコントロール上に配置されています。|
|押されている|CommonStates|コントロールが押されています。|
|無効|CommonStates|コントロールが無効になっています。|
|フォーカスされている|FocusStates|コントロールにフォーカスがあります。|
|フォーカスされていない|FocusStates|コントロールにフォーカスがありません。|
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがある `true` です。|
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがない `true` です。|

## <a name="repeatbutton-controltemplate-example"></a>RepeatButton の ControlTemplate の例

次の例は、<xref:System.Windows.Controls.Primitives.RepeatButton> コントロールの <xref:System.Windows.Controls.ControlTemplate> を定義する方法を示しています。

[!code-xaml[ControlTemplateExamples#RepeatButton](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/scrollbar.xaml#repeatbutton)]

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
