---
title: Windows Presentation Foundation の概要
description: この記事では、.NET Core に関連した Windows Presentation Foundation (WPF) の概要と、提供される機能について説明します。
ms.date: 07/18/2019
ms.topic: overview
ms.openlocfilehash: 63b2e431b5ab5fd3875887b8b574a77aa12018a6
ms.sourcegitcommit: 961ec21c22d2f1d55c9cc8a7edf2ade1d1fd92e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2020
ms.locfileid: "85840375"
---
# <a name="what-is-windows-presentation-foundation"></a>Windows Presentation Foundation の概要

Windows 用のデスクトップ クライアント アプリケーションを作成する UI フレームワークである、Windows Presentation Foundation (WPF) のデスクトップ ガイドです。 WPF の開発プラットフォームでは、アプリケーション モデル、コントロール、グラフィックス、データ バインディングなどのさまざまなアプリケーション開発機能の一式がサポートされています。 WPF では、Extensible Application Markup Language (XAML) の使用により、アプリケーションのプログラミング用の宣言型モデルが提供されます。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

WPF には、2 つの実装があります。

01. [GitHub](https://github.com/dotnet/wpf) 上でホストされる、オープンソース実装。 このバージョンは .NET Core 3.0 で実行されます。 XAML 用の WPF ビジュアル デザイナーでは、少なくとも [Visual Studio 2019 バージョン 16.3](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019+desktopguide) が必要です。

01. Visual Studio 2019 および Visual Studio 2017 でサポートされている、.NET Framework 実装。

このデスクトップ ガイドは、.NET Core 3.0 と WPF 向けに書かれています。 .NET Framework を使用した WPF に関する既存のドキュメントの詳細については、「[Framework Windows Presentation Foundation](../../framework/wpf/index.md)」を参照してください。

## <a name="xaml"></a>XAML

XAML は、WPF でリソースや UI 要素の定義などを行うために使用される、宣言型の XML ベースの言語です。 XAML で定義された要素は、アセンブリからのオブジェクトのインスタンス化を表します。 XAML は、バッキング型システムへの直接の結びつきのない、実行時に解釈される他のほとんどのマークアップ言語とは異なります。

次の例は、UI の一部としてボタンを作成する方法を示しています。 この例は、XAML でオブジェクトを表す方法を示すことを目的としています。`Button` は型、`Content` はプロパティです。

```xaml
<StackPanel>
    <Button Content="Click Me!" />
</StackPanel>
```

<!--For more information, see [XAML overview (WPF)](../../../framework/wpf/advanced/xaml-overview-wpf.md).-->

### <a name="xaml-extensions"></a>XAML 拡張機能

XAML には、マークアップ拡張の構文が用意されています。 マークアップ拡張を使用すると、属性形式またはプロパティ要素形式、あるいはその両方で、プロパティの値を指定できます。

たとえば、前の XAML コードでは、表示されるコンテンツがリテラル文字列 `"Click Me!"` に設定されたボタンを定義しましたが、代わりにコンテンツをサポートされているマークアップ拡張によって設定することもできます。 マークアップ拡張は、左中かっこと右中かっこ `{ }` を使用して定義されます。 その後、マークアップ拡張の種類は、左中かっこの直後の文字列トークンによって識別されます。

```xaml
<StackPanel>
    <Button Content="{MarkupType}" />
</StackPanel>
```

WPF には、データ バインディング用の `{Binding}` など、さまざまな XAML 用マークアップ拡張が用意されています。

詳細については、「[マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)」を参照してください。

## <a name="property-system"></a>プロパティ システム

WPF には、型の[プロパティ](../../standard/base-types/common-type-system.md#properties)の機能を拡張するために使用できる一連のサービスが用意されています。 これらのサービスはまとめて *WPF プロパティ システム*と呼ばれます。 WPF プロパティ システムによって使用されるプロパティは、依存関係プロパティと呼ばれています。

依存関係プロパティでは、プロパティをバッキングする <xref:System.Windows.DependencyProperty> 型の提供によって、プロパティ機能が拡張されます。 依存関係プロパティの型は、プライベート フィールドでプロパティをバッキングする標準パターンの代替実装です。

### <a name="dependency-property"></a>依存関係プロパティ

WPF では通常、依存関係プロパティは標準の .NET [プロパティ](../../standard/base-types/common-type-system.md#properties)として公開されます。 基本的なレベルでは、これらのプロパティを直接操作することができます。これらが依存関係プロパティとして実装されることは意識しません。

依存関係プロパティの目的は、他の入力の値に基づいてプロパティの値を計算する方法を提供することです。 これらの他の入力には、テーマやユーザー設定などのシステム プロパティや、データ バインディングやアニメーションからの Just-In-Time プロパティなどがあります。

依存関係プロパティを実装して、検証、既定値、他のプロパティに対する変更を監視するコールバックを提供できます。 新しいプロパティを作成したり既存のプロパティをオーバーライドしたりするのではなく、依存関係プロパティ メタデータをオーバーライドすることによって、派生クラスで既存のプロパティの特定の特性を変更することもできます。

### <a name="dependency-object"></a>依存関係オブジェクト

WPF プロパティ システムにとって重要なもう 1 つの型は、<xref:System.Windows.DependencyObject> です。 この型では、依存関係プロパティを登録および所有できる基本クラスが定義されます。 <xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> メソッドにより、依存関係オブジェクト インスタンスの依存関係プロパティのバッキング実装が提供されます。

次の例は、`ValueProperty` という名前の単一の依存関係プロパティ識別子を定義する依存関係オブジェクトを示しています。 依存関係プロパティは、`Value` .NET プロパティを使用して作成されます。

```csharp
public class TextField: DependencyObject
{
    public static readonly DependencyProperty ValueProperty =
        DependencyProperty.Register("Value", typeof(string), typeof(TextField), new PropertyMetadata(""));

    public string Value
    {
        get { return (string)GetValue(ValueProperty); }
        set { SetValue(ValueProperty, value); }
    }
}
```

依存関係プロパティは、上の例の `TextField` のように、依存関係オブジェクト型の静的メンバーとして定義されます。 依存関係プロパティは、依存関係オブジェクトを使用して登録する必要があります。

上の例の `Value` プロパティにより依存関係プロパティがラップされるため、使い慣れている標準の .NET プロパティ パターンが提供されます。

<!--For more information, see [Dependency properties overview](../../../framework/wpf/advanced/dependency-properties-overview.md).-->

## <a name="events"></a>イベント

WPF には、使い慣れている .NET 共通言語ランタイム (CLR) イベントの上に配置されたイベント処理システムが用意されています。 これらの WPF イベントは、ルーティング イベントと呼ばれます。

ルーティング イベントは、`RoutedEvent` クラスのインスタンスによってバッキングされ、WPF イベント システムに登録される CLR イベントです。 イベント登録から取得された `RoutedEvent` インスタンスは、通常、ルーティング イベントを登録し、したがって "*所有*" しているクラスの `public static readonly` フィールド メンバーとして保持されます。 一意の名前を持つ CLR イベント ("*ラッパー*" イベントとも呼ばれます) への接続は、CLR イベントの `add` および `remove` 実装をオーバーライドすることにより得られます。 ルーティング イベントのバッキングおよび接続メカニズムは、[依存関係プロパティ](#dependency-property)が、`DependencyProperty` クラスによってバッキングされ、WPF プロパティ システムに登録される CLR プロパティであるという概念に似ています。

ルーティング イベントシステムの主な利点は、ハンドラーを探しているコントロール要素ツリーに対してイベントが*通知*されることです。 たとえば、WPF には豊富なコンテンツ モデルがあるため、イメージ コントロールをボタン コントロールのコンテンツとして設定するとします。 イメージ コントロール上でマウスがクリックされると、マウス イベントが使用され、そのためにボタンが `Click` イベントを呼び出すきっかけとなるヒットテストが中断されることが予想されます。 従来の CLR イベント処理モデルでは、イメージとボタンの両方に同じハンドラーをアタッチすることで、この制限を回避できます。 しかしながらルーティング イベントシステムを使用すると、イメージ コントロール上で呼び出されたマウス イベント (選択など) は、親ボタン コントロールに通知されます。

<!--For more information, including other types of event models, see [Events overview](../../../framework/wpf/advanced/routed-events-overview.md).-->

## <a name="data-binding"></a>データ バインディング

WPF のデータ バインディングでは、アプリケーションでデータの表示や操作を行うための、シンプルかつ一貫した方法が提供されます。 要素は、共通言語ランタイム (CLR) オブジェクトおよび XML 形式のさまざまな種類のデータ ソースのデータにバインドできます。 WPF ではまた、ドラッグ アンド ドロップ操作によるデータ転送のメカニズムも提供されます。

データ バインディングとは、アプリケーションの UI とビジネス ロジックの間の接続を確立する処理です。 バインドが適切に設定され、データから適切な通知が提供される場合、データの値が変更されると、そのデータにバインドされている要素に変更が自動的に反映されます。 データ バインディングには、要素内のデータの外部表現が変更された場合、基になるデータが自動的に更新されて変更が反映されるという意味もあります。 たとえば、ユーザーが TextBox 要素の値を編集すると、基になるデータ値がその変更を反映するように自動的に更新されます。

データ バインディングは、XAML で `{Binding}` マークアップ拡張を使用して構成できます。 次の例は、データ オブジェクトの `ButtonText` プロパティへのバインディングを示しています。 そのバインディングが失敗した場合は、`Click Me!` の値が使用されます。

```xaml
<StackPanel>
    <Button Content="{Binding ButtonText, FallbackValue='Click Me!'}" />
</StackPanel>
```

詳しくは、「[データ バインディングの概要](../data/data-binding-overview.md)」をご覧ください。

## <a name="ui-components"></a>UI コンポーネント

WPF には、`Button`、`Label`、`TextBox`、`Menu`、`ListBox` など、ほとんどの Windows アプリケーションで使用される共通の UI コンポーネントが多数用意されています。 これまで、これらのオブジェクトはコントロールと呼ばれてきました。 WPF の SDK では、アプリケーションで表示可能なオブジェクトを表すクラスに、広義で「コントロール」という用語が使用され続けていますが、クラスは、表示可能な部分を持つために `Control` クラスを継承する必要がないことに注意してください。 `Control` クラスを継承するクラスには、`ControlTemplate` が含まれます。これを使用すると、コントロールのコンシューマーは、新しいサブクラスを作成しなくても、コントロールの外観を大幅に変更できます。

## <a name="styles-and-templates"></a>スタイルとテンプレート

WPF のスタイルとテンプレートは、アプリケーション、ドキュメント、または UI の設計者が視覚的に説得力のあるアプリケーションを作成し、製品に対して特定の外観を標準化できる、一連の機能 (スタイル、テンプレート、トリガー、およびストーリーボード) を表します。

WPF のスタイルモデルのもう 1 つの機能は、表示とロジックの分離です。つまり、開発者が別の場所でプログラミング ロジックの作業をしているときに、設計者は XAML を使用してアプリケーションの外観について作業できることを意味します。

また、スタイルとテンプレートの再利用を可能にするものである、リソースについて理解しておくことも重要です。

詳細については、[スタイルとテンプレート](../fundamentals/styles-templates-overview.md)に関するページをご覧ください。

## <a name="resources"></a>リソース

WPF のリソースは、アプリケーションのさまざまな場所で再利用できるオブジェクトです。 リソースの例としては、スタイル、テンプレート、色ブラシなどがあります。 リソースは、コードと XAML 形式の両方で定義および参照できます。

すべてのフレームワーク レベルの要素 (<xref:System.Windows.FrameworkElement> や <xref:System.Windows.FrameworkContentElement>) には、定義されたリソースを含む `Resources` プロパティ (<xref:System.Windows.ResourceDictionary> 型) があります。 すべての要素はフレームワーク レベルの要素から継承されるため、すべての要素でリソースを定義できます。 ただし、XAML ドキュメントのルート要素にリソースを定義するのが最も一般的です。

<!--For more information, see [XAML Resources](../../../framework/wpf/advanced/xaml-resources.md).-->

## <a name="next-steps"></a>次の手順

- [WPF アプリケーションを作成する。](https://docs.microsoft.com/visualstudio/get-started/csharp/tutorial-wpf?toc=/dotnet/desktop-wpf/toc.json&bc=/dotnet/breadcrumb/toc.json)
- [.NET Framework との違いを調べる。](../migration/differences-from-net-framework.md)
- [XAML について学習する。](../fundamentals/xaml.md)
