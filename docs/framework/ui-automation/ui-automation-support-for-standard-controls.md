---
title: UI オートメーションによる標準コントロールのサポート
ms.date: 03/30/2017
helpviewer_keywords:
- controls, UI Automation support for
- UI Automation, support for standard controls
ms.assetid: 3770ea8a-2655-4add-9c59-fe0610ad5084
ms.openlocfilehash: 36028d589e98177f6a0e83092edd656860b1a8d4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79179851"
---
# <a name="ui-automation-support-for-standard-controls"></a>UI オートメーションによる標準コントロールのサポート
> [!NOTE]
> このドキュメントは、[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] 名前空間で定義されているマネージド <xref:System.Windows.Automation> クラスを使用する .NET Framework 開発者を対象としています。 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]の最新情報については、「 [Windows Automation API: UI オートメーション](/windows/win32/winauto/entry-uiauto-win32)」をご覧ください。  
  
 このトピックでは、 [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] 、 Win32 、 Windows[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]フォーム の各フレームワーク用に開発されたアプリケーションでの標準コントロールのサポートについて説明します。  
  
<a name="Windows_Presentation_Foundation_Controls"></a>
## <a name="windows-presentation-foundation-controls"></a>Windows Presentation Foundation コントロール  
 ユーザー操作に関する情報やサポートを提供するすべての [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] コントロール要素は、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]を全面的にネイティブ サポートしています。 パネルなどのその他の要素は、 [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]からは認識できません。  
  
<a name="Win32_Controls"></a>
## <a name="win32-controls"></a>Win32 コントロール  
 ほとんどの Win32 コントロールは、[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]クライアント側プロバイダーを通じて公開されます。 このアセンブリは、UI オートメーション クライアント アプリケーションで使用するために、自動的に登録されます。  
  
 完全サポートは、バージョン 6 の*ComCtrl32.dll*のコントロールに対してのみ提供されます。  
  
 次のコントロールがサポートされています。  
  
|クラス名|コントロール型|  
|----------------|------------------|  
|ボタン|ボタン|  
|ボタン|RadioButton|  
|ボタン|グループ|  
|ボタン|CheckBox|  
|ボタン|ハイパーリンク|  
|ボタン|SplitButton|  
|ボタン|CheckBox|  
|ComboBoxEx32|コンボ ボックス|  
|コンボ ボックス|コンボ ボックス|  
|[編集]|ドキュメント|  
|[編集]|[編集]|  
|SysLink|ハイパーリンク|  
|静的|Text|  
|静的|Image|  
|SysIPAddress32|Custom|  
|SysHeader32|Header/HeaderItem|  
|SysListView32|DataGrid|  
|SysListView32|List|  
|ListBox|List|  
|ListBox|ListItem|  
|#32768|メニュー|  
|#32768|MenuItem|  
|msctls_progress32|ProgressBar|  
|RichEdit|ドキュメントです。 注を参照。|  
|RichEdit20A|ドキュメント|  
|RichEdit20W|ドキュメント|  
|RichEdit50W|ドキュメント|  
|ScrollBar|スライダー|  
|msctls_trackbar32|スライダー|  
|msctls_updown32|Spinner|  
|msctls_statusbar32|StatusBar|  
|SysTabControl32|タブ|  
|SysTabControl32|TabItem|  
|ToolbarWindow32|ToolBar|  
|ToolbarWindow32|MenuItem|  
|ToolbarWindow32|ボタン|  
|ToolbarWindow32|CheckBox|  
|ToolbarWindow32|RadioButton|  
|ToolbarWindow32|区切り記号|  
|tooltips_class32|ヒント|  
|#32774|ヒント|  
|ReBarWindow32|ツール バー|  
|SysTreeView32|ツリー|  
|SysTreeView32|TreeItem|  
  
 **注**コントロールは、Windows Vista に同梱されているバージョン (リッチエディット 3.1 以降、および MsftEdit.dll バージョン 4.1 以降) でのみサポートされます。  
  
 次のコントロールはサポートされていません。  
  
|クラス名|コントロール型|  
|----------------|------------------|  
|SysAnimate32|Image|  
|SysPager|Spinner|  
|SysDateTimePick32|Custom|  
|SysMonthCal32|Calendar|  
|MS_WINNOTE|[ツールヒント]|  
|VBBubble|[ツールヒント]|  
|ScrollBar (スタンドアロン コントロールとして使用される場合)|スライダー|  
|SuperGrid|Custom|  
  
<a name="Windows_Forms_Controls"></a>
## <a name="windows-forms-controls"></a>Windows フォーム コントロール  
 Windows フォーム コントロールは、[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]クライアント側プロバイダーを通じて公開されます。 このアセンブリは、UI オートメーション クライアント アプリケーションで使用するために、自動的に登録されます。  
  
 通常、Win32 コモン コントロールのマネージ ラッパーである Windows フォーム[!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]コントロールは、 でサポートされます。 次のコントロールがサポートされています。  
  
|Class Name (クラス名)|  
|----------------|  
|ボタン|  
|CheckBox|  
|CheckedListBox|  
|ColorDialog|  
|コンボ ボックス|  
|FolderBrowser|  
|FontDialog|  
|GroupBox|  
|HscrollBar|  
|ImageList|  
|Label|  
|ListBox|  
|ListView|  
|MainMenu/ContextMenu|  
|MonthCalendar|  
|NotifyIcon|  
|OpenFileDialog|  
|PageSetupDialog|  
|PrintDialog|  
|ProgressBar|  
|RadioButton|  
|RichTextBox|  
|SaveFileDialog|  
|ScrollableControl|  
|SoundPlayer|  
|StatusBar|  
|TabControl/TabPage|  
|TextBox|  
|Timer|  
|ツール バー|  
|ヒント|  
|TrackBar|  
|TreeView|  
|VscrollBar|  
|Web ブラウザー|  
  
 次のコントロールは、Microsoft[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)]のアクティブ なユーザー補助機能のサポートを通じてのみ公開されます。 一部の機能が使用できないことがあります。  
  
|コントロール名|  
|------------------|  
|BindingSource|  
|DataGrid|  
|DataGridView|  
|DataNavigator|  
|DomainUpDown|  
|ErrorProvider|  
|FlowLayoutPanel|  
|Form|  
|LinkLabel|  
|HelpProvider|  
|MaskedTextBox|  
|MenuStrip/ContextMenuStrip|  
|NumericUpDown|  
|パネル|  
|PictureBox|  
|PrintDocument|  
|PrintPreview-Control|  
|PrintPreview-Dialog|  
|PropertyGrid|  
|UserControl|  
|ToolStrip|  
|TableLayoutPanel|  
|SplitContainer/SplitterPanel|  
|スプリッター|  
|RaftingContainer|  
|StatusStrip|  
  
## <a name="see-also"></a>関連項目

- [UI オートメーション コントロール型](ui-automation-control-types.md)
