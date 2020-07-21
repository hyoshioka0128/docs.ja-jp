---
title: バインディング宣言の概要
description: Windows Presentation Foundation (WPF) でアプリケーション開発のバインディングを XAML で宣言する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- markup extensions [WPF]
- data binding [WPF], declarations
- object element syntax [WPF]
- binding data [WPF], declarations
- syntax [WPF], object elements
- binding declarations [WPF]
ms.assetid: b97fd626-4c0d-4761-872a-2bca5820da2c
ms.openlocfilehash: 8d4943de0cacb5fe0b5a0c37a5a68f15243ad528
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85619638"
---
# <a name="binding-declarations-overview"></a>バインディング宣言の概要

このトピックでは、バインディングを宣言するさまざまな方法について説明します。

<a name="Prereq"></a>

## <a name="prerequisites"></a>必須コンポーネント

このトピックを読む前に、マークアップ拡張機能の概念と使用方法について理解している必要があります。 マークアップ拡張機能の詳細については、 「[マークアップ拡張機能と WPF XAML](../advanced/markup-extensions-and-wpf-xaml.md)」を参照してください。

このトピックでは、データ バインディングの概念については説明しません。 データ バインディングの概念の詳細については、「[Data Binding Overview](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。

<a name="BindinginXAML"></a>

## <a name="declaring-a-binding-in-xaml"></a>XAML でのバインディングの宣言

このセクションでは、XAML でバインディングを宣言する方法について説明します。

<a name="MarkupExtensionSyntax"></a>

### <a name="markup-extension-usage"></a>マークアップ拡張機能の使用方法

<xref:System.Windows.Data.Binding> はマークアップ拡張機能です。 バインディング拡張機能を使用してバインディングを宣言するとき、この宣言は、`Binding` キーワードに続く一連の句で構成され、コンマ (,) で区切られます。 バインディング宣言内の句の順序は任意で、多数の組み合わせが可能です。 句は*名前*=*値*のペアで、"*名前*" は <xref:System.Windows.Data.Binding> プロパティの名前、"*値*" はこのプロパティに設定する値です。

マークアップでバインディング宣言文字列を作成する場合、この文字列はターゲット オブジェクトの特定の依存関係プロパティにアタッチする必要があります。 次の例では、バインディング拡張機能を使用して <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> プロパティをバインドし、<xref:System.Windows.Data.Binding.Source%2A> プロパティと <xref:System.Windows.Data.Binding.Path%2A> プロパティを指定する方法を示します。

[!code-xaml[SimpleBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/SimpleBinding/CSharp/Page1.xaml#L37-L37)]

<xref:System.Windows.Data.Binding> クラスのプロパティのほとんどをこの方法で指定できます。 バインディング拡張機能およびバインディング拡張機能を使用して設定できない <xref:System.Windows.Data.Binding> プロパティの一覧については、「[バインドのマークアップ拡張機能](../advanced/binding-markup-extension.md)」の概要を参照してください。

<a name="ObjectElementSyntax"></a>

### <a name="object-element-syntax"></a>オブジェクト要素構文

オブジェクト要素構文は、バインディング宣言を作成する代替の方法です。 ほとんどの場合は、マークアップ拡張機能の使用とオブジェクト要素構文の使用のどちらにも特別な利点はありません。 ただし、マークアップ拡張機能がサポートしないシナリオでは (プロパティ値が文字列タイプではなく、このタイプの変換が存在しない場合)、オブジェクト要素構文を使用する必要があります。

オブジェクト要素構文とマークアップ拡張機能の使用の両方の例を次に示します。

[!code-xaml[BindConversionMarkup#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversionMarkup/CSharp/Page1.xaml#1)]

この例では、拡張構文を使用してバインディングを宣言することによって <xref:System.Windows.Controls.TextBlock.Foreground%2A> プロパティをバインドします。 <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティのバインディング宣言では、オブジェクト要素構文を使用します。

別の用語の詳細については、「[XAML Syntax の詳細](../advanced/xaml-syntax-in-detail.md)」を参照してください。

<a name="MBandPB"></a>

### <a name="multibinding-and-prioritybinding"></a>MultiBinding と PriorityBinding

<xref:System.Windows.Data.MultiBinding> と <xref:System.Windows.Data.PriorityBinding> では、XAML 拡張構文はサポートされていません。 したがって、XAML で <xref:System.Windows.Data.MultiBinding> または <xref:System.Windows.Data.PriorityBinding> を宣言する場合は、オブジェクト要素構文を使用する必要があります。

<a name="BindinginCode"></a>

## <a name="creating-a-binding-in-code"></a>コードでバインディングを作成する方法

バインディングを指定する別の方法は、コードで <xref:System.Windows.Data.Binding> オブジェクトにプロパティを直接設定する方法です。 次の例では、<xref:System.Windows.Data.Binding> オブジェクトを作成し、コードでプロパティを指定する方法を示します。  この例では、`TheConverter` は <xref:System.Windows.Data.IValueConverter> インターフェイスを実装するオブジェクトです。

[!code-csharp[BindConversion#1](~/samples/snippets/csharp/VS_Snippets_Wpf/BindConversion/CSharp/Window1.xaml.cs#1)]
[!code-vb[BindConversion#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BindConversion/visualbasic/window1.xaml.vb#1)]

バインディングしているオブジェクトが <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> の場合、<xref:System.Windows.Data.BindingOperations.SetBinding%2A?displayProperty=nameWithType> を使用する代わりに、オブジェクトで `SetBinding` メソッドを直接呼び出すことができます。 例については、「[Create a Binding in Code](how-to-create-a-binding-in-code.md)」を参照してください。

<a name="Path_Syntax"></a>

## <a name="binding-path-syntax"></a>バインディング パス構文

<xref:System.Windows.Data.Binding.Path%2A> プロパティを使用して、バインドするソース値を指定します。

- 最も簡単なケースでは、<xref:System.Windows.Data.Binding.Path%2A> プロパティの値は、バインディングに使用するソース オブジェクトのプロパティの名前です (`Path=PropertyName` など)。

- プロパティのサブプロパティは、C# と同様の構文で指定できます。 たとえば、句 `Path=ShoppingCart.Order` は、バインディングをオブジェクトのサブプロパティ `Order` またはプロパティ `ShoppingCart` に設定します。

- 添付プロパティにバインドするには、添付プロパティをかっこで囲みます。 たとえば、添付プロパティ <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> にバインドする構文は `Path=(DockPanel.Dock)` です。

- プロパティのインデクサーは、インデクサーが適用されているプロパティ名の後ろの角かっこ内に指定できます。 たとえば、句 `Path=ShoppingCart[0]` は、プロパティの内部インデックスがリテラル文字列「0」を処理する方法に対応するインデックスへのバインディングを設定します。 入れ子になったインデクサーもサポートします。

- `Path` 句ではインデクサーとサブプロパティを混在させることができます。例: `Path=ShoppingCart.ShippingInfo[MailingAddress,Street].`

- インデクサー内では、コンマ (,) で区切って複数のインデクサー パラメーターを指定できます。 各パラメーターの型は、かっこで指定できます。 たとえば、`Path="[(sys:Int32)42,(sys:Int32)24]"` などと指定できます。この場合、`sys` は `System` 名前空間にマップされます。

- ソースがコレクション ビューの場合は、現在の項目をスラッシュ (/) で指定できます。 たとえば、句 `Path=/` では、ビューの現在の項目に対するバインディングが設定されます。 ソースがコレクションの場合、この構文では、既定のコレクション ビューの現在の項目を指定します。

- プロパティ名とスラッシュを組み合わせて、コレクションであるプロパティを走査することができます。 たとえば、`Path=/Offices/ManagerName` では、それもコレクションである `Offices` プロパティが含まれるソース コレクションの現在の項目が指定されます。 現在の項目は、`ManagerName` プロパティを含むオブジェクトです。

- 必要に応じて、ピリオド (.) のパスを使用して、現在のソースにバインドできます。 たとえば、`Text="{Binding}"` は、`Text="{Binding Path=.}"` と同じです。

### <a name="escaping-mechanism"></a>エスケープのしくみ

- インデクサー ([ ]) 内では、キャレット文字 (^) は次の文字をエスケープします。

- XAML で <xref:System.Windows.Data.Binding.Path%2A> を設定した場合、XML 言語定義で特別な意味を持つ特定の文字も (XML エンティティを使用して) エスケープする必要があります。

  - 文字 "&" をエスケープするには、`&amp;` を使用します。

  - 使用する`&gt;`終了タグをエスケープする">"です。

- さらに、マークアップ拡張構文を使用して属性のバインディング全体を記述する場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] マークアップ拡張機能パーサーで特別な意味を持つ文字を (円記号 \\ を使用して) エスケープする必要があります。

  - 円記号 (\\) はエスケープ文字そのものです。

  - 等号 (=) は、プロパティ名とプロパティの値を区切ります。

  - コンマ (,) はプロパティを区切ります。

  - 右中かっこ (}) は、マークアップ拡張機能の終わりです。

<a name="Default"></a>

## <a name="default-behaviors"></a>既定の動作

既定の動作は、宣言で指定されていない場合には次のとおりです。

- バインディング ソースの値とバインディング ターゲットの値の型変換を実行しようとする既定のコンバーターが作成されます。 変換を実行できない場合、既定のコンバーターは `null` を返します。

- <xref:System.Windows.Data.Binding.ConverterCulture%2A> を設定しない場合、バインディング エンジンではバインディング ターゲット オブジェクトの `Language` プロパティが使用されます。 XAML では、既定で "en-US" になるか、または明示的に設定されている場合にはページのルート要素 (または任意の要素) から値を継承します。

- バインディングに既にデータ コンテキスト (たとえば、親要素から継承したデータ コンテキスト) があり、そのコンテキストによって返される項目またはコンテキストが何であれ、さらなるパスの変更を必要とせずにバインディングに対して適切である限り、バインディング宣言に句がまったくなくてもかまいません: `{Binding}`。これは、多くの場合、データのスタイルに対してバインディングを指定する方法で、バインディングはコレクションに基づいて動作します。 詳細については、「[バインディング ソースの概要](binding-sources-overview.md)」の「バインディング ソースとして使用する全体オブジェクト」セクションを参照してください。

- 既定の <xref:System.Windows.Data.Binding.Mode%2A> は、バインドされている依存関係プロパティによって一方向と双方向で異なります。 常にバインディング モードを明示的に宣言し、バインディングに目的の動作があることを確認できます。 一般に、ユーザーが編集できる <xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> や <xref:System.Windows.Controls.Primitives.RangeBase.Value%2A?displayProperty=nameWithType> などのコントロール プロパティは既定で双方向のバインディングであり、それ以外のほとんどのプロパティは既定で一方向のバインドになります。

- 既定の <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> 値は、バインドされている依存関係プロパティによっても <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> と <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> で異なります。 ほとんどの依存関係プロパティの既定値は <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged> です。ただし、<xref:System.Windows.Controls.TextBox.Text%2A?displayProperty=nameWithType> プロパティの既定値は <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus> です。

## <a name="see-also"></a>関連項目

- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
- [データ バインディング](../advanced/optimizing-performance-data-binding.md)
- [PropertyPath の XAML 構文](../advanced/propertypath-xaml-syntax.md)
