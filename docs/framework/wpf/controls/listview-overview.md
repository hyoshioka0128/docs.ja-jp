---
title: ListView の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], ListView
- ListView controls [WPF], about ListView control
ms.assetid: 989e12b0-260e-4570-95c6-489284003ce2
ms.openlocfilehash: 2f336d1eb8dcdfec3c3c8059ba865147c6b6c825
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187513"
---
# <a name="listview-overview"></a>ListView の概要
<xref:System.Windows.Controls.ListView> コントロールには、さまざまなレイアウトまたはビューにデータ項目のセットを表示するためのインフラストラクチャが用意されています。 たとえば、ユーザーは、テーブルにデータ項目を表示し、その列を並べ替えできます。  

<a name="WhatisaListView"></a>
## <a name="what-is-a-listview"></a>ListView とは  
 <xref:System.Windows.Controls.ListView> コントロールは、<xref:System.Windows.Controls.ListBox> から派生された <xref:System.Windows.Controls.ItemsControl> です。 通常、その項目はデータ コレクションのメンバーであり、<xref:System.Windows.Controls.ListViewItem> オブジェクトとして表されます。 <xref:System.Windows.Controls.ListViewItem> は <xref:System.Windows.Controls.ContentControl> であり、子要素を 1 つだけ含むことができます。 ただし、その子要素は、任意のビジュアル要素にできます。  
  
<a name="DefiningaListViewView"></a>
## <a name="defining-a-view-mode-for-a-listview"></a>ListView の表示モードの定義  
 <xref:System.Windows.Controls.ListView> コントロールの内容の表示モードを指定するには、<xref:System.Windows.Controls.ListView.View%2A> プロパティを設定します。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で提供されている 1 つの表示モードは <xref:System.Windows.Controls.GridView> で、これはカスタマイズ可能な列を持つテーブルにデータ項目のコレクションが表示されます。  
  
 次の例では、従業員情報を表示する <xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.GridView> を定義する方法を示します。  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 次の図は、前の例でのデータの表示方法を示しています。  
  
 ![GridView の出力が表示された ListView のスクリーンショット。](./media/gridview-overview/listview-gridview-output.jpg)  
  
 <xref:System.Windows.Controls.ViewBase> クラスを継承するクラスを定義することによって、カスタム表示モードを作成できます。 <xref:System.Windows.Controls.ViewBase> クラスには、カスタム ビューを作成するために必要なインフラストラクチャが用意されています。 カスタム ビューを作成する方法の詳細については、[ Create a Custom View Mode for a ListView ](how-to-create-a-custom-view-mode-for-a-listview.md)を参照してください。  
  
