---
title: データ テンプレートの概要
description: Windows Presentation Foundation (WPF) でデータ プレゼンテーションを定義するデータ テンプレート モデルの柔軟性について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], templates
- binding data [WPF], templates
- templates [WPF], data
- data templates [WPF]
ms.assetid: 0f4d9f8c-0230-4013-bd7b-e8e7fed01b4a
ms.openlocfilehash: 0226085a82cf97ea799a5a2d38e879b239d9b52a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619651"
---
# <a name="data-templating-overview"></a>データ テンプレートの概要
WPF のデータ テンプレート モデルは、データのプレゼンテーションを定義する優れた柔軟性を提供します。 WPF のコントロールには、データ プレゼンテーションのカスタマイズをサポートする組み込み機能があります。 このトピックでは、最初に <xref:System.Windows.DataTemplate> の定義方法を示した後、カスタム ロジックに基づくテンプレートの選択や、階層データの表示のサポートなど、他のデータ テンプレート機能について説明します。

<a name="Prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント
 このトピックは、データ テンプレートの機能に関するものであり、データ バインディングの概念の紹介ではありません。 データ バインディングの基本概念については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」をご覧ください。

 <xref:System.Windows.DataTemplate> はデータのプレゼンテーションに関するものであり、WPF のスタイルおよびテンプレート モデルによって提供される多くの機能の 1 つです。 <xref:System.Windows.Style> を使ってコントロールのプロパティを設定する方法など、WPF のスタイルおよびテンプレート モデルの概要については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」のトピックをご覧ください。

 さらに、`Resources` について理解することが重要です。これは、基本的に、<xref:System.Windows.Style> や <xref:System.Windows.DataTemplate> などのオブジェクトを再利用できるようにするものです。 リソースについて詳しくは、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」をご覧ください。

