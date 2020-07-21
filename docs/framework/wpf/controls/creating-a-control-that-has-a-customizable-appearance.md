---
title: 外観をカスタマイズできるコントロールの作成
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], customizing
- VisualStateManager [WPF], managing the state of a control
- ControlTemplate [WPF], customizing appearance
- controls [WPF], defining the visual structure and behavior of
- customizing appearance [WPF], ControlTemplate
- managing control states [WPF], VisualStateManager
- VisualStateManager [WPF], best practice
ms.assetid: 9e356d3d-a3d0-4b01-a25f-2d43e4d53fe5
ms.openlocfilehash: d9cf092cf47d4fb70b15033d039777d3279b633a
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283574"
---
# <a name="creating-a-control-that-has-a-customizable-appearance"></a>外観をカスタマイズできるコントロールの作成

<a name="introduction"></a>
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、外観をカスタマイズできるコントロールを作成できます。 たとえば、新しい <xref:System.Windows.Controls.ControlTemplate> を作成することにより、設定されるプロパティを超えて <xref:System.Windows.Controls.CheckBox> の外観を変更できます。 次の図は、既定の <xref:System.Windows.Controls.ControlTemplate> を使用する <xref:System.Windows.Controls.CheckBox> と、カスタム <xref:System.Windows.Controls.ControlTemplate> を使用する <xref:System.Windows.Controls.CheckBox> を示したものです。

![既定のコントロール テンプレートを使用するチェックボックス。](./media/ndp-checkboxdefault.png "NDP_CheckBoxDefault")
既定のコントロール テンプレートを使用する CheckBox

![カスタム コントロール テンプレートを使用するチェックボックス。](./media/ndp-checkboxcustom.png "NDP_CheckBoxCustom")
カスタム コントロール テンプレートを使用する CheckBox

コントロールを作成するときにパーツと状態モデルに従うと、コントロールの外観がカスタマイズ可能になります。 Blend for Visual Studio などのデザイナー ツールではパーツと状態モデルがサポートされているため、このモデルに従うと、そのような種類のアプリケーションでコントロールをカスタマイズできるようになります。  このトピックでは、パーツと状態モデルについてと、独自のコントロールを作成するときにそれに従う方法について説明します。 このトピックでは、カスタム コントロール `NumericUpDown` の例を使用して、このモデルの原理を示します。  `NumericUpDown` コントロールには数値が表示され、ユーザーはコントロールのボタンをクリックすることによって、その値を増減できます。  次の図は、このトピックで説明する `NumericUpDown` コントロールを示したものです。

![NumericUpDown カスタム コントロール。](./media/ndp-numericupdown.png "NDP_NumericUPDown")
カスタム NumericUpDown コントロール

このトピックは、次のセクションで構成されています。

