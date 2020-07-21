---
title: バインディング ソースの概要
description: Windows Presentation Foundation (WPF) でアプリケーションのバインディング ソースとして使用できるオブジェクトの型について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- binding data [WPF], binding sources
- data binding [WPF], binding source
- binding sources [WPF]
ms.assetid: 2df2cd11-6aac-4bdf-ab7b-ea5f464cd5ca
ms.openlocfilehash: 11d19d904e632ca2c7c7795946d350d078c38e70
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619625"
---
# <a name="binding-sources-overview"></a>バインディング ソースの概要
データ バインディングでは、バインディング ソース オブジェクトは、データの取得元のオブジェクトを表します。 このトピックでは、バインディング ソースとして使用できるオブジェクトの型について説明します。

<a name="binding_sources"></a>
## <a name="binding-source-types"></a>バインディング ソースの型
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] データ バインディングでは、次のバインディング ソースの型がサポートされています。

|バインディング ソース|説明|
|--------------------|-----------------|
|共通言語ランタイム (CLR) のオブジェクト|任意の共通言語ランタイム (CLR) オブジェクトのパブリック プロパティ、サブプロパティ、およびインデクサーにバインドできます。 バインディング エンジンでは、CLR リフレクションを使用してプロパティの値が取得されます。 または、<xref:System.ComponentModel.ICustomTypeDescriptor> を実装しているオブジェクトまたは <xref:System.ComponentModel.TypeDescriptionProvider> が登録されているオブジェクトも、バインディング エンジンで動作します。<br /><br /> バインディング ソースとして使用できるクラスを実装する方法の詳細については、このトピックで後述する「[バインディング ソースのクラスの実装](#classes)」を参照してください。|
|動的オブジェクト|<xref:System.Dynamic.IDynamicMetaObjectProvider> インターフェイスが実装されているオブジェクトの使用可能なプロパティおよびインデクサーにバインドできます。 コード内のメンバーにアクセスできる場合、これにバインドできます。 たとえば、動的オブジェクトを使用して `someObjet.AProperty` を介してコード内のメンバーにアクセスできる場合、バインディング パスを `AProperty` に設定してこのメンバーにバインドできます。|
|ADO.NET オブジェクト|<xref:System.Data.DataTable> などの ADO.NET オブジェクトにバインドできます。 ADO.NET の <xref:System.Data.DataView> では <xref:System.ComponentModel.IBindingList> インターフェイスが実装されており、バインディング エンジンがリッスンする変更通知が提供されます。|
|XML オブジェクト|`XPath` クエリにバインドし、<xref:System.Xml.XmlNode>、<xref:System.Xml.XmlDocument>、または <xref:System.Xml.XmlElement> に対して実行できます。 マークアップのバインディング ソースである XML データにアクセスする便利な方法は、<xref:System.Windows.Data.XmlDataProvider> オブジェクトを使用することです。 詳細については、「[XMLDataProvider と XPath クエリを使用して XML データにバインドする](how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)」を参照してください。<br /><br /> <xref:System.Xml.Linq.XElement> または <xref:System.Xml.Linq.XDocument> にバインドすることも、LINQ to XML を使用して、これらの型のオブジェクトで実行するクエリの結果にバインドすることも可能です。 LINQ to XML を使用してマークアップのバインディング ソースである XML データにアクセスする便利な方法は、<xref:System.Windows.Data.ObjectDataProvider> オブジェクトを使用することです。 詳細については、「[XDocument、XElement、または LINQ for XML クエリの結果にバインドする](how-to-bind-to-xdocument-xelement-or-linq-for-xml-query-results.md)」を参照してください。|
|<xref:System.Windows.DependencyObject> オブジェクト|任意の <xref:System.Windows.DependencyObject> の依存関係プロパティにバインドできます。 例については、「[2 つのコントロールのプロパティをバインドする](how-to-bind-the-properties-of-two-controls.md)」を参照してください。|

<a name="classes"></a>
## <a name="implementing-a-class-for-the-binding-source"></a>バインディング ソースのクラスの実装
 独自のバインディング ソースを作成できます。 このセクションでは、バインディング ソースとして機能するクラスを実装する場合に認識している必要のある事項について説明します。

### <a name="providing-change-notifications"></a>変更通知の提供
 <xref:System.Windows.Data.BindingMode.OneWay> または <xref:System.Windows.Data.BindingMode.TwoWay> バインディングを使用している場合は (バインディング ソース プロパティが動的に変化するときに [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を更新するため)、適切なプロパティ変更通知メカニズムを実装する必要があります。 CLR または動的クラスで <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装することをお勧めします。 詳細については、「[プロパティの変更通知を実装する](how-to-implement-property-change-notification.md)」を参照してください。

 <xref:System.ComponentModel.INotifyPropertyChanged> を実装しない CLR オブジェクトを作成する場合、独自の通知システムを使用して、バインディングで使用するデータを確実に最新に保つ必要があります。 変更通知対象にする各プロパティの `PropertyChanged` パターンをサポートすることによって、変更通知を提供できます。 このパターンをサポートするには、プロパティごとに *PropertyName*Changed イベントを定義します。*PropertyName* はプロパティの名前です。 プロパティが変更されるたびにイベントが発生します。

 バインディング ソースがこれらの通知メカニズムの 1 つを実装する場合、ターゲットの更新が自動的に発生します。 何らかの理由でバインディング ソースが適切なプロパティ変更通知を提供しない場合、<xref:System.Windows.Data.BindingExpression.UpdateTarget%2A> メソッドを使用してターゲット プロパティを明示的に更新できます。

### <a name="other-characteristics"></a>その他の特性
 その他の重要な点を次に示します。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] にオブジェクトを作成する場合は、クラスにパラメーターなしのコンストラクターが必要です。 C# などの一部の .NET 言語では、パラメーターなしのコンストラクターが自動的に作成される場合があります。

- バインディングのバインディング ソース プロパティとして使用するプロパティは、クラスのパブリック プロパティである必要があります。 明示的に定義されたインターフェイスのプロパティは、バインディングの目的ではアクセスできません。また、基本実装を持たない保護されたプロパティ、プライベート プロパティ、内部プロパティ、仮想プロパティも同様にバインディングの目的ではアクセスできません。

- パブリック フィールドにバインドすることはできません。

- クラスで宣言されたプロパティの型は、バインディングに渡される型です。 ただし、最終的にバインディングによって使用される型は、バインディング ソース プロパティの型ではなく、バインディング ターゲット プロパティの型によって決まります。 型の違いがある場合は、バインディングにカスタム プロパティを最初に渡す方法を処理するコンバーターを作成する必要があります。 詳細については、「<xref:System.Windows.Data.IValueConverter>」を参照してください。

<a name="objects"></a>
## <a name="using-entire-objects-as-a-binding-source"></a>バインディング ソースとしてオブジェクト全体を使用する
 バインディング ソースとしてオブジェクト全体を使用できます。 <xref:System.Windows.Data.Binding.Source%2A> または <xref:System.Windows.FrameworkElement.DataContext%2A> プロパティを使用してバインディング ソースを指定し、空のバインディング宣言 `{Binding}` を提供できます。 これが便利なシナリオには、文字列型のオブジェクトへのバインディング、対象とするプロパティが複数あるオブジェクトへのバインディング、またはコレクション オブジェクトへのバインディングなどがあります。 コレクション オブジェクト全体へのバインディングの例は、「[階層データでマスター詳細パターンを使用する](how-to-use-the-master-detail-pattern-with-hierarchical-data.md)」を参照してください。

 バインディング ターゲット プロパティに対してデータが意味を持つように、カスタム ロジックを適用する必要があることに注意してください。 カスタム ロジックは、カスタム コンバーター (既定の型変換が存在しない場合) または <xref:System.Windows.DataTemplate> の形式にできます。 コンバーターの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」の「データ変換」セクションを参照してください。 データ テンプレートの詳細については「 [データ テンプレートの概要](data-templating-overview.md)」を参照してください。

<a name="collections"></a>
## <a name="using-collection-objects-as-a-binding-source"></a>バインディング ソースとしてコレクション オブジェクトを使用する
 多くの場合、バインディング ソースとして使用するオブジェクトは、カスタム オブジェクトのコレクションです。 各オブジェクトは、反復されるバインディングの 1 つのインスタンスのソースとして機能します。 たとえば、`CustomerOrder` オブジェクトから構成される `CustomerOrders` コレクションがあり、アプリケーションが注文数およびそれぞれに含まれているデータを判別するためにコレクションとやり取りするとします。

 <xref:System.Collections.IEnumerable> インターフェイスを実装する任意のコレクションを列挙できます。 ただし、コレクションの挿入または削除によって [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] が自動的に更新されるように動的バインディングを設定するには、コレクションで <xref:System.Collections.Specialized.INotifyCollectionChanged> インターフェイスが実装されている必要があります。 このインターフェイスは、基盤のコレクションが変更されたときに必ず発生する必要があるイベントを公開します。

 <xref:System.Collections.ObjectModel.ObservableCollection%601> クラスは、<xref:System.Collections.Specialized.INotifyCollectionChanged> インターフェイスを公開するデータ コレクションの組み込みの実装です。 コレクション内の個々のデータ オブジェクトは、前の各セクションで説明されている要件を満たす必要があります。 例については、「[ObservableCollection を作成およびバインドする](how-to-create-and-bind-to-an-observablecollection.md)」を参照してください。 独自のコレクションを実装する前に、<xref:System.Collections.ObjectModel.ObservableCollection%601> または既存のコレクション クラス (<xref:System.Collections.Generic.List%601>、<xref:System.Collections.ObjectModel.Collection%601>、<xref:System.ComponentModel.BindingList%601> など) のいずれかを使用することを検討してください。

 WPF はコレクションに直接バインドすることはありません。 バインディング ソースとしてコレクションを指定すると、WPF は実際にはコレクションの既定のビューにバインドします。 既定のビューの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。

 高度なシナリオで独自のコレクションを実装する場合、<xref:System.Collections.IList> インターフェイスの使用を検討します。 <xref:System.Collections.IList> では、インデックスによって個別にアクセスできるオブジェクトの一般的ではないコレクションが提供され、パフォーマンスを向上できます。

<a name="permissions"></a>
## <a name="permission-requirements-in-data-binding"></a>データ バインディングでのアクセス許可要件
 データ バインディング時、アプリケーションの信頼レベルを考慮する必要があります。 次の表は、完全信頼または部分信頼で実行しているアプリケーションにおいてバインドできるプロパティの型のまとめです。

|プロパティの型<br /><br /> (すべてのアクセス修飾子)|動的オブジェクトのプロパティ|動的オブジェクトのプロパティ|CLR プロパティ|CLR プロパティ|依存関係プロパティ|依存関係プロパティ|
|------------------------------------------------|-----------------------------|-----------------------------|------------------|------------------|-------------------------|-------------------------|
|**信頼レベル**|**完全信頼**|**部分信頼**|**完全信頼**|**部分信頼**|**完全信頼**|**部分信頼**|
|パブリック クラス|はい|はい|はい|はい|はい|はい|
|非パブリック クラス|はい|×|はい|×|はい|はい|

 この表では、データ バインディングのアクセス許可要件について次の重要事項を説明します。

- CLR プロパティでは、バインディング エンジンが、リフレクションを使用してバインディング ソースのプロパティにアクセスできる限り、データ バインディングは機能します。 それ以外の場合、バインディング エンジンは、プロパティを検出できないという警告を発行し、フォールバック値または既定値を使用します (使用できる場合)。

- コンパイル時または実行時に定義されている動的オブジェクトのプロパティにバインドできます。

- 依存関係プロパティには常にバインドできます。

 XML バインディングのアクセス許可要件は同様です。 部分信頼サンド ボックスでは、<xref:System.Windows.Data.XmlDataProvider> は、指定されたデータにアクセスする権限がない場合には失敗します。

 匿名型のオブジェクトは内部です。 完全信頼で実行されている場合にのみ、匿名型のプロパティにバインドできます。 匿名型の詳細については、「[Anonymous Types (C# Programming Guide)](../../../csharp/programming-guide/classes-and-structs/anonymous-types.md)」または「[Anonymous Types (Visual Basic)](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)」を参照してください。

 部分信頼セキュリティの詳細については、「[WPF 部分信頼セキュリティ](../wpf-partial-trust-security.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.ObjectDataProvider>
- <xref:System.Windows.Data.XmlDataProvider>
- [バインディング ソースを指定する](how-to-specify-the-binding-source.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [LINQ to XML による WPF のデータ バインディングの概要](wpf-data-binding-with-linq-to-xml-overview.md)
- [データ バインディングのパフォーマンスを最適化する](../advanced/optimizing-performance-data-binding.md)
