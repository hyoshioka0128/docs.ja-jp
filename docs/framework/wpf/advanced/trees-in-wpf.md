---
title: ツリー
ms.date: 03/30/2017
helpviewer_keywords:
- logical tree [WPF]
- element tree [WPF]
- visual tree [WPF]
ms.assetid: e83f25e5-d66b-4fc7-92d2-50130c9a6649
ms.openlocfilehash: aed4350f1a7084b7894a70ac9d6d00cf25b39e34
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646199"
---
# <a name="trees-in-wpf"></a>WPF のツリー
多くのテクノロジでは、要素とコンポーネントはツリー構造で構成されており、開発者はツリー内のオブジェクト ノードを直接操作して、アプリケーションのレンダリングや動作に影響を与えます。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でも、プログラム要素間の関係を定義するために、いくつかのツリー構造のメタファーが使用されます。 ほとんどの場合、WPF の開発者は、概念的にオブジェクト ツリーのメタファーについて検討しながら、アプリケーションをコードで作成したり、XAML でアプリケーションの部分を定義したりできますが、それを行うには特定の API を呼び出したり、特定のマークアップを使用したりするのであり、XML DOM で使用するような一般的なオブジェクト ツリー操作 API ではありません。 WPF では、ツリー メタファー ビューを提供する <xref:System.Windows.LogicalTreeHelper> と <xref:System.Windows.Media.VisualTreeHelper> の 2 つのヘルパー クラスが公開されています。 ビジュアル ツリーと論理ツリーという用語は、これらの同じツリーが特定の主要な WPF 機能の動作を理解するのに役立つため、WPF ドキュメントでも使用されています。 このトピックでは、ビジュアル ツリーと論理ツリーが表す内容を定義し、そのようなツリーが全体的なオブジェクト ツリーの概念とどのように関連しているかについて説明し、<xref:System.Windows.LogicalTreeHelper> と <xref:System.Windows.Media.VisualTreeHelper> を紹介します。  

<a name="element_tree"></a>
## <a name="trees-in-wpf"></a>WPF のツリー  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での最も完全なツリー構造は、オブジェクト ツリーです。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でアプリケーション ページを定義した後、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を読み込むと、マークアップ内の要素の入れ子関係に基づいてツリー構造が作成されます。 アプリケーションまたはアプリケーションの一部をコードで定義した場合、特定のオブジェクトのコンテンツ モデルを実装するプロパティに対してプロパティ値を割り当てる方法に基づいて、ツリー構造が作成されます。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、完全なオブジェクト ツリーを概念化してパブリック API に報告する方法として、論理ツリーとビジュアル ツリーの 2 つがあります。 論理ツリーとビジュアル ツリーの違いは必ずしも重要であるとは限りませんが、特定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] サブシステムで問題が発生したり、マークアップまたはコードで行った選択に影響したりすることがあります。  
  
 論理ツリーまたはビジュアル ツリーを常に直接操作するわけではありませんが、ツリーが相互作用する方法の概念を理解していると、WPF をテクノロジとして理解するのに役立ちます。 ある種のツリー メタファーとして WPF を考えることは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でのプロパティの継承とイベント ルーティングのしくみを理解する上でも重要です。  
  
> [!NOTE]
> オブジェクト ツリーは実際の API より概念的であるため、概念を考えるもう 1 つの方法はオブジェクト グラフです。 実際には、実行時にツリー メタファーが分割されるオブジェクト間には関係があります。 そうではあっても、特に XAML で定義された UI の場合、ツリー メタファーは、この一般的な概念を参照するときにほとんどの WPF ドキュメントでオブジェクト ツリーという用語が使用されることに関係しています。  
  
