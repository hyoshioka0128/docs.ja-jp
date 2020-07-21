---
title: コントロールのスタイルを作成する
description: Windows Presentation Foundation と .NET Core でコントロールのスタイルを作成して参照する方法について説明します。
author: adegeo
ms.author: adegeo
ms.date: 09/12/2019
dev_langs:
- csharp
- vb
ms.openlocfilehash: de186cd6da83ffef8a5cd59df581e88b24bc474d
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325791"
---
# <a name="create-a-style-for-a-control-in-wpf"></a>WPF でコントロールのスタイルを作成する

Windows Presentation Foundation (WPF) を使用すると、独自の再利用可能なスタイルを使用して、既存のコントロールの外観をカスタマイズできます。 スタイルは、アプリ、ウィンドウ、ページにグローバルに適用することも、コントロールに直接適用することもできます。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="create-a-style"></a>スタイルの作成

<xref:System.Windows.Style> は、一連のプロパティ値を 1 つ以上の要素に適用する便利な方法と考えることができます。 <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> から派生する任意の要素 (<xref:System.Windows.Window> や <xref:System.Windows.Controls.Button> など) にスタイルを使用できます。

スタイルを宣言する最も一般的な方法は、XAML ファイルの `Resources` セクションでリソースとして行うというものです。 スタイルはリソースであるため、すべてのリソースに適用されるものと同じスコープ規則に従います。 つまり、スタイルを宣言する場所は、スタイルを適用できる場所に影響するということです。 たとえば、アプリ定義の XAML ファイルのルート要素でスタイルを宣言すると、そのスタイルはアプリ内のどこでも使用できます。

