---
title: GridView の概要
ms.date: 03/30/2017
helpviewer_keywords:
- GridView view mode [WPF]
- ListView controls [WPF], GridView view mode
- controls [WPF], ListView
ms.assetid: b2d02267-32b3-40ce-8e9f-06972d8749d9
ms.openlocfilehash: 98bc7985172cabeab19469af4b4c21e13a6bce73
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79181901"
---
# <a name="gridview-overview"></a>GridView の概要
<xref:System.Windows.Controls.GridView> ビュー モードは、<xref:System.Windows.Controls.ListView> コントロールのビュー モードの 1 つです。 <xref:System.Windows.Controls.GridView> クラスおよびそのサポート クラスでは、通常、ボタンを対話型の列ヘッダーとして使用するテーブルに項目のコレクションを表示できます。 このトピックでは、<xref:System.Windows.Controls.GridView> クラスをご紹介し、その用途の概要をご説明します。  

<a name="DefiningaListViewthatusesGridViewView"></a>
## <a name="what-is-a-gridview-view"></a>GridView のビューとは?  
 <xref:System.Windows.Controls.GridView> ビュー モードでは、データ フィールドを列にバインドして、列ヘッダーを表示してそのフィールドを識別することによってデータ項目の一覧を表示します。 既定値の <xref:System.Windows.Controls.GridView> スタイルでは、ボタンを列ヘッダーとして実装します。 列ヘッダーにボタンを使用することで、重要なユーザー対話機能を実装することができます。たとえば、ユーザーは列ヘッダーをクリックして、その列の内容に従って <xref:System.Windows.Controls.GridView> データを並べ替えることができます。  
  
> [!NOTE]
> <xref:System.Windows.Controls.GridView> が列ヘッダーに使用するボタン コントロールは、<xref:System.Windows.Controls.Primitives.ButtonBase> から得られます。  
  
 次の図は、<xref:System.Windows.Controls.ListView> コンテンツの <xref:System.Windows.Controls.GridView> ビューを示したものです。  

 ![ListView コンテンツの GridView ビューを示すスクリーンショット。](./media/gridview-overview/styled-listview-content.png)  
  
 <xref:System.Windows.Controls.GridView> 列は <xref:System.Windows.Controls.GridViewColumn> オブジェクトによって表され、そのサイズはコンテンツに合わせて自動的に調整できます。 必要に応じて、<xref:System.Windows.Controls.GridViewColumn> の幅を明示的に設定することもできます。 列のサイズは、列ヘッダー間のグリッパーをドラッグすることで変更できます。 また、列は動的に追加、削除、置換、順序変更することもできます。これは、これらの動的機能が <xref:System.Windows.Controls.GridView> に組み込まれているためです。 ただし、<xref:System.Windows.Controls.GridView> は、それが表示するデータを直接には更新できません。  
  
 次の例では、従業員データを表示する <xref:System.Windows.Controls.GridView> を定義する方法を説明します。 この例では、<xref:System.Windows.Controls.ListView> で `EmployeeInfoDataSource` が <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> と定義されています。 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> のプロパティ定義により、<xref:System.Windows.Controls.GridViewColumn> コンテンツが `EmployeeInfoDataSource` のデータ区分にバインドされます。  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 次の図は、前の例により作成されるテーブルを示しています。 GridView コントロールには、ItemsSource オブジェクトからのデータが表示します。

 ![GridView の出力が表示された ListView のスクリーンショット。](./media/gridview-overview/listview-gridview-output.jpg)  
  
<a name="GridViewLayoutandStyle"></a>
## <a name="gridview-layout-and-style"></a>GridView のレイアウトとスタイル  
 <xref:System.Windows.Controls.GridViewColumn> の列セルと列ヘッダーの幅は同じです。 既定では、各列の幅がコンテンツに合わせて調整されます。 列を固定幅に設定することもできます。  
  
 関連するデータのコンテンツは水平方向の行に表示されます。 たとえば前の図では、各従業員の姓と名と ID 番号が横一列に並ぶため 1 つのセットとして表示されています。  
  
