---
title: DataGrid
ms.date: 03/30/2017
helpviewer_keywords:
- DataGrid column types [WPF]
- DataGrid scenarios [WPF]
- DataGrid control [WPF]
- controls [WPF], DataGrid
- DataGrid [WPF], common tasks for
- DataGrid [WPF], customizing the appearance of
- DataGrid columns [WPF], using
ms.assetid: bf89ea63-79b6-422b-bc9f-0485ad803216
ms.openlocfilehash: cdf4bfff8182b62d55f56b823c7ff129de4f9f1c
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646116"
---
# <a name="datagrid"></a>DataGrid
<xref:System.Windows.Controls.DataGrid> コントロールを使用すると、SQL データベース、LINQ クエリ、その他のバインド可能なデータ ソースなど、さまざまなソースのデータを表示および編集できます。 詳しくは、「[バインディング ソースの概要](../data/binding-sources-overview.md)」をご覧ください。  
  
 列には、テキスト、<xref:System.Windows.Controls.ComboBox> などのコントロール、または画像、ボタン、テンプレートに含まれる任意のコンテンツなどの他の WPF コンテンツを表示できます。 <xref:System.Windows.Controls.DataGridTemplateColumn> を使用すると、テンプレートで定義されているデータを表示できます。 次の表では、既定で提供される列の型の一覧を示します。  
  
|生成される列の型|データの種類|  
|---------------------------|---------------|  
|<xref:System.Windows.Controls.DataGridTextColumn>|<xref:System.String>|  
|<xref:System.Windows.Controls.DataGridCheckBoxColumn>|<xref:System.Boolean>|  
|<xref:System.Windows.Controls.DataGridComboBoxColumn>|<xref:System.Enum>|  
|<xref:System.Windows.Controls.DataGridHyperlinkColumn>|<xref:System.Uri>|  
  
 <xref:System.Windows.Controls.DataGrid> では、セルのフォント、色、サイズなどの外観をカスタマイズできます。 <xref:System.Windows.Controls.DataGrid> では、他の WPF コントロールのすべてのスタイル設定およびテンプレート機能がサポートされています。 また、<xref:System.Windows.Controls.DataGrid> には、編集、並べ替え、検証のための既定の動作とカスタマイズ可能な動作も含まれています。  
  
 次の表では、<xref:System.Windows.Controls.DataGrid> の一般的なタスクとその実行方法を示します。 関連する API を表示することによって、詳細情報とサンプル コードを参照できます。  
  
