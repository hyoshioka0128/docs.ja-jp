---
title: '方法: テンプレートを使用して、GridView を使用する ListView のスタイルを設定する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 94bf964b-96c8-4bdf-a0c3-f5271b7cb565
ms.openlocfilehash: 1caa652c4a2a3a7d0a8d40fe703df7a3e8038c9b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699124"
---
# <a name="how-to-use-templates-to-style-a-listview-that-uses-gridview"></a>方法: テンプレートを使用して、GridView を使用する ListView のスタイルを設定する
この例からは、<xref:System.Windows.DataTemplate> オブジェクトと <xref:System.Windows.Style> オブジェクトを使用することで、<xref:System.Windows.Controls.GridView> 表示モードを使用する <xref:System.Windows.Controls.ListView> コントロールの外観を指定する方法がわかります。  
  
## <a name="example"></a>例  
 次の例では、<xref:System.Windows.Controls.GridViewColumn> の列ヘッダーの外観をカスタマイズする <xref:System.Windows.Style> オブジェクトと <xref:System.Windows.DataTemplate> オブジェクトを示します。  
  
 [!code-xaml[ListViewTemplate#GridViewHeaderStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheaderstyle)]  
  
 [!code-xaml[ListViewTemplate#GridViewHeaderTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewheadertemplate)]  
  
 次の例では、これらの <xref:System.Windows.Style> オブジェクトと <xref:System.Windows.DataTemplate> オブジェクトを使用し、<xref:System.Windows.Controls.GridViewColumn> の <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> プロパティと <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> プロパティを設定する方法を示します。 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> プロパティによって列セルの内容が定義されます。  
  
 [!code-xaml[ListViewTemplate#GridViewColumnTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcolumntemplate)]  
  
 <xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A> と <xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> は、<xref:System.Windows.Controls.GridView> コントロールの列ヘッダーの外観をカスタマイズできるいくつかのプロパティのうちの 2 つにすぎません。 詳細については、[GridView の列ヘッダーのスタイルとテンプレートの概要](gridview-column-header-styles-and-templates-overview.md)を参照してください。  
  
 次の例では、<xref:System.Windows.Controls.GridViewColumn> 内のセルの外観をカスタマイズする <xref:System.Windows.DataTemplate> を定義する方法を示します。  
  
 [!code-xaml[ListViewTemplate#GridViewCellTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#gridviewcelltemplate)]  
  
 次の例では、この <xref:System.Windows.DataTemplate> を使用し、<xref:System.Windows.Controls.GridViewColumn> セルのコンテンツを定義する方法を示します。 このテンプレートは、前の <xref:System.Windows.Controls.GridViewColumn> の例に含まれる <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> プロパティの代わりに使用されています。  
  
 [!code-xaml[ListViewTemplate#CellTemplateProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewTemplate/CS/window1.xaml#celltemplateproperty)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [GridView の概要](gridview-overview.md)
- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
