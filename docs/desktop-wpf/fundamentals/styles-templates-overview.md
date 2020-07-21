---
title: スタイルとテンプレート
description: Windows Presentation Foundation (WPF) for .NET Core の XAML リソースについて説明します。 スタイルとテーマに関連する XAML リソースの種類について説明します。
author: adegeo
ms.author: adegeo
ms.date: 09/09/2019
dev_langs:
- csharp
- vb
ms.openlocfilehash: faa54e0a3c827717114ca6ca4f033c1c4c3acfa8
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325781"
---
# <a name="styles-and-templates-in-wpf"></a>WPF のスタイルとテンプレート

Windows Presentation Foundation (WPF) のスタイルとテンプレートは、開発者と設計者が視覚的に説得力のある効果と、製品の一貫した外観を作成するために使用できる一連の機能を指します。 アプリの外観をカスタマイズするときは、アプリ内およびアプリ間での外観の保守と共有を可能にする、強力なスタイルとテンプレートのモデルが必要です。 WPF はそのモデルを提供します。

WPF スタイル モデルのもう 1 つの機能は、表示とロジックの分離です。 設計者は、開発者が C# や Visual Basic を使用してプログラミング ロジックの作業を行っているのと同時に、XAML のみを使用してアプリの外観に関する作業を行うことができます。

この概要では、アプリのスタイルとテンプレートの側面に焦点を当てており、データ バインディングの概念については説明しません。 データ バインディングの詳細については、「[データ バインディングの概要](../data/data-binding-overview.md)」を参照してください。

スタイルとテンプレートの再利用を可能にするものである、リソースについて理解しておくことも重要です。 リソースの詳細については、「[XAML Resources](xaml-resources-define.md)」を参照してください。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="sample"></a>サンプル

この概要で提供されているサンプル コードは、次の図に示す[単純な写真閲覧アプリケーション](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)に基づいています。

![スタイル設定された ListView](./media/styles-and-templates-overview/stylingintro-triggers.png "StylingIntro_triggers")

この単純な写真のサンプルは、スタイルとテンプレートを使用して、視覚的に説得力のあるユーザー エクスペリエンスを作成します。 このサンプルには、2 つの <xref:System.Windows.Controls.TextBlock> 要素と、画像一覧にバインドされた <xref:System.Windows.Controls.ListBox> コントロールがあります。

完全なサンプルについては、「[Introduction to Styling and Templating Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)」を参照してください。

## <a name="styles"></a>スタイル

<xref:System.Windows.Style> は、一連のプロパティ値を複数の要素に適用する便利な方法と考えることができます。 <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> から派生する任意の要素 (<xref:System.Windows.Window> や <xref:System.Windows.Controls.Button> など) にスタイルを使用できます。

スタイルを宣言する最も一般的な方法は、XAML ファイルの `Resources` セクションでリソースとして行うものです。 スタイルはリソースであるため、すべてのリソースに適用されるものと同じスコープ規則に従います。 つまり、スタイルを宣言する場所は、スタイルを適用できる場所に影響するということです。 たとえば、アプリ定義 XAML ファイルのルート要素でスタイルを宣言すると、そのスタイルは、アプリ内のどこでも使用できます。

たとえば、次の XAML コードは、`TextBlock` の 2 つのスタイルを宣言しています。1 つは、すべての `TextBlock` 要素に自動的に適用され、もう 1 つは明示的に参照する必要があります。