<a name="DefiningandStylingColumnsinaGridView"></a>
### <a name="defining-and-styling-columns-in-a-gridview"></a>GridView の列の定義およびスタイル設定  
 <xref:System.Windows.Controls.GridViewColumn> に表示するデータ フィールドを定義するときには、<xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> プロパティ、<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> プロパティ、または <xref:System.Windows.Controls.GridViewColumn.CellTemplateSelector%2A> プロパティを使用します。 <xref:System.Windows.Controls.GridViewColumn.DisplayMemberBinding%2A> プロパティはいずれのテンプレート プロパティよりも優先されます。  
  
 <xref:System.Windows.Controls.GridView>の列のコンテンツの配置を指定するには、<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> を定義します。 <xref:System.Windows.Controls.GridView> を使用して表示される <xref:System.Windows.Controls.ListView> コンテンツには、<xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> プロパティと <xref:System.Windows.Controls.Control.VerticalContentAlignment%2A> プロパティを使用しないでください。  
  
 列ヘッダーのテンプレートとスタイルのプロパティを指定するには、<xref:System.Windows.Controls.GridView> クラスと <xref:System.Windows.Controls.GridViewColumn> クラスと <xref:System.Windows.Controls.GridViewColumnHeader> クラスを使用します。 詳細については、[GridView の列ヘッダーのスタイルとテンプレートの概要](gridview-column-header-styles-and-templates-overview.md)を参照してください。  
  
<a name="AddingVisualElementstoaGridViewView"></a>
### <a name="adding-visual-elements-to-a-gridview"></a>GridView への視覚的要素の追加  
 <xref:System.Windows.Controls.CheckBox> コントロールや <xref:System.Windows.Controls.Button> コントロールなどといった視覚的要素を <xref:System.Windows.Controls.GridView> ビュー モードに追加するには、テンプレートまたはスタイルを使用します。  
  
 視覚的要素をデータ項目として明示的に定義する場合、<xref:System.Windows.Controls.GridView> でそれを 1 回だけ表示できます。 この制限が存在する理由は 1 つの要素は 1 つの親しか持てないためです。したがって視覚的要素をビジュアル ツリーに 1 回だけ表示できます。  
  
<a name="StylingRowsinaGridViewView"></a>
### <a name="styling-rows-in-a-gridview"></a>GridView での行のスタイル設定  
 <xref:System.Windows.Controls.GridViewRowPresenter> クラスと <xref:System.Windows.Controls.GridViewHeaderRowPresenter> クラスを使用して、<xref:System.Windows.Controls.GridView> の行の書式設定と表示を行います。 <xref:System.Windows.Controls.GridView> ビュー モードの行のスタイル設定方法については、「[GridView を実装する ListView で行のスタイルを設定する](how-to-style-a-row-in-a-listview-that-implements-a-gridview.md)」を参照してください。  
  
<a name="AlignmentIssuesWhenUsingItemContainerStyle"></a>
### <a name="alignment-issues-when-you-use-itemcontainerstyle"></a>ItemContainerStyle 使用時の配置問題  
 列ヘッダーとセルの配置の問題を防ぐには、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> 内の項目の幅に影響するプロパティの設定や、そのようなテンプレートの指定は行わないでください。 たとえば、<xref:System.Windows.Controls.ListView> コントロールで定義されている <xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> に <xref:System.Windows.Controls.CheckBox> を追加する <xref:System.Windows.FrameworkElement.Margin%2A> プロパティの設定や、そのような <xref:System.Windows.Controls.ControlTemplate> の指定は行わないでください。 代わりに、<xref:System.Windows.Controls.GridView> ビュー モードを定義するクラスの列幅に直接影響を与えるプロパティとテンプレートを指定します。  
  
 たとえば、<xref:System.Windows.Controls.CheckBox> を <xref:System.Windows.Controls.GridView> ビュー モードの行に追加するには、<xref:System.Windows.Controls.CheckBox> を <xref:System.Windows.DataTemplate> に追加した上で、<xref:System.Windows.Controls.GridViewColumn.CellTemplate%2A> プロパティをその <xref:System.Windows.DataTemplate> に設定します。  
  
<a name="InteractingwithaGridViewControl"></a>
## <a name="user-interactions-with-a-gridview"></a>ユーザーによる GridView の操作  
 アプリケーションで <xref:System.Windows.Controls.GridView> を使用すると、ユーザーは <xref:System.Windows.Controls.GridView> の操作やフォーマット変更を実行できます。 たとえばユーザーは、列の順序の変更、列のサイズの変更、テーブルのアイテムの選択、コンテンツのスクロールを実行できます。 ユーザーが列ヘッダーのボタンをクリックしたときに応答するイベント ハンドラーを定義することもできます。 イベント ハンドラーは、列の内容に合わせて <xref:System.Windows.Controls.GridView> に表示されるデータを並べ替えるなどの処理を実行できます。  
  
 次のリストに、<xref:System.Windows.Controls.GridView> を使用したユーザー操作の機能についてさらに詳しく説明されています。  
  
