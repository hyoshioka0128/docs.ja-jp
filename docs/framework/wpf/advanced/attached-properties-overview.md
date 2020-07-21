---
title: 添付プロパティの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- attached properties [WPF Designer]
ms.assetid: 75928354-dc01-47e8-a018-8409aec1f32d
ms.openlocfilehash: b207db459776c9f8fa7ea247d01071eeb8c995cf
ms.sourcegitcommit: 465547886a1224a5435c3ac349c805e39ce77706
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2020
ms.locfileid: "81739293"
---
# <a name="attached-properties-overview"></a>添付プロパティの概要

添付プロパティは、XAML によって定義された概念です。 添付プロパティは、任意のオブジェクトに設定可能なグローバル プロパティの型として使用されることを意図しています。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では通常、添付プロパティは従来のプロパティ "ラッパー" を含まない依存関係プロパティの特殊な形式として定義されています。

## <a name="prerequisites"></a>前提条件 <a name="prerequisites"></a>

この記事では、ユーザーが [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] クラスの既存の依存関係プロパティの使用という観点から依存関係プロパティを理解し、「[依存関係プロパティの概要](dependency-properties-overview.md)」トピックを通読していることを前提としています。 この記事の例について理解するには、XAML および WPF アプリケーションの記述方法について知っておく必要もあります。

## <a name="why-use-attached-properties"></a>添付プロパティを使用する理由 <a name="attached_properties_usage"></a>

添付プロパティの目的の 1 つは、親要素に定義されているプロパティに対する一意の値を、異なる子要素が指定できるようにすることです。 このシナリオの適用例として、子要素から親要素に、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] での表示方法を通知させることがあります。 1 つの例として、<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> プロパティがあります。 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> プロパティは添付プロパティとして作成されます。このプロパティが、<xref:System.Windows.Controls.DockPanel> 自体ではなく、<xref:System.Windows.Controls.DockPanel> の内部に含まれる要素に設定されるように設計されているためです。 <xref:System.Windows.Controls.DockPanel> クラスでは <xref:System.Windows.Controls.DockPanel.DockProperty> という名前の静的な <xref:System.Windows.DependencyProperty> フィールドが定義されており、<xref:System.Windows.Controls.DockPanel.GetDock%2A> および <xref:System.Windows.Controls.DockPanel.SetDock%2A> メソッドが添付プロパティのパブリック アクセサーとして提供されます。

## <a name="attached-properties-in-xaml"></a>XAML の添付プロパティ <a name="attached_properties_xaml"></a>

XAML では、構文 *AttachedPropertyProvider*.*PropertyName* を使用して添付プロパティを設定します

XAML での <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> の設定方法の例を次に示します。

