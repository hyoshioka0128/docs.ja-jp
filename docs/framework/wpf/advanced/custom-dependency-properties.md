---
title: カスタム依存関係プロパティ
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- implementing [WPF], wrappers
- registering properties [WPF]
- properties [WPF], metadata
- metadata [WPF], for properties
- custom dependency properties [WPF]
- properties [WPF], registering
- wrappers [WPF], implementing
- dependency properties [WPF], custom
ms.assetid: e6bfcfac-b10d-4f58-9f77-a864c2a2938f
ms.openlocfilehash: e4117d7add2a34d6d989d9222e7688361cf6b379
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646348"
---
# <a name="custom-dependency-properties"></a>カスタム依存関係プロパティ

このトピックは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーション開発者およびコンポーネントの作成者が、カスタム依存関係プロパティを作成したくなる理由を説明し、実装手順にくわえ、プロパティのパフォーマンス、使いやすさ、または多用性を向上させることができるいくつかの実装オプションについて説明します。

<a name="prerequisites"></a>

## <a name="prerequisites"></a>必須コンポーネント

このトピックは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスの既存の依存関係プロパティのコンシューマーの観点から依存関係プロパティを理解しており、「[依存関係プロパティの概要](dependency-properties-overview.md)」というトピックを読んでいることを前提としています。 このトピックの例を理解するには、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] について理解し、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの作成方法に精通している必要があります。

<a name="whatis"></a>

## <a name="what-is-a-dependency-property"></a>依存関係プロパティとは

共通言語ランタイム (CLR) プロパティを依存関係プロパティとして実装することで、プロパティでスタイル設定、データ バインディング、継承、アニメーション、および既定値のサポートを有効にすることができます。 依存関係プロパティは、<xref:System.Windows.DependencyProperty.Register%2A> メソッド (または <xref:System.Windows.DependencyProperty.RegisterReadOnly%2A>) を呼び出すことで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティ システムに登録され、<xref:System.Windows.DependencyProperty> 識別子フィールドによってバッキングされるプロパティです。 依存関係プロパティは、<xref:System.Windows.DependencyObject> 型でのみ使用できますが、<xref:System.Windows.DependencyObject> は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラス階層でかなり上位にあるため、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で使用可能なほとんどのクラスで依存関係プロパティをサポートすることができます。 依存関係プロパティと、これらをこの SDK で説明するために使用されている用語と規則の詳細については、「[依存関係プロパティの概要](dependency-properties-overview.md)」を参照してください。

<a name="example_dp"></a>

## <a name="examples-of-dependency-properties"></a>依存関係プロパティの例

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスで実装される依存関係プロパティの例は、<xref:System.Windows.Controls.Control.Background%2A> プロパティ、<xref:System.Windows.FrameworkElement.Width%2A> プロパティ、<xref:System.Windows.Controls.TextBox.Text%2A> など、多数あります。 クラスによって公開される各依存関係プロパティには、同じクラスで公開されている <xref:System.Windows.DependencyProperty> 型の対応するパブリックな静的フィールドがあります。 これが依存関係プロパティの識別子です。 この識別子は規則を使用して命名されます。依存関係プロパティの名前と文字列 `Property` がこれに付加されます。 たとえば、<xref:System.Windows.Controls.Control.Background%2A> プロパティに対応する <xref:System.Windows.DependencyProperty> 識別子フィールドは <xref:System.Windows.Controls.Control.BackgroundProperty> です。 識別子には、登録時の依存関係プロパティに関する情報が格納され、識別子はその後、<xref:System.Windows.DependencyObject.SetValue%2A> の呼び出しなど、依存関係プロパティが関係するその他の操作に使用されます。

「[依存関係プロパティの概要](dependency-properties-overview.md)」で説明されているように、"ラッパー" の実装により、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内のすべての依存関係プロパティ (ほとんどの添付プロパティを除く) も CLR プロパティです。 そのため、他の CLR プロパティで使用するのと同じ方法でラッパーが定義されている CLR アクセサーを呼び出すことで、コードから依存関係プロパティを取得または設定できます。 確立された依存関係プロパティのコンシューマーは、基になるプロパティ システムへの接続ポイントである、<xref:System.Windows.DependencyObject> のメソッド <xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> を、通常は使用しません。 むしろ、CLR プロパティの既存の実装では、識別子のフィールドを適切に使用して、プロパティの `get` および `set` のラッパーの実装内で、<xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> が既に呼び出されています。 カスタム依存関係プロパティを自分で実装する場合、同様の方法でラッパーを定義します。