[!code-xaml[AppResources](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/App.xaml#AppResources)]

スタイルをアプリの XAML ファイルのいずれかで宣言すると、そのスタイルはその XAML ファイルでのみ使用できます。 リソースのスコープの規則の詳細については、「[XAML Resources](xaml-resources-define.md)」を参照してください。

[!code-xaml[AppResources](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/WindowSingleResource.xaml#WindowResources)]

スタイルは、スタイルが適用される要素のプロパティを設定する `<Setter>` 子要素で構成されます。 上記の例では、`TargetType` 属性を使用して `TextBlock` の型に適用するようにスタイルが設定されていることに注意してください。 このスタイルは、<xref:System.Windows.Controls.Control.FontSize%2A> を `15` に設定し、<xref:System.Windows.Controls.Control.FontWeight%2A> を `ExtraBold` に設定します。 スタイルが変更するプロパティごとに `<Setter>` を追加します。

## <a name="apply-a-style-implicitly"></a>スタイルを暗黙的に適用する

<xref:System.Windows.Style> は、一連のプロパティ値を複数の要素に適用する便利な方法です。 たとえば、次の <xref:System.Windows.Controls.TextBlock> 要素と、ウィンドウでのその既定の外観について考えてみます。

[!code-xaml[TextBlocks](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window1.xaml#SnippetTextBlocks)]

![スタイル サンプルのスクリーンショット](./media/styles-and-templates-overview/stylingintro-textblocksbefore.png "StylingIntro_TextBlocksBefore")

各 <xref:System.Windows.Controls.TextBlock> 要素に <xref:System.Windows.Controls.Control.FontSize%2A> や <xref:System.Windows.Controls.Control.FontFamily%2A>などのプロパティを直接設定することにより、既定の外観を変更できます。 ただし、<xref:System.Windows.Controls.TextBlock> の要素でいくつかのプロパティを共有する場合は、次に示すように、XAML ファイルの `Resources` セクションに <xref:System.Windows.Style> を作成できます。

[!code-xaml[DefaultTextBlockStyle](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window1.xaml#SnippetDefaultTextBlockStyle)]

スタイルの <xref:System.Windows.Style.TargetType%2A> を <xref:System.Windows.Controls.TextBlock> 型に設定し、`x:Key` 属性を省略すると、そのスタイルにスコープ指定されているすべての <xref:System.Windows.Controls.TextBlock> 要素 (通常、XAML ファイル自体) にスタイルが適用されます。

これにより、<xref:System.Windows.Controls.TextBlock> 要素は次のように表示されます。

![スタイル サンプルのスクリーンショット](./media/styles-and-templates-overview/stylingintro-textblocksbasestyle.png "StylingIntro_TextBlocksBaseStyle")

## <a name="apply-a-style-explicitly"></a>スタイルを明示的に適用する

値が含まれる `x:Key` 属性をスタイルに追加すると、そのスタイルは <xref:System.Windows.Style.TargetType%2A> のすべての要素に暗黙的に適用されなくなります。 スタイルを明示的に参照する要素だけに、スタイルが適用されます。

次に示すのは、前のセクションのスタイルですが、`x:Key` 属性を使用して宣言されています。

[!code-xaml[ExplicitStyleDeclare](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/WindowExplicitStyle.xaml#ExplicitStyleDeclare)]

スタイルを適用するには、次に示すように、[StaticResource markup extension](../../framework/wpf/advanced/staticresource-markup-extension.md) を使用して、要素の <xref:System.Windows.FrameworkElement.Style%2A> プロパティを `x:Key` 値に設定します。

[!code-xaml[ExplicitStyleReference](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/WindowExplicitStyle.xaml#ExplicitStyleReference)]

最初の <xref:System.Windows.Controls.TextBlock> 要素にはスタイルが適用され、2 番目の TextBlock 要素は未変更のままであることに注意してください。 前のセクションの暗黙的なスタイルは、`x:Key` 属性を宣言したスタイルに変更されました。つまり、このスタイルの影響を受ける要素は、スタイルを直接参照したものだけであるということです。

![スタイル サンプルのスクリーンショット](./media/styles-and-templates-overview/create-a-style-explicit-textblock.png "create-a-style-explicit-textblock")

スタイルは明示的または暗黙的に適用されると、シールされて、変更できなくなります。 適用されているスタイルを変更する場合は、新しいスタイルを作成して、既存のスタイルを置き換えてください。 詳細については、<xref:System.Windows.Style.IsSealed%2A> プロパティを参照してください。

カスタム ロジックに基づいて適用するスタイルを選択するオブジェクトを作成できます。 例については、<xref:System.Windows.Controls.StyleSelector> クラスで提供されている例を参照してください。

## <a name="apply-a-style-programmatically"></a>プログラムを使用してスタイルを適用する

プログラムを使用して名前付きスタイルを要素に割り当てるには、リソース コレクションからスタイルを取得し、それを要素の <xref:System.Windows.FrameworkElement.Style%2A> プロパティに割り当てます。 リソース コレクションの項目は <xref:System.Object> 型です。 そのため、取得したスタイルは、`Style` プロパティに割り当てる前に <xref:System.Windows.Style?displayProperty=fullName> にキャストする必要があります。 たとえば、次のコードは、`textblock1` という名前の `TextBlock` のスタイルを、定義されているスタイル `TitleText` に設定します。

[!code-csharp[SetStyleCode](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window2.xaml.cs#SnippetSetStyleCode)]
[!code-vb[SetStyleCode](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/vb/MainWindow.xaml.vb#SnippetSetStyleCode)]

## <a name="extend-a-style"></a>スタイルを拡張する

たとえば、2 つの <xref:System.Windows.Controls.TextBlock> 要素で、<xref:System.Windows.Controls.Control.FontFamily%2A> や中央揃えされた <xref:System.Windows.FrameworkElement.HorizontalAlignment%2A> などのいくつかのプロパティ値を共有する必要がある場合があります。 しかし、同時に、**My Pictures** というテキストにいくつかの追加プロパティを持たせる必要もあります。 次に示すように、これは、最初のスタイルに基づく新しいスタイルを作成することで実現できます。

[!code-xaml[DefaultTextBlockStyleBasedOn](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window2.xaml#SnippetDefaultTextBlockStyleBasedOn)]

[!code-xaml[TextBlocksExplicit](~/samples/snippets/desktop-guide/wpf/styles-and-templates-intro/csharp/Window2.xaml#SnippetTextBlocksExplicit)]

例に示されているように、現在、この `TextBlock` スタイルは中央揃えされており、サイズ `26` の `Comic Sans MS` フォントを使用し、前景色は <xref:System.Windows.Media.LinearGradientBrush> に設定されています。 基本スタイルの <xref:System.Windows.Controls.Control.FontSize%2A> 値がオーバーライドされていることに注意してください。 同じプロパティを指す <xref:System.Windows.Setter> が <xref:System.Windows.Style> に複数ある場合は、最後に宣言された `Setter` が優先されます。

<xref:System.Windows.Controls.TextBlock> 要素が現在どのように表示されるかを次に示します。

![スタイル設定された TextBlock](./media/styles-and-templates-overview/stylingintro-textblocks.png "StylingIntro_TextBlocks")

この `TitleText` スタイルは、`BasedOn="{StaticResource {x:Type TextBlock}}"` で参照される、<xref:System.Windows.Controls.TextBlock> 型に対して作成されているスタイルを拡張します。 スタイルの `x:Key` を使用して `x:Key` を持つスタイルを拡張することもできます。 たとえば、`Header1` という名前のスタイルがあり、そのスタイルを拡張する必要がある場合は、`BasedOn="{StaticResource Header1}"` を使用します。

## <a name="relationship-of-the-targettype-property-and-the-xkey-attribute"></a>TargetType プロパティと X:key 属性の関係

前述のように、スタイルに `x:Key` を割り当てずに <xref:System.Windows.Style.TargetType%2A> プロパティを `TextBlock` に設定すると、すべての <xref:System.Windows.Controls.TextBlock> 要素にそのスタイルが適用されます。 ここでは、`x:Key` は暗黙的に `{x:Type TextBlock}` に設定されます。 これは、`x:Key` 値を `{x:Type TextBlock}` 以外の値に明示的に設定すると、<xref:System.Windows.Style> はすべての `TextBlock` 要素には自動的に適用されないことを意味します。 代わりに、(`x:Key` の値を使用して) スタイルを `TextBlock` 要素に明示的に適用する必要があります。 スタイルがリソース セクションにあり、スタイルに `TargetType` プロパティを設定していない場合は、`x:Key` 属性を設定する必要があります。

`TargetType` プロパティは、`x:Key` の既定値を提供するだけでなく、セッター プロパティが適用される型を指定します。 `TargetType` を指定しない場合は、`Property="ClassName.Property"` の構文を使用して、<xref:System.Windows.Setter> オブジェクト内のプロパティをクラス名で修飾する必要があります。 たとえば、`Property="FontSize"` を設定するのではなく、<xref:System.Windows.Setter.Property%2A> を `"TextBlock.FontSize"` または `"Control.FontSize"` に設定する必要があります。

また、多くの WPF コントロールは、その他の WPF コントロールの組み合わせで構成されていることに注意してください。 型のすべてのコントロールに適用されるスタイルを作成する場合、予期しない結果になる可能性があります。 たとえば、<xref:System.Windows.Window> 内の <xref:System.Windows.Controls.TextBlock> 型を対象とするスタイルを作成すると、`TextBlock` が別のコントロール (<xref:System.Windows.Controls.ListBox>など) の一部であったとしても、ウィンドウ内のすべての `TextBlock` コントロールにそのスタイルが適用されます。

## <a name="see-also"></a>関連項目

<!-- - [Create a style for a control](styles-templates-create-apply-template.md) -->
- [XAML リソースの概要](xaml-resources-define.md)
- [XAML の概要 (WPF と .NET Core)](xaml.md)
