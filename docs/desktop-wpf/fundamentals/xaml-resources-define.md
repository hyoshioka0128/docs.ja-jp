---
title: XAML リソースの定義
description: .NET Core 用の WPF の XAML リソースについて説明します。 XAML リソースの種類を理解し、XAML リソースの定義方法を学びます。
author: adegeo
ms.author: adegeo
ms.date: 08/21/2019
ms.openlocfilehash: f8eaf3fd931aa6804b0b9a9c19c6bcc042678ebf
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325720"
---
# <a name="overview-of-xaml-resources"></a>XAML リソースの概要

リソースは、アプリ内のさまざまな場所で再利用できるオブジェクトです。 リソースの例として、ブラシやスタイルがあります。 この概要では、Extensible Application Markup Language (XAML) でのリソースの使用方法について説明します。 また、コードを使用して、リソースを作成してアクセスすることもできます。

> [!NOTE]
> この記事で説明する XAML リソースは、 "*アプリ リソース*" とは異なります。アプリ リソースは一般に、コンテンツ、データ、埋め込みファイルなど、アプリに追加されるファイルです。

<!-- TODO: File redirect from docs\framework\wpf\advanced\xaml-resources.md -->

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="using-resources-in-xaml"></a>XAML でのリソースの使用

次の例では、ページのルート要素のリソースとして <xref:System.Windows.Media.SolidColorBrush> を定義します。 この例では、次にそのリソースを参照し、それを使用して、<xref:System.Windows.Shapes.Ellipse>、<xref:System.Windows.Controls.TextBlock>、<xref:System.Windows.Controls.Button> など、いくつかの子要素のプロパティを設定します。