<a name="logical_tree"></a>
## <a name="the-logical-tree"></a>論理ツリー  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、UI 要素の基になっているオブジェクトのプロパティを設定することにより、要素にコンテンツを追加します。 たとえば、<xref:System.Windows.Controls.ListBox> コントロールに項目を追加するには、その <xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティを操作します。 これにより、<xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティ値である <xref:System.Windows.Controls.ItemCollection> に項目が配置されます。 同様に、オブジェクトを <xref:System.Windows.Controls.DockPanel> に追加するには、その <xref:System.Windows.Controls.Panel.Children%2A> プロパティ値を操作します。 ここでは、<xref:System.Windows.Controls.UIElementCollection> にオブジェクトを追加します。 コード例については、「[方法: 要素を動的に追加する](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms752374(v=vs.100))」を参照してください。  
  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、<xref:System.Windows.Controls.ListBox> にリスト項目を配置したり、<xref:System.Windows.Controls.DockPanel> にコントロールや他の UI 要素を配置するときは、次の例のように、明示的または暗黙的に、<xref:System.Windows.Controls.ItemsControl.Items%2A> および <xref:System.Windows.Controls.Panel.Children%2A> プロパティも使用します。  
  
 [!code-xaml[TreeOvwsSupport#AllCode](~/samples/snippets/csharp/VS_Snippets_Wpf/TreeOvwsSupport/CS/page1.xaml#allcode)]  
  
 この XAML をドキュメント オブジェクト モデルの XML として処理し、暗黙的にコメント アウトされたタグを含めた場合 (これは有効なことです)、結果の XML DOM ツリーには、`<ListBox.Items>` とその他の暗黙的な項目の要素が含まれます。 しかし、XAML では、マークアップを読み取ってオブジェクトに書き込むときに、このような処理は行われません。結果として得られるオブジェクト グラフには、`ListBox.Items` は含まれません。 ただし、<xref:System.Windows.Controls.ItemCollection> を含む `Items` という名前の <xref:System.Windows.Controls.ListBox> プロパティが作成され、その <xref:System.Windows.Controls.ItemCollection> は初期化されますが、<xref:System.Windows.Controls.ListBox> XAML が処理されるときは空です。 その後、<xref:System.Windows.Controls.ListBox> のコンテンツとして存在する各子オブジェクト要素が、`ItemCollection.Add` のパーサー呼び出しによって <xref:System.Windows.Controls.ItemCollection> に追加されます。 オブジェクト ツリーに対する XAML の処理のこの例は、作成されるオブジェクト ツリーが基本的に論理ツリーである例のように見えます。  
  
 しかし、XAML の暗黙的な構文項目が考慮されていない場合でも、論理ツリーは実行時にアプリケーション UI に存在するオブジェクト グラフ全体ではありません。その主な理由は、ビジュアルとテンプレートです。 たとえば、<xref:System.Windows.Controls.Button> について考えてみます。 論理ツリーでは、<xref:System.Windows.Controls.Button> オブジェクトとその文字列の `Content` が報告されます。 しかし、実行時のオブジェクト ツリーには、このボタンに関してさらに多くのことが含まれます。 具体的には、特定の <xref:System.Windows.Controls.Button> コントロール テンプレートが適用されたため、ボタンは画面にそのように表示されるだけです。 実行時に論理ツリーを見ている場合でも (表示されている UI からの入力イベントを処理してから、論理ツリーを読み取る場合など)、適用されたテンプレートによるビジュアルは (テンプレートで定義されている、ビジュアル ボタンの周りのダーク グレーの <xref:System.Windows.Controls.Border> など)、論理ツリーでは報告されません。 テンプレートのビジュアルを調べるには、代わりにビジュアル ツリーを調べる必要があります。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の構文が作成されたオブジェクト グラフにどのようにマップされるか、および XAML で暗黙の構文の詳細については、「[XAML 構文の詳細](xaml-syntax-in-detail.md)」または [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md) に関する記事を参照してください。  
  
<a name="tree_property_inheritance_event_routing"></a>
### <a name="the-purpose-of-the-logical-tree"></a>論理ツリーの目的  
 論理ツリーは、コンテンツ モデルが子オブジェクトを簡単に反復処理できるようにし、コンテンツ モデルを拡張できるようにするために存在します。 また、論理ツリーでは、論理ツリー内のすべてのオブジェクトが読み込まれたときなど、特定の通知のためのフレームワークが提供されます。 基本的に、論理ツリーはフレームワーク レベルでの実行時のオブジェクト グラフの近似であり、ビジュアルは除外されますが、独自の実行時アプリケーションの構成に対する多くのクエリ操作には適しています。  
  
 さらに、静的リソース参照と動的リソース参照の両方が解決されます。そのためには、最初に要求しているオブジェクトで <xref:System.Windows.FrameworkElement.Resources%2A> コレクションの論理ツリーを上方に検索し、その後引き続き論理ツリーを上方に各 <xref:System.Windows.FrameworkElement> (または <xref:System.Windows.FrameworkContentElement>) で、そのキーを含む可能性のある <xref:System.Windows.ResourceDictionary> が含まれる別の `Resources` の値を調べます。 論理ツリーは、論理ツリーとビジュアル ツリーの両方が存在する場合に、リソース検索に使用されます。 リソース ディクショナリと検索の詳細については、[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
<a name="composition"></a>
### <a name="composition-of-the-logical-tree"></a>論理ツリーの構成  
 論理ツリーは WPF フレームワーク レベルで定義されます。これは、論理ツリーの操作に最も関係する WPF の基本要素が、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> であることを意味します。 ただし、<xref:System.Windows.LogicalTreeHelper> API を実際に使用するとわかるように、論理ツリーには <xref:System.Windows.FrameworkElement> でも <xref:System.Windows.FrameworkContentElement> でもないノードが含まれる場合があります。 たとえば、論理ツリーでは <xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Text%2A> の値が報告されますが、これは文字列です。  
  
<a name="override_logical_tree"></a>
### <a name="overriding-the-logical-tree"></a>論理ツリーのオーバーライド  
 高度なコントロールの作成者は、一般的なオブジェクトまたはコンテンツ モデルによって論理ツリー内のオブジェクトが追加または削除される方法が定義されているいくつかの API をオーバーライドすることにより、論理ツリーをオーバーライドできます。 論理ツリーをオーバーライドする方法の例については、[論理ツリーのオーバーライド](how-to-override-the-logical-tree.md)に関する記事を参照してください。  
  
<a name="pvi"></a>
### <a name="property-value-inheritance"></a>プロパティ値の継承  
 プロパティ値の継承は、ハイブリッド ツリーを介して動作します。 プロパティの継承を可能にする <xref:System.Windows.FrameworkPropertyMetadata.Inherits%2A> プロパティが含まれる実際のメタデータは、WPF フレームワーク レベルの <xref:System.Windows.FrameworkPropertyMetadata> クラスです。 したがって、元の値を保持する親と、その値を継承する子オブジェクトは両方とも、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> である必要があり、両方とも何らかの論理ツリーの一部である必要があります。 ただし、プロパティの継承をサポートする既存の WPF プロパティの場合は、論理ツリーに存在しない中間オブジェクトを介して、プロパティ値の継承を永続化できます。 これは主に、テンプレート化されたインスタンスで設定されている継承されたプロパティ値、またはページ レベル構成の (したがって論理ツリーでの) より高いレベルで設定されている継承されたプロパティ値を、テンプレートの要素で使用する場合に関連します。 このような境界を越えてプロパティ値の継承が一貫して機能するには、継承プロパティを添付プロパティとして登録する必要があります。また、プロパティの継承動作でカスタム依存関係プロパティを定義する場合は、このパターンに従う必要があります。 プロパティの継承に使用される正確なツリーは、実行時でも、ヘルパー クラスのユーティリティ メソッドで完全に予想することはできません。 詳細については、「[プロパティ値の継承](property-value-inheritance.md)」を参照してください。  
  
<a name="two_trees"></a>
## <a name="the-visual-tree"></a>ビジュアル ツリー  
 論理ツリーの概念に加えて、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] にはビジュアル ツリーの概念もあります。 ビジュアル ツリーには、<xref:System.Windows.Media.Visual> の基底クラスによって表されるビジュアル オブジェクトの構造が記述されています。 コントロールのテンプレートを作成するときは、そのコントロールに適用されるビジュアル ツリーを定義または再定義します。 また、ビジュアル ツリーは、パフォーマンスと最適化のために描画を低レベルで制御したい開発者にとっても重要です。 従来の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション プログラミングの一部としてビジュアル ツリーが使用される場合の 1 つとして、ルーティング イベントのイベント ルートは、論理ツリーではなく、ほとんどの場合、ビジュアル ツリーに沿って移動します。 この微妙なルーティング イベントの動作は、コントロールの作成者でない限り、すぐにはわからない場合があります。 ビジュアル ツリーを通したイベントのルーティングにより、ビジュアル レベルでコンポジションを実装するコントロールで、イベントを処理したり、イベント セッターを作成したりできます。  
  
<a name="trees_content"></a>
## <a name="trees-content-elements-and-content-hosts"></a>ツリー、コンテンツ要素、コンテンツ ホスト  
 コンテンツ要素 (<xref:System.Windows.ContentElement> の派生クラス) は、ビジュアル ツリーの一部ではありません。これらは、<xref:System.Windows.Media.Visual> を継承せず、ビジュアル表現も持ちません。 UI に表示されるようにするには、<xref:System.Windows.Media.Visual> であり論理ツリーに含まれるコンテンツ ホストで、<xref:System.Windows.ContentElement> をホストする必要があります。 通常、このようなオブジェクトは <xref:System.Windows.FrameworkElement> です。 コンテンツ ホストはコンテンツに対する "ブラウザー" のようなものであり、ホストが制御する画面領域内にそのコンテンツを表示する方法を選択すると考えることができます。 コンテンツがホストされているときは、通常はビジュアル ツリーに関連付けられる特定のツリー プロセスに、コンテンツを参加させることができます。 一般に、<xref:System.Windows.FrameworkElement> ホスト クラスには、ホストされているコンテンツが真のビジュアル ツリーの一部ではない場合でも、ホストされている <xref:System.Windows.ContentElement> をコンテンツの論理ツリーのサブノードを介してイベント ルートに追加する実装コードが含まれています。 これは、<xref:System.Windows.ContentElement> がそれ自体以外の任意の要素にルーティングされるルーティング イベントを送信できるようにするために必要です。  
  
<a name="tree_traversal"></a>
## <a name="tree-traversal"></a>ツリー トラバーサル  
 <xref:System.Windows.LogicalTreeHelper> クラスでは、論理ツリーのトラバーサル用に <xref:System.Windows.LogicalTreeHelper.GetChildren%2A>、<xref:System.Windows.LogicalTreeHelper.GetParent%2A>、<xref:System.Windows.LogicalTreeHelper.FindLogicalNode%2A> の各メソッドが提供されています。 ほとんどの場合、既存のコントロールの論理ツリーをトラバースする必要はありません。これらのコントロールでは、ほとんどの場合、論理的な子要素が、`Add` やインデクサーなどのコレクション アクセスをサポートする専用のコレクション プロパティとして公開されるためです。 ツリー トラバーサルは、主に、コレクション プロパティが既に定義されていて <xref:System.Windows.Controls.ItemsControl> や <xref:System.Windows.Controls.Panel> などの目的のコントロール パターンからの派生を行わず、独自のコレクション プロパティのサポートを提供することを、コントロールの作成者が選択した場合に使用されるシナリオです。  
  
 ビジュアル ツリーでは、ビジュアル ツリー トラバーサル用のヘルパー クラス <xref:System.Windows.Media.VisualTreeHelper> もサポートされています。 ビジュアル ツリーは、コントロール固有のプロパティによって使いやすく公開されないため、プログラミングのシナリオでビジュアル ツリーをトラバースする必要がある場合は、<xref:System.Windows.Media.VisualTreeHelper> クラスが推奨される手段です。 詳しくは、「[WPF グラフィックス レンダリングの概要](../graphics-multimedia/wpf-graphics-rendering-overview.md)」をご覧ください。  
  
> [!NOTE]
> 適用されているテンプレートのビジュアル ツリーを調べることが必要になる場合があります。 この手法を使用する場合は注意が必要です。 自分でテンプレートを定義しているコントロールのビジュアル ツリーをトラバースする場合でも、コントロールの使用者はいつでもインスタンスの <xref:System.Windows.Controls.Control.Template%2A> プロパティを設定することによってテンプレートを変更することができ、エンド ユーザーでさえ、システムのテーマを変更することによって、適用されるテンプレートに影響を与えることができます。  
  
<a name="routes"></a>
## <a name="routes-for-routed-events-as-a-tree"></a>"ツリー" としてのルーティング イベントのルート  
 前に説明したように、特定のルーティング イベントのルートは、ビジュアル ツリーと論理ツリーの表現のハイブリッドである、ツリーの単一の事前定義されたパスに沿って移動します。 イベント ルートは、ルーティング イベントのトンネルかバブルかに応じて、ツリー内を上方または下方に移動できます。 イベント ルートの概念では、実際にルーティングするイベントを発生させずにイベント ルートを "移動" するために使用できるヘルパー クラスは直接サポートされていません。 ルートを表すクラス <xref:System.Windows.EventRoute> はありますが、そのクラスのメソッドは一般に内部でのみ使用されます。  
  
<a name="resourcesandtrees"></a>
## <a name="resource-dictionaries-and-trees"></a>リソース ディクショナリとツリー  
 ページで定義されているすべての `Resources` に対するリソース ディクショナリの参照では、基本的に論理ツリーがトラバースされます。 論理ツリーに含まれていないオブジェクトでは、キー付きリソースを参照できますが、リソース参照シーケンスは、そのオブジェクトが論理ツリーに接続されているポイントから開始されます。 WPF では、論理ツリーのノードだけが <xref:System.Windows.ResourceDictionary> を含む `Resources` プロパティを持つことができるため、<xref:System.Windows.ResourceDictionary> からキー付きリソースを探してビジュアル ツリーをトラバースする利点はありません。  
  
 ただし、リソースの検索は、直接の論理ツリーの範囲を超えて拡張することもできます。 アプリケーション マークアップの場合、リソースの検索をアプリケーション レベルのリソース ディクショナリまで続け、次に、静的なプロパティまたはキーとして参照されるテーマのサポートとシステム値まで進めることができます。 また、リソース参照が動的である場合は、テーマ自体で、テーマの論理ツリーの外側にあるシステム値を参照することもできます。 リソース ディクショナリと参照ロジックの詳細については、[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
## <a name="see-also"></a>関連項目

- [入力の概要](input-overview.md)
- [WPF グラフィックス レンダリングの概要](../graphics-multimedia/wpf-graphics-rendering-overview.md)
- [ルーティング イベントの概要](routed-events-overview.md)
- [オブジェクト ツリーに存在しないオブジェクト要素の初期化](initialization-for-object-elements-not-in-an-object-tree.md)
- [WPF アーキテクチャ](wpf-architecture.md)
