---
title: WPF でテンプレートを作成する - .NET デスクトップ
description: Windows Presentation Foundation と .NET Core でコントロール テンプレートを作成して参照する方法について説明します。
author: adegeo
ms.author: adegeo
ms.date: 11/15/2019
no-loc:
- <Window>
- <ControlTemplate>
- <Ellipse>
- <ContentPresenter>
- <Trigger>
- <Setter>
- <PropertyTrigger>
- <Grid>
- <VisualStateManager.VisualStateGroups>
- <VisualStateGroup>
- <VisualState>
- <Storyboard>
- SizeToContent
- MinWidth
- TargetType
- Title
helpviewer_keywords:
- control contract [WPF]
- controls [WPF], visual structure changes
- ControlTemplate [WPF], customizing for existing controls
- skinning controls [WPF]
- controls [WPF], appearance specified by state
- templates [WPF], custom for existing controls
ms.openlocfilehash: c372659676b450cde789c96e45c7ec5de2aea194
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325730"
---
# <a name="create-a-template-for-a-control"></a>コントロールのためのテンプレートを作成する

Windows Presentation Foundation (WPF) を使用すると、独自の再利用可能なテンプレートを使用して、既存のコントロールの視覚的な構造と動作をカスタマイズできます。 テンプレートは、アプリケーション、ウィンドウ、ページにグローバルに適用することも、コントロールに直接適用することもできます。 新しいコントロールを作成する必要があるほとんどのシナリオは、代わりに既存のコントロール用の新しいテンプレートを作成することによってカバーできます。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

この記事では、<xref:System.Windows.Controls.Button> コントロールの新しい <xref:System.Windows.Controls.ControlTemplate> を作成する方法について説明します。

## <a name="when-to-create-a-controltemplate"></a>ControlTemplate を作成するタイミング

コントロールには、<xref:System.Windows.Controls.Border.Background%2A>、<xref:System.Windows.Controls.Control.Foreground%2A>、<xref:System.Windows.Controls.Control.FontFamily%2A> などの多くのプロパティがあります。 これらのプロパティは、コントロールの外観のさまざまな側面を制御しますが、これらのプロパティを設定することによって行うことができる変更は制限されます。 たとえば、<xref:System.Windows.Controls.CheckBox> では、<xref:System.Windows.Controls.Control.Foreground%2A> プロパティを青に、<xref:System.Windows.Controls.Control.FontStyle%2A> を斜体に設定できます。 コントロールの他のプロパティを設定するだけでは、必要な外見のカスタマイズが十分にできない場合は、<xref:System.Windows.Controls.ControlTemplate> を作成します。

ほとんどのユーザー インターフェイスのボタンの外観はテキストが記載されている四角形で、基本的には同じです。 丸いボタンを作成する場合は、ボタンを継承する新しいコントロールを作成するか、ボタンの機能を再作成します。 さらに、新しいユーザー コントロールによって、円形のビジュアルを指定できます。

新しいコントロールを作成しないようにするには、既存のコントロールの視覚的なレイアウトをカスタマイズします。 丸いボタンを使用して、目的の視覚的なレイアウトで <xref:System.Windows.Controls.ControlTemplate> を作成します。

一方、新しい機能、異なるプロパティ、および新しい設定を持つコントロールが必要な場合は、新しい <xref:System.Windows.Controls.UserControl> を作成します。

## <a name="prerequisites"></a>必須コンポーネント

新しい WPF アプリケーションを作成し、*MainWindow.xaml* (または任意の別のウィンドウ) の **\<Window>** 要素で次のプロパティを設定します。

|     |     |
| --- | --- |
| **Title**         | `Template Intro Sample` |
| **SizeToContent** | `WidthAndHeight` |
| **MinWidth**      | `250` |

**\<Window>** 要素のコンテンツを次の XAML に設定します。

