---
title: ストーリーボードの概要
desription: Organize and apply animations in storyboards. Use property-targeting syntax and combine timelines in Windows Presentation Foundation (WPF).
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Storyboard syntax [WPF]
- syntax [WPF], Storyboard
- timelines [WPF]
ms.assetid: 1a698c3c-30f1-4b30-ae56-57e8a39811bd
ms.openlocfilehash: 50f45953da3801bf73016c09b78a6a1b54878bc0
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853642"
---
# <a name="storyboards-overview"></a>ストーリーボードの概要

ここでは、<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用してアニメーションを編成および適用する方法を示します。 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを対話的に操作する方法について説明し、間接的なプロパティの対象化についての構文を示します。

## <a name="prerequisites"></a>必須コンポーネント

このトピックを理解するには、さまざまな種類のアニメーションとその基本的な機能に精通している必要があります。 アニメーションの概要については、「[アニメーションの概要](animation-overview.md)」を参照してください。 また、添付プロパティの使用方法についても理解しておく必要があります。 添付プロパティの詳細については、「[添付プロパティの概要](../advanced/attached-properties-overview.md)」を参照してください。

<a name="whatisatimeline"></a>

## <a name="what-is-a-storyboard"></a>ストーリーボードとは何か

タイムラインの型で役に立つのは、アニメーションだけではありません。 他にも一連のタイムラインの編成を容易にし、タイムラインをプロパティに適用するための Timeline クラスが提供されています。 コンテナー タイムラインは <xref:System.Windows.Media.Animation.TimelineGroup> クラスから派生し、<xref:System.Windows.Media.Animation.ParallelTimeline> と <xref:System.Windows.Media.Animation.Storyboard> があります。

<xref:System.Windows.Media.Animation.Storyboard> はコンテナー タイムラインの一種であり、含まれる複数のタイムラインの対象情報を提供します。 ストーリーボードには、その他のコンテナー タイムラインやアニメーションなど、任意の種類の <xref:System.Windows.Media.Animation.Timeline> を格納できます。 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用すると、さまざまなオブジェクトおよびプロパティに影響を与える複数のタイムラインを 1 つのタイムライン ツリーに結合でき、複雑なタイミング動作の編成および制御が容易になります。 たとえば、次の 3 つのことを実行するボタンを必要としているとします。

- ユーザーに選択されると、拡大して色が変わる。

- クリックされると、いったん縮小してから元のサイズに戻る。

- 無効にされると、縮小し、50% の不透明度になる。

この場合、同じオブジェクトに適用するアニメーションのセットを複数用意し、ボタンの状態に応じてさまざまな場合に再生します。 <xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用すると、アニメーションを編成し、これらをグループ化して 1 つ以上のオブジェクトに適用できます。

<a name="wherecanyouuseastoryboard"></a>

## <a name="where-can-you-use-a-storyboard"></a>ストーリーボードはどこで使用できるか

<xref:System.Windows.Media.Animation.Storyboard> を使用すると、アニメーション可能なクラスの依存関係プロパティをアニメーション化ができます (クラスをアニメーション可能にする方法の詳細については、「[アニメーションの概要](animation-overview.md)」をご覧ください)。 ただし、ストーリーボードはフレームワーク レベルの機能であるため、オブジェクトは <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> の <xref:System.Windows.NameScope> に属している必要があります。

たとえば、<xref:System.Windows.Media.Animation.Storyboard> を使用すると、次の処理を実行できます。

- ボタン (<xref:System.Windows.FrameworkElement> 型) の背景を描画する <xref:System.Windows.Media.SolidColorBrush> (非フレームワーク要素) をアニメーション化します。

- <xref:System.Windows.Controls.Image> (<xref:System.Windows.FrameworkElement>) を使用して表示された <xref:System.Windows.Media.GeometryDrawing> (非フレームワーク要素) の塗りつぶしを描画する <xref:System.Windows.Media.SolidColorBrush> (非フレームワーク要素) をアニメーション化します。

