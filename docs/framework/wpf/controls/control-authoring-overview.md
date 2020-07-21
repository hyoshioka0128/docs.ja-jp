---
title: コントロールの作成の概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [WPF], authoring overview
- authoring overview for controls [WPF]
ms.assetid: 3d864748-cff0-4e63-9b23-d8e5a635b28f
ms.openlocfilehash: a6ab5463cc28aa590454ae1304714d3d12ee7c6b
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646136"
---
# <a name="control-authoring-overview"></a>コントロールの作成の概要

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コントロール モデルの機能拡張により、新しいコントロールを作成する必要性が大幅に削減されます。 ただし、場合によっては、カスタム コントロールを作成する必要があります。 このトピックでは、カスタム コントロールを作成する必要性を最小限に抑える機能と、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のさまざまなコントロール作成モデルについて説明します。 また、新しいコントロールを作成する方法も示します。

<a name="when_to_write_a_new_control"></a>

## <a name="alternatives-to-writing-a-new-control"></a>新しいコントロールの作成に代わる方法

従来は、既存のコントロールをカスタマイズする場合、背景色、境界線の幅、フォントのサイズなど、コントロールの標準プロパティを変更するなどの範囲に制限されていました。 これらの定義済みのパラメーター以外に、コントロールの外観や動作にまでカスタマイズを拡張しようとすると、通常、既存のコントロールを継承し、コントロールを描画するメソッドをオーバーライドして、新しいコントロールを作成する必要がありました。  その方法は今でも選択できますが、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の場合、リッチ コンテンツ モデル、スタイル、テンプレート、トリガーを使用して、既存のコントロールをカスタマイズできます。 新しいコントロールを作成しなくても、これらの機能を使用して、カスタマイズされた一貫性のあるエクスペリエンスを得られる方法としては、次のような例が挙げられます。

