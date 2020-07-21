---
title: x:Name ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- x:Name
- xName
- Name
helpviewer_keywords:
- x:Name attribute [XAML Services]
- XAML [XAML Services], x:Name attribute
- Name attribute in XAML [XAML Services]
ms.assetid: b7e61222-e8cf-48d2-acd0-6df3b7685d48
ms.openlocfilehash: 9f812a49a3217a563be1bd7f1d999b641c28463d
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432714"
---
# <a name="xname-directive"></a>x:Name ディレクティブ

XAML 名前スコープ内の XAML で定義された要素を一意に識別します。 フレームワークが API を提供する場合、または実行時に XAML で作成されたオブジェクト グラフにアクセスする動作を実装する場合、XAML 名前スコープとその一意性モデルをインスタンス化されたオブジェクトに適用できます。

## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法

```xaml
<object x:Name="XAMLNameValue".../>
```

## <a name="xaml-values"></a>XAML 値

|||
|-|-|
|`XAMLNameValue`|[XamlName の文法](xamlname-grammar.md)の制限に準拠する文字列。|

## <a name="remarks"></a>解説

フレームワーク`x:Name`のバッキング プログラミング モデルに適用された後、名前は、オブジェクト参照またはコンストラクターによって返されるインスタンスを保持する変数と同じです。

ディレクティブの使用法`x:Name`の値は、XAML 名前スコープ内で一意である必要があります。 既定では、.NET XAML サービス API によって使用される場合、プライマリ XAML 名前スコープは、単一の XAML 運用環境の XAML ルート要素で定義され、その XAML 運用環境に含まれる要素を包含します。 1 つの XAML プロダクション内で発生する可能性のある別々の XAML 名前スコープを、特定のシナリオに対処するためにフレームワークによって定義できます。 たとえば、WPF では、新しい XAML 名前スコープは、その XAML の運用環境でも定義されている任意のテンプレートによって定義および作成されます。 XAML 名前スコープの詳細については、(WPF 用に作成されたが、多くの XAML 名前スコープの概念に関連する)[を参照してください](../../framework/wpf/advanced/wpf-xaml-namescopes.md)。

一般に`x:Name`、 を使用`x:Key`する状況では適用しないでください。 特定の既存のフレームワークによる XAML 実装では、`x:Key`と`x:Name`の間に置換の概念が導入されていますが、これは推奨される方法ではありません。 NET XAML サービスは、 や<xref:System.Windows.Markup.INameScope><xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>などの名前/キー情報を処理する際に、このような置換の概念をサポートしていません。

許可の規則と名前`x:Name`の一意性の適用は、特定の実装フレームワークによって定義される可能性があります。 ただし、.NET XAML Services で使用できるようにするには、XAML 名前スコープの一意性のフレームワーク定義は、このドキュメント<xref:System.Windows.Markup.INameScope>の情報の定義と一致し、情報が適用される場所に関して同じ規則を使用する必要があります。 たとえば、実装では[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)]、リソース ディクショナリ、ページ レベル<xref:System.Windows.NameScope>の XAML、テンプレート、およびその他の遅延コンテンツによって作成された論理ツリーなど、さまざまなマークアップ要素を別々の範囲に分割し、それらの XAML 名前スコープ内で XAML 名前の一意性を適用します。

.NET XAML サービス XAML オブジェクト ライターを使用するカスタム型の場合`x:Name`、型にマップされるプロパティを確立または変更できます。 この動作は、型定義コードでマップ<xref:System.Windows.Markup.RuntimeNamePropertyAttribute>するプロパティの名前を参照することによって定義します。  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute>は、型レベルの属性です。

XAML サービス<xref:System.Windows.Markup.INameScope>Using.NET、XAML 名前スコープのサポートのバッキング ロジックは、インターフェイスを実装することで、フレームワークに依存しない方法で定義できます。

## <a name="wpf-usage-notes"></a>WPF の使用上の注意

XAML、部分クラス、および分離[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]コードを使用するアプリケーションの標準ビルド構成では、マークアップ コンパイル`x:Name`ビルド タスクによって処理されるときに[!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)]基になるコードで作成されるフィールドの名前が指定され、そのフィールドはオブジェクトへの参照を保持します。 既定では、作成されるフィールドは内部フィールドです。 フィールド アクセスを変更するには、 [x:FieldModifier 属性](xfieldmodifier-directive.md)を指定します。 WPF および Silverlight では、マークアップ コンパイルで部分クラスのフィールドを定義して名前を付けますが、値は最初は空です。 次に、生成されたメソッド`InitializeComponent`がクラス コンストラクタ内から呼び出されます。 `InitializeComponent`は、`FindName`部分クラスの XAML`x:Name`定義部分に存在する各値を入力文字列として使用する呼び出しで構成されます。 その後、戻り値は、XAML 解析から作成されたオブジェクトでフィールド値を埋めるために、名前の似たフィールド参照に代入されます。 実行`InitializeComponent`すると、XAML 定義オブジェクトへの参照が必要な場合はいつでも`x:Name`明示的に呼び出す`FindName`必要がなくても、/ フィールド名を使用して実行時オブジェクト グラフを直接参照できます。