[!code-xaml[FEResourceSH_snip#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xaml)]

すべてのフレームワーク レベルの要素 (<xref:System.Windows.FrameworkElement> や <xref:System.Windows.FrameworkContentElement>) には、定義されたリソースを含む <xref:System.Windows.ResourceDictionary> 型の <xref:System.Windows.FrameworkElement.Resources%2A> プロパティがあります。 リソースは、<xref:System.Windows.Controls.Button> など、任意の要素に定義できます。 ただし、ほとんどの場合、リソースはルート要素 (例では <xref:System.Windows.Controls.Page>) に定義されます。

リソース ディクショナリ内の各リソースには、一意のキーが必要です。 マークアップでリソースを定義する場合は、[x:Key ディレクティブ](../xaml-services/xkey-directive.md)を使用して一意のキーを割り当てます。 通常、キーは文字列です。ただし、適切なマークアップ拡張機能を使用して、他のオブジェクトの型に設定することもできます。 リソースの文字列以外のキーは、WPF の特定の機能領域、特に、スタイル、コンポーネント リソース、データ スタイルに使用されます。

定義されたリソースは、リソースのキー名を指定するリソース マークアップ拡張構文で使用できます。 たとえば、リソースを別の要素のプロパティの値として使用します。

[!code-xaml[FEResourceSH_snip#KeyNameUsage](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#keynameusage)]

上記の例では、XAML ローダーで <xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> プロパティの値 `{StaticResource MyBrush}` が処理されるときに、リソース検索ロジックではまず、<xref:System.Windows.Controls.Button> 要素のリソース ディクショナリが確認されます。 <xref:System.Windows.Controls.Button> にリソース キー `MyBrush` の定義がない場合 (この例では定義がありません。そのリソース コレクションは空です)、検索では次に <xref:System.Windows.Controls.Button> の親要素 (<xref:System.Windows.Controls.Page>) が確認されます。 <xref:System.Windows.Controls.Page> ルート要素にリソースを定義すると、<xref:System.Windows.Controls.Page> の論理ツリー内のすべての要素がそれにアクセスできます。 さらに、同じリソースを再利用して、そのリソースが表すものと同じ型を受け入れるプロパティの値を設定できます。 前の例では、同じ `MyBrush` リソースで 2 つの異なるプロパティ (<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> と、<xref:System.Windows.Shapes.Rectangle> の <xref:System.Windows.Shapes.Shape.Fill%2A>) が設定されています。

## <a name="static-and-dynamic-resources"></a>静的および動的なリソース

リソースは、静的または動的として参照できます。 参照は、[StaticResource のマークアップ拡張機能](../../framework/wpf/advanced/staticresource-markup-extension.md)または [DynamicResource のマークアップ拡張機能](../../framework/wpf/advanced/dynamicresource-markup-extension.md)を使用して作成します。 マークアップ拡張機能は XAML の機能であり、マークアップ拡張機能が属性文字列を処理し、オブジェクトを XAML ローダーに返すことで、オブジェクト参照を指定できるようにします。 マークアップ拡張機能の動作の詳細については、 「[マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)」を参照してください。

マークアップ拡張機能を使用する場合、通常は、その特定のマークアップ拡張機能によって処理される 1 つ以上のパラメーターを文字列形式で指定します。 [StaticResource のマークアップ拡張機能](../../framework/wpf/advanced/staticresource-markup-extension.md)では、使用可能なすべてのリソース ディクショナリでそのキーの値を検索することでキーが処理されます。 処理は読み込み中に行われます。これは、読み込みプロセスでプロパティ値を割り当てる必要がある場合です。 [DynamicResource のマークアップ拡張機能](../../framework/wpf/advanced/dynamicresource-markup-extension.md)では、それに代わり、式を作成してキーが処理されます。この式は、アプリが実行される時点までは未評価のままであり、その時点で式が評価され、値が提供されます。

リソースを参照する場合、静的リソース参照と動的リソース参照のどちらを使用するかに対し、次の考慮事項が影響する可能性があります。

- アプリ用リソースの作成方法の全体的な設計 (ページ単位、アプリ内、Loose XAML で、またはリソースのみのアセンブリで) を決定する際は、次の点を考慮してください。

- アプリの機能。 リソースをリアルタイムで更新することは、アプリの要件に含まれていますか。
- そのリソース参照の種類の、それぞれの検索動作。
- 特定のプロパティまたはリソースの種類と、それらの種類のネイティブ動作。

## <a name="static-resources"></a>静的リソース

静的リソース参照は、次のような状況に最適です。

- アプリの設計で、そのほとんどのリソースがページまたはアプリケーション レベルのリソース ディクショナリに集中している。 静的リソース参照が、ページの再読み込みなどの実行時の動作に基づいて再評価されない。 そのため、リソースやアプリの設計上必要とされない大量の動的リソース参照を回避するという、パフォーマンス上の利点があります。

- <xref:System.Windows.DependencyObject> にも <xref:System.Windows.Freezable> にもないプロパティの値を設定しようとしている。

- DLL にコンパイルされ、アプリの一部としてパッケージ化、またはアプリ間で共有されるリソース ディクショナリを作成しようとしている。

- カスタム コントロール用のテーマを作成していて、そのテーマ内で使用されるリソースを定義しようとしている。 この場合は通常、動的リソース参照の検索動作は望ましくありません。代わりに、検索が予測可能になり、テーマに対して自己完結するように、静的リソース参照動作を使用する必要があります。 動的リソース参照では、テーマ内の参照でも実行時までは未評価のままになります。 また、場合によっては、テーマが適用されるときに、何らかのローカル要素によって、テーマで参照が試みられているキーが再定義され、検索でテーマ自体より前にそのローカル要素が失敗します。 これが起こると、テーマは想定どおりに動作しません。

- リソースを使用して、多数の依存関係プロパティを設定しようとしている。 依存関係プロパティには、プロパティ システムによって有効になる有効値キャッシュがあります。そのため、読み込み時に評価できる依存関係プロパティに値を指定すると、依存関係プロパティは再評価される式を確認する必要がなく、最後の有効値を返すことができます。 この手法ではパフォーマンス上の利点が得られる可能性があります。

- すべてのコンシューマー用の基礎リソースを変更する必要がある、または [x:Shared 属性](../xaml-services/xshared-attribute.md)を使用してコンシューマーごとに別個の書き込み可能インスタンスを保持する必要がある。

### <a name="static-resource-lookup-behavior"></a>静的リソースの検索動作

静的リソースがプロパティまたは要素によって参照されるときに自動的に行われる検索プロセスについて、下記で説明します。

01. 検索プロセスでは、プロパティを設定する要素によって定義されたリソース ディクショナリ内で、要求されたキーが確認されます。

01. 検索プロセスでは次に、親要素とそのリソース ディクショナリに向かって、論理ツリーが上方向に走査されます。 このプロセスは、ルート要素に到達するまで続けられます。

01. アプリ リソースが確認されます。 アプリ リソースとは、WPF アプリの <xref:System.Windows.Application> オブジェクトによって定義されたリソース ディクショナリ内のリソースのことです。

リソース ディクショナリ内からの静的リソース参照では、リソース参照の前に既に辞書的に定義されているリソースを参照する必要があります。 前方参照は、静的リソース参照では解決できません。 このため、リソースがそれぞれのリソース ディクショナリの先頭または先頭付近で定義されるように、リソース ディクショナリの構造を設計してください。

静的リソース検索はテーマまたはシステム リソースにまで拡張できますが、この検索は、XAML ローダーによって要求が遅延されるという理由だけでサポートされています。 この遅延は、ページの読み込み時のランタイム テーマがアプリに適切に適用されるようにするために必要です。 ただし、テーマ内、またはシステム リソースとしてのみ存在することがわかっているキーに対する静的リソース参照はお勧めできません。このような参照は、テーマがユーザーによってリアルタイムで変更された場合に再評価されないためです。 テーマまたはシステム リソースを要求するときは、動的リソース参照の方が信頼性が高くなります。 例外は、テーマ要素自体が別のリソースを要求する場合です。 これらの参照は、前述の理由で、静的リソース参照でなければなりません。

静的リソース参照が見つからない場合の例外動作にはさまざまなものがあります。 リソースが遅延された場合、例外は実行時に発生します。 リソースが遅延されなかった場合、例外は読み込み時に発生します。

## <a name="dynamic-resources"></a>動的リソース

動的リソースは、次の場合に最適です。

- リソース (システム リソースや、その他のユーザー設定可能なリソースを含む) の値が、実行時までわからない条件に依存している。 たとえば、<xref:System.Windows.SystemColors>、<xref:System.Windows.SystemFonts>、または <xref:System.Windows.SystemParameters>によって公開されるシステム プロパティを参照するセッター値を作成できます。 これらの値は最終的にはユーザーとオペレーティング システムのランタイム環境から取得されるため、本当の意味で動的です。 また、変更される可能性のあるアプリケーションレベルのテーマを使用している場合もあります。この場合、ページレベルのリソースへのアクセスでもその変更を取り込む必要があります。

- カスタム コントロールのテーマ スタイルを作成または参照している。

- アプリの有効期間中に <xref:System.Windows.ResourceDictionary> の内容を調整するつもりである。

- 相互依存関係を含む複雑なリソース構造を使用していて、前方参照が必要になる可能性がある。 前方参照は静的リソース参照ではサポートされません。ただし、動的リソース参照ではサポートされます。この理由は、リソースは実行時まで評価される必要がなく、前方参照が重要性の高い概念ではないためです。

- コンパイルまたは作業セットの観点では大規模であるリソースを参照していて、そのリソースはページの読み込み時にすぐに使用されない可能性がある。 静的リソース参照は常に、ページの読み込み時に XAML から読み込まれます。 しかし、動的リソース参照は、使用されるまで読み込まれません。

- セッター値がテーマやその他のユーザー設定に影響される他の値から取得される可能性のあるスタイルを作成しようとしている。

- アプリの有効期間中に論理ツリー内で親が変更される可能性のある要素にリソースを適用しようとしている。 親を変更するとリソース検索スコープも変更される可能性があるため、親が変更された要素のリソースが新しいスコープに基づいて再評価されるようにする場合は、常に動的リソース参照を使用してください。

### <a name="dynamic-resource-lookup-behavior"></a>動的リソースの検索動作

動的リソース参照でのリソース検索動作は、<xref:System.Windows.FrameworkElement.FindResource%2A> または <xref:System.Windows.FrameworkElement.SetResourceReference%2A>を呼び出す場合のコード内での検索動作に似ています。

01. 検索では、プロパティを設定する要素によって定義されたリソース ディクショナリ内で、要求されたキーが確認されます。

    - 要素で <xref:System.Windows.FrameworkElement.Style%2A> プロパティが定義される場合、その要素の <xref:System.Windows.FrameworkElement.Style?displayProperty=fullName> ではその<xref:System.Windows.Style.Resources> ディクショナリが確認されます。

    - 要素で <xref:System.Windows.Controls.Control.Template%2A> プロパティが定義される場合、その要素の <xref:System.Windows.FrameworkTemplate.Resources?displayProperty=fullName> ディクショナリが確認されます。

01. 検索では、親要素とそのリソース ディクショナリに向かって、論理ツリーが上方向に走査されます。 このプロセスは、ルート要素に到達するまで続けられます。

01. アプリ リソースが確認されます。 アプリ リソースとは、WPF アプリの <xref:System.Windows.Application> オブジェクトによって定義されたリソース ディクショナリ内のリソースのことです。

01. テーマのリソース ディクショナリは、現在アクティブなテーマについて確認されます。 実行時にテーマが変更された場合、値は再評価されます。

01. システム リソースが確認されます。

例外の動作 (存在する場合) にはさまざまなものがあります。

- リソースが <xref:System.Windows.FrameworkElement.FindResource%2A> 呼び出しによって要求され、見つからなかった場合、例外がスローされます。

- リソースが <xref:System.Windows.FrameworkElement.TryFindResource%2A> 呼び出しによって要求され、見つからなかった場合、例外はスローされず、戻り値は `null` になります。 設定するプロパティで `null` が受け入れられない場合でも、設定対象の個々のプロパティに応じて、より深刻な例外がスローされる可能性があります。

- リソースが XAML の動的リソース参照によって要求され、見つからなかった場合、その動作は一般的なプロパティ システムによって決まります。 一般的な動作は、リソースが存在するレベルでプロパティ設定操作が行われなかった場合と同様です。 たとえば、評価できなかったリソースを使用して個別のボタン要素の背景を設定しようとすると、値は設定されませんが、プロパティ システムの他の参加項目から値の優先順位で有効な値を取得できます。 たとえば、背景値は、ローカルに定義されたボタン スタイルまたはテーマ スタイルから取得される可能性があります。 テーマ スタイルによって定義されていないプロパティの場合、リソースの評価に失敗した後の有効な値は、プロパティ メタデータの既定値から取得される可能性があります。

### <a name="restrictions"></a>制約

動的リソース参照には、注意が必要な制約がいくつか存在します。 次の条件のうち、少なくとも 1 つが満たされている必要があります。

- 設定するプロパティは、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> のプロパティでなければなりません。 そのプロパティは、<xref:System.Windows.DependencyProperty> によってサポートされている必要があります。

- 参照が `StyleSetter` 内の値を対象としています。

- 設定するプロパティは、<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> プロパティの値または <xref:System.Windows.Setter> 値として指定される、<xref:System.Windows.Freezable> のプロパティでなければなりません。

設定するプロパティは <xref:System.Windows.DependencyProperty> または <xref:System.Windows.Freezable> プロパティでなければならないため、ほとんどのプロパティ変更が UI に反映される可能性があります。プロパティの変更 (動的リソース値の変更) はプロパティ システムによって確認されるためです。 ほとんどのコントロールには、<xref:System.Windows.DependencyProperty> が変更され、そのプロパティがレイアウトに影響する可能性がある場合に、コントロールの別のレイアウトを強制的に適用するロジックが組み込まれています。 ただし、[DynamicResource のマークアップ拡張機能](../../framework/wpf/advanced/dynamicresource-markup-extension.md)を値として含むすべてのプロパティで、UI のリアルタイム更新が確実に行われるわけではありません。 この機能は、プロパティに応じて、およびプロパティを所有する型に応じて、または場合によってはアプリの論理構造に応じて異なる可能性があります。

## <a name="styles-datatemplates-and-implicit-keys"></a>スタイル、DataTemplates、暗黙的なキー

<xref:System.Windows.ResourceDictionary> 内のすべての項目にキーが必要ですが、それは、すべてのリソースに明示的な `x:Key` が必要であることを意味するわけではありません。 リソースとして定義されている場合、いくつかのオブジェクトの型で暗黙的なキーがサポートされます。その場合、キーの値は、別のプロパティの値に関連付けられます。 この種類のキーが暗黙的なキーと呼ばれます。それに対し、`x:Key` 属性は明示的なキーです。 暗黙的なキーを上書きするには、明示的なキーを指定します。

リソースの重要シナリオの 1 つに、<xref:System.Windows.Style> を定義する場合が挙げられます。 事実、<xref:System.Windows.Style> はほとんどの場合、リソース ディクショナリ内のエントリとして定義されます。スタイルが本来、再利用を目的としているためです。 スタイルの詳細については、「[スタイルとテンプレート](styles-templates-overview.md)」を参照してください。

コントロールのスタイルは、暗黙的なキーを使用して作成と参照の両方を行うことができます。 コントロールの既定の外観を定義するテーマ スタイルは、この暗黙的なキーに依存しています。 それを要求する側の観点では、暗黙的なキーはコントロール自体の <xref:System.Type> です。 リソースを定義する側の観点では、暗黙的なキーはスタイルの <xref:System.Windows.Style.TargetType%2A> です。 したがって、カスタム コントロールのテーマを作成する場合、または既存のテーマ スタイルと相互に作用するスタイルを作成する場合は、その <xref:System.Windows.Style> に対して [x:Key ディレクティブ](../xaml-services/xkey-directive.md)を指定する必要はありません。 また、テーマ スタイルを使用する場合に、スタイルを指定する必要はいっさいありません。 たとえば、<xref:System.Windows.Style> リソースにキーがないように見える場合でも、次のスタイル定義は機能します。

[!code-xaml[FEResourceSH_snip#ImplicitStyle](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page2.xaml#implicitstyle)]

このスタイルには実際にはキー、つまり暗黙的なキー `typeof(System.Windows.Controls.Button)` があります。 マークアップでは、<xref:System.Windows.Style.TargetType%2A> を型名として直接指定して (または、必要に応じて [{x:Type...}](../xaml-services/xtype-markup-extension.md) を使用して)、 <xref:System.Type> が返されるようにすることができます。

WPF によって使用される既定のテーマ スタイル メカニズムを通じて、そのスタイルは、ページに <xref:System.Windows.Controls.Button> のランタイム スタイルとして適用されます。これは、その <xref:System.Windows.Controls.Button> 自体で、スタイルに対するその <xref:System.Windows.FrameworkElement.Style%2A> プロパティまたは特定のリソース参照の指定が試みられない場合でも行われます。 ページで定義されたスタイルは、テーマ ディクショナリ スタイルが持つキーと同じキーを使用して、検索シーケンス内でテーマ ディクショナリ スタイルより早く見つけられます。 ページ内の任意の場所で `<Button>Hello</Button>` を指定するだけで、`Button` の <xref:System.Windows.Style.TargetType%2A> によって定義したスタイルがそのボタンに適用されます。 必要であれば、マークアップを明確にするために、<xref:System.Windows.Style.TargetType%2A> と同じ型の値を持つスタイルに明示的にキーを付けることもできますが、これは任意です。

<xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> が `true` の場合、スタイルの暗黙的なキーはコントロールに適用されません。 (<xref:System.Windows.FrameworkElement.OverridesDefaultStyle%2A> は、コントロールのインスタンスで明示的に設定されるのではなく、コントロール クラスのネイティブ動作の一部として設定される場合があることにも注意してください。)また、派生クラスのシナリオで暗黙的なキーをサポートするには、コントロールで <xref:System.Windows.FrameworkElement.DefaultStyleKey%2A> がオーバーライドされる必要があります (WPF の一部として提供される既存のすべてのコントロールにこのオーバーライドが含まれています)。 スタイル、テーマ、コントロールの設計の詳細については、「[スタイルの設定が可能なコントロールを設計するためのガイドライン](../../framework/wpf/controls/guidelines-for-designing-stylable-controls.md)」を参照してください。

<xref:System.Windows.DataTemplate> には暗黙的なキーもあります。 <xref:System.Windows.DataTemplate> の暗黙的なキーは、<xref:System.Windows.DataTemplate.DataType%2A> プロパティ値です。 <xref:System.Windows.DataTemplate.DataType%2A> は、[{x:Type...}](../xaml-services/xtype-markup-extension.md) を使用して明示的に指定するのではなく、型の名前として指定することもできます。 詳細については、「[データ テンプレートの概要](../../framework/wpf/data/data-templating-overview.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.ResourceDictionary>
- [アプリケーション リソース](../../framework/wpf/advanced/optimizing-performance-application-resources.md)
- [リソースとコード](../../framework/wpf/advanced/resources-and-code.md)
- [リソースを定義および参照する](../../framework/wpf/advanced/how-to-define-and-reference-a-resource.md)
- [アプリケーション管理の概要](../../framework/wpf/app-development/application-management-overview.md)
- [x:Type マークアップ拡張機能](../xaml-services/xtype-markup-extension.md)
- [StaticResource のマークアップ拡張機能](../../framework/wpf/advanced/staticresource-markup-extension.md)
- [DynamicResource のマークアップ拡張機能](../../framework/wpf/advanced/dynamicresource-markup-extension.md)
