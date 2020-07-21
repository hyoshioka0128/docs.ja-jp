---
title: データ バインディングの概要
description: .NET Core 向けの Windows Presentation Foundation でプロジェクトに追加できるさまざまなデータ ソースについて説明します。 データ ソースは、動的なアプリを作成するために XAML 要素にバインドできます。
author: adegeo
ms.date: 09/19/2019
ms.author: adegeo
dev_langs:
- csharp
- vb
ms.openlocfilehash: 829c93e97990b87e6e568614236de9708ef080d9
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325758"
---
# <a name="data-binding-overview-in-wpf"></a>WPF のデータ バインディングの概要

Windows Presentation Foundation (WPF) のデータ バインディングでは、アプリでデータの表示や操作を行うための、シンプルかつ一貫した方法を提供しています。 要素は、.NET オブジェクトおよび XML の形式のさまざまなデータ ソースのデータにバインドできます。 すべての <xref:System.Windows.Controls.ContentControl> (<xref:System.Windows.Controls.Button> など)、およびすべての <xref:System.Windows.Controls.ItemsControl> (<xref:System.Windows.Controls.ListBox> や <xref:System.Windows.Controls.ListView> など) には、1 つのデータ項目またはデータ項目のコレクションを柔軟にスタイル設定できる組み込みの機能があります。 並べ替えビュー、フィルター ビュー、およびグループ ビューは、データの上に生成できます。

WPF のデータ バインディング機能には、広範なプロパティによるデータ バインディング固有のサポート、データの柔軟な UI 表現、および UI からのビジネス ロジックの明確な分離など、従来のモデルより優れた長所がいくつかあります。

この記事では、WPF データ バインディングの基本となる概念を最初に説明した後、<xref:System.Windows.Data.Binding> クラスの使用とデータ バインディングのその他の機能について説明します。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="what-is-data-binding"></a>データ バインディングとは

データ バインディングとは、アプリの UI と、そこに表示されるデータとの間の接続を確立する処理です。 バインドが適切に設定され、データから適切な通知が提供される場合、データの値が変更されると、そのデータにバインドされている要素に変更が自動的に反映されます。 データ バインディングには、要素内のデータの外部表現が変更された場合、基になるデータを自動的に更新して変更を反映できるという意味もあります。 たとえば、ユーザーが `TextBox` 要素の値を編集すると、基になるデータ値がその変更を反映するように自動的に更新されます。

データ バインディングの一般的な用途は、サーバーまたはローカルの構成データをフォームやその他の UI コントロールに配置することです。 WPF では、この概念には幅広いプロパティのバインドからさまざまなデータ ソースのバインドまで含まれます。 WPF では、要素の依存関係プロパティは .NET オブジェクト (ADO.NET オブジェクトまたは Web サービスおよび Web プロパティに関連付けられているオブジェクトを含む) および XML データにバインドできます。

データ バインディングの例については、[データ バインディング デモ][data-binding-demo]に関するページの次のアプリ UI を参照してください。ここでは、オークション品目の一覧が表示されています。

![データ バインディングのサンプルのスクリーンショット](./media/data-binding-overview/demo.png "DataBinding_DataBindingDemo")

このアプリは、データ バインディングの次の機能を示しています。

- ListBox のコンテンツは、*AuctionItem* オブジェクトのコレクションにバインドされています。 *AuctionItem* オブジェクトには、*Description*、*StartPrice*、*StartDate*、*Category*、*SpecialFeatures* などのプロパティがあります。