Microsoft Visual Basic のターゲットを使用し、ビルド アクションに`Page`XAML ファイルを含む WPF アプリケーションの場合、`WithEvents`コンパイル時に、イベント ハンドラー`x:Name`デリゲートの`Handles`構文をサポートするために、 を持つすべての要素にキーワードを追加する個別の参照プロパティが作成されます。 このプロパティは常にパブリックです。 詳細については、「[Visual Basic と WPF のイベント処理](../../framework/wpf/advanced/visual-basic-and-wpf-event-handling.md)」を参照してください。

`x:Name`は、ページがビルド アクション (リソース ディクショナリの緩い XAML など) によってマークアップ コンパイルされていない場合でも、読み込み時に XAML 名前スコープに名前を登録するために WPF XAML プロセッサによって使用されます。 この動作の理由の 1`x:Name`つは、 が<xref:System.Windows.Data.Binding.ElementName%2A>バインドに必要になる可能性があるためです。 詳細については、「[データ バインディングの概要](../data/data-binding-overview.md)」を参照してください。

前に述べたように`x:Name`、 `Name`( または ) は、 も`x:Key`使用する状況では適用しないでください。 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]には、XAML 名前スコープとして定義するが、この動作を強制する方法として API の<xref:System.Windows.Markup.INameScope>Not Implemented 値または null 値を返す特別な動作<xref:System.Windows.ResourceDictionary>があります。 WPF XAML パーサーが`Name`XAML`x:Name`で定義された<xref:System.Windows.ResourceDictionary>を検出した場合、または XAML で定義された名前は、XAML 名前スコープに追加されません。 XAML 名前スコープとそのメソッドからその名前を`FindName`検索しようとしても、有効な結果が返されません。

### <a name="xname-and-name"></a>x:名前と名前

WPF アプリケーションの多くのシナリオでは、属性の`x:Name`使用を回避できます`Name`。 <xref:System.Windows.FrameworkElement> <xref:System.Windows.FrameworkContentElement> フレームワーク レベルでプロパティを持たない`Name`要素へのコード アクセスが重要な一般的な XAML および WPF のシナリオがまだいくつか存在します。 たとえば、特定のアニメーションおよびストーリーボードサポートクラスはプロパティを`Name`サポートしていませんが、アニメーションを制御するためにコードで参照する必要がよくあります。 後でコード`x:Name`から参照する場合は、XAML で作成されるタイムラインと変換の属性として指定する必要があります。

クラス<xref:System.Windows.FrameworkElement.Name%2A>のプロパティとして使用でき、<xref:System.Windows.FrameworkElement.Name%2A>属性として同じ`x:Name`意味で使用できますが、同じ要素に両方が指定されている場合は解析例外が発生します。 XAML がマークアップ コンパイルされている場合、例外はマークアップ コンパイルで発生します。

<xref:System.Windows.FrameworkElement.Name%2A>XAML 属性構文を使用して、コード内で設定<xref:System.Windows.DependencyObject.SetValue%2A>できます。ただし、コードでプロパティ<xref:System.Windows.FrameworkElement.Name%2A>を設定しても、XAML が既に読み込まれているほとんどの状況では、XAML 名前スコープ内での代表的なフィールド参照は作成されません。 コードで設定<xref:System.Windows.FrameworkElement.Name%2A>する代わりに、適切な名前<xref:System.Windows.NameScope>スコープに対してコードのメソッドを使用します。

<xref:System.Windows.FrameworkElement.Name%2A>内部テキストを含むプロパティ要素構文を使用して設定することもできますが、これは一般的ではありません。 これに対し`x:Name`、XAML プロパティ要素構文や、コードでの設定は<xref:System.Windows.DependencyObject.SetValue%2A>できません。ディレクティブであるため、オブジェクトに対する属性構文を使用してのみ設定できます。

## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意

Silverlight 用の `x:Name` に関しては、別途ドキュメントが用意されています。 詳細については[、「XAML 名前空間 (x:)」を参照してください。言語機能 (シルバーライト)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc188995(v=vs.95))

## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=nameWithType>
- <xref:System.Windows.FrameworkContentElement.Name%2A?displayProperty=nameWithType>
- [WPF のツリー](../../framework/wpf/advanced/trees-in-wpf.md)