- コード内で、<xref:System.Windows.Media.SolidColorBrush> をアニメーション化します (宣言されたクラスに <xref:System.Windows.FrameworkElement> も含まれていて、<xref:System.Windows.Media.SolidColorBrush> の名前がその <xref:System.Windows.FrameworkElement> に登録されている場合)。

ただし、<xref:System.Windows.Media.Animation.Storyboard> を使用して <xref:System.Windows.Media.SolidColorBrush> をアニメーション化できないことがあります。これは、名前が <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> に登録されていない場合、あるいは、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> のプロパティの設定に使用されなかった場合です。

<a name="applyanimationswithastoryboard"></a>

## <a name="how-to-apply-animations-with-a-storyboard"></a>ストーリーボードを使用してアニメーションを適用する方法

<xref:System.Windows.Media.Animation.Storyboard> を使用してアニメーションを編成および適用するには、<xref:System.Windows.Media.Animation.Storyboard> の子タイムラインとしてアニメーションを追加します。 <xref:System.Windows.Media.Animation.Storyboard> クラスでは、<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> および <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> 添付プロパティが提供されます。 これらのプロパティをアニメーションで設定して、アニメーションのターゲット オブジェクトとターゲット プロパティを指定します。

これらのターゲットにアニメーションを適用するには、トリガー アクションまたはメソッドを使用して <xref:System.Windows.Media.Animation.Storyboard> を開始します。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、<xref:System.Windows.Media.Animation.BeginStoryboard> オブジェクトを、<xref:System.Windows.EventTrigger>、<xref:System.Windows.Trigger>、または <xref:System.Windows.DataTrigger> で使用します。 コード内で <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドを使用することもできます。

各 <xref:System.Windows.Media.Animation.Storyboard> の開始方法がサポートされているさまざまな場所 (インスタンス単位、スタイル、コントロール テンプレート、データ テンプレート) を次の表に示します。 "インスタンス単位" とは、スタイル、コントロール テンプレート、またはデータ テンプレート内のインスタンスではなく、オブジェクトのインスタンスに直接アニメーションまたはストーリーボードを適用する方法のことです。

