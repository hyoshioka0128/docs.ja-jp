---
title: コンテンツ モデル
ms.date: 03/30/2017
helpviewer_keywords:
- UIElement class [WPF], displaying content
- content model [WPF], controls
- controls [WPF], displaying text
- content display [WPF], controls
- controls [WPF], formatting text
- displaying content [WPF]
- arbitrary content classes [WPF], content model
- ContentControl class [WPF], displaying content
ms.assetid: 214da5ef-547a-4cf8-9b07-4aa8a0e52cdd
ms.openlocfilehash: ec4e96c0883489135b77f09a3c19f144cb4d30bc
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187405"
---
# <a name="wpf-content-model"></a>WPF のコンテンツ モデル
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、多くのコントロールやコントロールのような型を提供する表示プラットフォームで、その主な目的は、異なる種類のコンテンツを表示することです。 使用するコントロールまたは派生元のコントロールを判断するには、特定のコントロールが最適に表示できるオブジェクトの種類を理解する必要があります。  
  
 このトピックは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールとコントロールのような型に関するコンテンツ モデルのまとめです。 コンテンツ モデルは、どのようなコンテンツをコントロールで使用できるかについて説明します。 このトピックは、各コンテンツ モデルのコンテンツのプロパティもリストします。 コンテンツのプロパティは、オブジェクトのコンテンツの格納に使用されるプロパティです。  

<a name="classes_that_contain_arbitrary_content"></a>
## <a name="classes-that-contain-arbitrary-content"></a>任意のコンテンツを含むクラス  
 一部のコントロールには、文字列、<xref:System.DateTime> オブジェクト、追加項目のコンテナーである <xref:System.Windows.UIElement> など、任意の型のオブジェクトを含めることができます。 たとえば、<xref:System.Windows.Controls.Button> には、1 つの画像といくつかのテキストを含めることができます。また、<xref:System.Windows.Controls.CheckBox> には、<xref:System.DateTime.Now%2A?displayProperty=nameWithType> の値を含めることができます。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、任意のコンテンツを含めることができる 4 つのクラスがあります。 次の表では、<xref:System.Windows.Controls.Control> を継承するクラスの一覧を示します。  
  
|任意のコンテンツを含むクラス|Content|  
|-------------------------------------------|-------------|  
|<xref:System.Windows.Controls.ContentControl>|1 つの任意のオブジェクト。|  
|<xref:System.Windows.Controls.HeaderedContentControl>|ヘッダーと 1 つの項目。両方とも任意のオブジェクトです。|  
|<xref:System.Windows.Controls.ItemsControl>|任意のオブジェクトのコレクション。|  
|<xref:System.Windows.Controls.HeaderedItemsControl>|ヘッダーと項目のコレクション。すべて任意のオブジェクトです。|  
  
 これらのクラスから継承するコントロールは、同じ種類のコンテンツを格納でき、同じ方法でコンテンツを処理することができます。 次の図では、画像とテキストを含む各コンテンツ モデルの 1 つのコントロールを示します。  
  
 ![各コンテンツ モデルから 1 つずつ、4 つの異なるコントロールを示すスクリーンショット。](./media/wpf-content-model/control-content-model-image-text.png)  
  
### <a name="controls-that-contain-a-single-arbitrary-object"></a>任意の 1 つのオブジェクトを格納しているコントロール  
 <xref:System.Windows.Controls.ContentControl> クラスには、任意のコンテンツが 1 つ含まれます。 そのコンテンツ プロパティは <xref:System.Windows.Controls.ContentControl.Content%2A> です。 次のコントロールでは <xref:System.Windows.Controls.ContentControl> が継承され、そのコンテンツ モデルが使用されます。  
  
- <xref:System.Windows.Controls.Button>  
  
- <xref:System.Windows.Controls.Primitives.ButtonBase>  
  
- <xref:System.Windows.Controls.CheckBox>  
  
- <xref:System.Windows.Controls.ComboBoxItem>  
  
- <xref:System.Windows.Controls.ContentControl>  
  