<a name="backing_with_dp"></a>

## <a name="when-should-you-implement-a-dependency-property"></a>依存関係プロパティを実装すべき状況

クラスにプロパティを実装する場合、クラスが <xref:System.Windows.DependencyObject> から派生している限り、プロパティを <xref:System.Windows.DependencyProperty> 識別子でバッキングして、依存関係プロパティにすることができます。 シナリオのニーズによっては、プロパティを依存関係プロパティにすることが必要ない場合や適切でない場合もあります。 場合によっては、プロパティをプライベート フィールドでバッキングする一般的な手法で十分な場合もあります。 ただし、プロパティで次の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 機能の 1 つ以上をサポートする場合には、常に依存関係プロパティとしてプロパティを実装する必要があります。

- プロパティをスタイルで設定可能にする。 詳しくは、「 [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」をご覧ください。

- プロパティでデータ バインディングをサポートする。 データ バインディングの依存関係プロパティの詳細については、「[2 つのコントロールのプロパティをバインドする](../data/how-to-bind-the-properties-of-two-controls.md)」を参照してください。

- プロパティを動的リソース参照で設定可能にする。 詳細については、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」を参照してください。

- 要素ツリーの親要素からプロパティ値を自動的に継承する。 この場合、CLR アクセスのプロパティ ラッパーも作成する場合でも、<xref:System.Windows.DependencyProperty.RegisterAttached%2A> メソッドに登録します。 詳細については、「[プロパティ値の継承](property-value-inheritance.md)」を参照してください。

- プロパティをアニメーション化できるようにする。 詳しくは、「 [アニメーションの概要](../graphics-multimedia/animation-overview.md)」をご覧ください。

- プロパティの前の値が、プロパティ システム、環境、または、ユーザーによって行われたアクションによって変更された場合、または読み取りおよびスタイルの使用によって変更された場合に、プロパティ システムに報告させる。 プロパティのメタデータを使用すると、プロパティ システムがプロパティ値が明らかに変更されたと判断するたびに呼び出されるコールバック メソッドをプロパティで指定できます。 関連する概念は、プロパティ値の強制型変換です。 詳しくは、「[依存関係プロパティのコールバックと検証](dependency-property-callbacks-and-validation.md)」を参照してください。

- プロパティ値の変更に、要素のビジュアルを再構成するためのレイアウト システムが必要かどうかを報告するなど、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロセスでも使用されている確立されたメタデータ規則を使用する。 または、派生クラスが既定値などのメタデータに基づく特性を変更できるように、メタデータのオーバーライドを使用できるようする。

- カスタム コントロールのプロパティで、 **[プロパティ]** ウィンドウの編集などの Visual Studio WPF デザイナーのサポートを受ける。 詳しくは、「[コントロールの作成の概要](../controls/control-authoring-overview.md)」を参照してください。

これらのシナリオを検討するときに、完全に新しいプロパティを実装するよりも、既存の依存関係プロパティのメタデータをオーバーライドすることで、シナリオを実現できるかどうかも考慮する必要があります。 メタデータのオーバーライドが実用的かどうかは、シナリオとそのシナリオが既存の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 依存関係プロパティとクラスでの実装にどのくらい似ているかによって異なります。 既存のプロパティでメタデータをオーバーライドする方法の詳細については、「[依存関係プロパティのメタデータ](dependency-property-metadata.md)」を参照してください。

<a name="checklist"></a>

## <a name="checklist-for-defining-a-dependency-property"></a>依存関係プロパティを定義するためのチェックリスト

依存関係プロパティの定義は、次の 4 つの異なる概念で構成されます。 これらの概念は、一部は実装で最終的に 1 行のコードとして結合されるため、必ずしも厳密な手順である必要はありません。

- (省略可能) 依存関係プロパティのプロパティ メタデータを作成します。

- 所有者型とプロパティ値の型を指定して、プロパティ システムにプロパティ名を登録します。 プロパティのメタデータも指定します (使用している場合)。

- 所有者型で <xref:System.Windows.DependencyProperty> 識別子を `public` `static` `readonly` フィールドとして定義します。

- 名前が依存関係プロパティの名前と一致する CLR "ラッパー" プロパティを定義します。 CLR "ラッパー" プロパティの `get` と `set` のアクセサーを実装して、バッキングする依存関係プロパティと接続します。

<a name="registering"></a>

### <a name="registering-the-property-with-the-property-system"></a>プロパティ システムにプロパティを登録する

プロパティを依存関係プロパティにするためには、そのプロパティをプロパティ システムが保持するテーブルに登録し、その後のプロパティ システム操作で修飾子として使用する一意の識別子をプロパティに設定します。 これらの操作は、内部操作にすることも、プロパティ システム API を呼び出す独自のコードにすることもできます。 プロパティを登録するには、クラスの本文内 (クラス内部だが任意のメンバーの定義の外側) で <xref:System.Windows.DependencyProperty.Register%2A> メソッドを呼び出します。 識別子フィールドも <xref:System.Windows.DependencyProperty.Register%2A> メソッドの呼び出しによって、戻り値として提供されます。 <xref:System.Windows.DependencyProperty.Register%2A> の呼び出しが他のメンバー定義の外部で行われる理由は、この戻り値を使用して、<xref:System.Windows.DependencyProperty> 型の `public` `static` `readonly` フィールドをクラスの一部として割り当ておよび作成するからです。 このフィールドは、依存関係プロパティの識別子になります。

[!code-csharp[WPFAquariumSln#RegisterAG](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerag)]
[!code-vb[WPFAquariumSln#RegisterAG](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerag)]

<a name="nameconventions"></a>

### <a name="dependency-property-name-conventions"></a>依存関係プロパティの命名規則

依存関係プロパティについては、確立されている命名規則があり、例外的な状況を除き、必ず従う必要があります。

依存関係プロパティ自体には、基本的な名前 (この例では "AquariumGraphic") があります。この名前は、<xref:System.Windows.DependencyProperty.Register%2A> の最初のパラメーターとして指定されます。 この名前は、それぞれの登録型内で一意である必要があります。 基本型から継承された依存関係プロパティは、登録型の一部に既になっていると見なされ、継承されたプロパティの名前は、再度登録することはできません。 しかし、その依存関係プロパティが継承されていない場合でも、依存関係プロパティの所有者としてクラスを追加する方法があります。詳細については、「[依存関係プロパティのメタデータ](dependency-property-metadata.md)」を参照してください。

識別子フィールドを作成するときに、登録したプロパティの名前にサフィックス `Property` を付けて、このフィールドに名前を付けます。 このフィールドは、依存関係プロパティの識別子です。これは後でラッパー内で行う <xref:System.Windows.DependencyObject.SetValue%2A> と <xref:System.Windows.DependencyObject.GetValue%2A> の呼び出しの入力として、プロパティにアクセスする他のコード、独自のコード、許可した任意の外部コードのアクセス、プロパティ システムによって使用され、また [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサによって潜在的に使用されます。

> [!NOTE]
> クラス本体で依存関係プロパティを定義することは一般的な実装ですが、クラスの静的コンストラクターで依存関係プロパティを定義することもできます。 依存関係プロパティを初期化するために複数行のコードが必要な場合には、このアプローチが適している場合があります。

<a name="wrapper1"></a>

### <a name="implementing-the-wrapper"></a>"ラッパー" を実装する

ラッパーの実装では、`get` の実装で <xref:System.Windows.DependencyObject.GetValue%2A> を呼び出し、`set` の実装で <xref:System.Windows.DependencyObject.SetValue%2A> を呼び出す必要があります (わかりやすくするため、ここには元の登録の呼び出しとフィールドも示されています)。

例外的な状況を除き、ラッパーの実装では <xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> の操作のみをそれぞれ実行する必要があります。 この理由については、「[XAML 読み込みと依存関係プロパティ](xaml-loading-and-dependency-properties.md)」のトピックで説明しています。

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスで提供されているすべての既存のパブリックな依存関係プロパティは、この単純なラッパー実装モデルを使用します。依存関係プロパティのしくみの複雑さの大部分は、本質的にプロパティ システムの動作であるか、強制変換やプロパティ メタデータを通じたプロパティ変更のコールバックなど、その他の概念を通じて実装されます。

[!code-csharp[WPFAquariumSln#AGWithWrapper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#agwithwrapper)]
[!code-vb[WPFAquariumSln#AGWithWrapper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#agwithwrapper)]

ここでも、規則により、ラッパー プロパティの名前は、プロパティを登録した <xref:System.Windows.DependencyProperty.Register%2A> 呼び出しの最初のパラメーターとして選択して指定した名前と同じである必要があります。 プロパティが規則に従っていない場合、すべての可能な使用を無効にする必要はありませんが、次のような注目すべき問題がいくつか発生します。

- スタイルとテンプレートの一部が機能しない。

- ほとんどのツールとデザイナーは、適切に [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] をシリアル化するため、またはプロパティごとのレベルでのデザイナー環境のサポートを提供するために命名規則に依存する必要があります。

- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ローダーの現在の実装は、属性値を処理するときに、ラッパーを完全にバイパスして、名前付け規則に依存しています。 詳しくは、「[XAML 読み込みと依存関係プロパティ](xaml-loading-and-dependency-properties.md)」を参照してください。

<a name="metadata"></a>

### <a name="property-metadata-for-a-new-dependency-property"></a>新しい依存関係プロパティのプロパティ メタデータ

依存関係プロパティを登録するときに、プロパティ システムを通じて登録すると、プロパティの特性を格納するメタデータ オブジェクトが作成されます。 これらの特性の多くには、プロパティが <xref:System.Windows.DependencyProperty.Register%2A> の単純なシグネチャで登録された場合に設定される既定の設定があります。 <xref:System.Windows.DependencyProperty.Register%2A> の他のシグネチャでは、プロパティを登録するときに好みのメタデータを指定できます。 依存関係プロパティに指定される最も一般的なメタデータは、プロパティを使用する新しいインスタンスに適用される既定値を与えるためのものです。

<xref:System.Windows.FrameworkElement> の派生クラスに存在する依存関係プロパティを作成する場合、基底クラス <xref:System.Windows.PropertyMetadata> ではなく、より専門的なメタデータ クラス <xref:System.Windows.FrameworkPropertyMetadata> を使用できます。 <xref:System.Windows.FrameworkPropertyMetadata> クラスのコンストラクターには、複数のシグネチャがあり、組み合わせてさまざまなメタデータの特性を指定できます。 既定値のみを指定する場合は、型 <xref:System.Object> の 1 つのパラメーターを受け取るシグネチャを使用します。 そのオブジェクトのパラメーターをプロパティの型固有の既定値として渡します (提供された既定値は、<xref:System.Windows.DependencyProperty.Register%2A> の呼び出しで `propertyType` パラメーターとして指定した型である必要があります)。

<xref:System.Windows.FrameworkPropertyMetadata> に対しては、プロパティのメタデータのオプション フラグを指定することもできます。 これらのフラグは、登録後にプロパティ メタデータで個々のプロパティに変換され、特定の条件をレイアウト エンジンなどの他のプロセスに伝えるために使用されます。

#### <a name="setting-appropriate-metadata-flags"></a>適切なメタデータ フラグの設定

- プロパティ (またはその値の変更) が[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] に影響する場合、特にレイアウト システムのサイズ設定またはページへの要素のレンダリング方法に影響を及ぼす場合は、<xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsMeasure>、<xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsArrange>、<xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsRender> のフラグを 1 つ以上設定します。

  - <xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsMeasure> は、含まれるオブジェクトが親内の領域を多かれ少なかれ必要とする場合がある場所でこのプロパティを変更するには、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] レンダリングへの変更が必要なことを示します。 たとえば、"Width" プロパティには、このフラグが設定されている必要があります。

  - <xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsArrange> は、このプロパティを変更するには、通常は専用領域の変更の必要がない [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] レンダリングへの変更が必要なことを示しますが、領域内での配置は変更されたことを示します。 たとえば、"Alignment" プロパティには、このフラグが設定されている必要があります。

  - <xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsRender> は、レイアウトとメジャーには影響しないものの、別のレンダリングを必要とするその他の変更が発生していることを示します。 "Background" など、既存の要素の色を変更するプロパティはその一例です。

  - これらのフラグは、プロパティ システムやレイアウトのコールバックの独自のオーバーライド実装のためのメタデータのプロトコルとしてよく使用されます。 たとえば、インスタンスの任意のプロパティが値の変更を報告し、そのメタデータ内で <xref:System.Windows.FrameworkPropertyMetadata.AffectsArrange%2A> が `true` に設定されている場合は、<xref:System.Windows.UIElement.InvalidateArrange%2A> を呼び出す <xref:System.Windows.DependencyObject.OnPropertyChanged%2A> コールバックを使用できます。

- 上記で説明した必要なサイズを変更する方法に加え、一部のプロパティは含まれる親要素のレンダリング特性に影響する場合があります。 例として、フロー ドキュメント モデルで使用される <xref:System.Windows.Documents.Paragraph.MinOrphanLines%2A> プロパティがあります。これは、そのプロパティへの変更によって、段落を含むフロー ドキュメントの全体的なレンダリングを変更できます。 <xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsParentArrange> または <xref:System.Windows.FrameworkPropertyMetadataOptions.AffectsParentMeasure> を使用して、独自のプロパティで同様のケースを特定します。

- 既定では、依存関係プロパティはデータ バインディングをサポートします。 データ バインディングにとって現実的なシナリオがない場合や、大きなオブジェクトのデータ バインディングのパフォーマンスが問題として認識される場合には、意図的にデータ バインディングを無効にすることができます。

- 既定では、依存関係プロパティのデータ バインディング <xref:System.Windows.Data.Binding.Mode%2A> の既定値は <xref:System.Windows.Data.BindingMode.OneWay> です。 バインドはバインディング インスタンスごとにいつでも <xref:System.Windows.Data.BindingMode.TwoWay> に変更できます。詳細については、[バインディングの方向の指定](../data/how-to-specify-the-direction-of-the-binding.md)に関する記事を参照してください。 ただし、依存関係プロパティの作成者は、プロパティで <xref:System.Windows.Data.BindingMode.TwoWay> バインド モードを既定で使用するように選択することができます。 既存の依存関係プロパティの例として <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A?displayProperty=nameWithType> があります。このプロパティのシナリオでは、<xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> 設定ロジックと <xref:System.Windows.Controls.MenuItem> の合成により、既定のテーマ スタイルとの対話が行われます。 <xref:System.Windows.Controls.MenuItem.IsSubmenuOpen%2A> プロパティ ロジックでは、データ バインディングをネイティブに使用し、他の状態プロパティとメソッドの呼び出しに従って、プロパティの状態が維持されます。 既定で <xref:System.Windows.Data.BindingMode.TwoWay> をバインドするプロパティの別の例には、<xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> があります。

- <xref:System.Windows.FrameworkPropertyMetadataOptions.Inherits> フラグを設定することで、カスタム依存関係プロパティでプロパティの継承を有効にすることもできます。 プロパティの継承は、親要素と子要素に共通のプロパティがあるシナリオに便利で、子要素に、親に設定されたのと同じ値に設定した特定のプロパティ値を持たせることは理にかなっています。 継承可能なプロパティの例は、<xref:System.Windows.FrameworkElement.DataContext%2A> です。これは、データの表示に重要なマスターと詳細のシナリオを有効にするためのバインディング操作に使用されます。 <xref:System.Windows.FrameworkElement.DataContext%2A> を継承可能にすることで、すべての子要素もそのデータ コンテキストを継承します。 プロパティ値の継承により、ページまたはアプリケーションのルートでデータ コンテキストを指定できます。すべての使用可能な子要素内のバインディングに再度指定する必要はありません。 <xref:System.Windows.FrameworkElement.DataContext%2A> は、継承が既定値をオーバーライドするものの、常に特定の任意の子要素でローカルに設定できることを示す良い例でもあります。詳細については、[階層データでのマスター詳細パターンの使用](../data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)に関する記事を参照してください。 プロパティ値の継承にはパフォーマンスが低下する可能性があるため、控え目に使用する必要があります。詳細については、「[プロパティ値の継承](property-value-inheritance.md)」を参照してください。

- <xref:System.Windows.FrameworkPropertyMetadataOptions.Journal> フラグを設定して、依存関係プロパティをナビゲーション ジャーナリング サービスで検出または使用するかどうかを示します。 <xref:System.Windows.Controls.Primitives.Selector.SelectedIndex%2A> プロパティはその一例で、選択コントロールで選択されたすべての項目は、ジャーナリング履歴がナビゲートされるときに保持される必要があります。

<a name="RODP"></a>

## <a name="read-only-dependency-properties"></a>読み取り専用の依存関係プロパティ

読み取り専用の依存関係プロパティを定義することができます。 ただし、読み取り専用としてプロパティを定義する理由のシナリオには、プロパティ システムに登録して、識別子を公開するための手順が異なるため、若干の違いがあります。 詳細については、「[読み取り専用の依存関係プロパティ](read-only-dependency-properties.md)」を参照してください。

<a name="CTDP"></a>

## <a name="collection-type-dependency-properties"></a>コレクション型依存関係プロパティ

コレクション型依存関係プロパティには、考慮すべき実装問題が他にもいくつかあります。 詳細については、「[コレクション型依存関係プロパティ](collection-type-dependency-properties.md)」を参照してください。

<a name="SecurityC"></a>

## <a name="dependency-property-security-considerations"></a>依存関係プロパティのセキュリティに関する考慮事項

依存関係プロパティは、パブリック プロパティとして宣言する必要があります。 依存関係プロパティ識別子フィールドは、パブリック静的フィールドとして宣言する必要があります。 他のアクセス レベル (プロテクトなど) を宣言しようとした場合でも、依存関係プロパティには、プロパティ システム API と組み合わせた識別子を通じて、常にアクセスできます。 保護された識別子フィールドでも、潜在的にアクセス可能です。これは、メタデータのレポートまたは <xref:System.Windows.LocalValueEnumerator> などのプロパティ システムの一部である値決定の API によるものです。 詳細については、「[依存関係プロパティのセキュリティ](dependency-property-security.md)」を参照してください。

<a name="DPCtor"></a>

## <a name="dependency-properties-and-class-constructors"></a>依存関係プロパティとクラス コンストラクター

マネージド コード プログラミングでは、クラス コンストラクターが仮想メソッドを呼び出さないという一般的な方針があります (多くの場合は FxCop などのコード分析ツールによって適用されます)。 これは、派生クラスのコンストラクターの基本の初期化としてコンストラクターを呼び出すことができ、コンストラクターから仮想メソッドを入力することで、構築されるオブジェクトのインスタンスの初期化が不完全な状態で行われる可能性があるためです。 <xref:System.Windows.DependencyObject> から既に派生した任意のクラスから派生する場合、プロパティ システム自体が仮想メソッドを内部的に呼び出して公開することに注意してください。 これらの仮想メソッドは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティ システム サービスの一部です。 メソッドをオーバーライドすることで、派生クラスが値の決定に参加できるようになります。 ランタイムの初期化の潜在的な問題を回避するには、非常に特殊なコンストラクター パターンに従っている場合を除き、依存関係プロパティの値をクラスのコンストラクター内で設定しないでください。 詳細については、「[DependencyObject の安全なコンストラクター パターン](safe-constructor-patterns-for-dependencyobjects.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [依存関係プロパティの概要](dependency-properties-overview.md)
- [依存関係プロパティのメタデータ](dependency-property-metadata.md)
- [コントロールの作成の概要](../controls/control-authoring-overview.md)
- [コレクション型依存関係プロパティ](collection-type-dependency-properties.md)
- [依存関係プロパティのセキュリティ](dependency-property-security.md)
- [XAML 読み込みと依存関係プロパティ](xaml-loading-and-dependency-properties.md)
- [DependencyObject の安全なコンストラクター パターン](safe-constructor-patterns-for-dependencyobjects.md)
