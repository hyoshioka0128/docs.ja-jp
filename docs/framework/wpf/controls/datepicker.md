---
title: DatePicker
ms.date: 03/30/2017
helpviewer_keywords:
- controls [WPF], DatePicker
- DatePicker control [WPF]
ms.assetid: 619765c8-8d25-4315-aec2-79aea08fed9f
ms.openlocfilehash: 3e66b2306c11c54db14eb05cc6860257635cc653
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460356"
---
# <a name="datepicker"></a>DatePicker
<xref:System.Windows.Controls.DatePicker> コントロールを使用すると、ユーザーは、テキスト フィールドに入力するか、ドロップダウン <xref:System.Windows.Controls.Calendar> コントロールを使用して、日付を選択できます。  
  
 次の図は、<xref:System.Windows.Controls.DatePicker> を示しています。  
  
 ![DatePicker コントロール](./media/ndp-datepicker.png "NDP_DatePicker")  
DatePicker コントロール  
  
 <xref:System.Windows.Controls.DatePicker> コントロールのプロパティの多くは、その組み込みの <xref:System.Windows.Controls.Calendar> を管理するためのものであり、<xref:System.Windows.Controls.Calendar> の同等のプロパティと同じように機能します。 特に、<xref:System.Windows.Controls.DatePicker.IsTodayHighlighted%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.FirstDayOfWeek%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.BlackoutDates%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.DisplayDateStart%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.DisplayDateEnd%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.DisplayDate%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.DatePicker.SelectedDate%2A?displayProperty=nameWithType> の各プロパティは、対応する <xref:System.Windows.Controls.Calendar> の各プロパティと同じように機能します。 詳細については、「<xref:System.Windows.Controls.Calendar>」を参照してください。  
  
 ユーザーは、テキスト フィールドに日付を直接入力できます。これにより、<xref:System.Windows.Controls.DatePicker.Text%2A> プロパティが設定されます。 <xref:System.Windows.Controls.DatePicker> が、入力した文字列を有効な日付に変換できない場合は、<xref:System.Windows.Controls.DatePicker.DateValidationError> イベントが発生します。 既定では、これが例外の原因となりますが、<xref:System.Windows.Controls.DatePicker.DateValidationError> のイベント ハンドラーにより <xref:System.Windows.Controls.DatePickerDateValidationErrorEventArgs.ThrowException%2A> プロパティが `false` に設定されることで、例外の発生を回避することができます。  
  
## <a name="see-also"></a>関連項目

- [コントロール](index.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
