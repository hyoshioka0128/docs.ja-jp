---
title: 予定表
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], Calendar
- Calendar control [WPF]
ms.assetid: ee844e4a-eefe-48e2-bd0d-1d82cc5e960b
ms.openlocfilehash: e99a716e7ca8f7b2c9ed11543f37e0b8cb7422a6
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460810"
---
# <a name="calendar"></a>予定表
カレンダーを使用すると、ユーザーは、視覚的なカレンダーの表示を使用して日付を選択できます。  
  
 <xref:System.Windows.Controls.Calendar> コントロールは、単独で使用することも、<xref:System.Windows.Controls.DatePicker> コントロールのドロップダウン部分として使用することもできます。 詳細については、「<xref:System.Windows.Controls.DatePicker>」を参照してください。  
  
 次の図は、2 つの <xref:System.Windows.Controls.Calendar> コントロールを示しています。一方は日付が選択され、ブラックアウト日が表示されたもので、もう一方は選択された日付もブラックアウト日もありません。  
  
 ![Calendar コントロール](./media/ndp-calendarcontrols.png "NDP_CalendarControls")  
予定表コントロール  
  
 次の表では、<xref:System.Windows.Controls.Calendar>に通常関連付けられるタスクについて説明します。  
  
|タスク|実装|  
|----------|--------------------|  
|選択できない日付を指定する。|<xref:System.Windows.Controls.Calendar.BlackoutDates%2A> プロパティを使用します。|  
|<xref:System.Windows.Controls.Calendar> に 1 か月、1 年全体、または 10 年を表示する。|<xref:System.Windows.Controls.Calendar.DisplayMode%2A> プロパティを Month、Year、または Decade に設定します。|  
|ユーザーが日付、日付の範囲、または複数の日付の範囲のいずれを選択できるかを指定する。|<xref:System.Windows.Controls.Calendar.SelectionMode%2A> を使用します。|  
|<xref:System.Windows.Controls.Calendar> に表示する日付の範囲を指定する。|<xref:System.Windows.Controls.Calendar.DisplayDateStart%2A> プロパティおよび <xref:System.Windows.Controls.Calendar.DisplayDateEnd%2A> プロパティを使用します。|  
|現在の日付を強調表示するかどうかを指定する。|<xref:System.Windows.Controls.Calendar.IsTodayHighlighted%2A> プロパティを使用します。 既定では、<xref:System.Windows.Controls.Calendar.IsTodayHighlighted%2A> は `true` です。|  
|<xref:System.Windows.Controls.Calendar> のサイズを変更する。|<xref:System.Windows.Controls.Viewbox> を使用するか、または <xref:System.Windows.FrameworkElement.LayoutTransform%2A> プロパティを <xref:System.Windows.Media.ScaleTransform> に設定します。 <xref:System.Windows.Controls.Calendar> の <xref:System.Windows.FrameworkElement.Width%2A> および <xref:System.Windows.FrameworkElement.Height%2A> プロパティを設定する場合、実際のカレンダーのサイズは変更されないことにご注意ください。|  
  
 <xref:System.Windows.Controls.Calendar> コントロールは、マウスまたはキーボードのいずれかを使用する基本的なナビゲーションを提供します。 次の表では、キーボード ナビゲーションの概要を説明します。  
  
|キーの組み合わせ|<xref:System.Windows.Controls.Calendar.DisplayMode%2A>|アクション|  
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|------------|  
|矢印|<xref:System.Windows.Controls.CalendarMode.Month>|<xref:System.Windows.Controls.Calendar.SelectionMode%2A> プロパティが <xref:System.Windows.Controls.CalendarSelectionMode.None> に設定されていない場合、<xref:System.Windows.Controls.Calendar.SelectedDate%2A> を変更します。|  
|矢印|<xref:System.Windows.Controls.CalendarMode.Year>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> プロパティの月を変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されないことにご注意ください。|  
|矢印|<xref:System.Windows.Controls.CalendarMode.Decade>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> の年を変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されないことにご注意ください。|  
|Shift + 矢印|<xref:System.Windows.Controls.CalendarMode.Month>|<xref:System.Windows.Controls.Calendar.SelectionMode%2A> が <xref:System.Windows.Controls.CalendarSelectionMode.SingleDate> または <xref:System.Windows.Controls.CalendarSelectionMode.None> に設定されていない場合、選択された日付の範囲を拡張します。|  
|ホーム|<xref:System.Windows.Controls.CalendarMode.Month>|<xref:System.Windows.Controls.Calendar.SelectedDate%2A> を現在の月の 1 日に変更します。|  
|ホーム|<xref:System.Windows.Controls.CalendarMode.Year>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> の月をその年の 1 月に変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されません。|  
|ホーム|<xref:System.Windows.Controls.CalendarMode.Decade>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> の年を 10 年の最初の年に変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されません。|  
|End|<xref:System.Windows.Controls.CalendarMode.Month>|<xref:System.Windows.Controls.Calendar.SelectedDate%2A> を現在の月の末日に変更します。|  
|End|<xref:System.Windows.Controls.CalendarMode.Year>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> の月をその年の 12 月に変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されません。|  
|End|<xref:System.Windows.Controls.CalendarMode.Decade>|<xref:System.Windows.Controls.Calendar.DisplayDate%2A> の年を 10 年の最後の年に変更します。 <xref:System.Windows.Controls.Calendar.SelectedDate%2A> は変更されません。|  
|Ctrl + ↑|どれでも可|次に大きい <xref:System.Windows.Controls.Calendar.DisplayMode%2A> に切り替えます。 <xref:System.Windows.Controls.Calendar.DisplayMode%2A> が既に <xref:System.Windows.Controls.CalendarMode.Decade> である場合、何も実行されません。|  
|Ctrl +↓|どれでも可|次に小さい <xref:System.Windows.Controls.Calendar.DisplayMode%2A> に切り替えます。 <xref:System.Windows.Controls.Calendar.DisplayMode%2A> が既に <xref:System.Windows.Controls.CalendarMode.Month> である場合、何も実行されません。|  
|Space キーまたは Enter キー|<xref:System.Windows.Controls.CalendarMode.Year> または <xref:System.Windows.Controls.CalendarMode.Decade>|<xref:System.Windows.Controls.Calendar.DisplayMode%2A> を、フォーカスされている項目で表される <xref:System.Windows.Controls.CalendarMode.Month> または <xref:System.Windows.Controls.CalendarMode.Year> に切り替えます。|  
  
## <a name="see-also"></a>関連項目

- [コントロール](index.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