<a name="BindingDatatoaListView"></a>
## <a name="binding-data-to-a-listview"></a>ListView へのデータ バインディング  
 <xref:System.Windows.Controls.ListView> コントロールの項目を指定するには、<xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティと <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティを使用します。 次の例では、<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティに `EmployeeInfoDataSource` という名前のデータ コレクションを設定します。  
  
 [!code-xaml[ListViewCode#ItemsSource](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#itemssource)]  
  
 <xref:System.Windows.Controls.GridView> では、指定したデータ フィールドに <xref:System.Windows.Controls.GridViewColumn> オブジェクトがバインドされます。 次の例では、<xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> プロパティに対して <xref:System.Windows.Data.Binding> を指定することにより、<xref:System.Windows.Controls.GridViewColumn> オブジェクトをデータ フィールドにバインドします。  
  
 [!code-csharp[ListViewCode#GridViewColumnProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml.cs#gridviewcolumnproperties)]
 [!code-vb[ListViewCode#GridViewColumnProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewCode/visualbasic/window1.xaml.vb#gridviewcolumnproperties)]
 [!code-xaml[ListViewCode#GridViewColumnProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#gridviewcolumnproperties)]  
  
 列のセルのスタイルを指定するために使用する <xref:System.Windows.DataTemplate> の定義の一部として、<xref:System.Windows.Data.Binding> を指定することもできます。 次の例では、<xref:System.Windows.ResourceKey> によって示される <xref:System.Windows.DataTemplate> で、<xref:System.Windows.Controls.GridViewColumn> に対して <xref:System.Windows.Data.Binding> を設定します。 この例では <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> が定義されていないことに注意してください。定義すると、<xref:System.Windows.DataTemplate> によって指定されているバインディングがオーバーライドされるためです。  
  
 [!code-xaml[ListViewTemplate#GridViewCellTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 [!code-xaml[ListViewTemplate#CellTemplateProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
<a name="StylingaListView"></a>
## <a name="styling-a-listview-that-implements-a-gridview"></a>GridView を実装する ListView のスタイル設定  
 <xref:System.Windows.Controls.ListView> コントロールに含まれる <xref:System.Windows.Controls.ListViewItem> オブジェクトは、表示されるデータ項目を表します。 次のプロパティを使用して、データ項目の内容とスタイルを定義できます。  
  
- <xref:System.Windows.Controls.ListView> コントロールでは、<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>、<xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A>、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> の各プロパティを使用します。  
  
- <xref:System.Windows.Controls.ListViewItem> コントロールでは、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> プロパティと <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A> プロパティを使用します。  
  
 <xref:System.Windows.Controls.GridView> のセル間でのアライメントの問題を回避するために、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> を使用してプロパティを設定したり、<xref:System.Windows.Controls.ListView> の項目の幅に影響するコンテンツを追加したりしないでください。 たとえば、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> で <xref:System.Windows.FrameworkElement.Margin%2A> プロパティを設定すると、アライメントの問題が発生する可能性があります。 <xref:System.Windows.Controls.GridView> の項目の幅に影響するプロパティを指定したり、コンテンツを定義したりするには、<xref:System.Windows.Controls.GridView> クラスおよびそれに関連する <xref:System.Windows.Controls.GridViewColumn> などのクラスのプロパティを使用します。  
  
 <xref:System.Windows.Controls.GridView> およびそのサポート クラスを使用する方法の詳細については、「[GridView の概要](gridview-overview.md)」を参照してください。  
  
 <xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> を定義し、さらに <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> も定義する場合は、<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> が正常に動作するように、スタイルに <xref:System.Windows.Controls.ContentPresenter> を含める必要があります。  
  
 <xref:System.Windows.Controls.GridView> を使用して表示される <xref:System.Windows.Controls.ListView> コンテンツには、<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> プロパティと <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> プロパティを使用しないでください。 <xref:System.Windows.Controls.GridView> の列のコンテンツの配置を指定するには、<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> を定義します。  
  
<a name="UsingtheSameViewMoreThanOnce"></a>
## <a name="sharing-the-same-view-mode"></a>同じ表示モードの共有  
 2 つの <xref:System.Windows.Controls.ListView> コントロールで、同時に同じ表示モードを共有することはできません。 複数の <xref:System.Windows.Controls.ListView> コントロールで同じ表示モードを使用しようとすると、例外が発生します。  
  
 複数の <xref:System.Windows.Controls.ListView> で同時に使用できる表示モードを指定するには、テンプレートまたはスタイルを使用します。
  
<a name="CreatingaCustomView"></a>
## <a name="creating-a-custom-view-mode"></a>カスタム表示モードの作成  
 <xref:System.Windows.Controls.GridView> のようにカスタマイズされた表示は、<xref:System.Windows.Controls.ViewBase> 抽象クラスから派生されます。これには、<xref:System.Windows.Controls.ListViewItem> オブジェクトとして表されるデータ項目を表示するためのツールが用意されています。
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GridView>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.ListViewItem>
- <xref:System.Windows.Data.Binding>
- [GridView の概要](gridview-overview.md)
- [方法トピック](listview-how-to-topics.md)
- [コントロール](../advanced/optimizing-performance-controls.md)