- `ListBox` に表示されるデータ (*AuctionItem* オブジェクト) は、項目ごとに説明と現在の価格が表示されるようにテンプレート化されます。 テンプレートは、<xref:System.Windows.DataTemplate> を使用して作成されます。 さらに、各項目の外観は、表示されている *AuctionItem* の *SpecialFeatures* の値に依存します。 *AuctionItem* の *SpecialFeatures* の値が *Color* の場合、その項目には青の枠線が付きます。 値が *Highlight* の場合、その項目にはオレンジの枠線と星が付きます。 「[データ テンプレート](#data-templating)」セクションでは、データ テンプレートに関する情報を提供します。

- ユーザーは、提供されている `CheckBoxes` を使用して、データのグループ化、フィルター処理、または並べ替えを行うことができます。 上の図では、 **[Group by category]\(分類別にグループ化\)** と **[Sort by category and date]\(カテゴリと日付で並べ替え\)** の `CheckBoxes` が選択されています。 データが製品のカテゴリに基づいてグループ化され、カテゴリ名がアルファベット順になっていることが分かります。 図では分かりにくいですが、項目は各カテゴリ内での開始日でも並べ替えられています。 並べ替えは、*コレクション ビュー*を使用して行われます。 コレクション ビューについては、「[コレクションにバインドする](#binding-to-collections)」セクションで説明します。

- ユーザーが項目を選択すると、選択した項目の詳細が <xref:System.Windows.Controls.ContentControl> に表示されます。 このエクスペリエンスは、*マスター詳細シナリオ*と呼ばれます。 この種類のバインドに関する情報は、「[マスター詳細シナリオ](#master-detail-binding-scenario)」セクションにあります。

- *StartDate* プロパティの型は <xref:System.DateTime> で、ミリ秒までの時刻を含む日付を返します。 このアプリでは、より短い日付文字列を表示するため、カスタム コンバーターが使用されています。 コンバーターに関する情報は、「[データ変換](#data-conversion)」セクションにあります。

ユーザーが *[Add Product]\(製品の追加\)* ボタンを選択すると、次のフォームが表示されます。

![[Add Product Listing]\(製品一覧の追加\)](./media/data-binding-overview/demo-addproductlisting.png "DataBinding_Demo_AddProductListing") ページ

ユーザーは、フォーム内のフィールドを編集し、簡単なプレビューまたは詳細なプレビュー ウィンドウを使用して製品の一覧をプレビューしてから `Submit` をクリックして新しい製品の一覧を追加することができます。 既存のグループ化、フィルター処理および並べ替えの設定は、新しいエントリに適用されます。 この特定のケースでは、上のイメージで入力した項目が *Computer* カテゴリ内の 2 番目の項目として表示されます。

この図には示されていませんが、*Start Date\(開始日\)* <xref:System.Windows.Controls.TextBox> には検証ロジックが提供されています。 ユーザーが無効な日付 (無効な書式または過去の日付) を入力すると、<xref:System.Windows.Controls.ToolTip>、および <xref:System.Windows.Controls.TextBox> の横の赤い感嘆符でユーザーに通知されます。 検証ロジックの作成方法については、「[データの検証](#data-validation)」セクションで説明します。

上記で説明したデータ バインディングのさまざまな機能の説明に入る前に、まず WPF データ バインディングの理解に欠かせない基本概念について説明します。

## <a name="basic-data-binding-concepts"></a>基本的なデータ バインディングの概念

バインドする要素およびデータ ソースの性質に関係なく、各バインドは常に次の図で示したモデルに従います。

![基本的なデータ バインディング モデルを示す図。](./media/data-binding-overview/basic-data-binding-diagram.png)

図で示されているように、データ バインディングは、基本的にバインディング ターゲットとバインディング ソース間の橋渡しです。 図には、次の基本的な WPF データ バインディングの概念が示されています。

- 通常、各バインドには次の 4 つのコンポーネントがあります。

  - バインディング ターゲット オブジェクト。
  - ターゲット プロパティ。
  - バインディング ソース。
  - 使用するバインディン グソース内の値へのパス。
  
  > たとえば、`TextBox` のコンテンツを `Employee.Name` プロパティにバインドする場合、ターゲット オブジェクトは `TextBox`、ターゲット プロパティは <xref:System.Windows.Controls.TextBox.Text%2A> プロパティ、使用する値は *Name*、そしてソース オブジェクトは *Employee* オブジェクトになります。

- ターゲット プロパティは、依存関係プロパティである必要があります。 ほとんどの <xref:System.Windows.UIElement> プロパティは依存関係プロパティで、ほとんどの依存関係プロパティは、読み取り専用プロパティを除き、既定でデータ バインディングをサポートします。 (依存関係プロパティを定義できるのは、<xref:System.Windows.DependencyObject> から派生した型のみです。すべての <xref:System.Windows.UIElement> 型は `DependencyObject` から派生します。)

- 図では示されていませんが、バインディング ソース オブジェクトになりうるのは、カスタム .NET オブジェクトだけではないことに注意してください。 WPF データ バインディングでは、.NET オブジェクトおよび XML 形式のデータがサポートされます。 いくつかの例を示すと、バインディング ソースには、<xref:System.Windows.UIElement>、リスト オブジェクト、ADO.NET または Web サービス オブジェクト、または XML データを含む XmlNode を指定できます。 詳しくは、「[バインディング ソースの概要](../../framework/wpf/data/binding-sources-overview.md)」をご覧ください。

バインディングを確立するということは、バインディング ターゲットをバインディング ソース*に*バインドするということを理解することが重要です。 たとえば、データ バインディングを使用して、基になる複数の XML データを <xref:System.Windows.Controls.ListBox> で表示する場合は、`ListBox` を XML データにバインドします。

バインドを確立するには、<xref:System.Windows.Data.Binding> オブジェクトを使用します。 この記事の残りの部分では、`Binding` オブジェクトに関連付けられている概念の多くと、その一部のプロパティおよびその使用方法について説明します。

### <a name="direction-of-the-data-flow"></a>データ フローの方向

前の図の矢印で示されているように、バインドのデータ フローは、バインディング ターゲットからバインディング ソースへ流れます (たとえば、ユーザーが `TextBox` の値を編集するとソース値が変更されます)。また、バインディング ソースが適切な通知を提供する場合は、バインディング ソースからバインディング ターゲットへ流れます (たとえば、`TextBox` コンテンツはバインディング ソースの変更で更新されます)。

アプリでユーザーがデータを変更してそれをソース オブジェクトに反映できるようにすることができます。 または、ユーザーがソース データを更新できないようにすることもできます。 データのフローを制御するには、<xref:System.Windows.Data.Binding.Mode?displayProperty=nameWithType> を設定します。

この図は、さまざまなデータ フローの種類を示しています。

![データ バインディング データ フロー](./media/data-binding-overview/databinding-dataflow.png "DataBinding_DataFlow")

- <xref:System.Windows.Data.BindingMode.OneWay> バインディングによってソース プロパティが変更されたことにより、ターゲット プロパティは自動的に更新されますが、ターゲット プロパティへの変更は、ソース プロパティには反映されません。 この型のバインディングは、バインドされているコントロールが暗黙的な読み取り専用の場合に適しています。 たとえば、株価情報などのソースにバインドしたり、またはターゲット プロパティに、データ バインドされたテーブルの背景色などのように、変更用コントロール インターフェイスがない可能性もあります。 ターゲット プロパティの変更を監視する必要がない場合は、<xref:System.Windows.Data.BindingMode.OneWay> バインディング モードを使うことにより、<xref:System.Windows.Data.BindingMode.TwoWay> バインディング モードのオーバーヘッドを回避できます。

- <xref:System.Windows.Data.BindingMode.TwoWay> バインディングにより、ソース プロパティまたはターゲット プロパティのいずれかが変更され、もう一方も自動的に更新されます。 この種類のバインドは、編集可能なフォームやその他の完全にインタラクティブな UI シナリオに適しています。 ほとんどのプロパティは <xref:System.Windows.Data.BindingMode.OneWay> バインディングに既定で設定されていますが、一部の依存関係プロパティ (一般的に、<xref:System.Windows.Controls.TextBox.Text?displayProperty=nameWithType> や [CheckBox.IsChecked](xref:System.Windows.Controls.Primitives.ToggleButton.IsChecked) などのユーザーが編集可能なコントロールのプロパティ) は、規定で <xref:System.Windows.Data.BindingMode.TwoWay> バインディングに設定されています。 依存関係プロパティが既定で一方向と双方向のどちらでバインドされるかをプログラムで判断する 1 つの方法は、<xref:System.Windows.DependencyProperty.GetMetadata%2A?displayProperty=nameWithType> を使用してそのプロパティ メタデータを取得してから、<xref:System.Windows.FrameworkPropertyMetadata.BindsTwoWayByDefault%2A?displayProperty=nameWithType> プロパティのブール値を確認する方法です。

- <xref:System.Windows.Data.BindingMode.OneWayToSource> は <xref:System.Windows.Data.BindingMode.OneWay> バインディングの逆です。ターゲット プロパティが変更されると、ソース プロパティが更新されます。 1 つのシナリオ例は、UI からのソース値のみを再評価する必要があるかどうかです。

- この図には示されていませんが、<xref:System.Windows.Data.BindingMode.OneTime> バインディングにより、ソース プロパティによってターゲット プロパティが初期化されますが、それ以降の変更は反映されません。 データ コンテキストが変更されるか、データ コンテキスト内のオブジェクトが変更された場合に、その変更はターゲット プロパティに反映*されない*ことを意味します。 この種類のバインドは、現在の状態のスナップショットが適切な場合や、データが完全に静的である場合に適しています。 また、ソース プロパティの値を使用してターゲット プロパティを初期化するときにデータ コンテキストが事前にわからない場合にも、この型のバインディングは便利です。 基本的に、このモードは、<xref:System.Windows.Data.BindingMode.OneWay> バインディングを簡易化したもので、ソース値が変わらない場合にパフォーマンスが向上します。

ソースの変更を検出するには (<xref:System.Windows.Data.BindingMode.OneWay> および <xref:System.Windows.Data.BindingMode.TwoWay> バインディングに適用)、ソースに <xref:System.ComponentModel.INotifyPropertyChanged> などの適切なプロパティ変更通知メカニズムを実装する必要があります。 「[方法:プロパティの変更通知を実装する](../../framework/wpf/data/how-to-implement-property-change-notification.md)」を、<xref:System.ComponentModel.INotifyPropertyChanged> 実装の例として参照してください。

<xref:System.Windows.Data.Binding.Mode?displayProperty=nameWithType> プロパティには、バインディング モードに関する詳細とバインドの方向を指定する方法の例が記載されています。

### <a name="what-triggers-source-updates"></a>ソースの更新のトリガー

<xref:System.Windows.Data.BindingMode.TwoWay> または <xref:System.Windows.Data.BindingMode.OneWayToSource> のバインドは、ターゲット プロパティの変更をリッスンし、ソースに反映します。これは、ソースの更新と呼ばれます。 たとえば、TextBox のテキストを編集して、基になるソース値を変更できます。

しかし、ソース値が更新されるのは、テキストの編集中、またはテキストの編集が完了してコントロールがフォーカスを失った後でしょうか。 <xref:System.Windows.Data.Binding.UpdateSourceTrigger?displayProperty=nameWithType> プロパティは、ソースの更新をトリガーする対象を決定します。 次の図の右矢印の点は、<xref:System.Windows.Data.Binding.UpdateSourceTrigger?displayProperty=nameWithType> プロパティの役割を示しています。

![UpdateSourceTrigger プロパティの役割を示す図。](./media/data-binding-overview/data-binding-updatesource-trigger.png)

`UpdateSourceTrigger` 値が <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged?displayProperty=nameWithType> の場合、<xref:System.Windows.Data.BindingMode.TwoWay> または <xref:System.Windows.Data.BindingMode.OneWayToSource> バインディングの右矢印によって示される値は、ターゲット プロパティが変更されるとすぐに更新されます。 ただし、`UpdateSourceTrigger` 値が <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> の場合、この値は、ターゲット プロパティがフォーカスを失ってから、新しい値で更新されます。

<xref:System.Windows.Data.Binding.Mode%2A> プロパティと同様に、依存関係プロパティごとに異なる既定の <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 値が設定されます。 ほとんどの依存関係プロパティの既定値は <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> です。ただし、`TextBox.Text` プロパティの既定値は <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> です。 `PropertyChanged` は、通常、ターゲット プロパティが変更されるたびにソースの更新が行われることを意味します。 チェックボックスやその他の単純なコントロールについては、即座に変更を加えることができます。 ただし、テキスト フィールドについては、キー入力のたびに更新するとパフォーマンスが低下する可能性があり、また通常のように、新しい値をコミットする前にユーザーがバックスペースで入力ミスを消す機会がなくなります。

依存関係プロパティの既定値を検索する方法については、<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> プロパティ ページを参照してください。

次の表に、例として <xref:System.Windows.Controls.TextBox> を使用した <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 値ごとのシナリオ例を示します。

| UpdateSourceTrigger の値 | ソース値が更新されるとき | TextBox のシナリオ例 |
| ------------------------- | ---------------------------------- | ---------------------------- |
| `LostFocus` (<xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> の既定値) | TextBox コントロールがフォーカスを失ったとき。 | 検証ロジックに関連付けられている TextBox (以下の「[データの検証](#data-validation)」セクションを参照)。 |
| `PropertyChanged` | <xref:System.Windows.Controls.TextBox> に入力するとき。 | チャットルーム ウィンドウ内の TextBox コントロール。 |
| `Explicit` | アプリが <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> を呼び出すとき。 | 編集可能なフォーム内の TextBox コントロール (ユーザーが送信ボタンをクリックしたときにのみ、ソース値を更新)。 |

例については、「[方法: TextBox テキストでソースを更新するタイミングを制御する](../../framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md)」を参照してください。

## <a name="creating-a-binding"></a>バインドの作成

前のセクションで説明した概念の一部をもう一度説明するため、<xref:System.Windows.Data.Binding> オブジェクトを使用してバインディングを確立します。各バインドには通常、バインディング ターゲット、ターゲット プロパティ、バインディング ソース、および使用するソース値へのパスの 4 つのコンポーネントがあります。 このセクションでは、バインドの設定方法について説明します。

次の例について考えます。この例では、バインディング ソース オブジェクトは、*SDKSample* 名前空間で定義されている *MyData* という名前のクラスです。 デモンストレーション目的のため、*MyData* には、値が "Red" に設定された *ColorName* という名前の文字列プロパティがあります。 したがって、この例では、背景が赤のボタンが生成されます。

[!code-xaml[BindNonTextProperty](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/AutoConvertPropertyToColor.xaml#BindAutoConvertColor)]

バインディング宣言の構文の詳細およびコード内でバインドを設定する方法の例については、「[バインディング宣言の概要](../../framework/wpf/data/binding-declarations-overview.md)」を参照してください。

この例を基本的な図に適用すると、結果として得られる図は、次のようになります。 この図の Background プロパティは既定で <xref:System.Windows.Data.BindingMode.OneWay> バインディングをサポートしているため、これは <xref:System.Windows.Data.BindingMode.OneWay> バインディングを示しています。

![データ バインディングの Background プロパティを示す図。](./media/data-binding-overview/data-binding-button-background-example.png)

*ColorName* プロパティの型が文字列で <xref:System.Windows.Controls.Control.Background%2A> プロパティの型が <xref:System.Windows.Media.Brush>であるにもかかわらず、このバインドが機能することを不思議に思うかもしれません。 このバインドでは、既定の型変換が使用されます。これについては、「[データ変換](#data-conversion)」セクションで説明します。

### <a name="specifying-the-binding-source"></a>バインディング ソースの指定

前の例では、[DockPanel.DataContext](xref:System.Windows.FrameworkElement.DataContext) プロパティを設定することでバインディング ソースが指定されていることに注意してください。 <xref:System.Windows.Controls.Button> は、次にその親要素である <xref:System.Windows.Controls.DockPanel> から <xref:System.Windows.FrameworkElement.DataContext%2A> 値を継承します。 繰り返しますが、バインディング ソース オブジェクトは、バインディングの 4 つの必須コンポーネントの 1 つです。 したがって、バインディング ソース オブジェクトが指定されていないと、バインディングは機能しません。

バインディング ソース オブジェクトを指定するには複数の方法があります。 親要素で <xref:System.Windows.FrameworkElement.DataContext%2A> プロパティを使用すると、複数のプロパティを同じソースにバインドする場合に役立ちます。 ただし、個々のバインディング宣言でバインディング ソースを指定する方が適切な場合もあります。 前の例については、<xref:System.Windows.FrameworkElement.DataContext%2A> プロパティを使用する代わりに、次の例のように、<xref:System.Windows.Data.Binding.Source%2A?displayProperty=nameWithType> プロパティをボタンのバインディング宣言で直接設定することでバインディング ソースを指定できます。

[!code-xaml[BindNonTextPropertyCompactBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/AutoConvertPropertyToColor.xaml#BindAutoConvertColorCompactBinding)]

要素の <xref:System.Windows.FrameworkElement.DataContext%2A> プロパティを直接設定して先祖から <xref:System.Windows.FrameworkElement.DataContext%2A> 値を継承すること (最初の例にあるボタンなど)、およびバインディングの <xref:System.Windows.Data.Binding.Source%2A?displayProperty=nameWithType> プロパティを設定してバインディング ソースを明示的に指定すること (最後の例にあるボタンなど) 以外に、<xref:System.Windows.Data.Binding.ElementName?displayProperty=nameWithType> プロパティまたは <xref:System.Windows.Data.Binding.RelativeSource?displayProperty=nameWithType> プロパティを使用してバインディング ソースを指定することもできます。 <xref:System.Windows.Data.Binding.ElementName%2A> プロパティは、スライダーを使用してボタンの幅を調整する場合など、アプリ内の他の要素にバインドする場合に便利です。 <xref:System.Windows.Data.Binding.RelativeSource%2A> プロパティは、<xref:System.Windows.Controls.ControlTemplate> または <xref:System.Windows.Style> でバインドが指定されている場合に便利です。 詳細については、[「方法: バインディング ソースを指定する](../../framework/wpf/data/how-to-specify-the-binding-source.md)」を参照してください。

### <a name="specifying-the-path-to-the-value"></a>値にパスを指定する

バインディング ソースがオブジェクトの場合、<xref:System.Windows.Data.Binding.Path?displayProperty=nameWithType> プロパティを使用してバインドに使用する値を指定します。 XML データにバインドする場合は、<xref:System.Windows.Data.Binding.XPath?displayProperty=nameWithType> プロパティを使用して値を指定します。 場合によっては、データが XML の場合でも、<xref:System.Windows.Data.Binding.Path%2A> プロパティが使用できる場合があります。 たとえば、(XPath クエリの結果として) 返された XmlNode の Name プロパティにアクセスする場合、<xref:System.Windows.Data.Binding.XPath%2A> プロパティに加えて、<xref:System.Windows.Data.Binding.Path%2A> プロパティを使用する必要があります。

詳細については、<xref:System.Windows.Data.Binding.Path%2A> プロパティおよび <xref:System.Windows.Data.Binding.XPath%2A> プロパティを参照してください。

使用する値への <xref:System.Windows.Data.Binding.Path%2A> がバインディングの 4 つの必須コンポーネントの 1 つである点を強調してきましたが、オブジェクト全体にバインドするシナリオでは、使用する値はバインディング ソース オブジェクトと同じになります。 このような場合は、<xref:System.Windows.Data.Binding.Path%2A> を指定しないようにすることができます。 例を次に示します。

[!code-xaml[EmptyBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/EmptyBinding.xaml#EmptyBinding)]

上記の例では、空のバインド構文 {Binding} を使用しています。 この場合、<xref:System.Windows.Controls.ListBox> は DockPanel 親要素から DataContext を継承します (この例では示されていません)。 パスが指定されていない場合、既定では、オブジェクト全体にバインドします。 つまり、この例では、<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> プロパティをオブジェクト全体にバインドしているため、パスが省略されています。 (詳しい説明については、「[コレクションにバインドする](#binding-to-collections)」セクションを参照してください。)

コレクションにバインドする以外に、オブジェクトの 1 つのプロパティだけではなくオブジェクト全体にバインドするときにもこのシナリオは役立ちます。 たとえば、ソース オブジェクトが <xref:System.String> 型で、文字列そのものにバインドしたい場合などです。 もう 1 つの一般的なシナリオは、要素をいくつかのプロパティを持つオブジェクトにバインドする場合です。

バインディング ターゲット プロパティに対してデータが意味を持つように、カスタム ロジックを適用することが必要になる場合があります。 既定の型変換が存在しない場合、カスタム ロジックはカスタム コンバーターの形式になる場合があります。 コンバーターの詳細については、「[データ変換](#data-conversion)」を参照してください。

### <a name="binding-and-bindingexpression"></a>Binding と BindingExpression

データ バインディングの他の機能や使用方法に入る前に、<xref:System.Windows.Data.BindingExpression> クラスを紹介します。 前のセクションで説明したように、<xref:System.Windows.Data.Binding> クラスは、バインディング宣言のための高レベルのクラスです。このクラスには、バインドの特性を指定するための多数のプロパティが用意されています。 関連クラスである <xref:System.Windows.Data.BindingExpression> は、ソースとターゲットの間の接続を維持する基になるオブジェクトです。 バインドには、複数のバインド式の間で共有できるすべての情報が含まれています。 <xref:System.Windows.Data.BindingExpression> は、<xref:System.Windows.Data.Binding> のすべてのインスタンス情報を含む、共有できないインスタンス式です。

次の例を考えてみます。ここで `myDataObject` は `MyData` クラスのインスタンス、`myBinding` はソース <xref:System.Windows.Data.Binding> オブジェクト、`MyData` は `MyDataProperty` という名前の文字列プロパティを含む定義済みのクラスです。 この例では、<xref:System.Windows.Controls.TextBlock> のインスタンスである `myText` のテキストの内容を `MyDataProperty` にバインドします。

[!code-csharp[CodeOnlyBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/ManualBinding.cs#CodeOnlyBinding)]
[!code-vb[CodeOnlyBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/ManualBinding.vb#CodeOnlyBinding)]

同じ *myBinding* オブジェクトを使用して、他のバインディングを作成できます。 たとえば、*myBinding* オブジェクトを使用して、チェック ボックスのテキストの内容を *MyDataProperty* にバインドすることができます。 このシナリオには、*myBinding* オブジェクトを共有する 2 つの <xref:System.Windows.Data.BindingExpression> のインスタンスがあります。

<xref:System.Windows.Data.BindingExpression> オブジェクトは、データ バインドされたオブジェクトで <xref:System.Windows.Data.BindingOperations.GetBindingExpression%2A> を呼び出すことによって返されます。 次の記事では、<xref:System.Windows.Data.BindingExpression> クラスの使用方法について説明します。

- [バインドされているターゲット プロパティからのバインディング オブジェクトの取得](../../framework/wpf/data/how-to-get-the-binding-object-from-a-bound-target-property.md)

- [TextBox テキストでソースを更新するタイミングを制御する](../../framework/wpf/data/how-to-control-when-the-textbox-text-updates-the-source.md)

## <a name="data-conversion"></a>データ変換

<xref:System.Windows.Controls.Control.Background%2A> プロパティが "Red" という値を持つ文字列プロパティにバインドされているため、[[バインドの作成]](#creating-a-binding) セクションのボタンは赤色になります。 この文字列値は、文字列値を <xref:System.Windows.Media.Brush> に変換する型コンバーターが <xref:System.Windows.Media.Brush> 型に存在するために機能します。

この情報を「[バインドの作成](#creating-a-binding)」セクションにある図に追加すると、次のようになります。

![データ バインディングの既定のプロパティを示す図。](./media/data-binding-overview/data-binding-button-default-conversion.png)

しかし、バインディング ソース オブジェクトが文字列型のプロパティを持つ代わりに、<xref:System.Windows.Media.Color> 型の *Color* プロパティを持つ場合はどうなるでしょうか。 この場合、バインドが機能するためには、最初に *Color* プロパティ値を <xref:System.Windows.Controls.Control.Background%2A> プロパティが受け入れるものに変換する必要があります。 次の例のように、<xref:System.Windows.Data.IValueConverter> インターフェイスを実装することによって、カスタム コンバーターを作成する必要があります。

[!code-csharp[CodeOnlyBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/ColorBrushConverter.cs#ColorBrushConverter)]
[!code-vb[CodeOnlyBinding](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/ColorBrushConverter.vb#ColorBrushConverter)]

詳細については、「<xref:System.Windows.Data.IValueConverter>」を参照してください。

これで既定の変換の代わりにカスタム コンバーターが使用されるようになったので、図はこのようになります。

![データ バインディングのカスタム コンバーターを示す図。](./media/data-binding-overview/data-binding-converter-color-example.png)

繰り返しますが、バインドされている型に存在する型コンバーターにより、既定の変換が使用できます。 この動作は、ターゲットで利用可能な型コンバーターによって異なります。 独自のコンバーターを作成して、確認してみてください。

データ コンバーターを実装するのが合理的な典型的なシナリオをいくつか次に示します。

- カルチャに応じてデータを異なる方法で表示する必要がある場合。 たとえば、特定のカルチャで使用されている規則に基づいて、通貨コンバーターまたはカレンダー日付/時刻のコンバーターを実装することができます。

- 使用されているデータが必ずしもプロパティのテキスト値を変更することを意図しているわけではく、イメージのソースや表示テキストの色やスタイルなど、他のいくつかの値を変更することを意図している場合。 この場合、コンバーターを使用して、適切と思われないプロパティのバインディング (テキスト フィールドをテーブルのセルの Background プロパティにバインドするなど) を変換することができます。

- 複数のコントロールまたはコントロールの複数のプロパティが同じデータにバインドされている場合。 この場合、プライマリ バインドがテキストだけを表示する可能性があるのに対し、他のバインドは特定の表示に関する問題を処理しますが、同じバインドをソース情報として使用します。

- ターゲット プロパティには、<xref:System.Windows.Data.MultiBinding> と呼ばれるバインドのコレクションがあります。 <xref:System.Windows.Data.MultiBinding> では、カスタム <xref:System.Windows.Data.IMultiValueConverter> を使用して、バインドの値から最終的な値を生成します。 たとえば、色は赤、青、および緑の値から計算できますが、これらは同じまたは異なるバインディング ソース オブジェクトからの値にすることができます。 例と情報については、<xref:System.Windows.Data.MultiBinding> を参照してください。

## <a name="binding-to-collections"></a>コレクションにバインドする

バインディング ソース オブジェクトは、プロパティにデータが含まれている 1 つのオブジェクト、または、多くの場合グループ化されるポリモーフィック オブジェクト (データベースへのクエリの結果など) のデータ コレクションとして扱うことができます。 ここまでは、1 つのオブジェクトへのバインドについてのみ説明しました。 ただし、データ コレクションへのバインドは一般的なシナリオです。 たとえば、一般的なシナリオでは、<xref:System.Windows.Controls.ListBox>、<xref:System.Windows.Controls.ListView>、<xref:System.Windows.Controls.TreeView> などの <xref:System.Windows.Controls.ItemsControl> を使用して、データ コレクションを表示します。たとえば、「[データ バインディングとは](#what-is-data-binding)」のセクションで示されているアプリなどです。

幸い、基本的な図を引き続き使用できます。 <xref:System.Windows.Controls.ItemsControl> をコレクションにバインドする場合、図は次のようになります。

![データ バインディングの ItemsControl オブジェクトを示す図。](./media/data-binding-overview/data-binding-itemscontrol.png)

この図に示すように、<xref:System.Windows.Controls.ItemsControl> をコレクション オブジェクトにバインドするには <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A?displayProperty=nameWithType> プロパティを使用します。 `ItemsSource` は <xref:System.Windows.Controls.ItemsControl> のコンテンツと考えることができます。 `ItemsSource` プロパティは既定で `OneWay` バインディングをサポートしているため、バインドは <xref:System.Windows.Data.BindingMode.OneWay> になります。

### <a name="how-to-implement-collections"></a>コレクションを実装する方法

<xref:System.Collections.IEnumerable> インターフェイスを実装する任意のコレクションを列挙できます。 ただし、コレクションの挿入または削除によって UI が自動的に更新されるように動的バインドを設定するには、コレクションは <xref:System.Collections.Specialized.INotifyCollectionChanged> インターフェイスを実装する必要があります。 このインターフェイスは、基になるコレクションが変更されたときに発生させるイベントを公開します。

WPF には、<xref:System.Collections.Specialized.INotifyCollectionChanged> インターフェイスを公開するデータ コレクションの組み込みの実装である <xref:System.Collections.ObjectModel.ObservableCollection%601> クラスが用意されています。 ソース オブジェクトからターゲットへのデータ値の転送を完全にサポートするには、バインド可能なプロパティをサポートするコレクション内の各オブジェクトにも <xref:System.ComponentModel.INotifyPropertyChanged> インターフェイスを実装する必要があります。 詳しくは、「[バインディング ソースの概要](../../framework/wpf/data/binding-sources-overview.md)」をご覧ください。

独自のコレクションを実装する前に、<xref:System.Collections.ObjectModel.ObservableCollection%601> または既存のコレクション クラス (<xref:System.Collections.Generic.List%601>、<xref:System.Collections.ObjectModel.Collection%601>、<xref:System.ComponentModel.BindingList%601> など) のいずれかを使用することを検討してください。 高度なシナリオで独自のコレクションを実装する場合は、<xref:System.Collections.IList> の使用を検討します。これは、インデックスで個別にアクセスできる非ジェネリック オブジェクト コレクションを提供するため、最適なパフォーマンスが得られます。

### <a name="collection-views"></a>コレクション ビュー

<xref:System.Windows.Controls.ItemsControl> をデータ コレクションにバインドしたら、データを並べ替え、フィルター、またはグループ化することができます。 これを行うには、<xref:System.ComponentModel.ICollectionView> インターフェイスを実装するクラスであるコレクション ビューを使用します。

#### <a name="what-are-collection-views"></a>コレクション ビューとは

コレクション ビューは、基になるソース コレクション自体を変更することなく、並べ替え、フィルター、およびグループのクエリに基づくソース コレクションを移動および表示を可能にするバインディング ソース コレクションの上にある層です。 コレクション ビューには、コレクション内の現在の項目へのポインターも保持されます。 ソース コレクションが <xref:System.Collections.Specialized.INotifyCollectionChanged> インターフェイスを実装している場合、<xref:System.Collections.Specialized.INotifyCollectionChanged.CollectionChanged> イベントによって発生した変更はビューに反映されます。

ビューは基になるソース コレクションを変更しないため、各ソース コレクションは関連付けられた複数のビューを持つことができます。 たとえば、*Task* オブジェクトのコレクションを持つことができます。 ビューを使用すると、同じデータをさまざまな方法で表示できます。 たとえば、ページの左側に優先度で並べ替えられたタスクを表示し、右側に区分でグループ化されたタスクを表示できます。

#### <a name="how-to-create-a-view"></a>ビューの作成方法

ビューを作成して使用する方法の 1 つは、ビュー オブジェクトを直接インスタンス化して、それをバインディング ソースとして使用することです。 たとえば、「[データ バインディングとは](#what-is-data-binding)」セクションで示されている[データ バインディング デモ][data-binding-demo] アプリを考えてみましょう。 このアプリは、<xref:System.Windows.Controls.ListBox> をデータ コレクションに直接バインドせずに、データ コレクション経由でビューにバインドするように実装されています。 次の例は、[データ バインディング デモ][data-binding-demo] アプリから抽出されたものです。 <xref:System.Windows.Data.CollectionViewSource> クラスは、<xref:System.Windows.Data.CollectionView> から継承するクラスの XAML プロキシです。 この例では、ビューの <xref:System.Windows.Data.CollectionViewSource.Source%2A> が、現在のアプリ オブジェクトの *AuctionItems* コレクション (型 <xref:System.Collections.ObjectModel.ObservableCollection%601>) にバインドされています。

[!code-xaml[CollectionView](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml#CollectionView)]

これにより、リソース *listingDataView* は、<xref:System.Windows.Controls.ListBox> などのアプリ内の要素のバインディング ソースとして機能します。

[!code-xaml[ListBoxCollectionView](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml#ListBoxCollectionView)]

同じコレクションに対して別のビューを作成するには、別の <xref:System.Windows.Data.CollectionViewSource> インスタンスを作成して違う `x:Key` 名を付けます。

次の表に、既定のコレクション ビューとして作成される、またはソース コレクションの型に基づいて <xref:System.Windows.Data.CollectionViewSource> によって作成されるビューのデータ型を示します。

| ソース コレクションの型                    | コレクション ビューの型 | メモ |
| ----------------------------------------- | -------------------- | ----- |
| <xref:System.Collections.IEnumerable>     | <xref:System.Windows.Data.CollectionView> に基づく内部型 | 項目のグループ化は不可 |
| <xref:System.Collections.IList>           | <xref:System.Windows.Data.ListCollectionView> | 最も高速 |
| <xref:System.ComponentModel.IBindingList> | <xref:System.Windows.Data.BindingListCollectionView> | |

#### <a name="using-a-default-view"></a>既定のビューの使用

コレクション ビューを作成して使用する 1 つの方法は、バインディング ソースとしてコレクション ビューを指定することです。 WPF では、バインディング ソースとして使用されるすべてのコレクションに対して既定のコレクション ビューも作成されます。 コレクションに直接バインドすると、WPF はその既定のビューにバインドします。 この既定のビューは、同じコレクションにバインドされているすべてのバインドで共有されるため、1 つのバインド コントロールまたはコードによる既定のビューへの変更 (後述する並べ替えや現在の項目ポインターへの変更など) は、同じコレクションにバインドされている他のすべてのバインドに反映されます。

既定のビューを取得するには、<xref:System.Windows.Data.CollectionViewSource.GetDefaultView%2A> メソッドを使用します。 例については、「[データ コレクションの既定のビューを取得する](../../framework/wpf/data/how-to-get-the-default-view-of-a-data-collection.md)」を参照してください。

#### <a name="collection-views-with-adonet-datatables"></a>コレクション ビューと ADO.NET DataTable

パフォーマンスを向上させるために、ADO.NET <xref:System.Data.DataTable> または <xref:System.Data.DataView> オブジェクトのコレクション ビューは、並べ替えとフィルター処理を <xref:System.Data.DataView> に委任します。これにより、並べ替えとフィルター処理が、データ ソースのすべてのコレクション ビューで共有されます。 各コレクション ビューで独立して並べ替えとフィルター処理をできるようにするには、各コレクション ビューを独自の <xref:System.Data.DataView> オブジェクトを使って初期化します。

#### <a name="sorting"></a>並べ替え

前述したように、ビューでは並べ替え順序をコレクションに適用できます。 これは基になるコレクション内に存在するため、データに関連性がない場合や、本来の順序ではない場合もあります。 コレクションのビューでは、指定する比較の基準に基づいて、順序を強制したり、既定の順序を変更することができます。 これはデータのクライアント ベースのビューであるため、一般的なシナリオは、ユーザーが列に対応する値ごとに表形式のデータの列を並べ替える場合です。 ビューを使用することで、このようなユーザー主導の並べ替えを適用することができます。この場合も、基になるコレクションを変更したり、コレクションのコンテンツにクエリを再実行する必要はありません。 例については、「[ヘッダーがクリックされたときに GridView 列を並べ替える](../../framework/wpf/controls/how-to-sort-a-gridview-column-when-a-header-is-clicked.md)」を参照してください。

次の例では、「[データ バインディングとは](#what-is-data-binding)」セクションにあるアプリ UI の [Sort by category and date]\(カテゴリと日付で並べ替え\) <xref:System.Windows.Controls.CheckBox> の並べ替えロジックを示しています。

[!code-csharp[AddSortChecked](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml.cs#AddSortChecked)]
[!code-vb[AddSortChecked](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/CollectionView.xaml.vb#AddSortChecked)]

#### <a name="filtering"></a>フィルター処理

ビューでは、コレクションにフィルターを適用して、完全なコレクションの特定のサブセットのみが表示されるようにすることもできます。 データ内の条件をフィルターすることができます。 たとえば、「[データ バインディングとは](#what-is-data-binding)」セクションのアプリで行ったように、[Show only bargains]\(バーゲンのみを表示\) <xref:System.Windows.Controls.CheckBox> には、25 ドル以上の項目を除外するためのロジックが含まれています。 次のコードを実行すると、<xref:System.Windows.Controls.CheckBox> を選択したときに、*ShowOnlyBargainsFilter* が <xref:System.Windows.Data.CollectionViewSource.Filter> イベント ハンドラーとして設定されます。

[!code-csharp[ListingViewFilter](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml.cs#ListingViewFilter)]
[!code-vb[ListingViewFilter](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/CollectionView.xaml.vb#ListingViewFilter)]

*ShowOnlyBargainsFilter* イベント ハンドラーには、次の実装があります。

[!code-csharp[FilterEvent](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml.cs#FilterEvent)]
[!code-vb[FilterEvent](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/CollectionView.xaml.vb#FilterEvent)]

<xref:System.Windows.Data.CollectionViewSource> ではなく <xref:System.Windows.Data.CollectionView> クラスの 1 つを直接使用している場合は、<xref:System.Windows.Data.CollectionView.Filter%2A> プロパティを使用してコールバックを指定します。 例については、「[ビュー内のデータをフィルター処理する](../../framework/wpf/data/how-to-filter-data-in-a-view.md)」を参照してください。

#### <a name="grouping"></a>グループ化

<xref:System.Collections.IEnumerable> コレクションを表示する内部クラスを除き、すべてのコレクション ビューで*グループ化*がサポートされています。グループ化により、ユーザーはコレクション ビューでコレクションを論理グループに分割することができます。 グループは、明示的 (ユーザーがグループの一覧を提供する) または暗黙的 (グループがデータに応じて動的に生成される) にすることができます。

次の例では、[Group by category]\(分類別にグループ化\) <xref:System.Windows.Controls.CheckBox> のロジックを示しています。

[!code-csharp[ListingGroupCheck](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml.cs#ListingGroupCheck)]
[!code-vb[ListingGroupCheck](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/CollectionView.xaml.vb#ListingGroupCheck)]

別のグループ化の例については、「[GridView を実装する ListView の項目をグループ化する](../../framework/wpf/controls/how-to-group-items-in-a-listview-that-implements-a-gridview.md)」を参照してください。

#### <a name="current-item-pointers"></a>現在の項目ポインター

ビューでは、現在の項目の概念もサポートされています。 コレクション ビュー内のオブジェクト間を移動することができます。 移動するときに、項目のポインターを動かすことで、コレクション内の特定の場所に存在するオブジェクトを取得できます。 例については、「[データ CollectionView のオブジェクト間を移動する](../../framework/wpf/data/how-to-navigate-through-the-objects-in-a-data-collectionview.md)」を参照してください。

WPF はビュー (指定したビュー、またはコレクションの既定のビュー) を使用してコレクションのみにバインドするため、コレクションへのすべてのバインディングには現在の項目のポインターがあります。 ビューにバインドする際に、`Path` 値内のスラッシュ ("/") 文字は、ビューの現在の項目を指定します。 次の例では、データ コンテキストはコレクション ビューです。 最初の行は、コレクションにバインドします。 2 番目の行は、コレクション内の現在の項目にバインドします。 3 番目の行は、コレクション内の現在の項目の `Description` プロパティにバインドします。

```xaml
<Button Content="{Binding }" />
<Button Content="{Binding Path=/}" />
<Button Content="{Binding Path=/Description}" />
```

スラッシュとプロパティの構文をスタックして、コレクションの階層をトラバースすることもできます。 次の例では、ソース コレクションの現在の項目のプロパティでである、`Offices` という名前のコレクションの現在の項目にバインドします。

```xaml
<Button Content="{Binding /Offices/}" />
```

現在の項目のポインターは、コレクションに適用されている任意の並べ替えまたはフィルター処理の影響を受ける場合があります。 並べ替えは、現在の項目のポインターを最後に選択した項目に保持しますが、コレクション ビューはそれを中心に再構築されています (以前はリストの先頭にあった選択した項目が、現在はリストの中ほどにある場合があります)。フィルター処理後に選択した項目がビューに残っている場合、フィルター処理はその項目を保持します。 それ以外の場合は、現在の項目のポインターが、フィルター処理されたコレクション ビューの最初の項目に設定されます。

#### <a name="master-detail-binding-scenario"></a>マスターと詳細のバインディング シナリオ

現在の項目の概念は、コレクション内の項目間の移動に役立つだけでなく、マスターと詳細のバインディング シナリオにも役立ちます。 もう一度、「[データ バインディングとは](#what-is-data-binding)」セクションのアプリの UI を考えてみましょう。 そのアプリでは、<xref:System.Windows.Controls.ListBox> で選択した項目によって、<xref:System.Windows.Controls.ContentControl> に表示されるコンテンツが決定されます。 つまり、<xref:System.Windows.Controls.ListBox> 項目を選択すると、選択した項目の詳細が <xref:System.Windows.Controls.ContentControl> に表示されます。

同じビューにバインドされた 2 つ以上のコントロールがあるだけで、マスターと詳細のシナリオを実装できます。 [データ バインディングのデモ][data-binding-demo]の次の例では、<xref:System.Windows.Controls.ListBox> のマークアップと、「[データ バインディングとは](#what-is-data-binding)」セクションのアプリの UI に表示されている <xref:System.Windows.Controls.ContentControl> が示されています。

[!code-xaml[ListBoxContentControl](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml#ListBoxContentControl)]

両方のコントロールが同じソースである *listingDataView* 静的リソース (このリソースの定義は「[ビューの作成方法](#how-to-create-a-view)」セクションを参照してください) にバインドされていることに注目してください。 このバインドが機能するのは、シングルトン オブジェクト (この場合は <xref:System.Windows.Controls.ContentControl>) がコレクション ビューにバインドされると、ビューの <xref:System.Windows.Data.CollectionView.CurrentItem%2A> に自動的にバインドされるためです。 <xref:System.Windows.Data.CollectionViewSource> オブジェクトは、通貨と選択を自動的に同期します。 この例のように、リスト コントロールが <xref:System.Windows.Data.CollectionViewSource> オブジェクトにバインドされていない場合、機能させるには、その <xref:System.Windows.Controls.Primitives.Selector.IsSynchronizedWithCurrentItem%2A> プロパティを `true` に設定する必要があります。

その他の例については、「[コレクションにバインドして選択に基づく情報を表示する](../../framework/wpf/data/how-to-bind-to-a-collection-and-display-information-based-on-selection.md)」と「[階層データでマスター詳細パターンを使用する](../../framework/wpf/data/how-to-use-the-master-detail-pattern-with-hierarchical-data.md)」を参照してください。

上記の例では、テンプレートが使用されています。 実際、テンプレート (1 つは <xref:System.Windows.Controls.ContentControl> によって明示的に使用され、1 つは <xref:System.Windows.Controls.ListBox> によって暗黙的に使用されています) を使用しないと、データは希望どおりに表示されません。 次のセクションで、データ テンプレートについて説明します。

## <a name="data-templating"></a>データ テンプレート

データ テンプレートを使用しないと、「[データ バインディングとは](#what-is-data-binding)」セクションのアプリの UI は、次のようになります。

![データ テンプレートのないデータ バインディング デモ](./media/data-binding-overview/demo-no-template.png)

前のセクションの例で示したように、*コントロールと* はどちらも <xref:System.Windows.Controls.ListBox>AuctionItem<xref:System.Windows.Controls.ContentControl> のコレクション オブジェクト全体 (より具体的には、コレクション オブジェクトのビュー) にバインドされています。 データ コレクションの表示方法の具体的な指示がない場合、<xref:System.Windows.Controls.ListBox> は基になるコレクション内の各オブジェクトの文字列形式を表示し、<xref:System.Windows.Controls.ContentControl> はバインド先のオブジェクトの文字列形式を表示します。

この問題を解決するには、アプリで <xref:System.Windows.DataTemplate?text=DataTemplates> を定義します。 前のセクションの例で示したように、<xref:System.Windows.Controls.ContentControl> では、*detailsProductListingTemplate* データ テンプレートが明示的に使用されます。 <xref:System.Windows.Controls.ListBox> コントロールは、コレクション内の *AuctionItem* オブジェクトを表示するときに、次のデータ テンプレートを暗黙的に使用します。

[!code-xaml[AuctionItemDataTemplate](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/CollectionView.xaml#AuctionItemDataTemplate)]

これら 2 つの DataTemplates を使用して、結果として得られた UI が、「[データ バインディングとは](#what-is-data-binding)」セクションに示されているものです。 スクリーン ショットからわかるように、DataTemplates を使用すると、データをコントロールに配置できるだけでなく、データの説得力のあるビジュアルを定義できます。 たとえば、上記の <xref:System.Windows.DataTemplate> では、*SpecialFeatures* の値が *HighLight* になっている *AuctionItem* にオレンジ色の枠と星印が付いて表示されるように、<xref:System.Windows.DataTrigger> が使用されています。

データ テンプレートの詳細については、「[データ テンプレートの概要](../../framework/wpf/data/data-templating-overview.md)」を参照してください。

## <a name="data-validation"></a>データの検証

ユーザー入力を受け取るほとんどのアプリには、ユーザーが必要な情報を入力していることを確認する検証ロジックが必要です。 検証チェックは、型、範囲、形式、またはその他のアプリに固有の要件に基づいて作成できます。 このセクションでは、WPF でデータ検証がどのように機能するかについて説明します。

### <a name="associating-validation-rules-with-a-binding"></a>検証ルールをバインドに関連付ける

WPF データ バインディング モデルを使用すると、<xref:System.Windows.Data.Binding.ValidationRules%2A> を <xref:System.Windows.Data.Binding> オブジェクトに関連付けることができます。 たとえば、次の例では、<xref:System.Windows.Controls.TextBox> を `StartPrice` という名前のプロパティにバインドし、<xref:System.Windows.Data.Binding.ValidationRules%2A?displayProperty=nameWithType> プロパティに <xref:System.Windows.Controls.ExceptionValidationRule> オブジェクトを追加します。

[!code-xaml[TextboxStartPrice](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/DataValidation.xaml#TextboxStartPrice)]

<xref:System.Windows.Controls.ValidationRule> オブジェクトは、プロパティの値が有効かどうかを確認します。 WPF には、次の 2 種類の組み込み <xref:System.Windows.Controls.ValidationRule> オブジェクトがあります。

- <xref:System.Windows.Controls.ExceptionValidationRule> は、バインディング ソース プロパティの更新中にスローされた例外を確認します。 前述の例では、`StartPrice` は整数型です。 ユーザーが整数に変換できない値を入力すると、例外がスローされ、バインディングが無効としてマークされます。 <xref:System.Windows.Controls.ExceptionValidationRule> を明示的に設定する別の構文としては、<xref:System.Windows.Data.Binding> オブジェクトまたは <xref:System.Windows.Data.MultiBinding> オブジェクトで <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> プロパティを `true` に設定することが挙げられます。

- <xref:System.Windows.Controls.DataErrorValidationRule> オブジェクトは、<xref:System.ComponentModel.IDataErrorInfo> インターフェイスを実装するオブジェクトによって発生したエラーを確認します。 この検証規則の使用例については、<xref:System.Windows.Controls.DataErrorValidationRule> を参照してください。 <xref:System.Windows.Controls.DataErrorValidationRule> を明示的に設定する別の構文としては、<xref:System.Windows.Data.Binding> オブジェクトまたは <xref:System.Windows.Data.MultiBinding> オブジェクトで <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> プロパティを `true` に設定することが挙げられます。

<xref:System.Windows.Controls.ValidationRule> クラスから派生し、<xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドを実装することによって、独自の検証規則を作成することもできます。 次の例は、「[データ バインディングとは](#what-is-data-binding)」セクションの *[Add Product Listing]\(製品一覧の追加\)* の [Start Date\(開始日\)] <xref:System.Windows.Controls.TextBox> で使用されている規則を示します。

[!code-csharp[FutureDateRule](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/FutureDateRule.cs#FutureDateRule)]
[!code-vb[FutureDateRule](~/samples/snippets/desktop-guide/wpf/data-binding-overview/vb/FutureDateRule.vb#FutureDateRule)]

次の例に示すように、*StartDateEntryForm* <xref:System.Windows.Controls.TextBox> は、この *FutureDateRule* を使用します。

[!code-xaml[TextboxStartDate](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/DataValidation.xaml#TextboxStartDate)]

<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 値は <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> であるため、バインディング エンジンによって、キーが入力される度にソース値が更新されます。これは、キーが入力される度に、<xref:System.Windows.Data.Binding.ValidationRules%2A> コレクション内のすべての規則がチェックされることを意味します。 これについては、「検証プロセス」セクションで詳しく説明します。

### <a name="providing-visual-feedback"></a>視覚的なフィードバックを提供する

ユーザーが無効な値を入力した場合に、エラーに関する何らかのフィードバックをアプリ UI に送信することができます。 このようなフィードバックを送信する方法の 1 つとして、<xref:System.Windows.Controls.Validation.ErrorTemplate%2A?displayProperty=nameWithType> 添付プロパティをカスタム <xref:System.Windows.Controls.ControlTemplate> に設定する方法があります。 前のサブセクションで示したように、*StartDateEntryForm* <xref:System.Windows.Controls.TextBox> は *validationTemplate* と呼ばれる <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> を使用します。 次の例は、*validationTemplate* の定義を示します。

[!code-xaml[ControlTemplate](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/DataValidation.xaml#ControlTemplate)]

<xref:System.Windows.Controls.AdornedElementPlaceholder> 要素は、装飾されるコントロールを配置する場所を指定します。

さらに、<xref:System.Windows.Controls.ToolTip> を使用してエラー メッセージを表示することもできます。 *StartDateEntryForm* と *StartPriceEntryForm* <xref:System.Windows.Controls.TextBox> は、どちらも *textStyleTextBox* スタイルを使用します。これにより、エラー メッセージを表示する <xref:System.Windows.Controls.ToolTip> が作成されます。 次の例は、*textStyleTextBox* の定義を示します。 バインドされた要素のプロパティの 1 つ以上のバインドにエラーがある場合、添付プロパティ <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> は `true` になります。

[!code-xaml[TextBoxStyle](~/samples/snippets/desktop-guide/wpf/data-binding-overview/csharp/DataValidation.xaml#TextBoxStyle)]

カスタム <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> と <xref:System.Windows.Controls.ToolTip> では、検証エラーが発生した場合、*StartDateEntryForm* <xref:System.Windows.Controls.TextBox> は次のようになります。

![データ バインディング検証エラー](./media/data-binding-overview/demo-validation-date.png "DataBindingDemo_Validation")

<xref:System.Windows.Data.Binding> に検証規則が関連付けられているが、バインド コントロールで <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> が指定されていない場合、既定の <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> が使用され、検証エラーが発生したことがユーザーに通知されます。 既定の <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> は、装飾レイヤーの赤い枠線を定義するコントロール テンプレートです。 既定の <xref:System.Windows.Controls.Validation.ErrorTemplate%2A> と <xref:System.Windows.Controls.ToolTip> では、検証エラーが発生したときの *StartPriceEntryForm* <xref:System.Windows.Controls.TextBox> の UI は次のようになります。

![データ バインディング検証エラー](./media/data-binding-overview/demo-validation-price.png "DataBindingDemo_ValidationDefault")

ダイアログ ボックス内のすべてのコントロールを検証するためのロジックを提供する方法の例については、「[ダイアログ ボックスの概要](../../framework/wpf/app-development/dialog-boxes-overview.md)」の「カスタム ダイアログ ボックス」セクションを参照してください。

### <a name="validation-process"></a>検証プロセス

検証は通常、ターゲットの値がバインディング ソースのプロパティに転送されるときに発生します。 この転送は、<xref:System.Windows.Data.BindingMode.TwoWay> と <xref:System.Windows.Data.BindingMode.OneWayToSource> のバインドに対して行われます。 繰り返しますが、「<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>ソースの更新のトリガー[」セクションで説明したように、ソースが更新されるトリガーは、](#what-triggers-source-updates) プロパティの値に依存しています。

次の項目では、*検証*プロセスについて説明します。 このプロセス中の任意の時点で検証エラーまたはその他の種類のエラーが発生すると、プロセスは停止されます。

1. バインディング エンジンは、その <xref:System.Windows.Data.Binding> で <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.RawProposedValue> に設定されているカスタム <xref:System.Windows.Controls.ValidationRule> オブジェクトが定義されているかどうかを確認します。この場合は、いずれかでエラーが発生するまで、またはすべてが成功するまで、各 <xref:System.Windows.Controls.ValidationRule> に対して <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドを呼び出します。

2. その後、バインディング エンジンがコンバーターを呼び出します (ある場合)。

3. コンバーターが成功すると、バインディング エンジンは、その <xref:System.Windows.Data.Binding> で <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.ConvertedProposedValue> に設定されているカスタム <xref:System.Windows.Controls.ValidationRule> オブジェクトが定義されているかどうかを確認します。この場合は、いずれかでエラーが発生するまで、またはすべてが成功するまで、<xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.ConvertedProposedValue> に設定されている各 <xref:System.Windows.Controls.ValidationRule> に対して <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドを呼び出します。

4. バインディング エンジンは、ソース プロパティを設定します。

5. バインディング エンジンは、その <xref:System.Windows.Data.Binding> で <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されているカスタム <xref:System.Windows.Controls.ValidationRule> オブジェクトが定義されているかどうかを確認します。この場合は、いずれかでエラーが発生するまで、またはすべてが成功するまで、<xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されている各 <xref:System.Windows.Controls.ValidationRule> に対して <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドを呼び出します。 <xref:System.Windows.Controls.DataErrorValidationRule> がバインドに関連付けられており、その <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が既定の <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されている場合、この時点で <xref:System.Windows.Controls.DataErrorValidationRule> がチェックされます。 この時点で、<xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> が `true` に設定されているバインドがすべてオンになります。

6. バインディング エンジンは、その <xref:System.Windows.Data.Binding> で <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.CommittedValue> に設定されているカスタム <xref:System.Windows.Controls.ValidationRule> オブジェクトが定義されているかどうかを確認します。この場合は、いずれかでエラーが発生するまで、またはすべてが成功するまで、<xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.CommittedValue> に設定されている各 <xref:System.Windows.Controls.ValidationRule> に対して <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドを呼び出します。

<xref:System.Windows.Controls.ValidationRule> がこのプロセス全体を通じて成功しない場合、バインディング エンジンは <xref:System.Windows.Controls.ValidationError> オブジェクトを作成し、バインドされた要素の <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=nameWithType> コレクションに追加します。 バインディング エンジンは、特定の手順で <xref:System.Windows.Controls.ValidationRule> オブジェクトを実行する前に、バインドされた要素の <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=nameWithType> 添付プロパティに追加されたすべての <xref:System.Windows.Controls.ValidationError> を削除します。 たとえば、<xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されている <xref:System.Windows.Controls.ValidationRule> が失敗した場合、次回の検証プロセスの実行時に、バインディング エンジンは <xref:System.Windows.Controls.ValidationRule.ValidationStep%2A> が <xref:System.Windows.Controls.ValidationStep.UpdatedValue> に設定されているすべての <xref:System.Windows.Controls.ValidationRule> を呼び出す前に、その <xref:System.Windows.Controls.ValidationError> を削除します。

<xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=nameWithType> が空でない場合、要素の <xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `true` に設定されます。 また、<xref:System.Windows.Data.Binding> の <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A> プロパティが `true` に設定されている場合は、バインディング エンジンによって、要素で <xref:System.Windows.Controls.Validation.Error?displayProperty=nameWithType> 添付イベントが発生します。

また、有効な値をいずれかの方向 (ターゲットからソースまたはソースからターゲット) に転送すると、<xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=nameWithType> 添付プロパティが消去されることにも注意してください。

バインディングに関連付けられている <xref:System.Windows.Controls.ExceptionValidationRule> がある場合、または <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> プロパティが `true` に設定されていて、バインディング エンジンがソースを設定したときに例外がスローされた場合、バインディング エンジンによって <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A> があるかどうかが確認されます。 <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A> コールバックを使用して、例外を処理するためのカスタム ハンドラーを提供するオプションがあります。 <xref:System.Windows.Data.Binding> で <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A> が指定されていない場合、バインディング エンジンは例外を使用して <xref:System.Windows.Controls.ValidationError> を作成し、バインドされた要素の <xref:System.Windows.Controls.Validation.Errors%2A?displayProperty=nameWithType> コレクションに追加します。

## <a name="debugging-mechanism"></a>デバッグのメカニズム

バインド関連のオブジェクトに添付プロパティ <xref:System.Diagnostics.PresentationTraceSources.TraceLevel%2A?displayProperty=nameWithType> を設定して、特定のバインドの状態に関する情報を受け取ることができます。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.DataErrorValidationRule>
- [LINQ クエリの結果にバインドする](../../framework/wpf/data/how-to-bind-to-the-results-of-a-linq-query.md)
- [データ バインディング](../../framework/wpf/advanced/optimizing-performance-data-binding.md)
- [データ バインディング デモ][data-binding-demo]
- [ハウツー記事](../../framework/wpf/data/data-binding-how-to-topics.md)
- [ADO.NET データ ソースにバインドする](../../framework/wpf/data/how-to-bind-to-an-ado-net-data-source.md)

[data-binding-demo]: https://github.com/microsoft/WPF-Samples/tree/master/Sample%20Applications/DataBindingDemo "データ バインディング デモ アプリ"
