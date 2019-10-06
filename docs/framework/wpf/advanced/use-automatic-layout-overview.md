---
title: 自動レイアウトの使用の概要
ms.date: 03/30/2017
helpviewer_keywords:
- layout [WPF], automatic
- automatic layout [WPF]
ms.assetid: 6fed9264-18bb-4d05-8867-1fe356c6f687
ms.openlocfilehash: 0253c57f080705b648d9f416368d0fe974ac83ab
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834668"
---
# <a name="use-automatic-layout-overview"></a>自動レイアウトの使用の概要

このトピックでは、ローカライズ可能な [!INCLUDE[TLA#tla_ui#plural](../../../../includes/tlasharptla-uisharpplural-md.md)] を使用して [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションを作成する方法に関する開発者向けのガイドラインを紹介します。 以前は、UI のローカライズは時間のかかるプロセスでした。 UI が調整された各言語では、ピクセル単位の調整が必要でした。 現在、適切な設計と適切なコーディング標準を使用して [!INCLUDE[TLA2#tla_ui#plural](../../../../includes/tla2sharptla-uisharpplural-md.md)] を構築できます。これにより、ローカライザーのサイズと位置が小さくなります。 サイズ変更や位置変更が簡単になるアプリケーションを作成する方法は、自動レイアウトと呼ばれ、@no__t 0 アプリケーション設計を使用して実現できます。

<a name="advantages_of_autolayout"></a>

## <a name="advantages-of-using-automatic-layout"></a>自動レイアウトを使用する利点

@No__t 0 のプレゼンテーションシステムは強力で柔軟性があるため、さまざまな言語の要件に合わせて調整できるアプリケーションの要素をレイアウトする機能が用意されています。 次の一覧は、自動レイアウトの利点の一部を示しています。

- UI は任意の言語で表示されます。

- テキストを変換した後に、コントロールの位置とサイズを再調整する必要がなくなります。

- ウィンドウサイズを再調整する必要が少なくなります。

- UI レイアウトは任意の言語で正しくレンダリングされます。

- ローカライズは、文字列変換よりも少ないポイントに縮小することができます。

<a name="autolayout_controls"></a>

## <a name="automatic-layout-and-controls"></a>自動レイアウトとコントロール

自動レイアウトを使用すると、アプリケーションでコントロールのサイズを自動的に調整できます。 たとえば、文字列の長さに合わせてコントロールを変更できます。 この機能により、ローカライザーは文字列を変換できます。翻訳されたテキストに合わせてコントロールのサイズを変更する必要がなくなりました。 次の例では、英語のコンテンツを含むボタンを作成します。

[!code-xaml[LocalizationBtn_snip#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn_snip/CS/Pane1.xaml#1)]

この例では、スペイン語のボタンを作成するために必要なのは、テキストを変更することだけです。 例を次に示します。

[!code-xaml[LocalizationBtn#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationBtn/CS/Pane1.xaml#1)]

次の図は、コードサンプルの出力を示しています。

![テキストの言語が異なる同じボタン](./media/use-automatic-layout-overview/auto-resizable-button.png)

<a name="autolayout_coding"></a>

## <a name="automatic-layout-and-coding-standards"></a>自動レイアウトとコーディング標準

自動レイアウトアプローチを使用するには、完全にローカライズ可能な UI を生成するために、一連のコーディングと設計標準および規則が必要です。 次のガイドラインは、自動レイアウトコーディングを支援するものです。

**絶対位置を使用しない**

- 要素が絶対に配置されるため、<xref:System.Windows.Controls.Canvas> は使用しないでください。

- @No__t-0、<xref:System.Windows.Controls.StackPanel>、<xref:System.Windows.Controls.Grid> を使用して、コントロールを配置します。

さまざまな種類のパネルの詳細については、「[パネルの概要](../controls/panels-overview.md)」を参照してください。

**ウィンドウに固定サイズを設定しない**

- <xref:System.Windows.Window.SizeToContent%2A?displayProperty=nameWithType> を使用してください。 以下に例を示します。

  [!code-xaml[LocalizationGrid#2](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#2)]

**@No__t の追加-1**

- アプリケーションのルート要素に <xref:System.Windows.FrameworkElement.FlowDirection%2A> を追加します。

  WPF は、水平方向、双方向、および垂直方向のレイアウトをサポートするための便利な方法を提供します。 プレゼンテーションフレームワークでは、@no__t 0 プロパティを使用してレイアウトを定義できます。 フロー方向のパターンは次のとおりです。

  - <xref:System.Windows.FlowDirection.LeftToRight?displayProperty=nameWithType> (LrTb)-ラテン、東アジア言語などの横方向レイアウト。

  - <xref:System.Windows.FlowDirection.RightToLeft?displayProperty=nameWithType> (RlTb) —アラビア語、ヘブライ語などの双方向。

**物理フォントの代わりに複合フォントを使用する**

- 複合フォントでは、@no__t 0 のプロパティをローカライズする必要はありません。

- 開発者は、次のいずれかのフォントを使用することも、独自に作成することもできます。

  - グローバルユーザーインターフェイス
  - グローバル San Serif
  - グローバル Serif

**Xml の追加: lang**

- @No__t-0 属性を UI のルート要素に追加します。たとえば、English アプリケーションの場合は、`xml:lang="en-US"` のようになります。

- 複合フォントは `xml:lang` を使用して使用するフォントを決定するため、このプロパティを設定して、多言語シナリオをサポートします。

<a name="autolay_grids"></a>

## <a name="automatic-layout-and-grids"></a>自動レイアウトとグリッド

@No__t 0 要素は、開発者が要素を配置できるようにするため、自動レイアウトに便利です。 @No__t 0 コントロールは、列と行の配置を使用して、子要素間で使用可能な領域を分散できます。 UI 要素は複数のセルにまたがることができ、グリッド内にグリッドを含めることができます。 グリッドを使用すると、複雑な UI を作成して配置することができます。 次の例では、グリッドを使用していくつかのボタンとテキストを配置する方法を示します。 セルの高さと幅が <xref:System.Windows.GridUnitType.Auto>; に設定されていることに注意してください。そのため、イメージを含むボタンを含むセルは、イメージに合わせて調整されます。

[!code-xaml[LocalizationGrid#1](~/samples/snippets/csharp/VS_Snippets_Wpf/LocalizationGrid/CS/Pane1.xaml#1)]

次の図は、前のコードで生成されたグリッドを示しています。

![Grid の例](./media/glob-grid.png "glob_grid") grid

<a name="autolay_grids_issharedsizescope"></a>

## <a name="automatic-layout-and-grids-using-the-issharedsizescope-property"></a>System.windows.controls.grid.issharedsizescope プロパティを使用した自動レイアウトとグリッド

@No__t 0 要素は、ローカライズ可能なアプリケーションで、コンテンツに合わせて調整するコントロールを作成する場合に便利です。 ただし、コンテンツに関係なく、特定のサイズを維持する必要がある場合もあります。 たとえば、"OK"、"キャンセル"、および "参照" ボタンがある場合は、コンテンツに合わせてボタンのサイズを変更しないことをお勧めします。 この場合、<xref:System.Windows.Controls.Grid.IsSharedSizeScope%2A?displayProperty=nameWithType> 添付プロパティは、複数のグリッド要素間で同じサイズ設定を共有する場合に便利です。 次の例では、複数の <xref:System.Windows.Controls.Grid> 要素の間で、列と行のサイズ変更データを共有する方法を示します。

[!code-xaml[gridIssharedsizescopeProp#2](~/samples/snippets/csharp/VS_Snippets_Wpf/gridIssharedsizescopeProp/CSharp/Window1.xaml#2)]

> [!NOTE]
> 完全なコードサンプルについては、「[グリッド間でサイズ変更プロパティを共有](../controls/how-to-share-sizing-properties-between-grids.md)する」を参照してください。

## <a name="see-also"></a>関連項目

- [WPF のグローバリゼーション](globalization-for-wpf.md)
- [自動レイアウトを使用してボタンを作成する](how-to-use-automatic-layout-to-create-a-button.md)
- [自動レイアウト用のグリッドを使用する](how-to-use-a-grid-for-automatic-layout.md)
