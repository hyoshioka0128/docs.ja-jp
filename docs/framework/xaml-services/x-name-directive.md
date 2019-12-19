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
ms.openlocfilehash: d17d977384962980839fbe2b2c0a4708412d403d
ms.sourcegitcommit: a4f9b754059f0210e29ae0578363a27b9ba84b64
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74837221"
---
# <a name="xname-directive"></a>x:Name ディレクティブ
Xaml 名前スコープ内の XAML で定義された要素を一意に識別します。 XAML 名前スコープとその一意モデルは、インスタンス化されたオブジェクトに適用できます。フレームワークが Api を提供する場合や、実行時に XAML で作成されたオブジェクトグラフにアクセスする動作を実装する場合です。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用  
  
```xaml  
<object x:Name="XAMLNameValue".../>  
```  
  
## <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|`XAMLNameValue`|[XamlName 文法](xamlname-grammar.md)の制限に準拠する文字列。|  
  
## <a name="remarks"></a>Remarks  
 `x:Name` がフレームワークのバッキングプログラミングモデルに適用された後、名前は、オブジェクト参照を保持する変数、またはコンストラクターによって返されるインスタンスに相当します。  
  
 `x:Name` ディレクティブの使用の値は、XAML 名前スコープ内で一意である必要があります。 既定では .NET Framework XAML サービス API によって使用されるとき、プライマリ XAML 名前スコープは、1つの XAML 運用環境の XAML ルート要素で定義され、その XAML 運用環境に含まれる要素を含みます。 1つの XAML 運用環境で発生する可能性のある個別の XAML 名前スコープは、特定のシナリオに対応するためにフレームワークによって定義できます。 たとえば、WPF では、新しい XAML 名前スコープが定義され、その XAML 運用環境でも定義されている任意のテンプレートによって作成されます。 XAML 名前スコープの詳細については (WPF 用に記述されていますが、多くの XAML 名前スコープの概念に関連します)、「 [WPF Xaml 名前スコープ](../wpf/advanced/wpf-xaml-namescopes.md)」をご覧ください。  
  
 一般に、`x:Key`を使用する状況では、`x:Name` は適用しないでください。 特定の既存のフレームワークによる XAML の実装では、`x:Key` と `x:Name`間に代替の概念が導入されていますが、これは推奨される方法ではありません。 .NET Framework XAML サービスでは、<xref:System.Windows.Markup.INameScope> や <xref:System.Windows.Markup.DictionaryKeyPropertyAttribute>などの名前/キー情報を処理するときに、このような置換の概念はサポートされません。  
  
 `x:Name` の permittance および名前の一意性の強制に関する規則は、特定の実装フレームワークによって定義される可能性があります。 ただし、.NET Framework XAML サービスで使用できるようにするには、XAML 名前スコープの一意性のフレームワーク定義がこのドキュメントの <xref:System.Windows.Markup.INameScope> 情報の定義と一致している必要があります。また、情報が適用される場所については、同じ規則を使用する必要があります。 たとえば、[!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)] の実装では、さまざまなマークアップ要素を、リソースディクショナリ、ページレベルの XAML によって作成された論理ツリー、テンプレート、その他の遅延コンテンツなどの個別の <xref:System.Windows.NameScope> 範囲に分割し、各 XAML 名前スコープ内で XAML 名の一意性を適用します。  
  
 .NET Framework XAML サービスの XAML オブジェクトライターを使用するカスタム型の場合、型の `x:Name` にマップされるプロパティを確立または変更できます。 この動作を定義するには、プロパティの名前を参照して、型定義コードの <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> にマップします。  <xref:System.Windows.Markup.RuntimeNamePropertyAttribute> は、型レベルの属性です。  
  
 Using.NET Framework XAML サービスでは、XAML 名前スコープのサポートのバッキングロジックは、<xref:System.Windows.Markup.INameScope> インターフェイスを実装することによって、フレームワークに依存しない方法で定義できます。  
  