|ストーリーボードが開始される場所|インスタンス単位|スタイル|コントロール テンプレート|データ テンプレート|例|
|--------------------------------|-------------------|-----------|----------------------|-------------------|-------------|
|<xref:System.Windows.Media.Animation.BeginStoryboard> および <xref:System.Windows.EventTrigger>|はい|はい|はい|はい|[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard> およびプロパティ <xref:System.Windows.Trigger>|いいえ|はい|はい|はい|[プロパティ値が変化したときにアニメーションをトリガーする](how-to-trigger-an-animation-when-a-property-value-changes.md)|
|<xref:System.Windows.Media.Animation.BeginStoryboard> および <xref:System.Windows.DataTrigger>|いいえ|はい|はい|はい|[方法: データが変化したときにアニメーションをトリガーする](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/aa970679(v=vs.90))|
|<xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッド|はい|いいえ|いいえ|いいえ|[ストーリーボードを使ってプロパティをアニメーション化する](how-to-animate-a-property-by-using-a-storyboard.md)|

次の例では、<xref:System.Windows.Media.Animation.Storyboard> を使用して、<xref:System.Windows.Shapes.Rectangle> 要素の <xref:System.Windows.FrameworkElement.Width%2A> と、その <xref:System.Windows.Shapes.Rectangle> の描画に使用する <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> をアニメーション化します。

[!code-xaml[storyboards_ovw_snip_XAML#1](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#1)]

[!code-csharp[storyboards_ovw_snip#100](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#100)]

以下のセクションでは、<xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> および <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> 添付プロパティについて詳しく説明します。

<a name="targetingelementsandfreezables"></a>

## <a name="targeting-framework-elements-framework-content-elements-and-freezables"></a>フレームワーク要素、フレームワーク コンテンツ要素、およびフリーズ可能オブジェクトの対象化

アニメーションでは、そのターゲットを見つけるために、ターゲットの名前とアニメーション化するプロパティを認識する必要があることについては前のセクションで説明しました。 アニメーション化するプロパティを指定することは簡単で、アニメーション化するプロパティの名前を <xref:System.Windows.Media.Animation.Storyboard.TargetProperty?displayProperty=nameWithType> に設定するだけです。  アニメーション化するプロパティが含まれるオブジェクトの名前を指定するには、アニメーションの <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A?displayProperty=nameWithType> プロパティを設定します。

<xref:System.Windows.Setter.TargetName%2A> プロパティを機能させるには、ターゲット オブジェクトに名前が付いていなければなりません。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] での <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> への名前の割り当ては、<xref:System.Windows.Freezable> オブジェクトへの名前の割り当てとは異なります。

フレームワーク要素は、<xref:System.Windows.FrameworkElement> クラスを継承するクラスです。 フレームワーク要素の例としては、<xref:System.Windows.Window>、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Shapes.Rectangle> などがあります。 基本的に、ウィンドウ、パネル、およびコントロールはすべて要素です。 フレームワーク コンテンツ要素は、<xref:System.Windows.FrameworkContentElement> クラスを継承するクラスです。 フレームワーク コンテンツ要素の例としては、<xref:System.Windows.Documents.FlowDocument> や <xref:System.Windows.Documents.Paragraph> があります。 型がフレームワーク要素またはフレームワーク コンテンツ要素であるかどうかが明確でない場合は、Name プロパティが含まれているかどうかを確認します。 含まれている場合は、フレームワーク要素またはフレームワーク コンテンツ要素と考えられます。 確かめるには、その型のページの「継承階層」を参照してください。

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でフレームワーク要素またはフレームワーク コンテンツ要素の対象化を有効にするには、その <xref:System.Windows.FrameworkElement.Name%2A> プロパティを設定します。 コードでは、<xref:System.Windows.NameScope.RegisterName%2A> メソッドも使用する必要があります。要素の名前と要素を、それ用に作成した <xref:System.Windows.NameScope> に登録するためです。

次の例 (前の例からの抜粋) では、<xref:System.Windows.Shapes.Rectangle> (<xref:System.Windows.FrameworkElement> 型) に `MyRectangle` という名前を割り当てています。

[!code-xaml[storyboards_ovw_snip_XAML#2](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#2)]

[!code-csharp[storyboards_ovw_snip#102](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#102)]

名前が割り当てられると、その要素のプロパティはアニメーション化できます。

[!code-xaml[storyboards_ovw_snip_XAML#5](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#5)]

[!code-csharp[storyboards_ovw_snip#105](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#105)]

<xref:System.Windows.Freezable> 型は <xref:System.Windows.Freezable> クラスを継承するクラスです。 <xref:System.Windows.Freezable> の例として、<xref:System.Windows.Media.SolidColorBrush>、<xref:System.Windows.Media.RotateTransform>、<xref:System.Windows.Media.GradientStop> があります。

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で <xref:System.Windows.Freezable> をアニメーションの対象にするには、[x:Name ディレクティブ](../../../desktop-wpf/xaml-services/xname-directive.md)を使用して名前を割り当てます。 コードでは、<xref:System.Windows.NameScope.RegisterName%2A> メソッドを使用して、要素とその名前を、それ用に作成した <xref:System.Windows.NameScope> に登録します。

次の例では、<xref:System.Windows.Freezable> オブジェクトに名前を割り当てます。

[!code-xaml[storyboards_ovw_snip_XAML#3](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#3)]

[!code-csharp[storyboards_ovw_snip#103](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#103)]

これで、オブジェクトをアニメーションのターゲットにすることができます。

[!code-xaml[storyboards_ovw_snip_XAML#7](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/StoryboardsExample.xaml#7)]

[!code-csharp[storyboards_ovw_snip#107](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/StoryboardsExample.cs#107)]

<xref:System.Windows.Media.Animation.Storyboard> オブジェクトは、名前スコープを使用して <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> プロパティを解決します。 WPF 名前スコープの詳細については、「[WPF XAML 名前スコープ](../advanced/wpf-xaml-namescopes.md)」を参照してください。 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> プロパティが省略されている場合、アニメーションのターゲットは、アニメーションが定義されている要素、またはスタイルの場合にはスタイルが設定されている要素になります。

場合によっては、<xref:System.Windows.Freezable> オブジェクトに名前を割り当てることができません。 たとえば、<xref:System.Windows.Freezable> がリソースとして宣言されていたり、スタイル内でプロパティ値の設定に使用されている場合は、名前を割り当てることができません。 名前が割り当てられていないため、それを直接ターゲットにすることができません。ただし、間接的にターゲットにすることはできます。 以下のセクションでは、間接的な対象化の使用方法について説明します。

<a name="pathsyntaxforchangeable"></a>

## <a name="indirect-targeting"></a>間接的な対象化

<xref:System.Windows.Freezable> がリソースとして宣言されていたり、スタイル内でプロパティ値の設定に使用されているときなど、アニメーションで <xref:System.Windows.Freezable> を直接的にターゲットにできない場合があります。 この場合、直接的にターゲットにできなくても、<xref:System.Windows.Freezable> オブジェクトをアニメーション化することはできます。 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> プロパティに <xref:System.Windows.Freezable> の名前を設定するのではなく、<xref:System.Windows.Freezable> が "属している" 要素の名前を指定します。 たとえば、四角形要素の <xref:System.Windows.Shapes.Shape.Fill%2A> の設定に使用された <xref:System.Windows.Media.SolidColorBrush> はその四角形に属しています。 このブラシをアニメーション化するには、アニメーションの <xref:System.Windows.Media.Animation.Storyboard.TargetProperty> を設定するときに、<xref:System.Windows.Freezable> を使用して設定されたフレームワーク要素またはフレームワーク コンテンツ要素のプロパティで始まり、アニメーション化する <xref:System.Windows.Freezable> プロパティで終わるプロパティのチェーンを使用します。

[!code-xaml[storyboards_ovw_snip_XAML#33](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#33)]

[!code-csharp[storyboards_ovw_snip#134](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#134)]

<xref:System.Windows.Freezable> がフリーズしている場合は、複製が作成され、その複製がアニメーション化されることに注意してください。 この場合、元のオブジェクトは実際にはアニメーション化されないため、元のオブジェクトの <xref:System.Windows.Media.Animation.Animatable.HasAnimatedProperties%2A> プロパティは引き続き `false` を返します。 複製の詳細については、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。

また、間接的なプロパティの対象化を使用するとき、存在しないオブジェクトを対象化する可能性があることに注意してください。 たとえば、特定のボタンの <xref:System.Windows.Controls.Control.Background%2A> に <xref:System.Windows.Media.SolidColorBrush> が設定されているという想定でその色をアニメーション化しようとしたところ、実際にはボタンの背景を設定するために <xref:System.Windows.Media.LinearGradientBrush> が使用されていたとします。 このような場合、例外はスローされませんが、<xref:System.Windows.Media.LinearGradientBrush> が <xref:System.Windows.Media.SolidColorBrush.Color%2A> プロパティが変化に反応しないため、アニメーションには目に見える効果はありません。

以下のセクションでは、間接的なプロパティの対象化の構文について詳しく説明します。

<a name="xamlsyntaxchangeableproperty"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-xaml"></a>XAML でフリーズ可能オブジェクトのプロパティを間接的に対象化する

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] でフリーズ可能オブジェクトのプロパティをターゲットにするには、次の構文を使用します。

| |
|-|
|*ElementPropertyName* `.` *FreezablePropertyName*|

Where

- *ElementPropertyName* は、<xref:System.Windows.Freezable> を使用して設定される <xref:System.Windows.FrameworkElement> のプロパティです。

- *FreezablePropertyName* は、アニメーション化する <xref:System.Windows.Freezable> のプロパティです。

次のコードでは、四角形要素の <xref:System.Windows.Shapes.Shape.Fill%2A> の設定に使用された <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> をアニメーション化する方法を示します。

[!code-xaml[storyboards_ovw_snip_XAML#32](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#32)]

コレクションまたは配列に含まれるフリーズ可能オブジェクトをターゲットにしなければならない場合があります。

コレクションに含まれるフリーズ可能オブジェクトをターゲットにするには、次のパス構文を使用します。

| |
|-|
|*ElementPropertyName* `.Children[` *CollectionIndex* `].` *FreezablePropertyName*|

ここで、*CollectionIndex* は配列またはコレクションに含まれるオブジェクトのインデックスです。

たとえば、ある四角形の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.TransformGroup> リソースが適用されていて、それに含まれている変換の 1 つをアニメーション化しようとしているとします。

[!code-xaml[storyboards_ovw_snip_XAML#34](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#34)]

次のコードは、前の例で示した <xref:System.Windows.Media.RotateTransform> の <xref:System.Windows.Media.RotateTransform.Angle%2A> プロパティをアニメーション化する方法を示しています。

[!code-xaml[storyboards_ovw_snip_XAML#35](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip_XAML/CS/IndirectTargetingExample.xaml#35)]

<a name="targetingpropertyofchangeableincode"></a>

### <a name="indirectly-targeting-a-property-of-a-freezable-in-code"></a>コードでフリーズ可能オブジェクトのプロパティを間接的に対象化する

コードで、<xref:System.Windows.PropertyPath> オブジェクトを作成します。 <xref:System.Windows.PropertyPath> を作成するときに、<xref:System.Windows.PropertyPath.Path%2A> と <xref:System.Windows.PropertyPath.PathParameters%2A> を指定します。

<xref:System.Windows.PropertyPath.PathParameters%2A> を作成するには、依存関係プロパティ識別子フィールドの一覧が含まれる <xref:System.Windows.DependencyProperty> 型の配列を作成します。 最初の識別子フィールドは、<xref:System.Windows.Freezable> を使用して設定された <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> のプロパティ用です。 次の識別子フィールドは、ターゲットにする <xref:System.Windows.Freezable> のプロパティを表します。 これは、<xref:System.Windows.Freezable> を <xref:System.Windows.FrameworkElement> オブジェクトに結び付けるプロパティのチェーンと考えてください。

次の例に示す依存関係プロパティのチェーンでは、四角形要素の <xref:System.Windows.Shapes.Shape.Fill%2A> の設定に使用された <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> がターゲットになります。

[!code-csharp[storyboards_ovw_snip#135](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#135)]

<xref:System.Windows.PropertyPath.Path%2A> も指定する必要があります。 <xref:System.Windows.PropertyPath.Path%2A> は、<xref:System.Windows.PropertyPath.Path%2A> に <xref:System.Windows.PropertyPath.PathParameters%2A> の解釈方法を伝える <xref:System.String> です。 次の構文が使用されます。

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *FreezablePropertyArrayIndex* `)`|

Where

- *OwnerPropertyArrayIndex* は、<xref:System.Windows.Freezable> を使用して設定される <xref:System.Windows.FrameworkElement> オブジェクトのプロパティの識別子を含む <xref:System.Windows.DependencyProperty> 配列のインデックスです。

- *FreezablePropertyArrayIndex* は、ターゲットにするプロパティの識別子を含む <xref:System.Windows.DependencyProperty> 配列のインデックスです。

前の例で定義した <xref:System.Windows.PropertyPath.PathParameters%2A> を含む <xref:System.Windows.PropertyPath.Path%2A> の例を次に示します。

[!code-csharp[storyboards_ovw_snip#PropertyChainAndPath](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#propertychainandpath)]

次の例では、これまでの例のコードを組み合わせて、四角形要素の <xref:System.Windows.Shapes.Shape.Fill%2A> の設定に使用された <xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> をアニメーション化します。

[!code-csharp[storyboards_ovw_snip#137](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#137)]

コレクションまたは配列に含まれるフリーズ可能オブジェクトをターゲットにしなければならない場合があります。 たとえば、ある四角形の <xref:System.Windows.UIElement.RenderTransform%2A> プロパティに <xref:System.Windows.Media.TransformGroup> リソースが適用されていて、それに含まれている変換の 1 つをアニメーション化しようとしているとします。

[!code-xaml[storyboards_ovw_snip#142](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml#142)]

コレクションに含まれる <xref:System.Windows.Freezable> をターゲットにするには、次のパス構文を使用します。

| |
|-|
|`(` *OwnerPropertyArrayIndex* `).(` *CollectionChildrenPropertyArrayIndex* `)` `[` *CollectionIndex* `].(` *FreezablePropertyArrayIndex* `)`|

ここで、*CollectionIndex* は配列またはコレクションに含まれるオブジェクトのインデックスです。

<xref:System.Windows.Media.RotateTransform> の <xref:System.Windows.Media.RotateTransform.Angle%2A> プロパティ (<xref:System.Windows.Media.TransformGroup> 内の 2 番目の変換) をターゲットにするには、次の <xref:System.Windows.PropertyPath.Path%2A> および <xref:System.Windows.PropertyPath.PathParameters%2A>を使用します。

[!code-csharp[storyboards_ovw_snip#139](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#139)]

<xref:System.Windows.Media.TransformGroup> 内に含まれた <xref:System.Windows.Media.RotateTransform> の <xref:System.Windows.Media.RotateTransform.Angle%2A> をアニメーション化するためのコード全体を次の例に示します。

[!code-csharp[storyboards_ovw_snip#138](~/samples/snippets/csharp/VS_Snippets_Wpf/storyboards_ovw_snip/CSharp/IndirectTargetingExample.xaml.cs#138)]

### <a name="indirectly-targeting-with-a-freezable-as-the-starting-point"></a>開始点として Freezable を使用して間接的に対象化する

前のセクションで、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> で開始し、<xref:System.Windows.Freezable> サブプロパティへのプロパティ チェーンを作成することによって、<xref:System.Windows.Freezable> を間接的にターゲットにする方法について説明しました。 開始点として <xref:System.Windows.Freezable> を使用して、その <xref:System.Windows.Freezable> サブプロパティの 1 つを間接的にターゲットにすることもできます。 間接的な対象化で開始点として <xref:System.Windows.Freezable> を使用する際には、制限がもう 1 つ適用されます。開始 <xref:System.Windows.Freezable> と、間接的にターゲットにされたサブプロパティまでの各 <xref:System.Windows.Freezable> は、フリーズしてはなりません。

<a name="controllable_storyboards"></a>

## <a name="interactively-controlling-a-storyboard-in-xaml"></a>XAML での対話形式でのストーリーボードの制御

[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 内でストーリーボードを開始するには、<xref:System.Windows.Media.Animation.BeginStoryboard> トリガー アクションを使用します。 <xref:System.Windows.Media.Animation.BeginStoryboard> は、アニメーション化するオブジェクトおよびプロパティにアニメーションを配布し、ストーリーボードを開始します (このプロセスの詳細については「[アニメーションとタイミング システムの概要](animation-and-timing-system-overview.md)」をご覧ください)。<xref:System.Windows.Media.Animation.BeginStoryboard.Name%2A> プロパティを指定して <xref:System.Windows.Media.Animation.BeginStoryboard> に名前を付けると、制御可能なストーリーボードになります。 ストーリーボードが開始すると対話的に制御できます。 制御可能なストーリーボード アクションの一覧を次に示します。これらをイベント トリガーで使用して、ストーリーボードを制御します。

- <xref:System.Windows.Media.Animation.PauseStoryboard>:ストーリーボードを一時停止します。

- <xref:System.Windows.Media.Animation.ResumeStoryboard>:一時停止したストーリーボードを再開します。

- <xref:System.Windows.Media.Animation.SetStoryboardSpeedRatio>:ストーリーボードの速度を変更します。

- <xref:System.Windows.Media.Animation.SkipStoryboardToFill>:ストーリーボードをその塗りつぶし期間 (ある場合) の最後に進めます。

- <xref:System.Windows.Media.Animation.StopStoryboard>:ストーリーボードを停止します。

- <xref:System.Windows.Media.Animation.RemoveStoryboard>:ストーリーボードを削除します。

次の例では、制御可能なストーリーボード アクションを使用して、ストーリーボードを対話的に制御しています。

[!code-xaml[animation_ovws_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_snip/CS/ControllableStoryboardExample.xaml#controllablestoryboardexamplewholepage)]

<a name="controllable_storyboards_procedural"></a>

## <a name="interactively-controlling-a-storyboard-by-using-code"></a>コードを使用した対話形式でのストーリーボードの制御

トリガー アクションを使用してアニメーション化する方法については、前の例で説明しました。 コードでも、<xref:System.Windows.Media.Animation.Storyboard> クラスの対話型メソッドを使用してストーリーボードを制御できます。 コード内で <xref:System.Windows.Media.Animation.Storyboard> を対話型にするには、ストーリーボードの <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> メソッドの適切なオーバーロードを使用して、`true` を指定して制御可能にする必要があります。 詳細については、「<xref:System.Windows.Media.Animation.Storyboard.Begin%28System.Windows.FrameworkElement%2CSystem.Boolean%29>」ページをご覧ください。

<xref:System.Windows.Media.Animation.Storyboard> の開始後の操作に使用できるメソッドの一覧を次に示します。

- <xref:System.Windows.Media.Animation.Storyboard.Pause%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Resume%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Seek%2A>

- <xref:System.Windows.Media.Animation.Storyboard.SkipToFill%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Stop%2A>

- <xref:System.Windows.Media.Animation.Storyboard.Remove%2A>

これらのメソッドを使用する利点は、<xref:System.Windows.Trigger> または <xref:System.Windows.TriggerAction> オブジェクトを作成する必要がないことです。操作対象の制御可能な <xref:System.Windows.Media.Animation.Storyboard> の参照のみが必要です。

> [!NOTE]
> <xref:System.Windows.Media.Animation.Clock> で実行され、そのため <xref:System.Windows.Media.Animation.Storyboard> でも実行されるすべての対話形式のアクションは、タイミング エンジンの次の目盛りで発生します (これは次の描画の直前です)。 たとえば、<xref:System.Windows.Media.Animation.Storyboard.Seek%2A> メソッドを使用してアニメーション内の別のポイントにジャンプしても、プロパティ値はすぐには変化しません。値が変化するのはタイミング エンジンの次の目盛りです。

<xref:System.Windows.Media.Animation.Storyboard> クラスの対話型メソッドを使用して、アニメーションを適用および制御する方法を次の例に示します。

[!code-csharp[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/animation_ovws_procedural_snip/CSharp/ControllableStoryboardExample.cs#controllablestoryboardexamplewholepage)]
[!code-vb[animation_ovws_procedural_snip#ControllableStoryboardExampleWholePage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/animation_ovws_procedural_snip/visualbasic/controllablestoryboardexample.vb#controllablestoryboardexamplewholepage)]

<a name="usingstoryboardsinstyles"></a>

## <a name="animate-in-a-style"></a>スタイル内でアニメーション化を行う

<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用して <xref:System.Windows.Style> 内でアニメーションを定義できます。 <xref:System.Windows.Style> での <xref:System.Windows.Media.Animation.Storyboard> を使用したアニメーション化は、<xref:System.Windows.Media.Animation.Storyboard> を他の場所で使用する場合と似ていますが、次の 3 点が異なります。

- <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> を指定しません。常に、<xref:System.Windows.Media.Animation.Storyboard> のターゲットは <xref:System.Windows.Style> が適用される要素です。 <xref:System.Windows.Freezable> オブジェクトをターゲットにするには、間接的な対象化を使用する必要があります。 間接的な対象化の詳細については、「[間接的な対象化](#pathsyntaxforchangeable)」セクションを参照してください。

- <xref:System.Windows.EventTrigger> または <xref:System.Windows.Trigger> に <xref:System.Windows.EventTrigger.SourceName%2A> を指定できません。

- <xref:System.Windows.Media.Animation.Storyboard> またはアニメーションのプロパティ値を設定する際は、動的リソース参照およびデータ バインディング式を使用できません。 これは、<xref:System.Windows.Style> 内のものはすべてスレッドセーフである必要があり、タイイング システムは <xref:System.Windows.Media.Animation.Storyboard> オブジェクトをスレッドセーフにするために <xref:System.Windows.Freezable.Freeze%2A> を実行する必要があるためです。 <xref:System.Windows.Media.Animation.Storyboard> は、それ自体や子タイムラインに動的リソース参照またはデータ バインディング式が含まれる場合、フリーズできません。 フリーズおよびその他の <xref:System.Windows.Freezable> 機能の詳細については、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、<xref:System.Windows.Media.Animation.Storyboard> またはアニメーション イベントのイベント ハンドラーを宣言できません。

スタイル内でストーリーボードを定義する方法の例については、「[スタイル内でアニメーション化を行う](how-to-animate-in-a-style.md)」の例を参照してください。

<a name="defineAStoryboardInAControlTemplateSection"></a>

## <a name="animate-in-a-controltemplate"></a>ControlTemplate 内でアニメーション化を行う

<xref:System.Windows.Media.Animation.Storyboard> オブジェクトを使用して <xref:System.Windows.Controls.ControlTemplate> 内でアニメーションを定義できます。 <xref:System.Windows.Controls.ControlTemplate> での <xref:System.Windows.Media.Animation.Storyboard> を使用したアニメーション化は、<xref:System.Windows.Media.Animation.Storyboard> を他の場所で使用する場合と似ていますが、次の 2 点が異なります。

- <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> は、<xref:System.Windows.Controls.ControlTemplate> の子オブジェクトしか参照できません。 <xref:System.Windows.Media.Animation.Storyboard.TargetName%2A> が指定されない場合、アニメーションのターゲットは、<xref:System.Windows.Controls.ControlTemplate> が適用される要素になります。

- <xref:System.Windows.EventTrigger> または <xref:System.Windows.Trigger> の <xref:System.Windows.EventTrigger.SourceName%2A> は、<xref:System.Windows.Controls.ControlTemplate> の子オブジェクトしか参照できません。

- <xref:System.Windows.Media.Animation.Storyboard> またはアニメーションのプロパティ値を設定する際は、動的リソース参照およびデータ バインディング式を使用できません。 これは、<xref:System.Windows.Controls.ControlTemplate> 内のものはすべてスレッドセーフである必要があり、タイイング システムは <xref:System.Windows.Media.Animation.Storyboard> オブジェクトをスレッドセーフにするために <xref:System.Windows.Freezable.Freeze%2A> を実行する必要があるためです。 <xref:System.Windows.Media.Animation.Storyboard> は、それ自体や子タイムラインに動的リソース参照またはデータ バインディング式が含まれる場合、フリーズできません。 フリーズおよびその他の <xref:System.Windows.Freezable> 機能の詳細については、「[Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)」をご覧ください。

- [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、<xref:System.Windows.Media.Animation.Storyboard> またはアニメーション イベントのイベント ハンドラーを宣言できません。

<xref:System.Windows.Controls.ControlTemplate> でストーリーボードを定義する方法の例については、「[ControlTemplate 内でアニメーション化を行う](how-to-animate-in-a-controltemplate.md)」の例をご覧ください。

<a name="animateWhenAPropertyValueChanges"></a>

## <a name="animate-when-a-property-value-changes"></a>プロパティ値が変化したときにアニメーション化を行う

スタイル内およびコントロール テンプレート内では、トリガー オブジェクトを使用して、プロパティが変化したときにストーリーボードを開始します。 使用例については、「[方法: プロパティ値が変化したときにアニメーションをトリガーする](how-to-trigger-an-animation-when-a-property-value-changes.md)」および「[ControlTemplate 内でアニメーション化を行う](how-to-animate-in-a-controltemplate.md)」を参照してください。

プロパティの <xref:System.Windows.Trigger> オブジェクトによって適用されたアニメーションは、<xref:System.Windows.EventTrigger> アニメーションや、<xref:System.Windows.Media.Animation.Storyboard> メソッドで開始されたアニメーションより複雑な方法で動作します。  他の <xref:System.Windows.Trigger> オブジェクトによって定義されたアニメーションと "ハンドオフ" しますが、<xref:System.Windows.EventTrigger> およびメソッドでトリガーされたアニメーションとは複合 (Compose) されます。

## <a name="see-also"></a>関連項目

- [アニメーションの概要](animation-overview.md)
- [プロパティ アニメーションの手法の概要](property-animation-techniques-overview.md)
- [Freezable オブジェクトの概要](../advanced/freezable-objects-overview.md)
