---
title: '方法: XMLDataProvider と XPath クエリを使用して XML データにバインドする'
ms.date: 03/30/2017
helpviewer_keywords:
- XmlDataProvider [WPF], binding to XML data
- data binding [WPF], binding to XML data using XmlDataProvider queries
- binding [WPF], to XML data using XmlDataProvider queries
ms.assetid: 7dcd018f-16aa-4870-8e47-c1b4ea31e574
ms.openlocfilehash: a5ad7d8bce9bc0a760868e483278d1836f9472af
ms.sourcegitcommit: f8c36054eab877de4d40a705aacafa2552ce70e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75559704"
---
# <a name="how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries"></a>方法: XMLDataProvider と XPath クエリを使用して XML データにバインドする
この例では、<xref:System.Windows.Data.XmlDataProvider> を使用して XML データにバインドする方法を示します。  
  
 <xref:System.Windows.Data.XmlDataProvider> では、アプリケーションでデータ バインディングを介してアクセスできる基になるデータは、XML ノードの任意のツリーです。 つまり、<xref:System.Windows.Data.XmlDataProvider> では、XML ノードの任意のツリーをバインディング ソースとして使用するための便利な手段が提供されます。  
  
## <a name="example"></a>例  
 次の例では、データは XML の "*データ アイランド*" として <xref:System.Windows.FrameworkElement.Resources%2A> セクション内に直接埋め込まれます。 XML データ アイランドは、`<x:XData>` タグ内にラップされていることと、常にルート ノードを 1 つだけ (この例では *Inventory*) 持つことが必要です。  
  
> [!NOTE]
> XML データのルート ノードには、XML 名前空間を空の文字列に設定する **xmlns** 属性があります。 これは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページ内にインラインで配置されるデータ アイランドに XPath クエリを適用する場合に必須です。 このインラインの場合は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] と、必然的にデータ アイランドも、<xref:System.Windows> 名前空間を継承します。 このため、XPath クエリが <xref:System.Windows> 名前空間によって修飾されることを防ぐために、名前空間を空白に設定する必要があります。このようにしないと、クエリの検索範囲が本来のものとは異なってしまいます。  
  
 [!code-xaml[XMLDataSource#1](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource/CS/Window1.xaml#1)]  
  
 この例に示すように、同じバインディング宣言を属性構文で作成するには、特殊文字を適切にエスケープする必要があります。 詳しくは、「[XML Character Entities and XAML](../../../desktop-wpf/xaml-services/xml-character-entities.md)」(XML 文字エンティティと XAML) をご覧ください。  
  
 この例を実行すると、次の項目が <xref:System.Windows.Controls.ListBox> に表示されます。 これらは、*Books* の下のすべての要素のうち、*Stock* の値が "*out*" か、*Number* の値が 3 に等しいか 8 以上のものの *Title* です。 *CD* の項目が 1 つも返されないのは、<xref:System.Windows.Data.XmlDataProvider> に設定された <xref:System.Windows.Data.XmlDataProvider.XPath%2A> の値が、*Books* 要素のみを公開するように指定されている (本質的にはフィルターが設定されている) からであることに注意してください。  
  
 ![4 冊の書籍のタイトルを示す XPath の例のスクリーンショット。](./media/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries/xpath-example-listbox-details.png)  
  
 この例で書籍のタイトルが表示されるのは、<xref:System.Windows.DataTemplate> 内の <xref:System.Windows.Controls.TextBlock> バインディングの <xref:System.Windows.Data.Binding.XPath%2A> が "*Title*" に設定されているためです。 属性 (*ISBN* など) の値を表示するには、<xref:System.Windows.Data.Binding.XPath%2A> の値を "`@ISBN`" に設定します。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内の **XPath** プロパティは、XmlNode.SelectNodes メソッドによって処理されます。 別の結果を得るために、**XPath** クエリを変更できます。 前の例での、バインドされた <xref:System.Windows.Controls.ListBox> に対する <xref:System.Windows.Data.Binding.XPath%2A> クエリの例を次に示します。  
  
- `XPath="Book[1]"` は、最初の書籍要素 ("XML in Action") を返します。 **XPath** のインデックスが 0 ではなく 1 から開始することにご注意ください。  
  
- `XPath="Book[@*]"` は、任意の属性を持つすべての書籍要素を返します。  
  
- `XPath="Book[last()-1]"` は、最後から 2 番目の書籍要素 ("Introducing Microsoft .NET") を返します。  
  
- `XPath="*[position()>3]"` は、最初の 3 つを除くすべての書籍要素を返します。  
  
 **XPath** クエリを実行すると、1 つの <xref:System.Xml.XmlNode> または XmlNode のリストが返されます。 <xref:System.Xml.XmlNode> は共通言語ランタイム (CLR) オブジェクトです。つまり、<xref:System.Windows.Data.Binding.Path%2A> プロパティを使用して共通言語ランタイム (CLR) のプロパティにバインドできます。 前の例をもう一度考えてみます。 例の残りの部分はそのままで <xref:System.Windows.Controls.TextBlock> バインディングを次のように変更すると、返された XmlNode の名前が <xref:System.Windows.Controls.ListBox> に表示されます。 この場合、返されたノードの名前はすべて "*Book*" です。  
  
 [!code-xaml[XmlDataSourceVariation#XmlNodePath](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSourceVariation/CS/Page1.xaml#xmlnodepath)]  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページのソースに XML をデータ アイランドとして埋め込む方法では、コンパイル時に正確なデータ コンテンツが必要となるので、アプリケーションによっては不都合が生じます。 したがって、次の例のように、外部 XML ファイルからのデータの取得もサポートされています。  
  
 [!code-xaml[XMLDataSource2#XmlFileExample](~/samples/snippets/csharp/VS_Snippets_Wpf/XmlDataSource2/CS/Window1.xaml#xmlfileexample)]  
  
 XML データがリモートの XML ファイル内に存在する場合は、次のように、適切な URL を <xref:System.Windows.Data.XmlDataProvider.Source%2A> 属性に割り当てることによってデータへのアクセスを定義します。  
  
```xml  
<XmlDataProvider x:Key="BookData" Source="http://MyUrl" XPath="Books"/>  
```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.ObjectDataProvider>
- [XDocument、XElement、または LINQ for XML クエリの結果にバインドする](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)
- [階層 XML データでマスター詳細パターンを使用する](how-to-use-the-master-detail-pattern-with-hierarchical-xml-data.md)
- [バインディング ソースの概要](binding-sources-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
