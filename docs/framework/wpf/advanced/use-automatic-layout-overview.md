---
title: 自動レイアウトの使用の概要
ms.date: 03/30/2017
helpviewer_keywords:
- layout [WPF], automatic
- automatic layout [WPF]
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
ms.openlocfilehash: 2fe473da3eeabef3852e3003e61b3b9604332855
ms.sourcegitcommit: 9c3a4f2d3babca8919a1e490a159c1500ba7a844
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72291270"
---
# <a name="use-automatic-layout-overview"></a>自動レイアウトの使用の概要

このトピックでは、ローカライズ可能なユーザー インターフェイス (UI) を使用して [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションを記述する方法について、開発者向けのガイドラインを紹介します。 以前は、UI のローカライズは時間のかかるプロセスでした。 UI の適応対象の言語ごとに、ピクセル単位での調整が必要でした。 現在では、適切な設計と適切なコーディング標準を使用することで、ローカライザーが行うサイズ変更や位置変更が少なくて済むように、UI を構築できます。 サイズ変更や位置変更が簡単になるアプリケーションの作成方法は自動レイアウトと呼ばれ、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のアプリケーション設計を使用して実現できます。

<a name="advantages_of_autolayout"></a>

## <a name="advantages-of-using-automatic-layout"></a>自動レイアウトを使用する利点

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のプレゼンテーション システムは強力かつ柔軟であるため、さまざまな言語の要件に合わせてアプリケーションの要素のレイアウトを調整できます。 次の一覧では、自動レイアウトの利点の一部を示します。

- どのような言語でも UI が適切に表示されます。

- テキストを翻訳した後で、コントロールの位置とサイズを再調整する必要が減ります。

- ウィンドウ サイズを再調整する必要が少なくなります。

- どのような言語でも UI のレイアウトが正しくレンダリングされます。

- ローカライズの作業を、ほとんど文字列の翻訳にまで減らすことができます。

<a name="autolayout_controls"></a>

## <a name="automatic-layout-and-controls"></a>自動レイアウトとコントロール

自動レイアウトを使用すると、アプリケーションでコントロールのサイズを自動的に調整できます。 たとえば、文字列の長さに合わせてコントロールを変更できます。 この機能を使用して、ローカライザーは文字列を翻訳できます。翻訳されたテキストに合わせてコントロールのサイズを変更する必要はなくなります。 次の例では、内容が英語のボタンを作成します。

[!code-xaml[LocalizationBtn_snip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]

この例では、スペイン語のボタンを作成するために必要なのは、テキストを変更することだけです。 たとえば、オブジェクトに適用された

[!code-xaml[LocalizationBtn#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]

次の図は、コード サンプルの出力を示しています。

![テキストの言語が異なる同じボタン](./media/use-automatic-layout-overview/auto-resizable-button.png)

<a name="autolayout_coding"></a>

## <a name="automatic-layout-and-coding-standards"></a>自動レイアウトとコーディング標準

自動レイアウト アプローチを使用するには、完全にローカライズ可能な UI を生成するために、一連のコーディングと設計の標準および規則が必要です。 次のガイドラインは、自動レイアウトのコーディングに役立ちます。

**絶対位置を使用しない**

- 要素が絶対的に配置されるため、<xref:System.Windows.Controls.Canvas> は使用しないようにします。

- コントロールを配置するには、<xref:System.Windows.Controls.DockPanel>、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.Grid> を使用します。

さまざまな種類のパネルの詳細については、「[パネルの概要](../controls/panels-overview.md)」を参照してください。

**ウィンドウに固定サイズを設定しない**

- <xref:System.Windows.Window.SizeToContent%2A?displayProperty=nameWithType> を使用してください。 次に例を示します。

  [!code-xaml[LocalizationGrid#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]

**<xref:System.Windows.FrameworkElement.FlowDirection%2A> を追加する**

- アプリケーションのルート要素に <xref:System.Windows.FrameworkElement.FlowDirection%2A> を追加します。

  WPF では便利な方法で横書きレイアウト、双方向レイアウト、縦書きレイアウトを作成できます。 プレゼンテーション フレームワークでは、<xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティを使用してレイアウトを定義できます。 フローの方向パターンは次のとおりです。

  - <xref:System.Windows.FlowDirection.LeftToRight?displayProperty=nameWithType> (LrTb) — ラテン語や東アジア言語などのための横書きレイアウト。

  - <xref:System.Windows.FlowDirection.RightToLeft?displayProperty=nameWithType> (RlTb) — アラビア語やヘブライ語などのための双方向レイアウト。

**物理フォントの代わりに複合フォントを使用する**

- 複合フォントを使用すると、<xref:System.Windows.Controls.Control.FontFamily%2A> プロパティをローカライズする必要がありません。

- 開発者は、次のいずれかのフォントを使用することも、独自に作成することもできます。

  - Global User Interface
  - Global San Serif
  - Global Serif

**xml:lang を追加する**

- UI のルート要素に `xml:lang` 属性を追加します (英語アプリケーションの `xml:lang="en-US"` など)。

- 複合フォントでは `xml:lang` により使用するフォントが決定されるため、このプロパティを設定すると、多言語のシナリオがサポートされます。

<a name="autolay_grids"></a>

## <a name="automatic-layout-and-grids"></a>自動レイアウトとグリッド

<xref:System.Windows.Controls.Grid> 要素は、開発者が要素を配置できるようになるため、自動レイアウトに便利です。 <xref:System.Windows.Controls.Grid> コントロールでは、列と行の配置を使用して、使用可能なスペースを子要素間に分散できます。 UI 要素は複数のセルにまたがることができ、グリッド内にグリッドを作成することができます。 グリッドを使用すると、複雑な UI を作成して配置することができます。 次の例では、グリッドを使用してボタンとテキストを配置しています。 セルの高さと幅は <xref:System.Windows.GridUnitType.Auto> に設定されているため、イメージ付きのボタンを含むセルは、イメージに合わせて調整されることに注目してください。

[!code-xaml[LocalizationGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]

次の図では、前のコードによって生成されるグリッドを示します。

![グリッドの例](./media/glob-grid.png "glob_grid") グリッド

<a name="autolay_grids_issharedsizescope"></a>

## <a name="automatic-layout-and-grids-using-the-issharedsizescope-property"></a>IsSharedSizeScope プロパティを使用した自動レイアウトとグリッド

<xref:System.Windows.Controls.Grid> 要素は、ローカライズ可能なアプリケーションで、コンテンツに合わせて調整されるコントロールを作成する場合に便利です。 ただし、コンテンツに関係なく、コントロールを特定のサイズに維持することが必要な場合もあります。 たとえば、"OK"、"キャンセル"、"参照" ボタンがある場合は、おそらく、コンテンツに合わせてボタンのサイズが変更されないようにします。 このような場合は、<xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=nameWithType> 添付プロパティを使用して、複数のグリッド要素間で同じサイズ設定を共有するのが便利です。 次の例では、複数の <xref:System.Windows.Controls.Grid> 要素の間で、列と行のサイズ設定データを共有する方法を示します。

[!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]

> [!NOTE]
> 完全なコード サンプルについては、「[グリッド間でサイズ設定プロパティを共有する](../controls/how-to-share-sizing-properties-between-grids.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [WPF のグローバリゼーション](globalization-for-wpf.md)
- [自動レイアウトを使用してボタンを作成する](how-to-use-automatic-layout-to-create-a-button.md)
- [自動レイアウト用のグリッドを使用する](how-to-use-a-grid-for-automatic-layout.md)
