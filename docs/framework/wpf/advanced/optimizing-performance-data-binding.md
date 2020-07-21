---
title: 'パフォーマンスの最適化: データ バインディング'
ms.date: 03/30/2017
helpviewer_keywords:
- binding data [WPF], performance
- data binding [WPF], performance
ms.assetid: 1506a35d-c009-43db-9f1e-4e230ad5be73
ms.openlocfilehash: 3128f453378f9d74f867b571e30f2be4e8add8a4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186758"
---
# <a name="optimizing-performance-data-binding"></a>パフォーマンスの最適化: データ バインディング
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] データ バインディングは、アプリケーションがデータを提示し、データと対話するための簡単で一貫性のある方法を提供します。 要素は、CLR オブジェクトおよび XML の形式のさまざまなデータ ソースのデータにバインドできます。  
  
 このトピックでは、データ バインディングのパフォーマンスに関する推奨事項について説明します。  

<a name="HowDataBindingReferencesAreResolved"></a>
## <a name="how-data-binding-references-are-resolved"></a>データ バインディングの参照が解決されるしくみ  
 データ バインディングのパフォーマンスの問題に入る前に、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のデータ バインディング エンジンがバインディングのオブジェクト参照をどのように解決するのかを説明します。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のデータ バインディングのソースでは、任意の CLR オブジェクトを使用できます。 CLR オブジェクトのプロパティ、サブプロパティ、またはインデクサーにバインドできます。 バインディング参照は、Microsoft .NET Framework のリフレクションまたは <xref:System.ComponentModel.ICustomTypeDescriptor> を使用して解決されます。 次に、バインディングのオブジェクト参照を解決するための 3 つの方法について説明します。  
  
 1 つ目は、リフレクションを使用する方法です。 この場合、<xref:System.Reflection.PropertyInfo> オブジェクトを使用してプロパティの属性を検出し、プロパティ メタデータにアクセスします。 <xref:System.ComponentModel.ICustomTypeDescriptor> インターフェイスを使用している場合、データ バインディング エンジンはこのインターフェイスを使用してプロパティ値にアクセスします。 <xref:System.ComponentModel.ICustomTypeDescriptor> インターフェイスは、オブジェクトに静的なプロパティのセットがない場合に特に便利です。  
  
 <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装するか、または <xref:System.ComponentModel.TypeDescriptor> に関連付けられている変更通知を使用することによって、プロパティ変更通知を提供できます。 ただし、プロパティ変更通知を実装するには <xref:System.ComponentModel.INotifyPropertyChanged> を使用することをお勧めします。  
  
 ソース オブジェクトが CLR オブジェクトでソース プロパティが CLR プロパティの場合、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のデータ バインディング エンジンでは、最初にソース オブジェクトでリフレクションを使用して <xref:System.ComponentModel.TypeDescriptor> を取得した後、<xref:System.ComponentModel.PropertyDescriptor> を照会する必要があります。 パフォーマンスの観点から見た場合、このリフレクション操作のシーケンスには非常に時間がかかる可能性があります。  
  
 オブジェクト参照を解決するための 2 つ目の方法は、CLR ソース オブジェクトで <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスが実装されていて、ソース プロパティが CLR プロパティである場合に使用されます。 この場合、データ バインディング エンジンは、ソースの型に対してリフレクションを直接使用して必要なプロパティを取得します。 この方法も最適な方法とは言えませんが、最初の方法よりは作業セットの要件の負荷が小さくなります。  
  
 オブジェクト参照を解決するための 3 つ目の方法は、ソース オブジェクトが <xref:System.Windows.DependencyObject> で、ソース プロパティが <xref:System.Windows.DependencyProperty> である場合に使用されます。 この場合、データ バインディング エンジンはリフレクションを使用する必要はありません。 代わりに、プロパティ エンジンとデータ バインディング エンジンが連携してプロパティ参照を個別に解決します。 これが、データ バインディングに使用されているオブジェクト参照を解決するための最適な方法です。  
  
 これらの 3 つの方法を使用して 1000 個の <xref:System.Windows.Controls.TextBlock> 要素の <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティのデータ バインディングを行ったときの速度の比較を次の表に示します。  
  
|**TextBlock の Text プロパティのバインド先**|**バインディング時間 (ミリ秒)**|**レンダリング時間 -- バインディングを含む (ミリ秒)**|  
|--------------------------------------------------|-----------------------------|--------------------------------------------------|  
|CLR オブジェクトのプロパティ|115|314|  
|<xref:System.ComponentModel.INotifyPropertyChanged> を実装する CLR オブジェクトのプロパティ|115|305|  
|<xref:System.Windows.DependencyObject> の <xref:System.Windows.DependencyProperty>。|90|263|  
  
<a name="Binding_to_Large_CLR_Objects"></a>
## <a name="binding-to-large-clr-objects"></a>大きな CLR オブジェクトへのバインディング  
 何千ものプロパティを持つ 1 つの CLR オブジェクトへのデータ バインディングは、パフォーマンスに大きな影響を及ぼします。 この影響を最小限に抑えるには、その 1 つのオブジェクトを複数の CLR オブジェクトに分割して、個々のオブジェクトのプロパティの数を減らします。 次の表では、1 つの大きな CLR オブジェクトへのデータ バインディングと複数の小さなオブジェクトへのデータ バインディングのバインディング時間とレンダリング時間を示します。  
  
