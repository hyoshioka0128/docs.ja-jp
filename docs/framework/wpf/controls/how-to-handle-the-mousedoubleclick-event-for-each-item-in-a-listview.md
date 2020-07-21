---
title: '方法: ListView の各項目の MouseDoubleClick イベントを処理する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView controls [WPF], MouseDoubleClick event
ms.assetid: 81b39369-655a-4585-ac58-4640e5bb8fed
ms.openlocfilehash: 7bbc7bad36b3b1f2c92065e5f5699e5a86ac6189
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646108"
---
# <a name="how-to-handle-the-mousedoubleclick-event-for-each-item-in-a-listview"></a>方法: ListView の各項目の MouseDoubleClick イベントを処理する
<xref:System.Windows.Controls.ListView> 内の項目に対するイベントを処理するには、各 <xref:System.Windows.Controls.ListViewItem> にイベント ハンドラーを追加する必要があります。 <xref:System.Windows.Controls.ListView> がデータ ソースにバインドされている場合は、<xref:System.Windows.Controls.ListViewItem> を明示的には作成しませんが、<xref:System.Windows.Controls.ListViewItem> のスタイルに <xref:System.Windows.EventSetter> を追加することで、各項目のイベントを処理できます。  
  
## <a name="example"></a>例  
 次の例では、データ バインドされた <xref:System.Windows.Controls.ListView> を作成し、<xref:System.Windows.Style> を作成して、各 <xref:System.Windows.Controls.ListViewItem> にイベント ハンドラーを追加します。  
  
 [!code-xaml[ListViewHowTos#1](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#1)]  
[!code-xaml[ListViewHowTos#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#5)]  
[!code-xaml[ListViewHowTos#2](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml#2)]  
  
 次の例では、<xref:System.Windows.Controls.Control.MouseDoubleClick> イベントを処理します。  
  
 [!code-csharp[ListViewHowTos#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHowTos/CSharp/Window1.xaml.cs#6)]
 [!code-vb[ListViewHowTos#6](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ListViewHowTos/VisualBasic/Window1.xaml.vb#6)]  
  
> [!NOTE]
> <xref:System.Windows.Controls.ListView> をデータ ソースにバインドするのが最も一般的ですが、<xref:System.Windows.Controls.ListViewItem> を明示的に作成するかどうかにかかわらず、スタイルを使用することで、データ バインドされていない <xref:System.Windows.Controls.ListView> の各 <xref:System.Windows.Controls.ListViewItem> にイベント ハンドラーを追加できます。  <xref:System.Windows.Controls.ListViewItem> コントロールの明示的および暗黙的な作成の詳細については、<xref:System.Windows.Controls.ItemsControl> に関する記事を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Xml.XmlElement>
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [XMLDataProvider と XPath クエリを使用して XML データにバインドする](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)
- [ListView の概要](listview-overview.md)
