---
title: DataGrid のスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- states [WPF], DataGrid
- ControlTemplate [WPF], DataGrid
- DataGrid [WPF], styles and templates
- templates [WPF], DataGrid
- styles [WPF], DataGrid
- parts [WPF], DataGrid
ms.assetid: 9cb31d63-f148-4d25-b079-816e73f988c7
ms.openlocfilehash: 066e8c9ce1112399be8128d0821498f0d56a3dc3
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283804"
---
# <a name="datagrid-styles-and-templates"></a>DataGrid のスタイルとテンプレート
このトピックでは、<xref:System.Windows.Controls.DataGrid> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」を参照してください。  
  
## <a name="datagrid-parts"></a>DataGrid のパーツ  
 次の表は、<xref:System.Windows.Controls.DataGrid> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_ColumnHeadersPresenter|<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter>|列ヘッダーを含む行。|  
  
 <xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.Controls.ControlTemplate> を作成する場合、テンプレートで、<xref:System.Windows.Controls.ScrollViewer> 内に <xref:System.Windows.Controls.ItemsPresenter> が含まれる可能性があります (<xref:System.Windows.Controls.ItemsPresenter> は、<xref:System.Windows.Controls.DataGrid> 内の各項目を表示します。<xref:System.Windows.Controls.ScrollViewer> は、コントロール内でのスクロールを有効にします)。  <xref:System.Windows.Controls.ItemsPresenter> が <xref:System.Windows.Controls.ScrollViewer> の直接的な子ではない場合、<xref:System.Windows.Controls.ItemsPresenter> に名前 `ItemsPresenter` を指定する必要があります。  
  
 <xref:System.Windows.Controls.DataGrid> の既定のテンプレートには、<xref:System.Windows.Controls.ScrollViewer> コントロールが含まれます。 <xref:System.Windows.Controls.ScrollViewer> で定義されるパーツの詳細については、「[ScrollViewer のスタイルとテンプレート](scrollviewer-styles-and-templates.md)」を参照してください。  
  
## <a name="datagrid-states"></a>DataGrid の状態  
 次の表は、<xref:System.Windows.Controls.DataGrid> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|無効|CommonStates|コントロールが無効になっています。|  
|InvalidFocused|ValidationStates|コントロールが無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|コントロールが無効で、フォーカスがありません。|  
|有効|ValidationStates|コントロールは有効です。|  
  
## <a name="datagridcell-parts"></a>DataGridCell のパーツ  
 <xref:System.Windows.Controls.DataGridCell> 要素に名前付きパーツはありません。  
  
## <a name="datagridcell-states"></a>DataGridCell の状態  
 次の表は、<xref:System.Windows.Controls.DataGridCell> 要素の表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|MouseOver|CommonStates|マウス ポインターはセル上に配置されています。|  
|フォーカスされている|FocusStates|セルにフォーカスがあります。|  
|フォーカスされていない|FocusStates|セルにフォーカスはありません。|  
|[現在]|CurrentStates|セルは現在のセルです。|  
|Regular|CurrentStates|セルは現在のセルではありません。|  
|表示|InteractionStates|セルは表示モードです。|  
|編集|InteractionStates|セルは編集モードです。|  
|選択済み|SelectionStates|セルは選択されています。|  
|未選択|SelectionStates|セルは選択されていません。|  
|InvalidFocused|ValidationStates|セルは無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|セルは無効で、フォーカスがありません。|  
|有効|ValidationStates|セルは有効です。|  
  
## <a name="datagridrow-parts"></a>DataGridRow のパーツ  
 <xref:System.Windows.Controls.DataGridRow> 要素に名前付きパーツはありません。  
  
## <a name="datagridrow-states"></a>DataGridRow の状態  
 次の表は、<xref:System.Windows.Controls.DataGridRow> 要素の表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|MouseOver|CommonStates|マウス ポインターは行上に配置されています。|  
|MouseOver_Editing|CommonStates|マウス ポインターは行上に配置されており、行は編集モードです。|  
|MouseOver_Selected|CommonStates|マウス ポインターは行上に配置されており、行は選択されています。|  
|MouseOver_Unfocused_Editing|CommonStates|マウス ポインターは行上に配置されており、行は編集モードで、フォーカスはありません。|  
|MouseOver_Unfocused_Selected|CommonStates|マウス ポインターは行上に配置されており、行は選択されていて、フォーカスはありません。|  
|Normal_AlternatingRow|CommonStates|行は交互の行です。|  
|Normal_Editing|CommonStates|行は編集モードです。|  
|Normal_Selected|CommonStates|行は選択されています。|  
|Unfocused_Editing|CommonStates|行は編集モードで、フォーカスはありません。|  
|Unfocused_Selected|CommonStates|行は選択されており、フォーカスはありません。|  
|InvalidFocused|ValidationStates|コントロールが無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|コントロールが無効で、フォーカスがありません。|  
|有効|ValidationStates|コントロールは有効です。|  
  