- [必須コンポーネント](#prerequisites)

- [パーツと状態モデル](#parts_and_states_model)

- [ControlTemplate でのコントロールの視覚的構造と視覚的動作の定義](#defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate)

- [コードでの ControlTemplate のパーツの使用](#using_parts_of_the_controltemplate_in_code)

- [コントロール コントラクトの提供](#providing_the_control_contract)

- [完全な例](#complete_example)

<a name="prerequisites"></a>

## <a name="prerequisites"></a>必須コンポーネント

このトピックを理解するには、既存のコントロール用に新しい <xref:System.Windows.Controls.ControlTemplate> を作成する方法、コントロール コントラクトの要素、「[コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」で説明されている概念を理解している必要があります。

> [!NOTE]
> 外観をカスタマイズできるコントロールを作成するには、<xref:System.Windows.Controls.Control> クラスまたはそのサブクラスのうち <xref:System.Windows.Controls.UserControl> 以外のいずれかを継承するコントロールを作成する必要があります。  <xref:System.Windows.Controls.UserControl> を継承するコントロールはすばやく作成できるコントロールですが、<xref:System.Windows.Controls.ControlTemplate> が使用されておらず、外観をカスタマイズすることはできません。

<a name="parts_and_states_model"></a>

## <a name="parts-and-states-model"></a>パーツと状態モデル

パーツと状態モデルでは、コントロールの視覚的構造と視覚的動作を定義する方法を指定します。 パーツと状態モデルに従うには、次のようにする必要があります。

- コントロールの <xref:System.Windows.Controls.ControlTemplate> で、視覚的構造と視覚的動作を定義します。

- コントロールのロジックでコントロール テンプレートのパーツとやり取りするときに、特定のベスト プラクティスに従います。

- <xref:System.Windows.Controls.ControlTemplate> に含めるものを指定するコントロール コントラクトを提供します。

コントロールの <xref:System.Windows.Controls.ControlTemplate> で視覚的構造と視覚的動作を定義するとき、アプリケーションの作成者は、コードを記述するのではなく、新しい <xref:System.Windows.Controls.ControlTemplate> を作成することにより、コントロールの視覚的構造と視覚的動作を変更できます。   <xref:System.Windows.Controls.ControlTemplate> で定義する必要がある <xref:System.Windows.FrameworkElement> のオブジェクトと状態をアプリケーションの作成者に伝える、コントロール コントラクトを提供する必要があります。 <xref:System.Windows.Controls.ControlTemplate> 内のパーツを操作するときは、コントロールで不完全な <xref:System.Windows.Controls.ControlTemplate> が正しく処理されるように、いくつかのベスト プラクティスに従う必要があります。  これら 3 つの原則に従うと、アプリケーションの作成者は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に付属するコントロールの場合と同様に、コントロールの <xref:System.Windows.Controls.ControlTemplate> を簡単に作成できるようになります。  次のセクションでは、これらの推奨事項について詳しく説明します。

<a name="defining_the_visual_structure_and_visual_behavior_of_a_control_in_a_controltemplate"></a>

## <a name="defining-the-visual-structure-and-visual-behavior-of-a-control-in-a-controltemplate"></a>ControlTemplate でのコントロールの視覚的構造と視覚的動作の定義

パーツと状態モデルを使用してカスタム コントロールを作成するときは、コントロールの視覚的構造と視覚的動作を、そのロジックではなく、その <xref:System.Windows.Controls.ControlTemplate> で定義します。  コントロールの視覚的構造は、コントロールを構成する <xref:System.Windows.FrameworkElement> オブジェクトの複合です。  視覚的動作とは、コントロールが特定の状態になったときのコントロールの表示方法です。   コントロールの視覚的構造と視覚的動作を指定する <xref:System.Windows.Controls.ControlTemplate> を作成する方法の詳細については、「[コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」を参照してください。

`NumericUpDown` コントロールの例では、視覚的構造には 2 つの <xref:System.Windows.Controls.Primitives.RepeatButton> コントロールと 1 つの <xref:System.Windows.Controls.TextBlock> が含まれます。  これらのコントロールを `NumericUpDown` コントロールのコード (そのコンストラクターなど) で追加した場合、それらのコントロールの位置は変更できなくなります。  コントロールの視覚的構造と視覚的動作をコード内で定義するのではなく、<xref:System.Windows.Controls.ControlTemplate> で定義する必要があります。  そうすれば、<xref:System.Windows.Controls.ControlTemplate> を置き換えることができるので、アプリケーションの開発者は、ボタンと <xref:System.Windows.Controls.TextBlock> の位置をカスタマイズし、`Value` が負の場合に発生する動作を指定することができます。

次の例では、`NumericUpDown` コントロールの視覚的構造を示します。これには、`Value` を増やすための <xref:System.Windows.Controls.Primitives.RepeatButton>、`Value` を減らすための <xref:System.Windows.Controls.Primitives.RepeatButton>、`Value` を表示するための <xref:System.Windows.Controls.TextBlock> が含まれています。

[!code-xaml[VSMCustomControl#VisualStructure](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#visualstructure)]

`NumericUpDown` コントロールの視覚的動作は、値が負の場合は赤いフォントで表示することです。  `Value` が負のときにコードで <xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Foreground%2A> を変更すると、`NumericUpDown` では負の値が常に赤で表示されます。 <xref:System.Windows.Controls.ControlTemplate> でコントロールの視覚的動作を指定するには、<xref:System.Windows.Controls.ControlTemplate> に <xref:System.Windows.VisualState> オブジェクトを追加します。  次の例では、`Positive` 状態と `Negative` 状態に対する <xref:System.Windows.VisualState> オブジェクトを示します。  `Positive` と `Negative` は相互に排他的である (コントロールは常に必ず 2 つの状態のどちらか一方になります) ため、この例では <xref:System.Windows.VisualState> オブジェクトを 1 つの <xref:System.Windows.VisualStateGroup> に格納します。  コントロールが `Negative` 状態になると、<xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Foreground%2A> が赤に変わります。  コントロールが `Positive` 状態のときは、<xref:System.Windows.Controls.TextBlock.Foreground%2A> は元の値に戻ります。  <xref:System.Windows.Controls.ControlTemplate> での <xref:System.Windows.VisualState> オブジェクトの定義については、「[コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」で詳しく説明されています。

> [!NOTE]
> <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 添付プロパティの設定は、<xref:System.Windows.Controls.ControlTemplate> のルート <xref:System.Windows.FrameworkElement> で必ず行ってください。

[!code-xaml[VSMCustomControl#ValueStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]

<a name="using_parts_of_the_controltemplate_in_code"></a>

## <a name="using-parts-of-the-controltemplate-in-code"></a>コードでの ControlTemplate のパーツの使用

<xref:System.Windows.Controls.ControlTemplate> の作成者は、意図的にまたは誤って、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.VisualState> オブジェクトを省略する場合がありますが、コントロールのロジックでは、それらのパーツを正しく機能させることが必要な場合があります。 パーツと状態モデルでは、<xref:System.Windows.FrameworkElement> オブジェクトまたは <xref:System.Windows.VisualState> オブジェクトが不足している <xref:System.Windows.Controls.ControlTemplate> に対して、コントロールに回復性が必要であることが指定されています。  <xref:System.Windows.FrameworkElement>、<xref:System.Windows.VisualState>、または <xref:System.Windows.VisualStateGroup> が <xref:System.Windows.Controls.ControlTemplate> にない場合でも、コントロールで例外をスローしたり、エラーを報告したりしてはなりません。 ここでは、<xref:System.Windows.FrameworkElement> オブジェクトとの操作と状態の管理に関して推奨される方法について説明します。

### <a name="anticipate-missing-frameworkelement-objects"></a>FrameworkElement オブジェクトがない場合を想定する

<xref:System.Windows.Controls.ControlTemplate> で <xref:System.Windows.FrameworkElement> オブジェクトを定義した場合、コントロールのロジックでその一部を操作することが必要になる場合があります。  たとえば、`NumericUpDown` コントロールでは、`Value` を増減するためにボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントをサブスクライブし、<xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティを `Value` に設定します。 カスタム <xref:System.Windows.Controls.ControlTemplate> で <xref:System.Windows.Controls.TextBlock> またはボタンが省略されている場合、コントロールの機能が部分的に失われてもかまいませんが、コントロールが原因でエラーが発生しないようにする必要があります。 たとえば、<xref:System.Windows.Controls.ControlTemplate> に `Value` を変更するボタンが含まれていない場合、`NumericUpDown` の機能は失われますが、<xref:System.Windows.Controls.ControlTemplate> を使用するアプリケーションは実行を続けます。

次の方法を使用すると、<xref:System.Windows.FrameworkElement> オブジェクトがなくてもコントロールは正しく応答するようになります。

1. コードで参照する必要のある各 <xref:System.Windows.FrameworkElement> に対して、`x:Name` 属性を設定します。

2. 操作する必要がある各 <xref:System.Windows.FrameworkElement> に対して、プライベート プロパティを定義します。

3. <xref:System.Windows.FrameworkElement> プロパティの set アクセサーで、コントロールが処理するすべてのイベントをサブスクライブおよびサブスクライブ解除します。

4. ステップ 2 で定義した <xref:System.Windows.FrameworkElement> プロパティを、<xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> メソッドで設定します。 これは、<xref:System.Windows.Controls.ControlTemplate> 内の <xref:System.Windows.FrameworkElement> をコントロールで使用できる最も早い段階です。 それを <xref:System.Windows.Controls.ControlTemplate> から取得するには、<xref:System.Windows.FrameworkElement> の `x:Name` を使用します。

5. メンバーにアクセスする前に、<xref:System.Windows.FrameworkElement> が `null` ではないことを確認します。  `null` であっても、エラーを報告しないようにします。

次の例では、前の推奨事項一覧に従って、`NumericUpDown` コントロールで <xref:System.Windows.FrameworkElement> オブジェクトを操作する方法を示します。

<xref:System.Windows.Controls.ControlTemplate> で `NumericUpDown` コントロールの視覚的構造を定義する例では、`Value` を増やす <xref:System.Windows.Controls.Primitives.RepeatButton> の `x:Name` 属性が `UpButton` に設定されています。  次の例では、<xref:System.Windows.Controls.ControlTemplate> で宣言されている <xref:System.Windows.Controls.Primitives.RepeatButton> を表す `UpButtonElement` という名前のプロパティが宣言されています。 `set` アクセサーでは、`UpDownElement` が `null` ではない場合は、最初にボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントをサブスクライブ解除した後、プロパティを設定してから、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントをサブスクライブします。 他の <xref:System.Windows.Controls.Primitives.RepeatButton> に対しても `DownButtonElement` という名前のプロパティが定義されていますが、ここには示されていません。

[!code-csharp[VSMCustomControl#UpButtonProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#upbuttonproperty)]
[!code-vb[VSMCustomControl#UpButtonProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#upbuttonproperty)]

次の例では、`NumericUpDown` コントロールに対する <xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> を示します。  この例では、<xref:System.Windows.FrameworkElement.GetTemplateChild%2A> メソッドを使用して、<xref:System.Windows.Controls.ControlTemplate> から <xref:System.Windows.FrameworkElement> オブジェクトを取得します。  この例では、名前は指定されたものであっても型が予想とは異なる <xref:System.Windows.FrameworkElement> が <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> で検出された場合に対する保護が行われていることに注意してください。 また、`x:Name` は指定されたものであっても型が間違っている要素は無視することもベスト プラクティスです。

[!code-csharp[VSMCustomControl#ApplyTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
[!code-vb[VSMCustomControl#ApplyTemplate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]

前の例で示した手順に従うことで、<xref:System.Windows.Controls.ControlTemplate> に <xref:System.Windows.FrameworkElement> がない場合でもコントロールが実行を続けられるようにします。

### <a name="use-the-visualstatemanager-to-manage-states"></a>VisualStateManager を使用して状態を管理する

<xref:System.Windows.VisualStateManager> では、コントロールの状態が追跡され、状態間の遷移に必要なロジックが実行されます。 <xref:System.Windows.Controls.ControlTemplate> に <xref:System.Windows.VisualState> オブジェクトを追加する場合は、それらを <xref:System.Windows.VisualStateGroup> に追加し、<xref:System.Windows.VisualStateGroup> を <xref:System.Windows.VisualStateManager.VisualStateGroups%2A?displayProperty=nameWithType> 添付プロパティに追加して、<xref:System.Windows.VisualStateManager> でそれらにアクセスできるようにします。

次の例では、コントロールの `Positive` 状態と `Negative` 状態に対応する <xref:System.Windows.VisualState> オブジェクトを示す前の例を繰り返します。 `Negative` <xref:System.Windows.VisualState> の <xref:System.Windows.Media.Animation.Storyboard> では、<xref:System.Windows.Controls.TextBlock> の <xref:System.Windows.Controls.TextBlock.Foreground%2A> が赤に変更されます。   `NumericUpDown` コントロールが `Negative` 状態になると、`Negative` 状態のストーリーボードが開始されます。  その後、コントロールが `Positive` 状態に戻ると、`Negative` 状態の <xref:System.Windows.Media.Animation.Storyboard> は停止されます。  `Negative` の <xref:System.Windows.Media.Animation.Storyboard> が停止されると、<xref:System.Windows.Controls.TextBlock.Foreground%2A> は元の色に戻るため、`Positive` の <xref:System.Windows.VisualState> には <xref:System.Windows.Media.Animation.Storyboard> が含まれる必要はありません。

[!code-xaml[VSMCustomControl#ValueStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/window1.xaml#valuestates)]

<xref:System.Windows.Controls.TextBlock> には名前が指定されていますが、コントロールのロジックで <xref:System.Windows.Controls.TextBlock> が参照されないため、<xref:System.Windows.Controls.TextBlock> は `NumericUpDown` のコントロール コントラクトに含まれません。  <xref:System.Windows.Controls.ControlTemplate> で参照される要素には名前がありますが、コントロールの新しい <xref:System.Windows.Controls.ControlTemplate> でその要素を参照する必要がない場合があるため、コントロール コントラクトに含める必要はありません。  たとえば、`NumericUpDown` の新しい <xref:System.Windows.Controls.ControlTemplate> を作成する開発者は、<xref:System.Windows.Controls.Control.Foreground%2A> を変更することによって `Value` が負であることを示す必要はないと判断することがあります。  その場合、コードでも <xref:System.Windows.Controls.ControlTemplate> でも、<xref:System.Windows.Controls.TextBlock> は名前で参照されません。

コントロールの状態は、コントロールのロジックで変更する必要があります。 次の例では、`NumericUpDown` コントロールで <xref:System.Windows.VisualStateManager.GoToState%2A> メソッドを呼び出して、`Value` が 0 以上のときは `Positive` 状態に遷移し、`Value` が 0 未満のときは `Negative` 状態に遷移することを示します。

[!code-csharp[VSMCustomControl#ValueStateChange](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#valuestatechange)]
[!code-vb[VSMCustomControl#ValueStateChange](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#valuestatechange)]

<xref:System.Windows.VisualStateManager.GoToState%2A> メソッドでは、ストーリーボードを適切に開始および停止するために必要なロジックが実行されます。 コントロールで <xref:System.Windows.VisualStateManager.GoToState%2A> を呼び出してその状態を変更すると、<xref:System.Windows.VisualStateManager> では次のことが行われます。

- コントロールの遷移先の <xref:System.Windows.VisualState> に <xref:System.Windows.Media.Animation.Storyboard> がある場合は、そのストーリーボードが開始されます。 その後、コントロールの遷移元の <xref:System.Windows.VisualState> に <xref:System.Windows.Media.Animation.Storyboard> がある場合、そのストーリーボードは終了します。

- コントロールが既に指定された状態になっている場合、<xref:System.Windows.VisualStateManager.GoToState%2A> では何も行われず、`true` が返されます。

- 指定された状態が `control` の <xref:System.Windows.Controls.ControlTemplate> に存在しない場合、<xref:System.Windows.VisualStateManager.GoToState%2A> では何も行われず、`false` が返されます。

#### <a name="best-practices-for-working-with-the-visualstatemanager"></a>VisualStateManager の操作に関するベスト プラクティス

コントロールの状態を維持するには、次のようにすることをお勧めします。

- プロパティを使用して、状態を追跡します。

- ヘルパー メソッドを作成して、状態間の切り替えを行います。

`NumericUpDown` コントロールでは、`Value` プロパティを使用して、状態が `Positive` または `Negative` のどちらであるかを追跡します。  また、`NumericUpDown` コントロールでは、<xref:System.Windows.UIElement.IsFocused%2A> プロパティを追跡する `Focused` 状態と `UnFocused` 状態も定義されています。 コントロールのプロパティに本来対応していない状態を使用する場合は、プライベート プロパティを定義して状態を追跡できます。

すべての状態を 1 つのメソッドで更新することにより、<xref:System.Windows.VisualStateManager> の呼び出しを一元化し、コードを管理しやすくします。 次の例では、`NumericUpDown` コントロールのヘルパー メソッド `UpdateStates` を示します。 `Value` が 0 以上の場合、<xref:System.Windows.Controls.Control> は `Positive` 状態になります。  `Value` が 0 未満の場合、コントロールは `Negative` 状態になります。  <xref:System.Windows.UIElement.IsFocused%2A> が `true` の場合、コントロールは `Focused` 状態になります。それ以外の場合は、`Unfocused` 状態になります。  コントロールでは、変化する状態に関係なく、状態を変更する必要があるときは常に `UpdateStates` を呼び出すことができます。

[!code-csharp[VSMCustomControl#UpdateStates](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#updatestates)]
[!code-vb[VSMCustomControl#UpdateStates](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#updatestates)]

コントロールが既になっている状態の名前名を <xref:System.Windows.VisualStateManager.GoToState%2A> に渡すと、<xref:System.Windows.VisualStateManager.GoToState%2A> では何も行われないため、コントロールの現在の状態を確認する必要はありません。  たとえば、`Value` がある負の数値から別の負の数値に変化した場合、`Negative` 状態のストーリーボードは中断されず、ユーザーが目にするコントロールに変化はありません。

<xref:System.Windows.VisualStateManager.GoToState%2A> を呼び出すと、<xref:System.Windows.VisualStateManager> では <xref:System.Windows.VisualStateGroup> オブジェクトを使用して、終了する状態が決定されます。 コントロールは、その <xref:System.Windows.Controls.ControlTemplate> で定義されている各 <xref:System.Windows.VisualStateGroup> に対して常に 1 つの状態になり、同じ <xref:System.Windows.VisualStateGroup> から別の状態になるときにのみ状態が変わります。 たとえば、`NumericUpDown` コントロールの <xref:System.Windows.Controls.ControlTemplate> では、`Positive` と `Negative` の <xref:System.Windows.VisualState> オブジェクトが 1 つの <xref:System.Windows.VisualStateGroup> で定義されており、`Focused` と `Unfocused` の <xref:System.Windows.VisualState> オブジェクトが別のグループで定義されています。 (定義されている `Focused` と `Unfocused` の <xref:System.Windows.VisualState> は、このトピックの「[完全な例](#complete_example)」セクションで確認できます)。コントロールが `Positive` 状態から `Negative` 状態に変化すると、またはその逆に変化しても、コントロールは `Focused` 状態または `Unfocused` 状態のままになります。

コントロールの状態は、一般に次の 3 つの場合に変わる可能性があります。

- <xref:System.Windows.Controls.ControlTemplate> が <xref:System.Windows.Controls.Control> に適用されたとき。

- プロパティが変化したとき。

- イベントが発生したとき。

次の例では、これらの場合に `NumericUpDown` コントロールの状態を更新する方法を示します。

<xref:System.Windows.Controls.ControlTemplate> が適用されたときにコントロールが正しい状態で表示されるように、<xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> メソッドでコントロールの状態を更新する必要があります。 次の例では、<xref:System.Windows.FrameworkElement.OnApplyTemplate%2A> で `UpdateStates` を呼び出して、コントロールが適切な状態であることを確認しています。  たとえば、`NumericUpDown` コントロールを作成し、その <xref:System.Windows.Controls.Control.Foreground%2A> を緑に、`Value` を -5 に設定するとします。  `NumericUpDown` コントロールに <xref:System.Windows.Controls.ControlTemplate> が適用されたときに `UpdateStates` を呼び出さないと、コントロールは `Negative` 状態にならず、値は赤ではなく緑色になります。  `UpdateStates` を呼び出して、コントロールを `Negative` 状態にする必要があります。

[!code-csharp[VSMCustomControl#ApplyTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#applytemplate)]
[!code-vb[VSMCustomControl#ApplyTemplate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#applytemplate)]

プロパティが変化したら、多くの場合、コントロールの状態を更新する必要があります。 次の例では、`ValueChangedCallback` メソッド全体を示します。 `Value` が変化すると `ValueChangedCallback` が呼び出されるので、`Value` が正から負または負から正に変化したら、そのメソッドで `UpdateStates` を呼び出します。 `Value` は変化したが、正または負はそのままである場合でも、`UpdateStates` を呼び出してかまいません。その場合、コントロールの状態は変更されないためです。

[!code-csharp[VSMCustomControl#EntireValueChangedCallback](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#entirevaluechangedcallback)]
[!code-vb[VSMCustomControl#EntireValueChangedCallback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#entirevaluechangedcallback)]

また、イベントが発生したときも、状態の更新が必要になる場合があります。 次の例では、`NumericUpDown` で <xref:System.Windows.Controls.Control> に対して `UpdateStates` を呼び出し、<xref:System.Windows.UIElement.GotFocus> イベントを処理しています。

[!code-csharp[VSMCustomControl#OnGotFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#ongotfocus)]
[!code-vb[VSMCustomControl#OnGotFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#ongotfocus)]

<xref:System.Windows.VisualStateManager> は、コントロールの状態を管理するのに役立ちます。 <xref:System.Windows.VisualStateManager> を使用すると、コントロールの状態を正しく遷移させることができます。  このセクションで説明されている推奨事項に従って <xref:System.Windows.VisualStateManager> を操作すると、コントロールのコードが読みやすくなり、保守も容易になります。

<a name="providing_the_control_contract"></a>

## <a name="providing-the-control-contract"></a>コントロール コントラクトの提供

テンプレートに配置する内容を <xref:System.Windows.Controls.ControlTemplate> の作成者がわかるように、コントロール コントラクトを提供します。 コントロール コントラクトには、次の 3 つの要素があります。

- コントロールのロジックが使用する視覚的要素。

- コントロールの状態および各状態が所属するグループ。

- コントロールに対して視覚的に作用するパブリック プロパティ。

新しい <xref:System.Windows.Controls.ControlTemplate> を作成するときは、コントロールのロジックで使用されている <xref:System.Windows.FrameworkElement> オブジェクト、各オブジェクトの型、およびその名前を知っている必要があります。 また、<xref:System.Windows.Controls.ControlTemplate> の作成者は、コントロールが取ることのできる各状態の名前と、その状態が含まれる <xref:System.Windows.VisualStateGroup> も把握している必要があります。

`NumericUpDown` の例に戻ると、そのコントロールでは、<xref:System.Windows.Controls.ControlTemplate> に次の <xref:System.Windows.FrameworkElement> オブジェクトが含まれるものと想定されます。

- `UpButton` という名前の <xref:System.Windows.Controls.Primitives.RepeatButton>。

- `DownButton.` という名前の <xref:System.Windows.Controls.Primitives.RepeatButton>。

 コントロールは、次の状態になることができます。

- `ValueStates` の <xref:System.Windows.VisualStateGroup>

  - `Positive`

  - `Negative`

- `FocusStates` の <xref:System.Windows.VisualStateGroup>

  - `Focused`

  - `Unfocused`

コントロールで予期される <xref:System.Windows.FrameworkElement> オブジェクトを指定するには、<xref:System.Windows.TemplatePartAttribute> を使用して、予期される要素の名前と型を指定します。  コントロールで可能な状態を指定するには、<xref:System.Windows.TemplateVisualStateAttribute> を使用して、状態の名前と、それが属する <xref:System.Windows.VisualStateGroup> を指定します。  <xref:System.Windows.TemplatePartAttribute> と <xref:System.Windows.TemplateVisualStateAttribute> を、コントロールのクラス定義に追加します。

コントロールの外観に影響するすべてのパブリック プロパティも、コントロール コントラクトの一部です。

次の例では、`NumericUpDown` コントロールの <xref:System.Windows.FrameworkElement> オブジェクトと状態を指定しています。

[!code-csharp[VSMCustomControl#ControlContract](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controlcontract)]
[!code-vb[VSMCustomControl#ControlContract](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controlcontract)]

<a name="complete_example"></a>

## <a name="complete-example"></a>コード例全体

次の例は、`NumericUpDown` コントロールの完全な <xref:System.Windows.Controls.ControlTemplate> です。

[!code-xaml[VSMCustomControl#NUDTemplate](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/themes/generic.xaml#nudtemplate)]

次の例では、`NumericUpDown` のロジックを示します。

[!code-csharp[VSMCustomControl#ControlLogic](~/samples/snippets/csharp/VS_Snippets_Wpf/vsmcustomcontrol/csharp/numericupdown.cs#controllogic)]
[!code-vb[VSMCustomControl#ControlLogic](~/samples/snippets/visualbasic/VS_Snippets_Wpf/vsmcustomcontrol/visualbasic/numericupdown.vb#controllogic)]

## <a name="see-also"></a>関連項目

- [コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)
- [コントロールのカスタマイズ](control-customization.md)
