---
title: '方法: DataGrid コントロールに行の詳細を追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- DataTemplate [WPF], DataGrid
- row details [WPF], DataGrid
- DataGrid [WPF], row details
ms.assetid: 0bdc6f50-9b4c-483f-9df6-a47a1fde998b
ms.openlocfilehash: 4db414e1907d42071f7251c390077d4020fa577c
ms.sourcegitcommit: f8c36054eab877de4d40a705aacafa2552ce70e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75559678"
---
# <a name="how-to-add-row-details-to-a-datagrid-control"></a>方法: DataGrid コントロールに行の詳細を追加する
<xref:System.Windows.Controls.DataGrid> コントロールを使用する場合、行の詳細セクションを追加することで、データの表示をカスタマイズできます。 行の詳細セクションを追加すると、一部のデータをテンプレートにグループ化し、必要に応じて表示するか折りたたむことができます。 たとえば、行の詳細を <xref:System.Windows.Controls.DataGrid> に追加すると、<xref:System.Windows.Controls.DataGrid> の各行にはデータの概要のみが表示されますが、ユーザーが行を選択すると、より多くのデータ フィールドが表示されるようになります。 行の詳細セクションのテンプレートは、<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> プロパティで定義します。 次の図は、行の詳細セクションの例を示しています。  
  
 ![行の詳細が表示された DataGrid](./media/ndp-rowdetails.png "NDP_RowDetails")  
  
 行の詳細テンプレートは、インライン XAML またはリソースとして定義します。 両方の方法について次の手順で示します。 リソースとして追加されたデータ テンプレートは、テンプレートを再作成することなく、プロジェクト全体で使用できます。 インライン XAML として追加されたデータ テンプレートは、それが定義されているコントロールからのみアクセスできます。  
  
### <a name="to-display-row-details-by-using-inline-xaml"></a>インライン XAML を使用して行の詳細を表示するには  
  
1. データ ソースからのデータを表示する <xref:System.Windows.Controls.DataGrid> を作成します。  
  
2. <xref:System.Windows.Controls.DataGrid> 要素に、<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> 要素を追加します。  
  
3. 行の詳細セクションの外観を定義する <xref:System.Windows.DataTemplate> を作成します。  
  
     次の XAML は、<xref:System.Windows.Controls.DataGrid> と <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> をインラインで定義する方法を示しています。 <xref:System.Windows.Controls.DataGrid> を使用すると、各行に 3 つの値が表示され、行を選択するとさらに 3 つの値が表示されます。  
  
     [!code-xaml[DataGrid_RowDetails#1](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml#1)]  
  
     次のコードは、<xref:System.Windows.Controls.DataGrid> に表示されるデータを選択するために使用されるクエリを示しています。 この例では、クエリによって顧客情報を含むエンティティからデータが選択されます。  
  
     [!code-csharp[DataGrid_RowDetails#2](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/mainwindow.xaml.cs#2)]
     [!code-vb[DataGrid_RowDetails#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/datagrid_rowdetails/vb/mainwindow.xaml.vb#2)]  
  
### <a name="to-display-row-details-by-using-a-resource"></a>リソースを使用して行の詳細を表示するには  
  
1. データ ソースからのデータを表示する <xref:System.Windows.Controls.DataGrid> を作成します。  
  
2. <xref:System.Windows.FrameworkElement.Resources%2A> 要素を <xref:System.Windows.Window> コントロールや <xref:System.Windows.Controls.Page> コントロールなどのルート要素に追加するか、<xref:System.Windows.Application.Resources%2A> 要素を App.xaml (または Application.xaml) ファイルの <xref:System.Windows.Application> クラスに追加します。  
  
3. resources 要素に、行の詳細セクションの外観を定義する <xref:System.Windows.DataTemplate> を作成します。  
  
     次の XAML は、<xref:System.Windows.Application> クラスで定義された <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> を示しています。  
  
     [!code-xaml[DataGrid_RowDetails#3](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/app.xaml#3)]  
  
4. <xref:System.Windows.DataTemplate> に対して、[x:Key Directive](../../../desktop-wpf/xaml-services/xkey-directive.md) をデータ テンプレートを一意に識別する値に設定します。  
  
5. <xref:System.Windows.Controls.DataGrid> 要素で、<xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> プロパティを前の手順で定義したリソースに設定します。 リソースを静的リソースとして割り当てます。  
  
     次の XAML は、前の例のリソースに設定された <xref:System.Windows.Controls.DataGrid.RowDetailsTemplate%2A> プロパティを示しています。  
  
     [!code-xaml[DataGrid_RowDetails#4](~/samples/snippets/csharp/VS_Snippets_Wpf/datagrid_rowdetails/cs/window2.xaml#4)]  
  
### <a name="to-set-visibility-and-prevent-horizontal-scrolling-for-row-details"></a>可視性を設定し、行の詳細が水平方向にスクロールしないようにするには  
  
1. 必要に応じて <xref:System.Windows.Controls.DataGrid.RowDetailsVisibilityMode%2A> プロパティを <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode> 値に設定します。  
  
     既定では、この値は <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.VisibleWhenSelected> に設定されます。 すべての行の詳細を表示するには <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Visible> に、すべての行の詳細を非表示にするには <xref:System.Windows.Controls.DataGridRowDetailsVisibilityMode.Collapsed> に設定することができます。  
  
2. 必要に応じて、<xref:System.Windows.Controls.DataGrid.AreRowDetailsFrozen%2A> プロパティを `true` に設定して、行の詳細セクションが水平方向にスクロールしないようにします。