|**1000 個の TextBlock オブジェクトのデータ バインディングのバインド先**|**バインディング時間 (ミリ秒)**|**レンダリング時間 -- バインディングを含む (ミリ秒)**|  
|---------------------------------------------|-----------------------------|--------------------------------------------------|  
|1000 個のプロパティを持つ 1 つの CLR オブジェクト|950|1200|  
|1 つのプロパティを持つ 1000 個の CLR オブジェクト|115|314|  
  
<a name="Binding_to_an_ItemsSource"></a>
## <a name="binding-to-an-itemssource"></a>ItemsSource へのバインディング  
 <xref:System.Windows.Controls.ListBox> に表示する従業員リストが保持されている CLR <xref:System.Collections.Generic.List%601> オブジェクトがあるとします。 この 2 つのオブジェクトの間に対応関係を作成するには、従業員リストを <xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>プロパティにバインドします。 ここで、グループに新しい従業員が加わったとします。 バインドされた <xref:System.Windows.Controls.ListBox> 値にその新しい従業員を挿入するには、この従業員を従業員リストに追加するだけで、その変更が自動的にデータ バインディング エンジンに認識されると思われがちです。 しかし、実際にはそうはならず、その変更は <xref:System.Windows.Controls.ListBox> に自動的には反映されません。 これは、CLR の <xref:System.Collections.Generic.List%601> オブジェクトではコレクション変更イベントが自動的に発生しないからです。 <xref:System.Windows.Controls.ListBox> に変更を反映するには、従業員リストを再作成し、もう一度 <xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティに割り当てる必要があります。 この解決方法で問題は解決されますが、パフォーマンスへの影響はきわめて大きくなります。 <xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> を新しいオブジェクトに割り当てるたびに、<xref:System.Windows.Controls.ListBox> では最初に前の項目が削除され、リスト全体が再生成されます。 <xref:System.Windows.Controls.ListBox> が複雑な <xref:System.Windows.DataTemplate> にマップされている場合、パフォーマンスへの影響はさらに大きくなります。  
  
 この問題は、従業員リストを <xref:System.Collections.ObjectModel.ObservableCollection%601> にすることによってきわめて効率的に解決することができます。 <xref:System.Collections.ObjectModel.ObservableCollection%601> オブジェクトによって変更通知が生成され、それをデータ バインディング エンジンで受け取ることができます。 このイベントにより、リスト全体を再生成する必要なく、<xref:System.Windows.Controls.ItemsControl> の項目を追加または削除できます。  
  
 次の表では、項目を 1 つ追加した場合に <xref:System.Windows.Controls.ListBox> の更新にかかる時間を示します (UI の仮想化はオフ)。 1 行目の数字は、CLR の <xref:System.Collections.Generic.List%601> オブジェクトが <xref:System.Windows.Controls.ListBox> 要素の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> にバインドされるときの経過時間を表しています。 2 行目の数字は、<xref:System.Collections.ObjectModel.ObservableCollection%601> が <xref:System.Windows.Controls.ListBox> 要素の <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> にバインドされるときの経過時間を表しています。 <xref:System.Collections.ObjectModel.ObservableCollection%601> のデータ バインディング方法を使用すると時間を大幅に節約できることがわかります。  
  
|**ItemsSource のデータ バインディングのバインド先**|**1 項目の更新時間 (ミリ秒)**|  
|--------------------------------------|---------------------------------------|  
|CLR の <xref:System.Collections.Generic.List%601> オブジェクト|1656|  
|<xref:System.Collections.ObjectModel.ObservableCollection%601>|20|  
  
<a name="Binding_IList_to_ItemsControl_not_IEnumerable"></a>
## <a name="bind-ilist-to-itemscontrol-not-ienumerable"></a>IEnumerable ではなく IList を ItemsControl にバインドする  
 <xref:System.Windows.Controls.ItemsControl> オブジェクトに <xref:System.Collections.Generic.IList%601> または <xref:System.Collections.IEnumerable> のどちらをバインドするかを選択できる場合は、<xref:System.Collections.Generic.IList%601> オブジェクトを選択します。 <xref:System.Collections.IEnumerable> を <xref:System.Windows.Controls.ItemsControl> にバインドすると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でラッパー <xref:System.Collections.Generic.IList%601> オブジェクトが強制的に作成されます。これにより、追加のオブジェクトの不要なオーバーヘッドが発生するため、パフォーマンスに影響します。  
  
<a name="Do_not_Convert_CLR_objects_to_Xml_Just_For_Data_Binding"></a>
## <a name="do-not-convert-clr-objects-to-xml-just-for-data-binding"></a>データ バインディングのためだけに CLR オブジェクトを XML に変換しない  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、XML コンテンツへのデータ バインディングが可能です。ただし、XML コンテンツへのデータ バインディングは、CLR オブジェクトへのデータ バインディングに比べて低速です。 CLR オブジェクトのデータをデータ バインディングのためだけに XML に変換しないでください。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [ハードウェアの活用](optimizing-performance-taking-advantage-of-hardware.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [チュートリアル: WPF アプリケーション内のアプリケーション データのキャッシュ](walkthrough-caching-application-data-in-a-wpf-application.md)