- **ドラッグ アンド ドロップで列の順序を変更する**  
  
     ユーザーはマウスの左ボタンを押して <xref:System.Windows.Controls.GridView> の列の順序を変更できます。列ヘッダーの上にカーソルを移動させて対象の列を新しい位置にドラッグします。 ユーザーが列ヘッダーをドラッグしている間、そのヘッダーの浮動バージョンと、列を挿入する場所を示す黒い実線が表示されます。  
  
     ヘッダーの浮動バージョンの既定スタイルを変更したい場合は、<xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> プロパティが <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating> に設定されているときにトリガーされる <xref:System.Windows.Controls.GridViewColumnHeader> タイプの <xref:System.Windows.Controls.ControlTemplate> を指定します。 詳細については、[ドラッグした GridView 列ヘッダーのスタイルを作成する](how-to-create-a-style-for-a-dragged-gridview-column-header.md)を参照してください。  
  
- **内容に合わせて列のサイズを変更する**  
  
     ユーザーは列ヘッダーの右側にあるグリッパーをダブルクリックすると、内容に合わせて列のサイズを変更できます。  
  
    > [!NOTE]
    > <xref:System.Windows.Controls.GridViewColumn.Width%2A> プロパティを `Double.NaN` に設定すると同じ効果が得られます。  
  
- **行の項目を選択する**  
  
     ユーザーは <xref:System.Windows.Controls.GridView> の 1 つまたは複数の項目を選択できます。  
  
     選択した項目の <xref:System.Windows.Style> を変更したい場合には、「[トリガーを使用して、ListView で選択された項目のスタイルを設定する](how-to-use-triggers-to-style-selected-items-in-a-listview.md)」を参照してください。  
  
- **スクロールして画面に表示されていない内容を表示する**  
  
     すべての項目を表示するには <xref:System.Windows.Controls.GridView> のサイズが小さい場合、ユーザーは <xref:System.Windows.Controls.ScrollViewer> コントロールにより提供されるスクロールバーを使用すれば縦横にスクロールできます。 すべての内容が特定の方向で表示されると、<xref:System.Windows.Controls.Primitives.ScrollBar> は表示されません。 列ヘッダーは、垂直スクロール バーでのスクロール操作ではなく水平方向のスクロール操作を行います。  
  
- **列ヘッダーのボタンをクリックして列を操作する**  
  
     ユーザーは並べ替えアルゴリズムを指定しておけば、列ヘッダーのボタンをクリックして列に表示されているデータを並べ替えることができます。  
  
     列ヘッダーボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理して、並べ替えアルゴリズムなどの機能を提供することができます。 1 つの列ヘッダーの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理するには、<xref:System.Windows.Controls.GridViewColumnHeader> でイベント ハンドラーを設定します。 すべての列ヘッダーに対して <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理するようにイベント ハンドラーを設定するには、<xref:System.Windows.Controls.ListView> コントロールにそのハンドラーを設定します。  
  
<a name="Obtaining_Other_Custom_Views"></a>
## <a name="obtaining-other-custom-views"></a>その他のカスタム ビューの取得  
 <xref:System.Windows.Controls.GridView> クラスは、<xref:System.Windows.Controls.ViewBase> 抽象クラスから派生しており、<xref:System.Windows.Controls.ListView> クラスに使用できるビュー モードの 1 つです。 <xref:System.Windows.Controls.ViewBase> クラスから派生させることで、<xref:System.Windows.Controls.ListView> に対して別のカスタム ビューを作成できます。 カスタム ビュー モードの例については、[ListView のカスタム ビュー モードを作成する](how-to-create-a-custom-view-mode-for-a-listview.md)を参照してください。  
  
<a name="GridViewSupportingClasses"></a>
## <a name="gridview-supporting-classes"></a>GridViewサポート クラス  
 次のクラスは <xref:System.Windows.Controls.GridView> ビュー モードをサポートしています。  
  
- <xref:System.Windows.Controls.GridViewColumn>  
  
- <xref:System.Windows.Controls.GridViewColumnHeader>  
  
- <xref:System.Windows.Controls.GridViewRowPresenter>  
  
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>  
  
- <xref:System.Windows.Controls.GridViewColumnCollection>  
  
- <xref:System.Windows.Controls.GridViewColumnHeaderRole>  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.ListViewItem>
- <xref:System.Windows.Controls.GridViewColumn>
- <xref:System.Windows.Controls.GridViewColumnHeader>
- <xref:System.Windows.Controls.GridViewRowPresenter>
- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
- <xref:System.Windows.Controls.ViewBase>
- [ListView の概要](listview-overview.md)
- [ヘッダーがクリックされたときに GridView 列を並べ替える](how-to-sort-a-gridview-column-when-a-header-is-clicked.md)
- [方法トピック](listview-how-to-topics.md)
