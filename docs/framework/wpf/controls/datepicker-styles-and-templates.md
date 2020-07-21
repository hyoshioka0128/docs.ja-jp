---
title: DatePicker のスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- ControlTemplate [WPF], DatePicker
- DatePicker [WPF], styles and templates
- templates [WPF], DatePicker
- parts [WPF], DatePicker
- styles [WPF], DatePicker
- states [WPF], DatePicker
ms.assetid: c430a657-692f-44bd-a549-2341f92d6115
ms.openlocfilehash: 002d1c3271827239dcd3a319621f66fb5bc68d4e
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283772"
---
# <a name="datepicker-styles-and-templates"></a>DatePicker のスタイルとテンプレート
このトピックでは、<xref:System.Windows.Controls.DatePicker> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためにテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」をご覧ください。  
  
## <a name="datepicker-parts"></a>DatePicker のパーツ  
 次の表は、<xref:System.Windows.Controls.DatePicker> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_Root|<xref:System.Windows.Controls.Grid>|コントロールのルート。|  
|PART_Button|<xref:System.Windows.Controls.Button>|<xref:System.Windows.Controls.Calendar> を開いて閉じるボタン。|  
|PART_TextBox|<xref:System.Windows.Controls.Primitives.DatePickerTextBox>|日付を入力できるテキスト ボックス。|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|<xref:System.Windows.Controls.DatePicker> コントロールのポップアップ。|  
  
## <a name="datepicker-states"></a>DatePicker の状態  
 次の表は、<xref:System.Windows.Controls.DatePicker> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|無効|CommonStates|<xref:System.Windows.Controls.DatePicker> が無効になっています。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがある `true` です。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがない `true` です。|  
  
## <a name="datepickertextbox-parts"></a>DatePickerTextBox のパーツ  
 次の表は、<xref:System.Windows.Controls.Primitives.DatePickerTextBox> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_Watermark|<xref:System.Windows.Controls.ContentControl>|<xref:System.Windows.Controls.DatePicker> の最初のテキストを含める要素。|  
|PART_ContentElement|<xref:System.Windows.FrameworkElement>|<xref:System.Windows.FrameworkElement> を含めることができるビジュアル要素。 <xref:System.Windows.Controls.TextBox> のテキストがこの要素に表示されます。|  
  
## <a name="datepickertextbox-states"></a>DatePickerTextBox の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.DatePickerTextBox> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|無効|CommonStates|<xref:System.Windows.Controls.Primitives.DatePickerTextBox> が無効になっています。|  
|MouseOver|CommonStates|マウス ポインターが <xref:System.Windows.Controls.Primitives.DatePickerTextBox> の上に位置付けられています。|  
|ReadOnly|CommonStates|ユーザーは、<xref:System.Windows.Controls.Primitives.DatePickerTextBox> のテキストを変更することはできません。|  
|フォーカスされている|FocusStates|コントロールにフォーカスがあります。|  
|フォーカスされていない|FocusStates|コントロールにフォーカスがありません。|  
|Watermarked|WatermarkStates|コントロールには、最初のテキストが表示されています。  <xref:System.Windows.Controls.Primitives.DatePickerTextBox> は、ユーザーがテキストを入力していないか、日付を選択していない状態です。|  
|Unwatermarked|WatermarkStates|ユーザーが <xref:System.Windows.Controls.Primitives.DatePickerTextBox> にテキストを入力したか、<xref:System.Windows.Controls.DatePicker> で日付を選択しました。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがありません。|  
  
## <a name="datepicker-controltemplate-example"></a>DatePicker の ControlTemplate の例  
 次の例は、<xref:System.Windows.Controls.DatePicker> コントロールの <xref:System.Windows.Controls.ControlTemplate> を定義する方法を示しています。  
  
 [!code-xaml[ControlTemplateExamples#DatePicker](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datepicker.xaml#datepicker)]  
  
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