- **リッチ コンテンツ。** 標準の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの多くがリッチ コンテンツをサポートしています。 たとえば、<xref:System.Windows.Controls.Button> のコンテンツ プロパティは <xref:System.Object> 型であるため、理論的にはどのようなものでも <xref:System.Windows.Controls.Button> 上に表示できます。  ボタンに画像とテキストを表示するには、画像と <xref:System.Windows.Controls.TextBlock> を <xref:System.Windows.Controls.StackPanel> に追加し、その <xref:System.Windows.Controls.StackPanel> を <xref:System.Windows.Controls.ContentControl.Content%2A> プロパティに割り当てます。 コントロールには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の視覚的要素と任意のデータを表示できるため、複雑な視覚化をサポートするために、新しいコントロールを作成したり、既存のコントロールを変更したりする必要性が少なくなります。 <xref:System.Windows.Controls.Button> のコンテンツ モデルや [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のその他のコンテンツ モデルの詳細については、「[WPF のコンテンツ モデル](wpf-content-model.md)」を参照してください。

- **スタイル** <xref:System.Windows.Style> は、コントロールのプロパティを表す値のコレクションです。 スタイルを使用すると、新しいコントロールを作成しなくても、必要なコントロールの外観と動作を備えた再利用可能な表現を作成できます。 たとえば、すべての <xref:System.Windows.Controls.TextBlock> コントロールにフォント サイズ 14 の赤色の Arial フォントを設定するとします。 そこで、リソースとしてスタイルを作成し、それに応じて、適切なプロパティを設定します。 すると、アプリケーションに追加する <xref:System.Windows.Controls.TextBlock> はすべて同じ外観になります。

- **データ テンプレート。** <xref:System.Windows.DataTemplate> を使用すると、コントロールにデータを表示する方法をカスタマイズできます。 たとえば、<xref:System.Windows.DataTemplate> を使用して、<xref:System.Windows.Controls.ListBox> にデータを表示する方法を指定できます。  この例については、「[データ テンプレートの概要](../data/data-templating-overview.md)」を参照してください。  <xref:System.Windows.DataTemplate> については、データの表示方法のカスタマイズのほか、UI 要素を含めることもでき、カスタム UI の柔軟性を高めることができます。  たとえば、<xref:System.Windows.DataTemplate> を使用して、<xref:System.Windows.Controls.ComboBox> を作成し、その各項目にチェック ボックスを付けることができます。

- **コントロール テンプレート。** [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のコントロールの多くでは、<xref:System.Windows.Controls.ControlTemplate> を使用して、コントロールの構造と外観が定義されています。これにより、コントロールの外観と機能を分離できます。 コントロールの <xref:System.Windows.Controls.ControlTemplate> を再定義すると、その外観を大幅に変更できます。  たとえば、信号機のような外観のコントロールが必要だとします。 このコントロールのユーザー インターフェイスと機能は単純です。  コントロールは 3 つの円で構成され、一度に点灯するのはそのうちの 1 つだけです。 少し考えた結果、<xref:System.Windows.Controls.RadioButton> を使用すると、一度に 1 つだけ選択する機能を実現できることに気付いたとします。しかし、<xref:System.Windows.Controls.RadioButton> の既定の外観は信号機のライトとは全然似ていません。  <xref:System.Windows.Controls.RadioButton> では、コントロール テンプレートを使用して外観を定義しているため、コントロールの要件に合わせて <xref:System.Windows.Controls.ControlTemplate> を再定義し、オプション ボタンで信号機を実現するのは簡単です。

  > [!NOTE]
  > <xref:System.Windows.Controls.RadioButton> では <xref:System.Windows.DataTemplate> を使用できますが、この例の場合、<xref:System.Windows.DataTemplate> では不十分です。  <xref:System.Windows.DataTemplate> では、コントロールのコンテンツの外観が定義されます。 <xref:System.Windows.Controls.RadioButton> の場合、コンテンツとは、<xref:System.Windows.Controls.RadioButton> が選択されているかどうかを示す円の右側に表示される内容です。  信号機の例では、オプション ボタンに必要なのは "点灯" する円だけです。 信号機の外観の要件が <xref:System.Windows.Controls.RadioButton> の既定の外観とは大きく異なるため、<xref:System.Windows.Controls.ControlTemplate> を再定義する必要があります。  一般的に、コントロールのコンテンツ (またはデータ) を定義するために <xref:System.Windows.DataTemplate> を使用し、コントロールの構成方法を定義するために <xref:System.Windows.Controls.ControlTemplate> を使用します。

- **トリガー。** <xref:System.Windows.Trigger> を使用すると、新しいコントロールを作成しなくても、コントロールの外観と動作を動的に変更できます。 たとえば、複数の <xref:System.Windows.Controls.ListBox> コントロールを使用するアプリケーションがあり、各 <xref:System.Windows.Controls.ListBox> の選択項目を赤色の太字で表示するとします。 まず思いつくのは、<xref:System.Windows.Controls.ListBox> を継承したクラスを作成して、<xref:System.Windows.Controls.Primitives.Selector.OnSelectionChanged%2A> メソッドをオーバーライドし、選択項目の外観を変更する方法ですが、<xref:System.Windows.Controls.ListBoxItem> のスタイルに選択項目の外観を変更するトリガーを追加する方法の方が適切です。 トリガーを使用すると、プロパティ値を変更したり、プロパティ値に基づいた処理を実行したりできます。 <xref:System.Windows.EventTrigger> を使用すると、イベント発生時に処理を実行できます。

スタイル、テンプレート、トリガーの詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。

一般に、既存のコントロールと同じ機能を持ち、外観が異なるコントロールが必要な場合は、このセクションで説明した方法のいずれかを使用して、既存のコントロールの外観を変更できないかどうかをまず検討することをお勧めします。

<a name="models_for_control_authoring"></a>

## <a name="models-for-control-authoring"></a>コントロール作成モデル

リッチ コンテンツ モデル、スタイル、テンプレート、トリガーを使用すると、新しいコントロールを作成する必要性が最小限に抑えられます。 ただし、新しいコントロールを作成する必要がある場合は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の各種のコントロール作成モデルを理解することが重要です。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、コントロールを作成するための一般的なモデルが 3 つあり、各モデルはそれぞれ異なる機能と柔軟性レベルを備えています。 3 つのモデルの基底クラスは、<xref:System.Windows.Controls.UserControl>、<xref:System.Windows.Controls.Control>、<xref:System.Windows.FrameworkElement> です。

### <a name="deriving-from-usercontrol"></a>UserControl からの派生

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でコントロールを作成する方法で最も簡単なのは、<xref:System.Windows.Controls.UserControl> から派生する方法です。 <xref:System.Windows.Controls.UserControl> を継承するコントロールを作成するときは、<xref:System.Windows.Controls.UserControl> に既存のコンポーネントを追加し、コンポーネントに名前を付けて、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] でイベント ハンドラーを参照します。 次に、指定の要素を参照し、コードでイベント ハンドラーを定義します。 この開発モデルは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] でのアプリケーション開発に使用されるモデルとよく似ています。