## <a name="datagridrowheader-parts"></a>DataGridRowHeader のパーツ  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridRowHeader> 要素の名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_TopHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|行ヘッダーの上からの高さを変更するために使用される要素。|  
|PART_BottomHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|行ヘッダーの下からの高さを変更するために使用される要素。|  
  
## <a name="datagridrowheader-states"></a>DataGridRowHeader の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridRowHeader> 要素の表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|MouseOver|CommonStates|マウス ポインターは行上に配置されています。|  
|MouseOver_CurrentRow|CommonStates|マウス ポインターは行上に配置されており、行は現在の行です。|  
|MouseOver_CurrentRow_Selected|CommonStates|マウス ポインターは行上に配置されており、行は現在の行で選択されています。|  
|MouseOver_EditingRow|CommonStates|マウス ポインターは行上に配置されており、行は編集モードです。|  
|MouseOver_Selected|CommonStates|マウス ポインターは行上に配置されており、行は選択されています。|  
|MouseOver_Unfocused_CurrentRow_Selected|CommonStates|マウス ポインターは行上に配置されており、行は現在の行で選択されており、フォーカスはありません。|  
|MouseOver_Unfocused_EditingRow|CommonStates|マウス ポインターは行上に配置されており、行は編集モードで、フォーカスはありません。|  
|MouseOver_Unfocused_Selected|CommonStates|マウス ポインターは行上に配置されており、行は選択されていて、フォーカスはありません。|  
|Normal_CurrentRow|CommonStates|行は現在の行です。|  
|Normal_CurrentRow_Selected|CommonStates|行は現在の行で、選択されています。|  
|Normal_EditingRow|CommonStates|行は編集モードです。|  
|Normal_Selected|CommonStates|行は選択されています。|  
|Unfocused_CurrentRow_Selected|CommonStates|行は現在の行で、選択されており、フォーカスはありません。|  
|Unfocused_EditingRow|CommonStates|行は編集モードで、フォーカスはありません。|  
|Unfocused_Selected|CommonStates|行は選択されており、フォーカスはありません。|  
|InvalidFocused|ValidationStates|コントロールが無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|コントロールが無効で、フォーカスがありません。|  
|有効|ValidationStates|コントロールは有効です。|  
  
## <a name="datagridcolumnheaderspresenter-parts"></a>DataGridColumnHeadersPresenter のパーツ  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 要素の名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_FillerColumnHeader|<xref:System.Windows.Controls.Primitives.DataGridColumnHeader>|列ヘッダーのプレースホルダー。|  
  
## <a name="datagridcolumnheaderspresenter-states"></a>DataGridColumnHeadersPresenter の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridColumnHeadersPresenter> 要素の表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|InvalidFocused|ValidationStates|セルは無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|セルは無効で、フォーカスがありません。|  
|有効|ValidationStates|セルは有効です。|  
  
## <a name="datagridcolumnheader-parts"></a>DataGridColumnHeader のパーツ  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 要素の名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_LeftHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|列ヘッダーの左からの幅を変更するために使用される要素。|  
|PART_RightHeaderGripper|<xref:System.Windows.Controls.Primitives.Thumb>|列ヘッダーの右からの幅を変更するために使用される要素。|  
  
## <a name="datagridcolumnheader-states"></a>DataGridColumnHeader の状態  
 次の表は、<xref:System.Windows.Controls.Primitives.DataGridColumnHeader> 要素の表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|標準|CommonStates|既定の状態です。|  
|MouseOver|CommonStates|マウス ポインターがコントロール上に配置されています。|  
|押されている|CommonStates|コントロールが押されています。|  
|SortAscending|SortStates|列は昇順で並べ替えられています。|  
|SortDescending|SortStates|列は降順で並べ替えられています。|  
|並べ替えなし|SortStates|列は並べ替えられていません。|  
|InvalidFocused|ValidationStates|コントロールが無効で、フォーカスがあります。|  
|InvalidUnfocused|ValidationStates|コントロールが無効で、フォーカスがありません。|  
|有効|ValidationStates|コントロールは有効です。|  
  
## <a name="datagrid-controltemplate-example"></a>DataGrid ControlTemplate の例  
 次の例は、<xref:System.Windows.Controls.DataGrid> コントロールの <xref:System.Windows.Controls.ControlTemplate> とそれに関連付けられる型を定義する方法を示します。  
  
 [!code-xaml[ControlTemplateExamples#DataGrid](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/datagrid.xaml#datagrid)]  
  
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