## <a name="wpf-usage-notes"></a>WPF の使用上の注意  
 XAML、部分クラス、および分離コードを使用する [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの標準ビルド構成では、指定された `x:Name` は、マークアップコンパイルビルドタスクによって [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] が処理されるときに、基になるコードで作成されるフィールドの名前になります。また、そのフィールドはオブジェクトへの参照を保持します。 既定では、作成されたフィールドは internal です。 フィールドへのアクセスを変更するには、 [x:FieldModifier 属性](x-fieldmodifier-directive.md)を指定します。 WPF と Silverlight では、マークアップコンパイルが部分クラスのフィールドを定義して名前を指定しますが、この値は最初は空です。 次に、`InitializeComponent` という名前の生成されたメソッドが、クラスコンストラクター内から呼び出されます。 `InitializeComponent` は、部分クラスの XAML で定義された部分に存在する各 `x:Name` 値を入力文字列として使用する `FindName` 呼び出しで構成されます。 その後、戻り値は、like 名前のフィールド参照に割り当てられ、XAML 解析から作成されたオブジェクトでフィールド値が設定されます。 `InitializeComponent` の実行により、XAML で定義されたオブジェクトへの参照が必要になるたびに `FindName` 明示的に呼び出すのではなく、`x:Name`/フィールド名を使用して実行時オブジェクトグラフを直接参照することができます。  
  
 Microsoft Visual Basic ターゲットを使用し、`Page` ビルドアクションを含む XAML ファイルが含まれている WPF アプリケーションでは、コンパイル時に個別の参照プロパティが作成され、`x:Name`を持つすべての要素に `WithEvents` キーワードを追加して、イベントハンドラーデリゲートの `Handles` 構文をサポートします。 このプロパティは常にパブリックです。 詳細については、「[Visual Basic と WPF のイベント処理](../wpf/advanced/visual-basic-and-wpf-event-handling.md)」を参照してください。  
  
 `x:Name` は、ビルドアクション (たとえば、リソースディクショナリの疎な XAML) によってページがマークアップコンパイルされていない場合でも、WPF XAML プロセッサが読み込み時に XAML 名前スコープに名前を登録するために使用されます。 この動作の理由の1つは、<xref:System.Windows.Data.Binding.ElementName%2A> バインドに `x:Name` が必要になる可能性があるためです。 詳細については、「[データバインディングの概要](../../desktop-wpf/data/data-binding-overview.md)」を参照してください。  
  
 前述のように、`x:Key`も使用する状況では、`x:Name` (または `Name`) を適用しないでください。 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.ResourceDictionary> には、それ自体を XAML 名前スコープとして定義する特別な動作がありますが、この動作を適用する方法として <xref:System.Windows.Markup.INameScope> Api に対して実装されていない値または null 値が返されます。 WPF XAML パーサーが XAML で定義された <xref:System.Windows.ResourceDictionary>で `Name` または `x:Name` を検出した場合、名前はどの XAML 名前スコープにも追加されません。 XAML 名前スコープと `FindName` メソッドからその名前を検索しようとすると、有効な結果が返されません。  
  
### <a name="xname-and-name"></a>x:Name と名前  
 WPF アプリケーションの多くのシナリオでは、`x:Name` 属性を使用しないようにすることができます。これは、<xref:System.Windows.FrameworkElement> や <xref:System.Windows.FrameworkContentElement> など、いくつかの重要な基本クラスの既定の XAML 名前空間で指定されている `Name` 依存関係プロパティがこれと同じ目的を満たすためです。 フレームワークレベルで `Name` プロパティを持たない要素へのコードアクセスが重要である一般的な XAML と WPF のシナリオもいくつかあります。 たとえば、特定のアニメーションおよびストーリーボードサポートクラスは、`Name` プロパティをサポートしていませんが、多くの場合、アニメーションを制御するためにコード内で参照する必要があります。 後でコードから参照する場合は、XAML で作成されたタイムラインおよび変換の属性として `x:Name` を指定する必要があります。  
  
 <xref:System.Windows.FrameworkElement.Name%2A> をクラスのプロパティとして使用できる場合、<xref:System.Windows.FrameworkElement.Name%2A> と `x:Name` を属性として同義に使用できますが、両方が同じ要素に指定されている場合は、解析例外が発生します。 XAML がマークアップコンパイルされている場合は、マークアップコンパイル時に例外が発生します。それ以外の場合は、読み込み時に発生します。  
  
 <xref:System.Windows.FrameworkElement.Name%2A> は、XAML 属性構文を使用して設定できます。また、コードでは <xref:System.Windows.DependencyObject.SetValue%2A>を使用します。ただし、コードで <xref:System.Windows.FrameworkElement.Name%2A> プロパティを設定しても、XAML が既に読み込まれているほとんどの状況では、XAML 名前スコープ内で代表的なフィールド参照が作成されないことに注意してください。 コードで <xref:System.Windows.FrameworkElement.Name%2A> を設定するのではなく、適切な名前スコープに対してコードの <xref:System.Windows.NameScope> メソッドを使用します。  
  
 <xref:System.Windows.FrameworkElement.Name%2A> は、プロパティ要素構文と内部テキストを使用して設定することもできますが、これは一般的ではありません。 これに対し、`x:Name` は、XAML プロパティ要素の構文、または <xref:System.Windows.DependencyObject.SetValue%2A>を使用したコードでは設定できません。これは、オブジェクトの属性構文を使用してのみ設定できます。これは、オブジェクトがディレクティブであるためです。  
  
## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意  
 Silverlight 用の `x:Name` に関しては、別途ドキュメントが用意されています。 詳細については、「 [XAML 名前空間 (x:)」を参照してください。言語機能 (Silverlight)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc188995(v=vs.95))。  
  
## <a name="see-also"></a>参照

- <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=nameWithType>
- <xref:System.Windows.FrameworkContentElement.Name%2A?displayProperty=nameWithType>
- [WPF のツリー](../wpf/advanced/trees-in-wpf.md)