<xref:System.Windows.Controls.UserControl> が正しく構築されていれば、リッチ コンテンツ、スタイル、トリガーの利点を活用できます。 ただし、<xref:System.Windows.Controls.UserControl> を継承したコントロールの場合、そのユーザーは <xref:System.Windows.DataTemplate> または <xref:System.Windows.Controls.ControlTemplate> を使用して、外観をカスタマイズすることができません。  <xref:System.Windows.Controls.Control> クラスまたはその派生クラスのいずれか (<xref:System.Windows.Controls.UserControl> 以外) から派生して、テンプレートをサポートするカスタム コントロールを作成する必要があります。

#### <a name="benefits-of-deriving-from-usercontrol"></a>UserControl からの派生の利点

次のすべての項目に該当する場合、<xref:System.Windows.Controls.UserControl> から派生することを検討してください。

- アプリケーションの構築と同じ方法でコントロールをビルドする必要がある場合。

- コントロールが既存のコンポーネントのみで構成されている場合。

- 複雑なカスタマイズをサポートする必要がない場合。

### <a name="deriving-from-control"></a>Control からの派生

<xref:System.Windows.Controls.Control> クラスからの派生は、既存の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの多くで使用されるモデルです。 <xref:System.Windows.Controls.Control> クラスから継承したコントロールを作成するときは、テンプレートを使用して、その外観を定義します。 これにより、操作ロジックと視覚的表現とが分離されます。 また、イベントの代わりにコマンドとバインディングを使用し、<xref:System.Windows.Controls.ControlTemplate> での要素参照をできる限り避けることによって、UI とロジックを分離できます。  コントロールの UI とロジックが適切に分離されていると、コントロールのユーザーは、コントロールの <xref:System.Windows.Controls.ControlTemplate> を再定義して、その外観をカスタマイズできます。 カスタム <xref:System.Windows.Controls.Control> の作成は、<xref:System.Windows.Controls.UserControl> の作成ほど単純ではありませんが、カスタム <xref:System.Windows.Controls.Control> を使用すると、より高い柔軟性が得られます。

#### <a name="benefits-of-deriving-from-control"></a>Control からの派生の利点

次のいずれかの項目に該当する場合は、<xref:System.Windows.Controls.UserControl> クラスを使用する代わりに、<xref:System.Windows.Controls.Control> から派生することを検討してください。

- <xref:System.Windows.Controls.ControlTemplate> を使用して、コントロールの外観をカスタマイズ可能にする必要がある場合。

- コントロールがさまざまなテーマをサポートする必要がある場合。

### <a name="deriving-from-frameworkelement"></a>FrameworkElement からの派生

<xref:System.Windows.Controls.UserControl> または <xref:System.Windows.Controls.Control> から派生されたコントロールは、既存の要素の構成に依存します。 多くの状況では、それで問題ありません。<xref:System.Windows.FrameworkElement> を継承するどのオブジェクトも <xref:System.Windows.Controls.ControlTemplate> に含めることができるためです。 しかし、場合によっては、単純な要素コンポジションでは、コントロールの外観に必要な機能を実現できないことがあります。 このような状況では、<xref:System.Windows.FrameworkElement> のコンポーネントをベースにするのが適切な選択です。