- <xref:System.Windows.Controls.Frame>  
  
- <xref:System.Windows.Controls.GridViewColumnHeader>  
  
- <xref:System.Windows.Controls.GroupItem>  
  
- <xref:System.Windows.Controls.Label>  
  
- <xref:System.Windows.Controls.ListBoxItem>  
  
- <xref:System.Windows.Controls.ListViewItem>  
  
- <xref:System.Windows.Navigation.NavigationWindow>  
  
- <xref:System.Windows.Controls.RadioButton>  
  
- <xref:System.Windows.Controls.Primitives.RepeatButton>  
  
- <xref:System.Windows.Controls.ScrollViewer>  
  
- <xref:System.Windows.Controls.Primitives.StatusBarItem>  
  
- <xref:System.Windows.Controls.Primitives.ToggleButton>  
  
- <xref:System.Windows.Controls.ToolTip>  
  
- <xref:System.Windows.Controls.UserControl>  
  
- <xref:System.Windows.Window>  
  
 次の図では、<xref:System.Windows.Controls.ContentControl.Content%2A> が文字列、<xref:System.DateTime> オブジェクト、<xref:System.Windows.Shapes.Rectangle>、および <xref:System.Windows.Shapes.Ellipse> と <xref:System.Windows.Controls.TextBlock> が含まれる <xref:System.Windows.Controls.Panel> に設定されている 4 つのボタンを示します。  
  
 ![コンテンツの種類が異なる 4 つのボタンを示すスクリーンショット。](./media/wpf-content-model/control-content-model-buttons.png)  
  
 <xref:System.Windows.Controls.ContentControl.Content%2A> プロパティを設定する方法の例については、<xref:System.Windows.Controls.ContentControl> を参照してください。  
  
### <a name="controls-that-contain-a-header-and-a-single-arbitrary-object"></a>ヘッダーと任意の 1 つのオブジェクトを格納しているコントロール  
 <xref:System.Windows.Controls.HeaderedContentControl> クラスでは <xref:System.Windows.Controls.ContentControl> が継承され、ヘッダー付きのコンテンツが表示されます。 コンテンツ プロパティ <xref:System.Windows.Controls.ContentControl.Content%2A> は <xref:System.Windows.Controls.ContentControl> から継承され、<xref:System.Object> 型の <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> プロパティが定義されています。したがって、どちらも任意のオブジェクトにできます。  
  
 次のコントロールでは <xref:System.Windows.Controls.HeaderedContentControl> が継承され、そのコンテンツ モデルが使用されます。  
  
- <xref:System.Windows.Controls.Expander>  
  
- <xref:System.Windows.Controls.GroupBox>  
  
- <xref:System.Windows.Controls.TabItem>  
  
 次の図には、2 つの <xref:System.Windows.Controls.TabItem> オブジェクトが示されています。 1 つ目の <xref:System.Windows.Controls.TabItem> では、<xref:System.Windows.Controls.HeaderedContentControl.Header%2A> および <xref:System.Windows.Controls.ContentControl.Content%2A> として <xref:System.Windows.UIElement> オブジェクトが使用されています。 <xref:System.Windows.Controls.HeaderedContentControl.Header%2A> は、<xref:System.Windows.Shapes.Ellipse> と <xref:System.Windows.Controls.TextBlock> が含まれる <xref:System.Windows.Controls.StackPanel> に設定されています。 <xref:System.Windows.Controls.ContentControl.Content%2A> は、<xref:System.Windows.Controls.TextBlock> と <xref:System.Windows.Controls.Label> が含まれる <xref:System.Windows.Controls.StackPanel> に設定されています。 2 つ目の <xref:System.Windows.Controls.TabItem> は、<xref:System.Windows.Controls.HeaderedContentControl.Header%2A> が文字列で、<xref:System.Windows.Controls.ContentControl.Content%2A> が <xref:System.Windows.Controls.TextBlock> です。  
  
 ![Header プロパティで異なる型が使用されている TabControl。](./media/wpf-content-model/control-content-model-tab.png)  
  
 <xref:System.Windows.Controls.TabItem> オブジェクトを作成する方法の例については、<xref:System.Windows.Controls.HeaderedContentControl> を参照してください。  
  