[!code-xaml[Initial](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#Initial)]

最終的に、*MainWindow.xaml* ファイルは次のようになります。

[!code-xaml[InitialWhole](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#InitialWhole)]

アプリケーションを実行すると、次のようになります。

![スタイルが設定されていない 2 つのボタンがある WPF ウィンドウ](media/create-apply-template/unstyled-button.png)

## <a name="create-a-controltemplate"></a>ControlTemplate の作成

<xref:System.Windows.Controls.ControlTemplate> を宣言する最も一般的な方法は、XAML ファイルの `Resources` セクションのリソースとして宣言する方法です。 テンプレートはリソースなので、すべてのリソースに適用されるものと同じスコープ規則に従います。 つまり、テンプレートの宣言場所は、テンプレートの適用場所に影響するということです。 たとえば、アプリケーション定義 XAML ファイルのルート要素でテンプレートを宣言すると、そのテンプレートはアプリケーションのどこでも使用できるようになります。 ウィンドウでテンプレートを定義すると、そのテンプレートはウィンドウ内のコントロールでのみ使用できます。

まず、*MainWindow.xaml* ファイルに `Window.Resources` 要素を追加します。

[!code-xaml[WindowResStart](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window2.xaml#WindowResStart)]

次のプロパティ セットで新しい **\<ControlTemplate>** を作成します。

|     |     |
| --- | --- |
| **x:Key**         | `roundbutton` |
| **TargetType**    | `Button` |

このコントロール テンプレートは単純です。

- コントロールのルート要素である <xref:System.Windows.Controls.Grid>
- ボタンの丸みのある外観を描画するための <xref:System.Windows.Shapes.Ellipse>
- ユーザー指定のボタンの内容を表示する <xref:System.Windows.Controls.ContentPresenter>

[!code-xaml[ControlTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#ControlTemplate)]

### <a name="templatebinding"></a>TemplateBinding

新しい <xref:System.Windows.Controls.ControlTemplate> を作成した場合も、パブリック プロパティを使用して、コントロールの外観を変更する必要が生じる場合があります。 [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md) のマークアップ拡張機能は、<xref:System.Windows.Controls.ControlTemplate> 内の要素のプロパティを、コントロールで定義されたパブリック プロパティにバインドする機能です。 [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md) を使用すると、コントロールのプロパティをテンプレートのパラメーターとして機能させることができます。 つまり、コントロールのプロパティを設定すると、その値は [TemplateBinding](../../framework/wpf/advanced/templatebinding-markup-extension.md) が機能している要素に渡されます。

### <a name="ellipse"></a>Ellipse

**\<Ellipse>** 要素の **:::no-loc text="Fill":::** プロパティおよび **:::no-loc text="Stroke":::** プロパティが、コントロールの <xref:System.Windows.Controls.Control.Foreground> プロパティと <xref:System.Windows.Controls.Control.Background> プロパティにバインドされていることに注意してください。

### <a name="contentpresenter"></a>ContentPresenter

[\<ContentPresenter>](xref:System.Windows.Controls.ContentPresenter) 要素もテンプレートに追加されます。 このテンプレートはボタン用に設計されているため、ボタンは <xref:System.Windows.Controls.ContentControl> から継承されることを考慮します。 このボタンに、要素のコンテンツが表示されます。 ボタン内には、プレーンテキストや別のコントロールなど、任意のものを設定できます。 次のボタンは、いずれも有効です。

```xaml
<Button>My Text</Button>

<!-- and -->

<Button>
    <CheckBox>Checkbox in a button</CheckBox>
</Button>
```

前のどちらの例においても、テキストとチェック ボックスは [Button.Content](xref:System.Windows.Controls.ContentControl.Content) プロパティとして設定されています。 コンテンツとして設定されている内容は、テンプレートで実行される **\<ContentPresenter>** によって表示できます。

<xref:System.Windows.Controls.ControlTemplate> が <xref:System.Windows.Controls.ContentControl> 型 (`Button` など) に適用されている場合は、要素ツリー内で <xref:System.Windows.Controls.ContentPresenter> が検索されます。 `ContentPresenter` が見つかった場合、テンプレートはコントロールの <xref:System.Windows.Controls.ContentControl.Content> プロパティを `ContentPresenter` に自動的にバインドします。

## <a name="use-the-template"></a>テンプレートを使用する

この記事の冒頭で宣言したボタンを見つけます。

[!code-xaml[Initial](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window1.xaml#Initial)]

2 番目のボタンの <xref:System.Windows.Controls.Control.Template> プロパティを次のように `roundbutton` リソースに設定します。

[!code-xaml[StyledButton](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#StyledButton)]

プロジェクトを実行して結果を確認すると、ボタンの背景が丸められていることがわかります。

![テンプレートの楕円のボタンが 1 つ表示されている WPF ウィンドウ](media/create-apply-template/styled-button.png)

ボタンが円ではなく、歪曲されていることに気付いたかもしれません。 **\<Ellipse>** 要素の動作方法により、これらは常に空いているスペースを埋めるように拡張されます。 ボタンの **:::no-loc text="width":::** プロパティと **:::no-loc text="height":::** プロパティを同じ値に変更し、円を一定にします。

[!code-xaml[StyledButtonSize](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window3.xaml#StyledButtonSize)]

![テンプレートの円形のボタンが 1 つ表示されている WPF ウィンドウ](media/create-apply-template/styled-uniform-button.png)

## <a name="add-a-trigger"></a>トリガーの追加

テンプレートが適用されているボタンの見た目が異なる場合でも、他のボタンと同じように動作します。 このボタンを押すと、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントが発生します。 ただし、ボタンの上にマウスを移動しても、ボタンの見た目は変わりません。 これらの視覚的な相互作用は、すべてテンプレートによって定義されています。

WPF で提供されている動的イベントおよびプロパティ システムを使用して、特定のプロパティの値を監視し、必要に応じてテンプレートのスタイルを再作成することができます。 この例では、ボタンの <xref:System.Windows.UIElement.IsMouseOver> プロパティを見ていきます。 マウスがコントロールの上にあるときに、新しい色で **\<Ellipse>** のスタイルを設定します。 この種類のトリガーは、*PropertyTrigger* として知られています。

これを機能させるには、参照できる **\<Ellipse>** に名前を追加する必要があります。 **backgroundElement** という名前を指定します。

[!code-xaml[EllipseName](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window4.xaml#EllipseName)]

次に、[ControlTemplate.Triggers](xref:System.Windows.Controls.ControlTemplate.Triggers) コレクションに新しい <xref:System.Windows.Trigger> を追加します。 トリガーは、`true` 値の `IsMouseOver` イベントを監視します。

[!code-xaml[ControlTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window4.xaml?name=ControlTemplate&highlight=6-10)]

次に、 **\<Ellipse>** の **Fill** プロパティを新しい色に変更する **\<Trigger>** に **\<Setter>** を追加します。

[!code-xaml[MouseOver](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window5.xaml#MouseOver)]

プロジェクトを実行します。 ボタンの上にマウスを移動すると、 **\<Ellipse>** の色が変化する点に注意してください。

![WPF ボタンの上にマウスを移動したことで塗りつぶしの色が変化](media/create-apply-template/mouse-move-over-button.gif)

## <a name="use-a-visualstate"></a>VisualState を使用する

表示状態は、コントロールによって定義され、トリガーされます。 たとえば、マウスをコントロールの上に移動すると、`CommonStates.MouseOver` 状態がトリガーされます。 コントロールの現在の状態に基づいて、プロパティの変更にアニメーションを付けることができます。 前のセクションでは、 **\<PropertyTrigger>** を使用して、`IsMouseOver` プロパティが `true` である場合にボタンの前景が `AliceBlue` に変更されるようにしました。 代わりに、この色が変化するアニメーションを付けて、滑らかな遷移を実現する表示状態を作成します。 *VisualStates* の詳細については、[「WPF のスタイルとテンプレート」](../fundamentals/styles-templates-overview.md#visual-states)を参照してください。

**\<PropertyTrigger>** をアニメーションが付いた表示状態に変換するには、まず、テンプレートから **\<ControlTemplate.Triggers>** 要素を削除します。

[!code-xaml[CleanTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window5.xaml#CleanTemplate)]

次に、コントロール テンプレートの **\<Grid>** ルートで、`CommonStates` に **\<VisualStateGroup>** を指定して **\<VisualStateManager.VisualStateGroups>** 要素を追加します。 `Normal` と `MouseOver` の 2 つの状態を定義します。

[!code-xaml[VisualState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#VisualState)]

**\<VisualState>** で定義されているアニメーションは、その状態がトリガーされたときに適用されます。 各状態のアニメーションを作成します。 アニメーションは、 **\<Storyboard>** 要素に格納されます。 ストーリーボードの詳細については、「[ストーリーボードの概要](../../framework/wpf/graphics-multimedia/storyboards-overview.md)」を参照してください。

- 標準

  この状態では、楕円の塗りつぶしにアニメーションが付けられ、コントロールの `Background` の色に復元されます。

  [!code-xaml[NormalState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#NormalState)]

- MouseOver

  この状態では、楕円の `Background` の色から新しい色である `Yellow` に切り替わるようアニメーションが付けられます。

  [!code-xaml[MouseOverState](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window6.xaml#MouseOverState)]

**\<ControlTemplate>** は次のようになるはずです。

[!code-xaml[FinalTemplate](~/samples/snippets/desktop-guide/wpf/styles-templates-create-apply-template/csharp/Window7.xaml#FinalTemplate)]

プロジェクトを実行します。 ボタンの上にマウスを移動すると、 **\<Ellipse>** の色がアニメーションになる点に注意してください。

![WPF ボタンの上にマウスを移動したことで塗りつぶしの色が変化](media/create-apply-template/mouse-move-over-button-visualstate.gif)

## <a name="next-steps"></a>次の手順

- [WPF でコントロールのスタイルを作成する](../fundamentals/styles-templates-create-apply-style.md)
- [WPF のスタイルとテンプレート](../fundamentals/styles-templates-overview.md)
- [XAML リソースの概要](../fundamentals/xaml-resources-define.md)