<xref:System.Windows.FrameworkElement> ベースのコンポーネントを作成するには、ダイレクト レンダリングとカスタム要素コンポジションの 2 つの標準的な方法があります。 ダイレクト レンダリングでは、<xref:System.Windows.FrameworkElement> の <xref:System.Windows.UIElement.OnRender%2A> メソッドをオーバーライドし、コンポーネントのビジュアルを明示的に定義する <xref:System.Windows.Media.DrawingContext> 操作を実行します。 これは、<xref:System.Windows.Controls.Image> と <xref:System.Windows.Controls.Border> で使用される方法です。 カスタム要素コンポジションでは、<xref:System.Windows.Media.Visual> 型のオブジェクトを使用して、コンポーネントの外観を構成します。 例については、「[DrawingVisual オブジェクトの使用](../graphics-multimedia/using-drawingvisual-objects.md)」を参照してください。 <xref:System.Windows.Controls.Primitives.Track> は、カスタム要素コンポジションを使用する [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のコントロールの例です。 同じコントロールでダイレクト レンダリングとカスタム要素コンポジションを混在させることもできます。

#### <a name="benefits-of-deriving-from-frameworkelement"></a>FrameworkElement からの派生の利点

次のいずれかの項目に該当する場合、<xref:System.Windows.FrameworkElement> から派生することを検討してください。

- コントロールの外観について、単純な要素コンポジションが提供する以上の厳密な制御を必要とする場合。

- 独自のレンダリング ロジックを定義して、コントロールの外観を定義する必要がある場合。

- <xref:System.Windows.Controls.UserControl> および <xref:System.Windows.Controls.Control> を使用する方法では実現できない新しい方法で既存の要素を構成する必要がある場合。

<a name="control_authoring_basics"></a>

## <a name="control-authoring-basics"></a>コントロール作成の基本

既に説明したように、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の最も強力な機能の 1 つは、コントロールの基本的なプロパティ設定だけでは不可能な外観や動作の変更を実現し、しかもカスタム コントロールを作成する必要がないということです。 スタイル設定、データ バインディング、トリガーの各機能は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティ システムおよび [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] イベント システムによって実現されています。 以降のセクションでは、カスタム コントロールのユーザーが、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に付属のコントロールと同じように、これらの機能を使用できるようにするために、カスタム コントロールの作成に使用するモデルに関係なく、従う必要があるプラクティスについて説明します。

### <a name="use-dependency-properties"></a>依存関係プロパティの使用

プロパティが依存関係プロパティである場合、以下の操作が可能です。

- スタイルのプロパティを設定する。

- プロパティをデータ ソースにバインドする。

- プロパティの値として、動的リソースを使用する。

- プロパティ名をアニメーション化する。

コントロールのプロパティがこれらの機能のいずれかをサポートす必要がある場合、それを依存関係プロパティとして実装する必要があります。 次の例では、以下の処理を実行して、`Value` という名前の依存関係プロパティを定義します。

- `ValueProperty` という名前の <xref:System.Windows.DependencyProperty> 識別子を、`public` `static` `readonly` フィールドとして定義します。

- <xref:System.Windows.DependencyProperty.Register%2A?displayProperty=nameWithType> を呼び出して、プロパティ システムにプロパティ名を登録し、次の項目を指定します。

  - プロパティの名前。

  - プロパティの型。

  - プロパティを所有する型。

  - プロパティのメタデータ。 メタデータには、プロパティの既定値、<xref:System.Windows.CoerceValueCallback> および <xref:System.Windows.PropertyChangedCallback> が含まれています。

- プロパティの `get` アクセサーと `set` アクセサーを実装することにより、依存関係プロパティの登録名と同じ `Value` という名前で CLR ラッパー プロパティを定義します。 `get` アクセサーと `set` アクセサーは、それぞれ <xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> しか呼び出すことができないことに注意してください。 依存関係プロパティのアクセサーには、その他のロジックを含めないことをお勧めします。クライアントおよび [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、アクセサーが省略され、<xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> が直接呼び出されることがあるためです。 たとえば、プロパティがデータ ソースにバインドされている場合、プロパティの `set` アクセサーは呼び出されません。  get アクセサーと set アクセサーに他のロジックを追加するのではなく、<xref:System.Windows.ValidateValueCallback>、<xref:System.Windows.CoerceValueCallback>、および <xref:System.Windows.PropertyChangedCallback> の各デリゲートを使用して、値の変更時に応答したり、値を確認したりします。  これらのコールバックの詳細については、「[依存関係プロパティのコールバックと検証](../advanced/dependency-property-callbacks-and-validation.md)」を参照してください。

- <xref:System.Windows.CoerceValueCallback> に対応する、`CoerceValue` という名前のメソッドを定義します。 `CoerceValue` によって、`Value` は `MinValue` 以上で `MaxValue` 以下になります。

- <xref:System.Windows.PropertyChangedCallback> に対応する、`OnValueChanged` という名前のメソッドを定義します。 `OnValueChanged` では、<xref:System.Windows.RoutedPropertyChangedEventArgs%601> オブジェクトが作成され、`ValueChanged` ルーティング イベントの生成が準備されます。 ルーティング イベントについては、次のセクションで説明します。

[!code-csharp[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#dependencyproperty)]
[!code-vb[UserControlNumericUpDown#DependencyProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#dependencyproperty)]

詳細については、「[カスタム依存関係プロパティ](../advanced/custom-dependency-properties.md)」を参照してください。

### <a name="use-routed-events"></a>ルーティング イベントの使用

依存関係プロパティで CLR プロパティの概念が追加機能によって拡張されるのと同様に、ルーティング イベントでは、標準の CLR イベントの概念が拡張されます。 新しい [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロール作成する場合、イベントをルーティング イベントとして実装することをお勧めします。ルーティング イベントは以下の機能をサポートしているためです。

- 複数のコントロールの親でイベントを処理できます。 イベントがバブル イベントの場合、要素ツリー内の単一の親はイベントをサブスクライブできます。 これにより、アプリケーション開発者は、複数のコントロールのイベントに 1 つのハンドラーで対応できます。 たとえば、<xref:System.Windows.Controls.ListBox> の各項目に含まれるコントロール (<xref:System.Windows.DataTemplate> に含まれているため) の場合、アプリケーション開発者は、コントロールのイベントに対応するイベント ハンドラーを <xref:System.Windows.Controls.ListBox> で定義できます。 いずれかのコントロールでイベントが発生するたびに、そのイベント ハンドラーが呼び出されます。

- ルーティング イベントは <xref:System.Windows.EventSetter> で使用できます。これにより、アプリケーション開発者はイベントのハンドラーをスタイル内で指定できます。

- ルーティング イベントは <xref:System.Windows.EventTrigger> で使用でき、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用したプロパティのアニメーション化に役立ちます。 詳しくは、「 [アニメーションの概要](../graphics-multimedia/animation-overview.md)」をご覧ください。

次に示す例では、以下の処理を実行して、ルーティング イベントを定義します。

- `ValueChangedEvent` という名前の <xref:System.Windows.RoutedEvent> 識別子を、`public` `static` `readonly` フィールドとして定義します。

- <xref:System.Windows.EventManager.RegisterRoutedEvent%2A?displayProperty=nameWithType> メソッドを呼び出して、ルーティング イベントを登録します。 この例では、<xref:System.Windows.EventManager.RegisterRoutedEvent%2A> を呼び出すときに、次の情報を指定します。

  - イベントの名前が `ValueChanged` であること。

  - ルーティング方法が <xref:System.Windows.RoutingStrategy.Bubble> であること。ソース (イベントを発生させるオブジェクト) のイベント ハンドラーがまず呼び出され、その後、ソースの親要素のイベント ハンドラーが、最も近い親要素のイベント ハンドラーから順に呼び出されるルーティング方法です。

  - イベント ハンドラーの型が <xref:System.Windows.RoutedPropertyChangedEventHandler%601> で、<xref:System.Decimal> 型で構築されていること。

  - イベントを所有する型が `NumericUpDown` であること。

- `ValueChanged` という名前のパブリック イベントを宣言し、イベント アクセサー宣言を含めます。 この例では、`add` アクセサー宣言で <xref:System.Windows.UIElement.AddHandler%2A> を、`remove` アクセサーの宣言で <xref:System.Windows.UIElement.RemoveHandler%2A> をそれぞれ呼び出して、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] イベント サービスを使用します。

- `ValueChanged`イベントを発生させる、保護された仮想メソッド `OnValueChanged` を作成します。

[!code-csharp[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml.cs#routedevent)]
[!code-vb[UserControlNumericUpDown#RoutedEvent](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDown/visualbasic/numericupdown.xaml.vb#routedevent)]

詳細については、「[ルーティング イベントの概要](../advanced/routed-events-overview.md)」および「[カスタム ルーティング イベントを作成する](../advanced/how-to-create-a-custom-routed-event.md)」を参照してください。

### <a name="use-binding"></a>バインディングの使用

コントロールの UI とロジックを分離するには、データ バインディングを使用する方法もあります。 これは、<xref:System.Windows.Controls.ControlTemplate> を使用してコントロールの外観を定義する場合に、特に重要です。 データ バインディングを使用すると、コードから UI の特定の部分を参照する必要性がなくなる場合があります。 <xref:System.Windows.Controls.ControlTemplate> 内の要素の参照を避けることをお勧めします。コードで <xref:System.Windows.Controls.ControlTemplate> 内の要素を参照する場合、<xref:System.Windows.Controls.ControlTemplate> が変更されたときに、新しい <xref:System.Windows.Controls.ControlTemplate> に参照先の要素を含める必要があるためです。

次の例では、`NumericUpDown` コントロールの <xref:System.Windows.Controls.TextBlock> を更新し、名前を割り当てて、コード内の名前を使用してテキスト ボックスを参照しています。

[!code-xaml[UserControlNumericUpDownSimple#UIRefMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml#uirefmarkup)]

[!code-csharp[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDownSimple/CSharp/NumericUpDown.xaml.cs#uirefcode)]
[!code-vb[UserControlNumericUpDownSimple#UIRefCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/UserControlNumericUpDownSimple/VisualBasic/NumericUpDown.xaml.vb#uirefcode)]

次の例では、バインディングを使用して同じことを実現しています。

[!code-xaml[UserControlNumericUpDown#Binding](~/samples/snippets/csharp/VS_Snippets_Wpf/UserControlNumericUpDown/CSharp/NumericUpDown.xaml#binding)]

データ バインディングの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。

### <a name="design-for-designers"></a>デザイナーに対応したデザイン

Visual Studio 用の WPF デザイナーでカスタム WPF コントロールのサポート (たとえば、[プロパティ] ウィンドウでのプロパティ編集) を利用するには、以下のガイドラインに従います。  WPF デザイナーでの開発の詳細については、「[Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)」を参照してください。

#### <a name="dependency-properties"></a>依存関係プロパティ

「依存関係プロパティの使用」で説明したように、CLR の `get` アクセサーと `set` アクセサーを実装します。 デザイナーは、ラッパーを使用して依存関係プロパティの存在を検出する場合がありますが、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] およびコントロールのクライアントと同様、プロパティを取得または設定するときにアクセサーを呼び出す必要はありません。

#### <a name="attached-properties"></a>アタッチされるプロパティ

以下のガイドラインに従って、カスタム コントロールに添付プロパティを実装する必要があります。

- *PropertyName*`Property` という形式の `public` `static` `readonly` <xref:System.Windows.DependencyProperty> を、<xref:System.Windows.DependencyProperty.RegisterAttached%2A> メソッドを使用して作成します。 <xref:System.Windows.DependencyProperty.RegisterAttached%2A> に渡されるプロパティ名は、*PropertyName* と一致している必要があります。

- `Set`*PropertyName* および `Get`*PropertyName* という名前の `public` `static` CLR メソッドのペアを実装します。 いずれのメソッドでも、<xref:System.Windows.DependencyProperty> の派生クラスを最初の引数として受け取る必要があります。 また、`Set`*PropertyName* メソッドでは、プロパティの登録データ型と同じ型の引数も受け取ります。 `Get`*PropertyName*メソッドでは、同じ型の値を返す必要があります。 `Set`*PropertyName*メソッドがない場合、プロパティは読み取り専用としてマークされます。

- `Set`*PropertyName* および `Get`*PropertyName* は、それぞれ、対象の依存関係オブジェクトの <xref:System.Windows.DependencyObject.GetValue%2A> メソッドおよび <xref:System.Windows.DependencyObject.SetValue%2A> メソッドのに直接転送する必要があります。 デザイナーが添付プロパティにアクセスするには、メソッド ラッパー経由で呼び出す場合もあれば、対象の依存関係オブジェクトを直接呼び出す場合もあります。

添付プロパティの詳細については、「[添付プロパティの概要](../advanced/attached-properties-overview.md)」を参照してください。

### <a name="define-and-use-shared-resources"></a>共有リソースの定義と使用

アプリケーションと同じアセンブリにコントロールを含めることも、複数のアプリケーションが使用できる別のアセンブリにコントロールをパッケージ化することもできます。 このトピックで説明した情報の大部分は、使用する方法に関係なく適用されます。  ただし、1 つだけ例外があります。  アプリケーションと同じアセンブリ内にコントロールを配置する場合、App.xaml ファイルにグローバル リソースを自由に追加できます。 しかし、コントロールだけを含むアセンブリには、<xref:System.Windows.Application> オブジェクトが関連付けられないため、App.xaml ファイルは使用できません。

アプリケーションがリソースを検索するときは、次に示す順序で 3 つのレベルを検索します。

1. 要素レベル。

   システムは、リソースを参照する要素から検索を開始し、ルート要素に到達するまで、論理上の親のリソースの検索を継続します。

2. アプリケーション レベル。

   <xref:System.Windows.Application> オブジェクトで定義されたリソース。

3. テーマ レベル。

   テーマ レベルのディクショナリは、Themes という名前のサブフォルダーに格納されています。  Themes フォルダー内のファイルはテーマに対応しています。  たとえば、Aero.NormalColor.xaml、Luna.NormalColor.xaml、Royale.NormalColor.xaml などのファイルがあります。  generic.xaml という名前のファイルが含まれている場合もあります。  システムがテーマ レベルでリソースを検索するとき、最初にテーマ固有のファイル内を検索し、次に generic.xaml 内を検索します。

アプリケーションとは別のアセンブリ内にコントロールを含めるときは、グローバル リソースを要素レベルまたはテーマ レベルに配置する必要があります。 どちらに配置する場合も、それぞれの利点があります。

#### <a name="defining-resources-at-the-element-level"></a>要素レベルでのリソース定義

カスタムのリソース ディクショナリを作成し、それをコントロールのリソース ディクショナリと結合することによって、共有リソースを要素レベルで定義できます。  このメソッドで定義する場合は、リソース ファイルに任意の名前を付けて、コントロールと同じフォルダーに配置できます。 要素レベルでのリソースでは、単純な文字列をキーとして使用することもできます。 次の例では、Dictionary1.xaml という名前の <xref:System.Windows.Media.LinearGradientBrush> リソース ファイルを作成します。

[!code-xaml[SharedResources#1](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/Dictionary1.xaml#1)]

ディクショナリを定義したら、それをコントロールのリソース ディクショナリにマージする必要があります。  これには、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] またはコードを使用します。

次の例では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] を使用してリソース ディクショナリを結合します。

[!code-xaml[SharedResources#2](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml#2)]

この方法の欠点は、参照するたびに <xref:System.Windows.ResourceDictionary> オブジェクトが作成されることです。  たとえば、ライブラリ内に 10 個のカスタム コントロールがあり、XAML を使用して各コントロール用の共有リソース ディクショナリを結合する場合、同一の <xref:System.Windows.ResourceDictionary> オブジェクトが 10 個作成されます。  これを回避するには、コード内でリソースを結合し、結果として作成される <xref:System.Windows.ResourceDictionary> を返す、静的クラスを作成します。

次の例では、共有の <xref:System.Windows.ResourceDictionary> を返すクラスを作成します。

[!code-csharp[SharedResources#3](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/SharedDictionaryManager.cs#3)]

次の例では、`InitializeComponent` を呼び出す前に、共有リソースをコントロールのコンス トラクター内でカスタム コントロールのリソースと結合します。  `SharedDictionaryManager.SharedDictionary` は静的プロパティであるため、<xref:System.Windows.ResourceDictionary> が作成されるのは 1 回だけです。 `InitializeComponent` が呼び出される前に、リソース ディクショナリが結合されため、コントロールは [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル内でリソースを使用できます。

[!code-csharp[SharedResources#4](~/samples/snippets/csharp/VS_Snippets_Wpf/SharedResources/CS/ShapeResizer.xaml.cs#4)]

#### <a name="defining-resources-at-the-theme-level"></a>テーマ レベルでのリソース定義

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、さまざまな Windows テーマ用にリソースを作成できます。  コントロールの作成者は、特定のテーマ用のリソースを定義して、使用するテーマに応じてコントロールの外観を変更できます。 たとえば、Windows クラシックのテーマ (Windows 2000 の既定のテーマ) での <xref:System.Windows.Controls.Button> の外観は、Windows Luna テーマ (Windows XP の既定のテーマ) での <xref:System.Windows.Controls.Button> とは異なります。これは、<xref:System.Windows.Controls.Button> では、テーマごとに異なる <xref:System.Windows.Controls.ControlTemplate> が使用されるためです。

テーマ固有のリソースは、固有のファイル名でリソース ディクショナリに保持されます。 これらのファイルは、コントロールが格納されているフォルダーのサブフォルダーである `Themes` フォルダー内に配置する必要があります。 次の表は、リソース ディクショナリ ファイルと、各ファイルに関連付けられているテーマを示しています。

|リソース ディクショナリ ファイル名|Windows テーマ|
|-----------------------------------|-------------------|
|`Classic.xaml`|Windows XP のクラシックな Windows 9x/2000 の外観|
|`Luna.NormalColor.xaml`|Windows XP の既定の青のテーマ|
|`Luna.Homestead.xaml`|Windows XP のオリーブのテーマ|
|`Luna.Metallic.xaml`|Windows XP のシルバーのテーマ|
|`Royale.NormalColor.xaml`|Windows XP Media Center Edition の既定テーマ|
|`Aero.NormalColor.xaml`|Windows Vista の既定テーマ|

すべてのテーマのリソースを定義する必要はありません。 特定のテーマについてリソースが定義されていない場合、コントロールはリソースの `Classic.xaml` を確認します。 現在のテーマに対応するファイルや `Classic.xaml` でリソースが定義されていない場合、コントロールは汎用のリソースを使用します。汎用のリソースは、`generic.xaml` という名前のリソース ディクショナリ ファイルにあります。  `generic.xaml` ファイルは、テーマ固有のリソース ディクショナリ ファイルと同じフォルダーに配置されています。 `generic.xaml` は、特定の Windows テーマには対応していませんが、テーマ レベルのディクショナリであることに変わりありません。

[C#](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp) または [Visual Basic](https://github.com/dotnet/docs/tree/master/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic) の、テーマおよび UI オートメーションがサポートされた NumericUpDown カスタム コントロールのサンプルには、`NumericUpDown` コントロール用の 2 つのリソース ディクショナリが含まれています。1 つは generic.xaml で、もう 1 つは Luna.NormalColor.xaml です。

テーマ固有のリソース ディクショナリ ファイルのいずれかに <xref:System.Windows.Controls.ControlTemplate> を配置する場合、次の例に示すように、コントロール用の静的コンストラクターを作成し、<xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> で <xref:System.Windows.DependencyProperty.OverrideMetadata%28System.Type%2CSystem.Windows.PropertyMetadata%29> メソッドを呼び出す必要があります。

[!code-csharp[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/CSharp/NumericUpDown.cs#staticconstructor)]
[!code-vb[CustomControlNumericUpDownOneProject#StaticConstructor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDownOneProject/visualbasic/numericupdown.vb#staticconstructor)]

##### <a name="defining-and-referencing-keys-for-theme-resources"></a>テーマ リソース用のキーの定義と参照

要素レベルでリソースを定義するときに、文字列をキーとして割り当て、その文字列を使用してリソースにアクセスできます。 テーマ レベルでリソースを定義するときは、<xref:System.Windows.ComponentResourceKey> をキーとして使用する必要があります。  次の例では、generic.xaml でリソースを定義します。

[!code-xaml[ThemeResourcesControlLibrary#5](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/Themes/generic.xaml#5)]

次の例では、<xref:System.Windows.ComponentResourceKey> をキーとして指定して、リソースを参照します。

[!code-xaml[ThemeResourcesControlLibrary#6](~/samples/snippets/csharp/VS_Snippets_Wpf/ThemeResourcesControlLibrary/CS/NumericUpDown.xaml#6)]

##### <a name="specifying-the-location-of-theme-resources"></a>テーマ リソースの場所の指定

コントロールのリソースを見つけるには、アセンブリにコントロール固有のリソースが含まれていることを、ホスト アプリケーションが認識する必要があります。 これを可能にするには、コントロールが含まれているアセンブリに <xref:System.Windows.ThemeInfoAttribute> を追加します。 <xref:System.Windows.ThemeInfoAttribute> には、汎用のリソースの場所を指定する <xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> プロパティと、テーマ固有のリソースの場所を指定する <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> プロパティがあります。

次の例では、<xref:System.Windows.ThemeInfoAttribute.GenericDictionaryLocation%2A> プロパティと <xref:System.Windows.ThemeInfoAttribute.ThemeDictionaryLocation%2A> プロパティを <xref:System.Windows.ResourceDictionaryLocation.SourceAssembly> に設定し、汎用リソースとテーマ固有のリソースがコントロールと同じアセンブリ内にあることを指定しています。

[!code-csharp[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/csharp/VS_Snippets_Wpf/CustomControlNumericUpDown/CSharp/CustomControlLibrary/Properties/AssemblyInfo.cs#themessection)]
[!code-vb[CustomControlNumericUpDown#ThemesSection](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CustomControlNumericUpDown/visualbasic/customcontrollibrary/my project/assemblyinfo.vb#themessection)]

## <a name="see-also"></a>関連項目

- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [WPF におけるパッケージの URI](../app-development/pack-uris-in-wpf.md)
- [コントロールのカスタマイズ](control-customization.md)