### <a name="controls-that-contain-a-collection-of-arbitrary-objects"></a>任意のオブジェクトのコレクションを格納しているコントロール  
 <xref:System.Windows.Controls.ItemsControl> クラスでは <xref:System.Windows.Controls.Control> が継承され、文字列、オブジェクト、その他の要素など、複数の項目を含めることができます。 そのコンテンツ プロパティは、<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> と <xref:System.Windows.Controls.ItemsControl.Items%2A> です。 <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> は通常、<xref:System.Windows.Controls.ItemsControl> にデータ コレクションを設定するために使用されます。 <xref:System.Windows.Controls.ItemsControl> にコレクションを設定したくない場合は、<xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティを使用して項目を追加できます。  
  
 次のコントロールでは <xref:System.Windows.Controls.ItemsControl> が継承され、そのコンテンツ モデルが使用されます。  
  
- <xref:System.Windows.Controls.Menu>  
  
- <xref:System.Windows.Controls.Primitives.MenuBase>  
  
- <xref:System.Windows.Controls.ContextMenu>  
  
- <xref:System.Windows.Controls.ComboBox>  
  
- <xref:System.Windows.Controls.ItemsControl>  
  
- <xref:System.Windows.Controls.ListBox>  
  
- <xref:System.Windows.Controls.ListView>  
  
- <xref:System.Windows.Controls.TabControl>  
  
- <xref:System.Windows.Controls.TreeView>  
  
- <xref:System.Windows.Controls.Primitives.Selector>  
  
- <xref:System.Windows.Controls.Primitives.StatusBar>  
  
 次の図では、以下の種類の項目が含まれる <xref:System.Windows.Controls.ListBox> を示します。  
  
- 文字列。  
  
- <xref:System.DateTime> オブジェクト。  
  
- <xref:System.Windows.UIElement>。  
  
- <xref:System.Windows.Shapes.Ellipse> と <xref:System.Windows.Controls.TextBlock> が格納されている <xref:System.Windows.Controls.Panel>。  
  
 ![4 種類のコンテンツが含まれる ListBox を示すスクリーンショット。](./media/wpf-content-model/control-content-model-listbox.png)  
  
### <a name="controls-that-contain-a-header-and-a-collection-of-arbitrary-objects"></a>ヘッダーと任意のオブジェクトのコレクションを含むコントロール  
 <xref:System.Windows.Controls.HeaderedItemsControl> クラスでは <xref:System.Windows.Controls.ItemsControl> が継承され、文字列、オブジェクト、その他の要素やヘッダーなど、複数の項目を含めることができます。 <xref:System.Windows.Controls.ItemsControl> のコンテンツ プロパティ、<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>、<xref:System.Windows.Controls.ItemsControl.Items%2A> が継承され、任意のオブジェクトを使用できる <xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> プロパティが定義されています。  
  
 次のコントロールでは <xref:System.Windows.Controls.HeaderedItemsControl> が継承され、そのコンテンツ モデルが使用されます。  
  
- <xref:System.Windows.Controls.MenuItem>  
  
- <xref:System.Windows.Controls.ToolBar>  
  
- <xref:System.Windows.Controls.TreeViewItem>  
  
<a name="classes_that_contain_a_collection_of_uielement_objects"></a>
## <a name="classes-that-contain-a-collection-of-uielement-objects"></a>UIElement オブジェクトのコレクションを含むクラス  
 <xref:System.Windows.Controls.Panel> クラスでは、子の <xref:System.Windows.UIElement> オブジェクトが配置されて調整されます。 そのコンテンツ プロパティは <xref:System.Windows.Controls.Panel.Children%2A> です。  
  
 次のクラスでは <xref:System.Windows.Controls.Panel> クラスが継承され、そのコンテンツ モデルが使用されています。  
  