|シナリオ|方法|  
|--------------|--------------|  
|背景色の切り替え|<xref:System.Windows.Controls.ItemsControl.AlternationIndex%2A> プロパティを 2 以上に設定した後、<xref:System.Windows.Media.Brush> を <xref:System.Windows.Controls.DataGrid.RowBackground%2A> および <xref:System.Windows.Controls.DataGrid.AlternatingRowBackground%2A> プロパティに割り当てます。|  
|セルと行の選択動作を定義する|<xref:System.Windows.Controls.DataGrid.SelectionMode%2A> プロパティと <xref:System.Windows.Controls.DataGrid.SelectionUnit%2A> プロパティを設定します。|  
|ヘッダー、セル、行の外観をカスタマイズする|<xref:System.Windows.Controls.DataGrid.ColumnHeaderStyle%2A>、<xref:System.Windows.Controls.DataGrid.RowHeaderStyle%2A>、<xref:System.Windows.Controls.DataGrid.CellStyle%2A>、または <xref:System.Windows.Controls.DataGrid.RowStyle%2A> の各プロパティに新しい <xref:System.Windows.Style> を適用します。|  
|サイズ変更オプションを設定する|<xref:System.Windows.FrameworkElement.Height%2A>、<xref:System.Windows.FrameworkElement.MaxHeight%2A>、<xref:System.Windows.FrameworkElement.MinHeight%2A>、<xref:System.Windows.FrameworkElement.Width%2A>、<xref:System.Windows.FrameworkElement.MaxWidth%2A>、<xref:System.Windows.FrameworkElement.MinWidth%2A> の各プロパティを設定します。 詳細については、「[DataGrid コントロールのサイズ変更方法](sizing-options-in-the-datagrid-control.md)」を参照してください。|  
|選択された項目にアクセスする|選択されたセルを取得するには <xref:System.Windows.Controls.DataGrid.SelectedCells%2A> プロパティを、選択された行を取得するには <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems%2A> プロパティを調べます。 詳細については、「<xref:System.Windows.Controls.DataGrid.SelectedCells%2A>」を参照してください。|  
|エンド ユーザーの操作をカスタマイズする|<xref:System.Windows.Controls.DataGrid.CanUserAddRows%2A>、<xref:System.Windows.Controls.DataGrid.CanUserDeleteRows%2A>、<xref:System.Windows.Controls.DataGrid.CanUserReorderColumns%2A>、<xref:System.Windows.Controls.DataGrid.CanUserResizeColumns%2A>、<xref:System.Windows.Controls.DataGrid.CanUserResizeRows%2A>、<xref:System.Windows.Controls.DataGrid.CanUserSortColumns%2A> の各プロパティを設定します。|  
|自動生成された列をキャンセルまたは変更する|<xref:System.Windows.Controls.DataGrid.AutoGeneratingColumn> イベントを処理します。|  
|列を固定する|<xref:System.Windows.Controls.DataGrid.FrozenColumnCount%2A> プロパティを 1 に設定し、<xref:System.Windows.Controls.DataGridColumn.DisplayIndex%2A> プロパティを 0 に設定することで、列を左端の位置に移動します。|  
|データ ソースとして XML データを使用する|<xref:System.Windows.Controls.DataGrid> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> を、項目のコレクションを表す XPath クエリにバインドします。 <xref:System.Windows.Controls.DataGrid> に各列を作成します。 バインドの XPath を、項目ソースのプロパティを取得するクエリに設定することで、各列をバインドします。 例については、「<xref:System.Windows.Controls.DataGridTextColumn>」を参照してください。|  
  
## <a name="related-topics"></a>関連トピック  
  
|Title|説明|  
|-----------|-----------------|  
|[チュートリアル: DataGrid コントロールで SQL Server データベースのデータを表示する](walkthrough-display-data-from-a-sql-server-database-in-a-datagrid-control.md)|新しい WPF プロジェクトを設定する方法、Entity Framework 要素を追加する方法、ソースを設定する方法、およびデータを <xref:System.Windows.Controls.DataGrid> に表示する方法について説明します。|  
|[方法: DataGrid コントロールに行の詳細を追加する](how-to-add-row-details-to-a-datagrid-control.md)|<xref:System.Windows.Controls.DataGrid> の行の詳細を作成する方法について説明します。|  
|[方法: DataGrid コントロールを使用して検証を実装する](how-to-implement-validation-with-the-datagrid-control.md)|<xref:System.Windows.Controls.DataGrid> のセルと行で値を検証し、検証のフィードバックを表示する方法について説明します。|  
|[DataGrid コントロールの既定のキーボード動作とマウス動作](default-keyboard-and-mouse-behavior-in-the-datagrid-control.md)|キーボードとマウスを使用して <xref:System.Windows.Controls.DataGrid> コントロールを操作する方法について説明します。|  
|[方法: DataGrid コントロールでデータをグループ化、並べ替え、およびフィルター処理する](how-to-group-sort-and-filter-data-in-the-datagrid-control.md)|データをグループ化、並べ替え、フィルター処理し、さまざまな方法で <xref:System.Windows.Controls.DataGrid> にデータを表示する方法を説明します。|  
|[DataGrid コントロールのサイズ変更方法](sizing-options-in-the-datagrid-control.md)|<xref:System.Windows.Controls.DataGrid> での絶対サイズ設定と自動サイズ設定を制御する方法について説明します。|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataGrid>
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [データ テンプレートの概要](../data/data-templating-overview.md)
- [コントロール](index.md)
- [WPF のコンテンツ モデル](wpf-content-model.md)