[!code-xaml[PropertiesOvwSupport#APBasicUsage](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml#apbasicusage)]

使い方は静的プロパティに少し似ています。名前で指定されたインスタンスを参照するのではなく、添付プロパティを所有して登録する型 <xref:System.Windows.Controls.DockPanel> を常に参照します。

さらに、XAML の添付プロパティはマークアップに設定する属性であるため、設定操作にのみ関連性があります。 XAML でプロパティを直接取得することはできませんが、スタイルのトリガー (詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照) などの値を比較するための間接的な機構があります。

### <a name="attached-property-implementation-in-wpf"></a>WPF での添付プロパティの実装

[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、WPF 型の UI 関連の添付プロパティのほとんどが、依存関係プロパティとして実装されます。 添付プロパティは XAML の概念であり、依存関係プロパティは WPF の概念です。 WPF の添付プロパティは依存関係プロパティであるため、プロパティのメタデータ、そしてその既定値といった依存関係プロパティの概念がサポートされます。

## <a name="how-attached-properties-are-used-by-the-owning-type"></a>所有する型による添付プロパティの使用方法 <a name="howused"></a>

添付プロパティはどのオブジェクトにも設定できますが、プロパティを設定したことによって自動的に意味のある結果が得られるわけでも、値が別のオブジェクトによって使用されるわけでもありません。 一般に、添付プロパティの目的は、想定されるさまざまなクラス階層または論理関係から生じるオブジェクトが、添付プロパティを定義する型に共通する情報をレポートできるようにすることです。 添付プロパティを定義する型は、一般的に次のいずれかのモデルに従っています。

- 添付プロパティを定義する型が、添付プロパティの値を設定する要素の親要素になるように設計されている。 この型の子オブジェクトは、一部のオブジェクト ツリー構造で内部ロジックを反復し、値を取得して、その値に対する処理を実行します。

- 添付プロパティを定義する型が、想定されるさまざまな親要素およびコンテンツ モデルの子要素として使用される。

- 添付プロパティを定義する型が、サービスを表す。 その他の型は、添付プロパティの値を設定します。 プロパティを設定する要素がサービスのコンテキストで評価されると、添付プロパティの値がサービス クラスの内部ロジックにより取得されます。

### <a name="an-example-of-a-parent-defined-attached-property"></a>親定義の添付プロパティの例

WPF で添付プロパティが定義される最も一般的なシナリオは、親要素で子要素のコレクションがサポートされ、さらに動作の詳細が子要素ごとにレポートされるような動作が実装される場合です。

<xref:System.Windows.Controls.DockPanel> では <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 添付プロパティが定義されており、<xref:System.Windows.Controls.DockPanel> には、そのレンダリング ロジック (具体的には、<xref:System.Windows.Controls.DockPanel.MeasureOverride%2A> および <xref:System.Windows.Controls.DockPanel.ArrangeOverride%2A>) の一部としてクラスレベルのコードが含まれます。 <xref:System.Windows.Controls.DockPanel> インスタンスでは、直下の子要素のいずれかに <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> の値が設定されているかどうかが常に確認されます。 設定されている場合は、その値が、その子要素に適用されるレンダリング ロジックの入力になります。 入れ子になった <xref:System.Windows.Controls.DockPanel> インスタンスではそれぞれが所有する直下の子要素のコレクションが処理されますが、<xref:System.Windows.Controls.DockPanel> による <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> の値の処理方法は、実装によって異なります。 直接の親以外の要素に影響を与える添付プロパティを所有することは、理論上は可能です。 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 添付プロパティが要素で設定されており、その要素に影響を与える <xref:System.Windows.Controls.DockPanel> 親要素がない場合、エラーまたは例外は発生しません。 これは単に、グローバル プロパティ値が設定されているものの、その情報を消費する最新の <xref:System.Windows.Controls.DockPanel> の親が存在しないことを意味します。

## <a name="attached-properties-in-code"></a>コードの添付プロパティ <a name="attached_properties_code"></a>

WPF の添付プロパティには、取得と設定のアクセスを簡単にする、一般的な CLR の "ラッパー" メソッドは含まれていません。 これは、添付プロパティが、プロパティが設定されているインスタンスの CLR 名前空間の一部とは限らないためです。 ただし、XAML の解析時に XAML プロセッサがその値を設定できる必要があります。 有効な添付プロパティの使用をサポートするには、添付プロパティの所有者の種類ごとに **Get_PropertyName_** および **Set_PropertyName_** の形式で専用のアクセサー メソッドを実装する必要があります。 この専用のアクセサー メソッドは、コード内の添付プロパティの取得/設定でも役立ちます。 コードの観点では、添付プロパティはプロパティ アクセサーではなくメソッド アクセサーを含むバッキング フィールドに似ており、そのバッキング フィールドは特に定義することなくすべてのオブジェクトに存在することができます。

次の例は、コードに添付プロパティを設定する方法を示しています。 この例では、`myCheckBox` は <xref:System.Windows.Controls.CheckBox> クラスのインスタンスです。

[!code-csharp[PropertiesOvwSupport#APCode](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertiesOvwSupport/CSharp/page4.xaml.cs#apcode)]
[!code-vb[PropertiesOvwSupport#APCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertiesOvwSupport/visualbasic/page4.xaml.vb#apcode)]

XAML と同様、コードの 4 行目に `myDockPanel` の子要素として `myCheckBox` が追加されていない場合、45行目で例外が発生することはありませんが、プロパティ値が <xref:System.Windows.Controls.DockPanel> の親と対話しないため、処理が行われません。 <xref:System.Windows.Controls.DockPanel> 親要素の存在と組み合わされた子要素で値 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> が設定されている場合にのみ、レンダリングされたアプリケーションで有効な動作が発生します。 (この場合、添付プロパティを設定してからツリーに接続するか、 ツリーに接続してから添付プロパティを設定することができます。 どちらの操作でも、結果は同じです。)

## <a name="attached-property-metadata"></a>添付プロパティのメタデータ <a name="attached_properties_metadata"></a>

プロパティを登録すると、そのプロパティがレンダリング、測定などに影響するかどうかといったプロパティの特性を指定するように <xref:System.Windows.FrameworkPropertyMetadata> が設定されます。 添付プロパティのメタデータは、一般的に依存関係プロパティとの違いがありません。 オーバーライドの既定値を添付プロパティのメタデータに指定すると、その値がオーバーライドするクラスのインスタンスの暗黙的な添付プロパティの既定値になります。 具体的には、一部のプロセスが添付プロパティの `Get` メソッド アクセサーを使用してそのプロパティの値のクエリを行った場合に、メタデータを指定したクラスのインスタンスが指定されており、その添付プロパティの値が設定されていないと、既定値がレポートされます。

プロパティでプロパティ値の継承を有効にする場合は、未接続の依存関係プロパティではなく添付プロパティを使用する必要があります。 詳細については、「[プロパティ値の継承](property-value-inheritance.md)」を参照してください。

## <a name="custom-attached-properties"></a>カスタム添付プロパティ <a name="custom"></a>

### <a name="when-to-create-an-attached-property"></a>添付プロパティを作成するタイミング <a name="create_attached_properties"></a>

添付プロパティは、定義クラスではないクラスで使用できるプロパティ設定機構を用意する理由がある場合に作成できます。 この最も一般的なシナリオが、レイアウトです。 既存のレイアウト プロパティの例は、<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Panel.ZIndex%2A?displayProperty=nameWithType>、<xref:System.Windows.Controls.Canvas.Top%2A?displayProperty=nameWithType> などです。 これによって実現するシナリオは、レイアウト制御要素の子要素として存在する要素が、レイアウト親要素に対して個別にレイアウト要件を表現するというものです。親が添付プロパティとして定義したプロパティ値を、個々の子要素が設定します。

クラスがサービスを表しており、クラスでサービスをより透過的に統合できるようにしたい場合にも、添付プロパティを使用します。

さらに別のシナリオは、 **[プロパティ]** ウィンドウの編集など、Visual Studio WPF デザイナーのサポートを利用する場合です。 詳しくは、「[コントロールの作成の概要](../controls/control-authoring-overview.md)」を参照してください。

前述のように、プロパティ値の継承を使用する場合には、添付プロパティを登録する必要があります。

### <a name="how-to-create-an-attached-property"></a>添付プロパティの作成方法 <a name="how_do_i_create_attached_properties"></a>

クラスにおいて、他の型で使用する目的のみで添付プロパティが定義されている場合は、そのクラスを <xref:System.Windows.DependencyObject> から派生させる必要はありません。 ただし、添付プロパティが依存関係プロパティでもある、WPF モデル全体を使用する場合は、<xref:System.Windows.DependencyObject> から派生させる必要があります。

<xref:System.Windows.DependencyProperty> 型の `public static readonly` フィールドを宣言することにより、添付プロパティを依存関係プロパティとして定義します。 このフィールドは、<xref:System.Windows.DependencyProperty.RegisterAttached%2A> メソッドの戻り値を使用して定義します。 識別フィールドとそれが表すプロパティの名前付けに関して確立されている WPF のパターンに従うには、`Property` の文字列が付加され、フィールド名が添付プロパティ名と一致している必要があります。 添付プロパティのプロバイダーでは、添付プロパティのアクセサーとして **Get_PropertyName_** および **Set_PropertyName_** の静的メソッドを指定する必要があります。これを行わないと、プロパティ システムが添付プロパティを使用できません。

> [!NOTE]
> 添付プロパティの get アクセサーを省略すると、プロパティのデータ バインディングが Visual Studio や Blend for Visual Studio などのデザイン ツールで動作しません。

#### <a name="the-get-accessor"></a>Get アクセサー

**Get_PropertyName_** アクセサーのシグネチャは次の形式にする必要があります。

`public static object GetPropertyName(object target)`

- `target` オブジェクトは、実装のより具体的な型として指定することができます。 たとえば、<xref:System.Windows.Controls.DockPanel.GetDock%2A?displayProperty=nameWithType> メソッドでは、このパラメーターの型が <xref:System.Windows.UIElement> となっています。これは、添付プロパティが <xref:System.Windows.UIElement> インスタンスでのみ設定されることになっているからです。

- 戻り値は、実装のより具体的な型として指定することができます。 たとえば、<xref:System.Windows.Controls.DockPanel.GetDock%2A> メソッドの型は <xref:System.Windows.Controls.Dock> です。これは値が列挙型にしか設定できないためです。

#### <a name="the-set-accessor"></a>Set アクセサー

**Set_PropertyName_** アクセサーのシグネチャは次の形式にする必要があります。

`public static void SetPropertyName(object target, object value)`

- `target` オブジェクトは、実装のより具体的な型として指定することができます。 たとえば、<xref:System.Windows.Controls.DockPanel.SetDock%2A> メソッドでは、型が <xref:System.Windows.UIElement> となっています。これは、添付プロパティが <xref:System.Windows.UIElement> インスタンスでのみ設定されることになっているからです。

- `value` オブジェクトは、実装のより具体的な型として指定することができます。 たとえば、<xref:System.Windows.Controls.DockPanel.SetDock%2A> メソッドの型は <xref:System.Windows.Controls.Dock> です。これは値が列挙型にしか設定できないためです。 このメソッドの値は、マークアップの添付プロパティの使用で添付プロパティが検出されたときに XAML ローダーから生じる入力であることに注意してください。 この入力はマークアップの XAML 属性値として指定された値です。 したがって、適切な型を属性値 (最終的には単なる文字列) から作成できるように、使用する型の型変換、値シリアライザー、またはマークアップ拡張サポートが必要です。

次の例では、(<xref:System.Windows.DependencyProperty.RegisterAttached%2A> メソッドを使用した) 依存関係プロパティの登録と、**Get_PropertyName_** および **Set_PropertyName_** アクセサーを示します。 この例では、添付プロパティ名は `IsBubbleSource` です。 したがって、アクセサーの名前は `GetIsBubbleSource` および `SetIsBubbleSource` である必要があります。

[!code-csharp[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFAquariumSln/CSharp/WPFAquariumObjects/Class1.cs#registerattachedbubbler)]
[!code-vb[WPFAquariumSln#RegisterAttachedBubbler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFAquariumSln/visualbasic/wpfaquariumobjects/class1.vb#registerattachedbubbler)]

#### <a name="attached-property-attributes"></a>添付プロパティの属性

WPF では複数の .NET 属性が定義されています。これは添付プロパティに関する情報をリフレクション プロセス、リフレクションおよびプロパティ情報の一般的なユーザー (デザイナーなど) に提供することを目的としています。 添付プロパティに含まれる型は膨大な範囲に及ぶため、デザイナーには XAML を使用する特定のテクノロジの実装に定義されたすべての添付プロパティのグローバル リストがユーザーに表示されないようにするための手段が必要となります。 WPF で添付プロパティに対して定義されている .NET 属性を使用すると、指定した添付プロパティのみをプロパティ ウィンドウに表示することができます。 また、この属性をカスタム添付プロパティに適用するという選択肢もあります。 .NET 属性の目的および構文は、次の参照ページに記載されています。

- <xref:System.Windows.AttachedPropertyBrowsableAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableForChildrenAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableForTypeAttribute>

- <xref:System.Windows.AttachedPropertyBrowsableWhenAttributePresentAttribute>

## <a name="learning-more-about-attached-properties"></a>添付プロパティの詳細情報 <a name="more"></a>

- 添付プロパティの作成の詳細については、「[方法: 添付プロパティを登録する](how-to-register-an-attached-property.md)」を参照してください。

- 依存関係プロパティおよび添付プロパティの高度な使用シナリオについては、「[カスタム依存関係プロパティ](custom-dependency-properties.md)」を参照してください。

- プロパティは添付プロパティとしても依存関係プロパティとしても登録できますが、"ラッパー" 実装は公開したままにすることができます。 この場合、プロパティをその要素に設定することも、XAML の添付プロパティの構文を使用して任意の要素に設定することもできます。 標準使用および添付による使用の両方に適したシナリオでのプロパティの例は、<xref:System.Windows.FrameworkElement.FlowDirection%2A?displayProperty=nameWithType> です。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.DependencyProperty>
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [方法: 添付プロパティを登録する](how-to-register-an-attached-property.md)