- <xref:System.Windows.Controls.Canvas>  
  
- <xref:System.Windows.Controls.DockPanel>  
  
- <xref:System.Windows.Controls.Grid>  
  
- <xref:System.Windows.Controls.Primitives.TabPanel>  
  
- <xref:System.Windows.Controls.Primitives.ToolBarOverflowPanel>  
  
- <xref:System.Windows.Controls.Primitives.ToolBarPanel>  
  
- <xref:System.Windows.Controls.Primitives.UniformGrid>  
  
- <xref:System.Windows.Controls.StackPanel>  
  
- <xref:System.Windows.Controls.VirtualizingPanel>  
  
- <xref:System.Windows.Controls.VirtualizingStackPanel>  
  
- <xref:System.Windows.Controls.WrapPanel>  
  
 詳細については、「[Panels Overview](panels-overview.md)」を参照してください。  
  
<a name="classes_that_affects_the_appearance_of_a_uielement"></a>
## <a name="classes-that-affect-the-appearance-of-a-uielement"></a>UIElement の外観に影響を与えるクラス  
 <xref:System.Windows.Controls.Decorator> クラスでは、1 つの子 <xref:System.Windows.UIElement> またはその周囲に対して視覚効果が適用されます。 そのコンテンツ プロパティは <xref:System.Windows.Controls.Decorator.Child%2A> です。 次のクラスでは <xref:System.Windows.Controls.Decorator> が継承され、そのコンテンツ モデルが使用されます。  
  
- <xref:System.Windows.Documents.AdornerDecorator>  
  
- <xref:System.Windows.Controls.Border>  
  
- <xref:System.Windows.Controls.Primitives.BulletDecorator>  
  
- <xref:Microsoft.Windows.Themes.ButtonChrome>  
  
- <xref:Microsoft.Windows.Themes.ClassicBorderDecorator>  
  
- <xref:System.Windows.Controls.InkPresenter>  
  
- <xref:Microsoft.Windows.Themes.ListBoxChrome>  
  
- <xref:Microsoft.Windows.Themes.SystemDropShadowChrome>  
  
- <xref:System.Windows.Controls.Viewbox>  
  
 次の図では、周囲に <xref:System.Windows.Controls.Border> が使用されている (修飾されている) <xref:System.Windows.Controls.TextBox> を示します。  
  
 ![境界線が黒の TextBox](./media/layout-border-around-textbox.png "Layout_Border_around_TextBox")  
境界がある TextBlock  
  
<a name="classes_that_provides_visual_feedback_about_a_uielement"></a>
## <a name="classes-that-provide-visual-feedback-about-a-uielement"></a>UIElement についての視覚的なフィードバックを提供するクラス  
 <xref:System.Windows.Documents.Adorner> クラスでは、ユーザーに視覚的手掛かりが提供されます。 たとえば、要素に機能ハンドルを追加したり、コントロールに関する状態情報を提供したりするために、<xref:System.Windows.Documents.Adorner> を使用します。 <xref:System.Windows.Documents.Adorner> クラスでは、独自の装飾を作成できるように、フレームワークが提供されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は実装された装飾は提供しません。 詳しくは、[Adorners Overview](adorners-overview.md)をご覧ください。  
  
<a name="classes_that_enable_users_to_enter_text"></a>
## <a name="classes-that-enable-users-to-enter-text"></a>ユーザーがテキストを入力できるようにするクラス  
 WPF は、ユーザーがテキストを入力できるようにする 3 つの主なコントロールを提供します。 各コントロールは、異なる方法で、テキストを表示します。 次の表は、これら 3 つのテキスト関連のコントロール、テキストを表示するときのそれぞれの機能、およびコントロールのテキストを格納するそれぞれのプロパティの一覧です。  
  