<a name="DataTemplating_Basic"></a>
## <a name="data-templating-basics"></a>データ テンプレートの基礎

 <xref:System.Windows.DataTemplate> が重要である理由を示すため、データ バインディングの例を見ていきます。 この例では、`Task` オブジェクトのリストにバインドされた <xref:System.Windows.Controls.ListBox> があります。 各 `Task` オブジェクトには `TaskName` (string)、`Description` (string)、`Priority` (int)、および `TaskType` 型のプロパティがあり、これは値が `Home` と `Work` の `Enum` です。

 [!code-xaml[DataTemplatingIntro_snip#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#resources)]
[!code-xaml[DataTemplatingIntro_snip#UI1](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui1)]
[!code-xaml[DataTemplatingIntro_snip#UI2](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#ui2)]

<a name="without_a_datatemplate"></a>
### <a name="without-a-datatemplate"></a>DataTemplate がない場合
 <xref:System.Windows.DataTemplate> がないので、現在の <xref:System.Windows.Controls.ListBox> は次のようになります。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig1.png "DataTemplatingIntro_fig1")

 特定の指示がないと、<xref:System.Windows.Controls.ListBox> では、コレクションのオブジェクトを表示しようとしたときに、既定で `ToString` が呼び出されます。 したがって、`Task` オブジェクトによって `ToString` メソッドがオーバーライドされる場合、<xref:System.Windows.Controls.ListBox> では基になっているコレクションの各ソース オブジェクトの文字列表現が表示されます。

 たとえば、`Task` クラスが `ToString` メソッドを次のようにオーバーライドするものとします。`name` は `TaskName` プロパティのフィールドです。

 [!code-csharp[DataTemplatingIntro_snip#ToString](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Data.cs#tostring)]
 [!code-vb[DataTemplatingIntro_snip#ToString](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/data.vb#tostring)]

 <xref:System.Windows.Controls.ListBox> は次のようになります。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig2.png "DataTemplatingIntro_fig2")

 ただし、これは制限があり、柔軟性ではありません。 また、XML データにバインドしている場合、`ToString` をオーバーライドすることはできません。

<a name="defining_simple_datatemplate"></a>
### <a name="defining-a-simple-datatemplate"></a>簡単な DataTemplate の定義
 解決策は、<xref:System.Windows.DataTemplate> を定義することです。 そのための 1 つの方法として、<xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> プロパティを <xref:System.Windows.DataTemplate> に設定します。 <xref:System.Windows.DataTemplate> で指定したものが、データ オブジェクトの視覚的な構造になります。 次の <xref:System.Windows.DataTemplate> はかなり単純です。 各項目を <xref:System.Windows.Controls.StackPanel> 内の 3 つの <xref:System.Windows.Controls.TextBlock> 要素として表示するように指示しています。 各 <xref:System.Windows.Controls.TextBlock> 要素は、`Task` クラスのプロパティにバインドされています。

 [!code-xaml[DataTemplatingIntro_snip#Inline](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#inline)]

 このトピックの例の基になるデータは、CLR オブジェクトのコレクションです。 XML データにバインドしている場合は、基本的な概念は同じですが、構文がわずかに違います。 たとえば、`Path=TaskName` ではなく、<xref:System.Windows.Data.Binding.XPath%2A> を `@TaskName` に設定します (`TaskName` が XML ノードの属性の場合)。

 今度は、<xref:System.Windows.Controls.ListBox> は次のようになります。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig3.png "DataTemplatingIntro_fig3")

<a name="defining_datatemplate_as_a_resource"></a>
### <a name="creating-the-datatemplate-as-a-resource"></a>リソースとしての DataTemplate の作成
 上の例では、<xref:System.Windows.DataTemplate> をインラインで定義しました。 再利用可能なオブジェクトになるように、リソース セクションで定義する方が一般的です。次に例を示します。

 [!code-xaml[DataTemplatingIntro_snip#R1](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]
[!code-xaml[DataTemplatingIntro_snip#AsResource](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#asresource)]
[!code-xaml[DataTemplatingIntro_snip#R2](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]

 これで、次の例のように、`myTaskTemplate` をリソースとして使用できるようになります。

 [!code-xaml[DataTemplatingIntro_snip#MyTaskTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#mytasktemplate)]

 `myTaskTemplate` はリソースなので、<xref:System.Windows.DataTemplate> 型を受け取るプロパティがある他のコントロールで使うことができます。 上に示したように、<xref:System.Windows.Controls.ListBox> などの <xref:System.Windows.Controls.ItemsControl> オブジェクトの場合は、<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> プロパティです。 <xref:System.Windows.Controls.ContentControl> オブジェクトの場合は、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> プロパティです。

<a name="Styling_DataType"></a>
### <a name="the-datatype-property"></a>DataType プロパティ
 <xref:System.Windows.DataTemplate> クラスには、<xref:System.Windows.Style> クラスの <xref:System.Windows.Style.TargetType%2A> プロパティと非常によく似た <xref:System.Windows.DataTemplate.DataType%2A> プロパティがあります。 したがって、上の例の <xref:System.Windows.DataTemplate> に対して `x:Key` を指定する代わりに、次のように指定できます。

 [!code-xaml[DataTemplatingIntro_snip#DataType](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#datatype)]

 この <xref:System.Windows.DataTemplate> は、すべての `Task` オブジェクトに自動的に適用されます。 この場合、`x:Key` は暗黙的に設定されることに注意してください。 したがって、この <xref:System.Windows.DataTemplate> に `x:Key` 値を割り当てると、暗黙の `x:Key` がオーバーライドされて、<xref:System.Windows.DataTemplate> は自動的に適用されなくなります。

 <xref:System.Windows.Controls.ContentControl> を `Task` オブジェクトのコレクションにバインドしている場合、<xref:System.Windows.Controls.ContentControl> では上の <xref:System.Windows.DataTemplate> は自動的には使用されません。 これは、<xref:System.Windows.Controls.ContentControl> でのバインドが、コレクション全体または個別オブジェクトのどちらにバインドすればいいのかを区別するためにさらに情報を必要とするためです。 <xref:System.Windows.Controls.ContentControl> で <xref:System.Windows.Controls.ItemsControl> 型の選択が追跡されている場合は、<xref:System.Windows.Controls.ContentControl> バインディングの <xref:System.Windows.Data.Binding.Path%2A> プロパティを "`/`" に設定して、ユーザーが現在の項目に関心を持っていることを示すことができます。 この例については、「[コレクションにバインドして選択に基づく情報を表示する](how-to-bind-to-a-collection-and-display-information-based-on-selection.md)」をご覧ください。 そうでない場合は、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> プロパティを設定することにより、<xref:System.Windows.DataTemplate> を明示的に指定する必要があります。

 異なる型のデータ オブジェクトの <xref:System.Windows.Data.CompositeCollection> がある場合、<xref:System.Windows.DataTemplate.DataType%2A> プロパティは特に役に立ちます。 例については、「[CompositeCollection を実装する](how-to-implement-a-compositecollection.md)」をご覧ください。

<a name="adding_more_to_datatemplate"></a>
## <a name="adding-more-to-the-datatemplate"></a>DataTemplate へのその他の追加
 現在、データでは必要な情報が表示されますが、間違いなく改善の余地があります。 <xref:System.Windows.Controls.Border> 要素、<xref:System.Windows.Controls.Grid> 要素、および表示されているデータについて説明するいくつかの <xref:System.Windows.Controls.TextBlock> 要素を追加することで、プレゼンテーションを改善しましょう。

 [!code-xaml[DataTemplatingIntro#AddingMore](~/samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore)]
[!code-xaml[DataTemplatingIntro#AddingMore2](~/samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]

 次のスクリーンショットは、この変更した <xref:System.Windows.DataTemplate> を使用する <xref:System.Windows.Controls.ListBox> を示しています。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig4.png "DataTemplatingIntro_fig4")

 <xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> を <xref:System.Windows.HorizontalAlignment.Stretch> に設定して、項目の幅がスペース全体を占めるようにできます。

 [!code-xaml[DataTemplatingIntro_snip#Stretch](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#stretch)]

 <xref:System.Windows.Controls.Control.HorizontalContentAlignment%2A> プロパティが <xref:System.Windows.HorizontalAlignment.Stretch> に設定されているので、<xref:System.Windows.Controls.ListBox> は次のようになります。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig5.png "DataTemplatingIntro_fig5")

<a name="DataTrigger_to_Apply_Property_Values"></a>
### <a name="use-datatriggers-to-apply-property-values"></a>DataTrigger を使ってプロパティ値を適用する
 現在のプレゼンテーションでは、`Task` が家のタスクか会社のタスクかわかりません。 `Task` オブジェクトには `TaskType` 型の `TaskType` プロパティがあり、これは値が `Home` と `Work` の列挙であることを思い出してください。

 次の例の <xref:System.Windows.DataTrigger> では、`TaskType` プロパティが `TaskType.Home` である場合、`border` という名前の要素の <xref:System.Windows.Controls.Border.BorderBrush%2A> が `Yellow` に設定されます。

 [!code-xaml[DataTemplatingIntro#DT](~/samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#dt)]
[!code-xaml[DataTemplatingIntro#DataTrigger](~/samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#datatrigger)]
[!code-xaml[DataTemplatingIntro#AddingMore2](~/samples/snippets/xaml/VS_Snippets_Wpf/DataTemplatingIntro/xaml/window1.xaml#addingmore2)]

 これで、アプリケーションの表示は次のようになります。 家のタスクは黄色の境界線で、会社のタスクは水色の境界線で示されます。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig6.png "DataTemplatingIntro_fig6")

 この例では、<xref:System.Windows.DataTrigger> では <xref:System.Windows.Setter> を使ってプロパティの値が設定されます。 トリガー クラスには <xref:System.Windows.TriggerBase.EnterActions%2A> および <xref:System.Windows.TriggerBase.ExitActions%2A> プロパティもあり、アニメーションなどのアクションのセットを開始できます。 さらに、複数のデータ バインドされたプロパティ値に基づいて変更を適用できる <xref:System.Windows.MultiDataTrigger> クラスもあります。

 同じ効果を実現できるもう 1 つの方法は、<xref:System.Windows.Controls.Border.BorderBrush%2A> プロパティを `TaskType` プロパティにバインドし、値コンバーターを使って `TaskType` の値に基づく色を返すというものです。 コンバーターを使って上の効果を作成するのは、パフォーマンスに関して若干効率的です。 さらに、独自のコンバーターを作成すると、独自のロジックを提供できるので柔軟性が向上します。 最終的に、どの手法を選ぶかは、シナリオと設定に依存します。 コンバーターを作成する方法については、「<xref:System.Windows.Data.IValueConverter>」をご覧ください。

<a name="what_belongs_in_datatemplate"></a>
### <a name="what-belongs-in-a-datatemplate"></a>DataTemplate に含まれるもの

前の例では、<xref:System.Windows.DataTemplate.Triggers%2A?displayProperty=nameWithType> プロパティを使って <xref:System.Windows.DataTemplate> にトリガーを追加しました。 トリガーの <xref:System.Windows.Setter> では、<xref:System.Windows.DataTemplate> 内にある要素 (<xref:System.Windows.Controls.Border> 要素) のプロパティの値が設定されます。 ただし、`Setters` が関係するプロパティが現在の <xref:System.Windows.DataTemplate> 内にある要素のプロパティではない場合は、<xref:System.Windows.Controls.ListBoxItem> クラスの <xref:System.Windows.Style> を使ってプロパティを設定する方が適切な場合があります (バインドしているコントロールが <xref:System.Windows.Controls.ListBox> である場合)。 たとえば、項目がマウスでポイントされたときに項目の <xref:System.Windows.UIElement.Opacity%2A> の値を <xref:System.Windows.Trigger> でアニメーション化したい場合は、<xref:System.Windows.Controls.ListBoxItem> スタイルの中でトリガーを定義します。 例については、「[Introduction to Styling and Templating Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)」(スタイルとテンプレートのサンプルの概要) をご覧ください。

 一般に、<xref:System.Windows.DataTemplate> は生成される各 <xref:System.Windows.Controls.ListBoxItem> に適用されることに注意してください (実際に適用される方法と場所について詳しくは、「<xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>」のページをご覧ください)。 <xref:System.Windows.DataTemplate> は、データ オブジェクトのプレゼンテーションと外観だけに関係します。 ほとんどの場合、項目が選択されたときの表示や、<xref:System.Windows.Controls.ListBox> での項目のレイアウト方法など、プレゼンテーションの他のすべての部分は、<xref:System.Windows.DataTemplate> の定義には含まれません。 例については、「[ItemsControl のスタイルとテンプレートの設定](#DataTemplating_ItemsControl)」セクションをご覧ください。

<a name="Styling_StyleSelection"></a>
## <a name="choosing-a-datatemplate-based-on-properties-of-the-data-object"></a>データ オブジェクトのプロパティに基づく DataTemplate の選択
 「[DataType プロパティ](#Styling_DataType)」セクションでは、異なるデータ オブジェクトに対して異なるデータ テンプレートを定義できることを説明しました。 これは、異なる型の <xref:System.Windows.Data.CompositeCollection> または異なる型の項目を含むコレクションがある場合に特に便利です。 「[DataTrigger を使ってプロパティ値を適用する](#DataTrigger_to_Apply_Property_Values)」セクションでは、同じ型のデータ オブジェクトのコレクションがある場合は、<xref:System.Windows.DataTemplate> を作成し、トリガーを使って各データ オブジェクトのプロパティ値に基づく変更を適用できることを示しました。 ただし、トリガーではプロパティ値を適用したりアニメーションを開始することはできますが、データ オブジェクトの構造を再構築できるような柔軟性はありません。 シナリオによっては、型が同じでもプロパティが異なるデータ オブジェクトに対して異なる <xref:System.Windows.DataTemplate> を作成することが必要になる場合があります。

 たとえば、`Task` オブジェクトの `Priority` の値が `1` のときは、自分用の警告としてまったく異なる外観にしたいような場合です。 この場合は、高優先度の `Task` オブジェクトの表示用に <xref:System.Windows.DataTemplate> を作成します。 リソース セクションに次の <xref:System.Windows.DataTemplate> を追加してみましょう。

 [!code-xaml[DataTemplatingIntro_snip#ImportantTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#importanttemplate)]

この例では、[DataTemplate.Resources](xref:System.Windows.FrameworkTemplate.Resources%2A) プロパティを使用します。 そのセクションで定義されているリソースは、<xref:System.Windows.DataTemplate> 内の要素によって共有されます。

 データ オブジェクトの `Priority` の値に基づいて使用する <xref:System.Windows.DataTemplate> を選択するロジックを提供するには、<xref:System.Windows.Controls.DataTemplateSelector> のサブクラスを作成し、<xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> メソッドをオーバーライドします。 次の例の <xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> メソッドでは、`Priority` プロパティの値に基づいて適切なテンプレートを返すロジックが提供されます。 返すテンプレートは、囲んでいる <xref:System.Windows.Window> 要素のリソース内に見つかります。

 [!code-csharp[DataTemplatingIntro_snip#DTSClass](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/TaskListDataTemplateSelector.cs#dtsclass)]
 [!code-vb[DataTemplatingIntro_snip#DTSClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DataTemplatingIntro_snip/visualbasic/tasklistdatatemplateselector.vb#dtsclass)]

 その後、リソースとして `TaskListDataTemplateSelector` を宣言できます。

 [!code-xaml[DataTemplatingIntro_snip#R1](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r1)]
[!code-xaml[DataTemplatingIntro_snip#DTS](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#dts)]
[!code-xaml[DataTemplatingIntro_snip#R2](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#r2)]

 テンプレート セレクター リソースを使用するには、<xref:System.Windows.Controls.ListBox> の <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A> プロパティにそれを割り当てます。 <xref:System.Windows.Controls.ListBox> では、基になっているコレクションの項目ごとに `TaskListDataTemplateSelector` の <xref:System.Windows.Controls.DataTemplateSelector.SelectTemplate%2A> メソッドが呼び出されます。 呼び出しでは、項目パラメーターとしてデータ オブジェクトを渡します。 メソッドによって返される <xref:System.Windows.DataTemplate> が、そのデータ オブジェクトに適用されます。

 [!code-xaml[DataTemplatingIntro_snip#ItemTemplateSelector](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemtemplateselector)]

 テンプレート セレクターを追加した <xref:System.Windows.Controls.ListBox> は次のようになります。

 ![データ テンプレート サンプルのスクリーンショット](./media/datatemplatingintro-fig7.png "DataTemplatingIntro_fig7")

これがこの例の結論です。 完全なサンプルについては、「[Introduction to Data Templating Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Data%20Binding/DataTemplatingIntro)」(データ テンプレート サンプルの概要) をご覧ください。

<a name="DataTemplating_ItemsControl"></a>
## <a name="styling-and-templating-an-itemscontrol"></a>ItemsControl のスタイルとテンプレートの設定
 <xref:System.Windows.Controls.ItemsControl> は <xref:System.Windows.DataTemplate> で使用できる唯一のコントロールの種類ではありませんが、<xref:System.Windows.Controls.ItemsControl> をコレクションにバインドするのはとてもよくあるシナリオです。 「[DataTemplate に含まれるもの](#what_belongs_in_datatemplate)」セクションでは、<xref:System.Windows.DataTemplate> の定義はデータのプレゼンテーションに関するものだけである必要があることを説明しました。 <xref:System.Windows.DataTemplate> を使うのが適切ではない場合を知るには、<xref:System.Windows.Controls.ItemsControl> によって提供されるさまざまなスタイルとテンプレートのプロパティについて理解することが重要です。 次の例は、これらの各プロパティの機能がわかるように設計されています。 この例の <xref:System.Windows.Controls.ItemsControl> は、前の例と同じ `Tasks` コレクションにバインドされています。 わかりやすいように、この例のスタイルとテンプレートはすべてインラインで宣言されています。

 [!code-xaml[DataTemplatingIntro_snip#ItemsControlProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/DataTemplatingIntro_snip/CSharp/Window1.xaml#itemscontrolproperties)]

 次に示すのは、この例がレンダリングされたときのスクリーンショットです。

 ![ItemsControl の例のスクリーンショット](./media/databinding-itemscontrolproperties.png "DataBinding_ItemsControlProperties")

 <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> を使う代わりに <xref:System.Windows.Controls.ItemsControl.ItemTemplateSelector%2A> を使うことができることに注意してください。 例については、前のセクションをご覧ください。 同様に、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyle%2A> を使う代わりに、<xref:System.Windows.Controls.ItemsControl.ItemContainerStyleSelector%2A> を使うこともできます。

 ここでは示されていない <xref:System.Windows.Controls.ItemsControl> の他の 2 つのスタイル関連のプロパティは、<xref:System.Windows.Controls.ItemsControl.GroupStyle%2A> と <xref:System.Windows.Controls.ItemsControl.GroupStyleSelector%2A> です。

<a name="DataTemplating_HeirarchicalDataTemplate"></a>
## <a name="support-for-hierarchical-data"></a>階層データのサポート
 これまでは、1 つのコレクションにバインドして表示する方法のみを説明してきました。 場合によっては、コレクションに他のコレクションが含まれることがあります。 <xref:System.Windows.HierarchicalDataTemplate> クラスは、そのようなデータを表示するために、<xref:System.Windows.Controls.HeaderedItemsControl> 型と共に使われるように設計されています。 次の例で、`ListLeagueList` は `League` オブジェクトのリストです。 各 `League` オブジェクトには、`Name` と、`Division` オブジェクトのコレクションがあります。 各 `Division` には、`Name` と `Team` オブジェクトのコレクションがあり、各 `Team` オブジェクトには `Name` があります。

 [!code-xaml[HierarchicalDataTemplateSnippet#HDT](~/samples/snippets/csharp/VS_Snippets_Wpf/HierarchicalDataTemplateSnippet/CS/window1.xaml#hdt)]

 この例は、<xref:System.Windows.HierarchicalDataTemplate> を使うことで、他のリストを含むリスト データを簡単に表示できることを示しています。 次に示すのは、この例のスクリーンショットです。

 ![HierarchicalDataTemplate のサンプルのスクリーンショット](./media/databinding-hierarchicaldatatemplate.png "DataBinding_HierarchicalDataTemplate")

## <a name="see-also"></a>関連項目

- [データ バインディング](../advanced/optimizing-performance-data-binding.md)
- [DataTemplate によって生成された要素を検索する](how-to-find-datatemplate-generated-elements.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [GridView の列ヘッダー スタイルおよびテンプレートの概要](../controls/gridview-column-header-styles-and-templates-overview.md)