[!code-xaml[SnippetDefaultTextBlockStyleBasedOn](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window2.xaml#SnippetDefaultTextBlockStyleBasedOn)]

上記で宣言されたスタイルの使用例を次に示します。

[!code-xaml[SnippetTextBlocksExplicit](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window2.xaml#SnippetTextBlocksExplicit)]

![スタイル設定された TextBlock](./media/styles-and-templates-overview/stylingintro-textblocks.png)

詳細については、[コントロールのスタイルの作成](styles-templates-create-apply-style.md)に関するページを参照してください。

## <a name="controltemplates"></a>ControlTemplate

WPF では、コントロールの <xref:System.Windows.Controls.ControlTemplate> によって、コントロールの外観が定義されます。 コントロールの構造と外観を変更するには、新しい <xref:System.Windows.Controls.ControlTemplate> を定義し、それをコントロールに割り当てます。 多くの場合、テンプレートによって、独自のカスタム コントロールを作成する必要がない程度に十分な柔軟性を得られます。

各コントロールでは、[Control.Template](xref:System.Windows.Controls.Control.Template) プロパティに既定のテンプレートが割り当てられています。 このテンプレートは、コントロールの視覚表現とコントロールの機能を結びつけます。 テンプレートは XAML で定義するため、コードを記述することなく、コントロールの外観を変更することができます。 各テンプレートは、<xref:System.Windows.Controls.Button> などの特定のコントロール向けに設計されています。

一般に、テンプレートは、XAML ファイルの `Resources` セクションでリソースとして宣言します。 すべてのリソースと同様に、スコープ規則が適用されます。

コントロール テンプレートは、スタイルよりもはるかに複雑です。 これは、スタイルが単にプロパティ変更を既存のコントロールに適用するのに対し、コントロール テンプレートはコントロール全体の外観を書き換えるからです。 ただし、コントロールのテンプレートは、[Control.Template](xref:System.Windows.Controls.Control.Template) プロパティを設定して適用されるため、スタイルを使用してテンプレートを定義または設定することができます。

通常、デザイナーでは、既存のテンプレートのコピーを作成して変更することが許可されます。 たとえば、Visual Studio WPF デザイナーで `CheckBox` コントロールを選択してから、右クリックし、 **[テンプレートの編集]**  >  **[コピーの作成]** を選択します。 このコマンドは、"*テンプレートを定義するスタイル*" を生成します。

```xaml
<Style x:Key="CheckBoxStyle1" TargetType="{x:Type CheckBox}">
    <Setter Property="FocusVisualStyle" Value="{StaticResource FocusVisual1}"/>
    <Setter Property="Background" Value="{StaticResource OptionMark.Static.Background1}"/>
    <Setter Property="BorderBrush" Value="{StaticResource OptionMark.Static.Border1}"/>
    <Setter Property="Foreground" Value="{DynamicResource {x:Static SystemColors.ControlTextBrushKey}}"/>
    <Setter Property="BorderThickness" Value="1"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type CheckBox}">
                <Grid x:Name="templateRoot" Background="Transparent" SnapsToDevicePixels="True">
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="Auto"/>
                        <ColumnDefinition Width="*"/>
                    </Grid.ColumnDefinitions>
                    <Border x:Name="checkBoxBorder" Background="{TemplateBinding Background}" BorderThickness="{TemplateBinding BorderThickness}" BorderBrush="{TemplateBinding BorderBrush}" HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="1" VerticalAlignment="{TemplateBinding VerticalContentAlignment}">
                        <Grid x:Name="markGrid">
                            <Path x:Name="optionMark" Data="F1 M 9.97498,1.22334L 4.6983,9.09834L 4.52164,9.09834L 0,5.19331L 1.27664,3.52165L 4.255,6.08833L 8.33331,1.52588e-005L 9.97498,1.22334 Z " Fill="{StaticResource OptionMark.Static.Glyph1}" Margin="1" Opacity="0" Stretch="None"/>
                            <Rectangle x:Name="indeterminateMark" Fill="{StaticResource OptionMark.Static.Glyph1}" Margin="2" Opacity="0"/>
                        </Grid>
                    </Border>
                    <ContentPresenter x:Name="contentPresenter" Grid.Column="1" Focusable="False" HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" RecognizesAccessKey="True" SnapsToDevicePixels="{TemplateBinding SnapsToDevicePixels}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}"/>
                </Grid>
                <ControlTemplate.Triggers>
                    <Trigger Property="HasContent" Value="true">
                        <Setter Property="FocusVisualStyle" Value="{StaticResource OptionMarkFocusVisual1}"/>
                        <Setter Property="Padding" Value="4,-1,0,0"/>

... content removed to save space ...
```

テンプレートのコピーを編集することは、テンプレートの動作を理解するための優れた方法です。 新しい空のテンプレートを作成する代わりに、コピーを編集して、視覚表示のいくつかの側面を変更する方が簡単です。

詳細については、「[コントロールのためのテンプレートを作成する](../themes/how-to-create-apply-template.md)」を参照してください。

### <a name="templatebinding"></a>TemplateBinding

前のセクションで定義されたテンプレート リソースで、[TemplateBinding マークアップ拡張機能](../../framework/wpf/advanced/templatebinding-markup-extension.md)が使用されていることにお気付きかもしれません。 `TemplateBinding` は、テンプレート シナリオに合わせて最適化されたバインディングの形態であり、`{Binding RelativeSource={RelativeSource TemplatedParent}}` を使用して構築されたバインディングに似ています。 `TemplateBinding` は、テンプレートの一部をコントロールのプロパティにバインドするのに便利です。 たとえば、各コントロールには <xref:System.Windows.Controls.Control.BorderThickness> プロパティがあります。 `TemplateBinding` を使用して、テンプレート内のどの要素がこのコントロール設定の影響を受けるかを管理します。

### <a name="contentcontrol-and-itemscontrol"></a>ContentControl と ItemsControl

<xref:System.Windows.Controls.ContentPresenter> が <xref:System.Windows.Controls.ContentControl> の <xref:System.Windows.Controls.ControlTemplate> で宣言されている場合、<xref:System.Windows.Controls.ContentPresenter> は自動的に <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> および <xref:System.Windows.Controls.ContentControl.Content%2A> プロパティにバインドされます。 同様に、<xref:System.Windows.Controls.ItemsControl> の <xref:System.Windows.Controls.ControlTemplate> にある <xref:System.Windows.Controls.ItemsPresenter> は、自動的に <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> および <xref:System.Windows.Controls.ItemsControl.Items%2A> プロパティにバインドされます。

## <a name="datatemplates"></a>DataTemplate

このサンプル アプリには、写真のリストにバインドされている <xref:System.Windows.Controls.ListBox> コントロールがあります。

[!code-xaml[ListBox](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window3.xaml#SnippetListBox)]

現在、この <xref:System.Windows.Controls.ListBox> は次のようになっています。

![テンプレート適用前の ListBox](./media/styles-and-templates-overview/stylingintro-listboxbefore.png "StylingIntro_ListBoxBefore")

ほとんどのコントロールはいくつかの型のコンテンツを持ち、そのコンテンツは多くの場合バインディング先のデータから取得されます。 このサンプルでは、データは写真のリストです。 WPF では、<xref:System.Windows.DataTemplate> を使用してデータの視覚表現を定義します。 基本的には、<xref:System.Windows.DataTemplate> に配置するものによって、レンダリングされたアプリでのデータの表示方法が決まります。

サンプル アプリでは、各カスタム `Photo` オブジェクトに、画像のファイル パスを指定する文字列型の `Source` プロパティがあります。 現在のところ、写真オブジェクトは、ファイルのパスとして表示されます。

[!code-csharp[PhotoClass](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Photo.cs#PhotoClass)]
[!code-vb[PhotoClass](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/vb/Photo.vb#PhotoClass)]

写真を画像として表示するには、リソースとして <xref:System.Windows.DataTemplate> を作成します。

[!code-xaml[DataTemplate](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window4.xaml#SnippetDataTemplate)]

<xref:System.Windows.DataTemplate.DataType%2A> プロパティは <xref:System.Windows.Style> の <xref:System.Windows.Style.TargetType%2A> プロパティに似ていることに注意してください。 <xref:System.Windows.DataTemplate> がリソース セクションにある場合、<xref:System.Windows.DataTemplate.DataType%2A> プロパティを型に指定して `x:Key` を省略すると、その型が出現するたびに <xref:System.Windows.DataTemplate> が適用されます。 常に、<xref:System.Windows.DataTemplate> に `x:Key` を割り当ててから、それを <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> プロパティや <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> プロパティなど、<xref:System.Windows.DataTemplate> 型を取るプロパティの `StaticResource` として設定することもできます。

基本的に、上記の例の <xref:System.Windows.DataTemplate> は、`Photo` オブジェクトがあるときは必ず、<xref:System.Windows.Controls.Border> 内の <xref:System.Windows.Controls.Image> として表示するように定義しています。 この <xref:System.Windows.DataTemplate> を使用すると、アプリは次のようになります。

![写真の画像](./media/styles-and-templates-overview/stylingintro-photosasimages.png "StylingIntro_PhotosAsImages")

データ テンプレートのモデルでは、その他の機能を提供します。 たとえば、<xref:System.Windows.Controls.Menu> や <xref:System.Windows.Controls.TreeView> などの <xref:System.Windows.Controls.HeaderedItemsControl> 型を使用して他のコレクションを含むコレクション データを表示する場合は、<xref:System.Windows.HierarchicalDataTemplate> があります。 もう 1 つのデータ テンプレート機能は <xref:System.Windows.Controls.DataTemplateSelector> です。これを使用すると、カスタム ロジックに基づいて、使用する <xref:System.Windows.DataTemplate> を選択することができます。 詳細については、「[Data Templating Overview](../../framework/wpf/data/data-templating-overview.md)」を参照してください。ここでは、さまざまなデータ テンプレート機能を詳しく説明します。

## <a name="triggers"></a>トリガー

トリガーは、プロパティ値が変更されたときまたはイベントが発生したときに、プロパティを設定するかまたはアニメーションなどのアクションを開始します。 <xref:System.Windows.Style>、<xref:System.Windows.Controls.ControlTemplate>、および <xref:System.Windows.DataTemplate> はすべて、一連のトリガーを含むことができる `Triggers` プロパティ備えています。 トリガーにはいくつかの種類があります。

### <a name="propertytriggers"></a>PropertyTrigger

プロパティの値を設定したりプロパティの値に基づいてアクションを開始したりする <xref:System.Windows.Trigger> は、プロパティ トリガーと呼ばれます。

プロパティ トリガーを使用する方法を示すために、選択されていない限り、各 <xref:System.Windows.Controls.ListBoxItem> を部分的に透明にすることができます。 次のスタイルは、<xref:System.Windows.Controls.ListBoxItem> の <xref:System.Windows.UIElement.Opacity%2A> 値を `0.5` に設定します。 ただし、<xref:System.Windows.Controls.ListBoxItem.IsSelected%2A> プロパティが `true` の場合、<xref:System.Windows.UIElement.Opacity%2A> は `1.0` に設定されます。

[!code-xaml[PropertyTrigger](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window5.xaml#SnippetPropertyTrigger)]

この例は、<xref:System.Windows.Trigger> を使用してプロパティ値を設定しますが、<xref:System.Windows.Trigger> クラスには、トリガーがアクションを実行できるようにする <xref:System.Windows.TriggerBase.EnterActions%2A> および <xref:System.Windows.TriggerBase.ExitActions%2A> プロパティも含まれていることに注意してください。

<xref:System.Windows.Controls.ListBoxItem> の <xref:System.Windows.FrameworkElement.MaxHeight%2A> プロパティが `75` に設定されていることに注意してください。 次の図では、3 番目の項目が選択されている項目です。

![スタイル設定された ListView](./media/styles-and-templates-overview/stylingintro-triggers.png "StylingIntro_triggers")

### <a name="eventtriggers-and-storyboards"></a>Eventtrigger とストーリー ボード

別の種類のトリガーは <xref:System.Windows.EventTrigger> です。これは、イベントの発生に基づいて一連のアクションを開始します。 たとえば、次の <xref:System.Windows.EventTrigger> オブジェクトは、マウス ポインターが <xref:System.Windows.Controls.ListBoxItem> に入ると、<xref:System.Windows.FrameworkElement.MaxHeight%2A> プロパティが `0.2` 秒間 `90` の値にアニメーション化されることを指定しています。 この項目からマウスを遠ざけると、`1` 秒間、元の値に戻ります。 <xref:System.Windows.ContentElement.MouseLeave> アニメーションに対して <xref:System.Windows.Media.Animation.DoubleAnimation.To%2A> 値を指定する必要がないことに注意してください。 これは、アニメーションが元の値を追跡できるからです。

[!code-xaml[StyleEventTriggers](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window6.xaml#SnippetStyleEventTriggers)]

詳細については、「[ストーリーボードの概要](../../framework/wpf/graphics-multimedia/storyboards-overview.md)」を参照してください。

次の図では、マウスは3 番目の項目を指しています。

![スタイル サンプルのスクリーンショット](./media/styles-and-templates-overview/stylingintro-eventtriggers.png "StylingIntro_EventTriggers")

### <a name="multitriggers-datatriggers-and-multidatatriggers"></a>MultiTriggers、DataTriggers、および MultiDataTriggers

<xref:System.Windows.Trigger> と <xref:System.Windows.EventTrigger> に加えて、他の種類のトリガーがあります。 <xref:System.Windows.MultiTrigger> を使用すると、複数の条件に基づいてプロパティ値を設定できます。 条件のプロパティがデータバインドされている場合は、<xref:System.Windows.DataTrigger> と <xref:System.Windows.MultiDataTrigger> を使用します。

## <a name="visual-states"></a>表示状態

コントロールは常に、特定の**状態**にあります。 たとえば、マウスがコントロールの画面上を移動しているとき、そのコントロールは一般的な `MouseOver` の状態であると見なされます。 特定の状態のないコントロールは、一般的な `Normal` 状態であると見なされます。 状態はグループに分割され、前に述べた状態は `CommonStates` という状態グループの一部です。 ほとんどのコントロールには、`CommonStates` と `FocusStates` の 2 つの状態グループがあります。 コントロールに適用される各状態グループのコントロールは、`CommonStates.MouseOver` や `FocusStates.Unfocused` など、常に各グループの 1 つの状態になります。 ただし、コントロールは、`CommonStates.Normal` や `CommonStates.Disabled` など、同じグループ内で 2 つの異なる状態であることはできません。 大部分のコントロールが認識して使用する状態の表を次に示します。

| VisualState 名 | VisualStateGroup 名 | 説明 |
| ---------------- | --------------------- | ----------- |
| 標準           | CommonStates          | 既定の状態です。 |
| MouseOver        | CommonStates          | マウス ポインターがコントロール上に配置されています。 |
| 押されている          | CommonStates          | コントロールが押されています。 |
| 無効         | CommonStates          | コントロールが無効になっています。 |
| フォーカスされている          | FocusStates           | コントロールにフォーカスがあります。 |
| フォーカスされていない        | FocusStates           | コントロールにフォーカスがありません。 |

コントロール テンプレートのルート要素に <xref:System.Windows.VisualStateManager?displayProperty=fullName> を定義することで、コントロールが特定の状態になったときにアニメーションをトリガーできます。 `VisualStateManager` は、監視する <xref:System.Windows.VisualStateGroup> と <xref:System.Windows.VisualState> の組み合わせを宣言します。 コントロールが監視している状態になると、`VisaulStateManager` によって定義されたアニメーションが開始されます。

たとえば、次の XAML コードは、`CommonStates.MouseOver` 状態を監視して、`backgroundElement` という名前の要素の塗りつぶしの色をアニメーション化します。 コントロールが `CommonStates.Normal` 状態に戻ると、`backgroundElement` という名前の要素の塗りつぶしの色が復元されます。

```xaml
<ControlTemplate x:Key="roundbutton" TargetType="Button">
    <Grid>
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup Name="CommonStates">
                <VisualState Name="Normal">
                    <ColorAnimation Storyboard.TargetName="backgroundElement"
                                    Storyboard.TargetProperty="(Shape.Fill).(SolidColorBrush.Color)"
                                    To="{TemplateBinding Background}"
                                    Duration="0:0:0.3"/>
                </VisualState>
                <VisualState Name="MouseOver">
                    <ColorAnimation Storyboard.TargetName="backgroundElement"
                                    Storyboard.TargetProperty="(Shape.Fill).(SolidColorBrush.Color)"
                                    To="Yellow"
                                    Duration="0:0:0.3"/>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

        ...
```

ストーリーボードの詳細については、「[ストーリーボードの概要](../../framework/wpf/graphics-multimedia/storyboards-overview.md)」を参照してください。

## <a name="shared-resources-and-themes"></a>共有リソースとテーマ

標準的な WPF アプリには、アプリ全体で適用される複数の UI リソースがある場合があります。 ひとまとめにして、この一連のリソースをアプリのテーマと見なすことができます。 WPF では、<xref:System.Windows.ResourceDictionary> クラスとしてカプセル化されているリソース ディクショナリを使用して UI リソースをテーマとしてパッケージ化することをサポートしています。

WPF のテーマは、要素のビジュアルをカスタマイズするために WPF が公開しているスタイルとテンプレートのメカニズムを使用して定義されます。

WPF のテーマのリソースは、埋め込みリソース ディクショナリに格納されます。 これらのリソース ディクショナリは署名されたアセンブリ内に埋め込む必要があり、コード自体と同じアセンブリまたはサイド バイ サイド アセンブリで埋め込むことができます。 WPF コントロールを含むアセンブリである PresentationFramework.dll の場合、テーマのリソースは、一連の side-by-sede アセンブリに含まれます。

テーマは、要素のスタイルを検索するときに最後に検索する場所になります。 通常、検索を行うには、まず適切なリソースを探索して要素ツリーをたどり、次にアプリのリソース コレクションを調べ、最後にシステムに対してクエリを実行します。 こうすることで、アプリ開発者は、テーマに到達する前に、ツリーまたはアプリのレベルで任意のオブジェクトのスタイルを再定義できます。

リソース ディクショナリは、複数のアプリ間でのテーマの再利用を可能にする個別ファイルとして定義できます。 また、同じ種類のリソースだが値が異なる複数のリソース ディクショナリを定義して、交換できるテーマを作成することもできます。 アプリをスキニングする場合、これらのスタイルまたはその他のリソースをアプリ レベルで再定義することをお勧めします。

スタイルおよびテンプレートを含む一連のリソースをアプリ間で共有するには、XAML ファイルを作成し、`shared.xaml` ファイルへの参照を含む <xref:System.Windows.ResourceDictionary> を定義します。

```xaml
<ResourceDictionary.MergedDictionaries>
  <ResourceDictionary Source="Shared.xaml" />
</ResourceDictionary.MergedDictionaries>
```

これは、一連のスタイルとブラシのリソースが含まれた <xref:System.Windows.ResourceDictionary> をそれ自体が定義している `shared.xaml` の共有です。これにより、アプリのコントロールに一貫した外観を持たせることができます。

詳細については、「[マージされたリソース ディクショナリ](../../framework/wpf/advanced/merged-resource-dictionaries.md)」を参照してください。

カスタム コントロールのテーマを作成する場合は、「[コントロールの作成の概要](../../framework/wpf/controls/control-authoring-overview.md#defining-resources-at-the-theme-level)」の「**テーマ レベルでのリソースの定義**」セクションを参照してください。

## <a name="see-also"></a>関連項目

- [WPF におけるパッケージの URI](../../framework/wpf/app-development/pack-uris-in-wpf.md)
- [方法: ControlTemplate によって生成された要素を検索する](../../framework/wpf/controls/how-to-find-controltemplate-generated-elements.md)
- [DataTemplate によって生成された要素を検索する](../../framework/wpf/data/how-to-find-datatemplate-generated-elements.md)