|Control|テキストの表示形態|コンテンツのプロパティ|  
|-------------|--------------------------|----------------------|  
|<xref:System.Windows.Controls.TextBox>|プレーンテキスト|<xref:System.Windows.Controls.TextBox.Text%2A>|  
|<xref:System.Windows.Controls.RichTextBox>|書式付きテキスト|<xref:System.Windows.Controls.RichTextBox.Document%2A>|  
|<xref:System.Windows.Controls.PasswordBox>|非表示のテキスト (文字はマスクされます)|<xref:System.Windows.Controls.PasswordBox.Password%2A>|  
  
<a name="classes_that_display_text"></a>
## <a name="classes-that-display-your-text"></a>テキストを表示するクラス  
 いくつかのクラスを使用して、プレーン テキストまたは書式設定されたテキストを表示できます。 <xref:System.Windows.Controls.TextBlock> を使用すると、少量のテキストを表示できます。 大量のテキストを表示する場合は、<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、または <xref:System.Windows.Controls.FlowDocumentScrollViewer> のいずれかのコントロールを使用します。  
  
 <xref:System.Windows.Controls.TextBlock> には、<xref:System.Windows.Controls.TextBlock.Text%2A> と <xref:System.Windows.Controls.TextBlock.Inlines%2A> という 2 つのコンテンツ プロパティがあります。 一貫した書式設定を使用するテキストを表示するときの最適な選択肢は、多くの場合 <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティです。 テキスト全体でさまざまな書式設定を使用する場合は、<xref:System.Windows.Controls.TextBlock.Inlines%2A> プロパティを使用します。 <xref:System.Windows.Controls.TextBlock.Inlines%2A> プロパティは、<xref:System.Windows.Documents.Inline> オブジェクトのコレクションであり、テキストを書式設定する方法を指定します。  
  
 次の表は、<xref:System.Windows.Controls.FlowDocumentReader>、<xref:System.Windows.Controls.FlowDocumentPageViewer>、<xref:System.Windows.Controls.FlowDocumentScrollViewer> の各クラスのコンテンツ プロパティの一覧です。  
  
|Control|コンテンツのプロパティ|コンテンツのプロパティの型|  
|-------------|----------------------|---------------------------|  
|<xref:System.Windows.Controls.FlowDocumentPageViewer>|ドキュメント|<xref:System.Windows.Documents.IDocumentPaginatorSource>|  
|<xref:System.Windows.Controls.FlowDocumentReader>|ドキュメント|<xref:System.Windows.Documents.FlowDocument>|  
|<xref:System.Windows.Controls.FlowDocumentScrollViewer>|ドキュメント|<xref:System.Windows.Documents.FlowDocument>|  
  
 <xref:System.Windows.Documents.FlowDocument> では、<xref:System.Windows.Documents.IDocumentPaginatorSource> インターフェイスが実装されています。したがって、3 つのクラスすべてで、コンテンツとして <xref:System.Windows.Documents.FlowDocument> を使用できます。  
  
<a name="classes_that_format_text"></a>
## <a name="classes-that-format-your-text"></a>テキストを書式設定するクラス  
 <xref:System.Windows.Documents.TextElement> とその関連クラスでは、テキストを書式設定できます。 <xref:System.Windows.Documents.TextElement> オブジェクトを使うと、<xref:System.Windows.Controls.TextBlock> オブジェクトと <xref:System.Windows.Documents.FlowDocument> オブジェクトにテキストを格納して書式設定できます。 <xref:System.Windows.Documents.TextElement> オブジェクトの 2 つの主な種類は、<xref:System.Windows.Documents.Block> 要素と <xref:System.Windows.Documents.Inline> 要素です。 <xref:System.Windows.Documents.Block> 要素は、段落やリストなどのテキストのブロックを表します。 <xref:System.Windows.Documents.Inline> 要素は、ブロック内のテキストの一部を表します。 多くの <xref:System.Windows.Documents.Inline> クラスでは、適用対象のテキストの書式が指定されます。 各 <xref:System.Windows.Documents.TextElement> には、独自のコンテンツ モデルがあります。 詳細については、「[TextElement Content Model Overview](../advanced/textelement-content-model-overview.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [詳細設定](../advanced/index.md)
