---
title: カレンダーのスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], Calendar
- templates [WPF], Calendar
- states [WPF], Calendar
- parts [WPF], Calendar
- Calendar [WPF], styles and templates
- ControlTemplate [WPF], Calendar
ms.assetid: f4fcf046-7a8f-41b8-b5a8-534b64e0345c
ms.openlocfilehash: 64cb62a3459a3eeea6aa5e91b433a58a88ab08ea
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283555"
---
# <a name="calendar-styles-and-templates"></a>カレンダーのスタイルとテンプレート
このトピックでは、<xref:System.Windows.Controls.Calendar> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」を参照してください。  
  
## <a name="calendar-parts"></a>Calendar のパーツ  
 次の表は、<xref:System.Windows.Controls.Calendar> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_CalendarItem|<xref:System.Windows.Controls.Primitives.CalendarItem>|<xref:System.Windows.Controls.Calendar> に現在表示されている月または年。|  
|PART_Root|<xref:System.Windows.Controls.Panel>|<xref:System.Windows.Controls.Primitives.CalendarItem> を格納しているパネル。|  
  
## <a name="calendar-states"></a>Calendar の状態  
 次の表は、<xref:System.Windows.Controls.Calendar> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|----------------------|---------------------------|-----------------|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスはありません。|  
  
## <a name="calendaritem-parts"></a>CalendarItem のパーツ  
 次の表は、<xref:System.Windows.Controls.Primitives.CalendarItem> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_Root|<xref:System.Windows.FrameworkElement>|コントロールのルート。|  
|PART_PreviousButton|<xref:System.Windows.Controls.Button>|クリックされたときにカレンダーの前のページを表示するボタン。|  
|PART_NextButton|<xref:System.Windows.Controls.Button>|クリックされたときにカレンダーの次のページを表示するボタン。|  
|PART_HeaderButton|<xref:System.Windows.Controls.Button>|月モード、年モード、10 年モード間の切り替えに使用できるボタン。|  
|PART_MonthView|<xref:System.Windows.Controls.Grid>|月モードの場合にコンテンツをホストします。|  
|PART_YearView|<xref:System.Windows.Controls.Grid>|年または 10 年モードの場合にコンテンツをホストします。|  
|PART_DisabledVisual|<xref:System.Windows.FrameworkElement>|無効状態のオーバーレイ。|  
|DayTitleTemplate|<xref:System.Windows.DataTemplate>|ビジュアル構造を記述する <xref:System.Windows.DataTemplate>。|  
  
## <a name="calendaritem-states"></a>CalendarItem の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.CalendarItem> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|Normal State|CommonStates|既定の状態です。|  
|Disabled State|CommonStates|<xref:System.Windows.UIElement.IsEnabled%2A> が `false`のときのカレンダーの状態。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスはありません。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスはありません。|  
  
## <a name="calendardaybutton-parts"></a>CalendarDayButton のパーツ  
 <xref:System.Windows.Controls.Primitives.CalendarDayButton> コントロールに名前付きパーツはありません。  
  
## <a name="calendardaybutton-states"></a>CalendarDayButton の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.CalendarDayButton> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|無効|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> が無効になっています。|  
|MouseOver|CommonStates|マウス ポインターが <xref:System.Windows.Controls.Primitives.CalendarDayButton> の上に位置付けられています。|  
|押されている|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarDayButton> が押されています。|  
|選択済み|SelectionStates|ボタンが選択されています。|  
|未選択|SelectionStates|ボタンは選択されていません。|  
|CalendarButtonFocused|CalendarButtonFocusStates|ボタンにフォーカスがあります。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|ボタンにフォーカスはありません。|  
|フォーカスされている|FocusStates|ボタンにフォーカスがあります。|  
|フォーカスされていない|FocusStates|ボタンにフォーカスはありません。|  
|アクティブ|ActiveStates|ボタンはアクティブです。|  
|非アクティブ|ActiveStates|ボタンは非アクティブです。|  
|RegularDay|DayStates|ボタンは、<xref:System.DateTime.Today%2A?displayProperty=nameWithType> を表していません。|  
|今日|DayStates|ボタンは、<xref:System.DateTime.Today%2A?displayProperty=nameWithType> を表しています。|  
|NormalDay|BlackoutDayStates|ボタンは、選択できる日を表しています。|  
|BlackoutDay|BlackoutDayStates|ボタンは、選択できない日を表しています。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスはありません。|  
  
## <a name="calendarbutton-parts"></a>CalendarButton のパーツ  
 <xref:System.Windows.Controls.Primitives.CalendarButton> コントロールに名前付きパーツはありません。  
  
## <a name="calendarbutton-states"></a>CalendarButton の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.CalendarButton> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|無効|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> が無効になっています。|  
|MouseOver|CommonStates|マウス ポインターが <xref:System.Windows.Controls.Primitives.CalendarButton> の上に位置付けられています。|  
|押されている|CommonStates|<xref:System.Windows.Controls.Primitives.CalendarButton> が押されています。|  
|選択済み|SelectionStates|ボタンが選択されています。|  
|未選択|SelectionStates|ボタンは選択されていません。|  
|CalendarButtonFocused|CalendarButtonFocusStates|ボタンにフォーカスがあります。|  
|CalendarButtonUnfocused|CalendarButtonFocusStates|ボタンにフォーカスはありません。|  
|フォーカスされている|FocusStates|ボタンにフォーカスがあります。|  
|フォーカスされていない|FocusStates|ボタンにフォーカスはありません。|  
|アクティブ|ActiveStates|ボタンはアクティブです。|  
|非アクティブ|ActiveStates|ボタンは非アクティブです。|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスがあります。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` で、コントロールにフォーカスはありません。|  
  
## <a name="calendar-controltemplate-example"></a>Calendar の ControlTemplate の例  
 次の例は、<xref:System.Windows.Controls.Calendar> コントロールの <xref:System.Windows.Controls.ControlTemplate> とそれに関連付けられる型を定義する方法を示します。  
  
 [!code-xaml[ControlTemplateExamples#Calendar](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/calendar.xaml#calendar)]  
  
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
