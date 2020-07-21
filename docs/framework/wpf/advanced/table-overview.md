---
title: テーブルの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- flow content elements [WPF], Table
- documents [WPF], tables
- tables [WPF]
ms.assetid: 5e1105f4-8fc4-473a-ba55-88c8e71386e6
ms.openlocfilehash: 4bd747cea43755116c56b16f1de9a6ffb59935ed
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187269"
---
# <a name="table-overview"></a>テーブルの概要
<xref:System.Windows.Documents.Table> は、フロー ドキュメント コンテンツのグリッド式の表示をサポートする、ブロック レベルの要素です。 この要素は、その柔軟性により非常に便利ですが、正しく理解して使用するのが難しいとも言えます。  
  
 このトピックは、次のセクションで構成されています。  
  
- [テーブルの基本](#table_basics)  
  
- [テーブルとグリッドの相違点](#table_vs_Grid)  
  
- [テーブルの基本構造](#basic_table_structure)  
  
- [テーブルの内容](#table_containment)  
  
- [行グループ](#row_groupings)  
  
- [背景のレンダリングの優先順位](#rendering_precedence)  
  
- [複数の行または列にまたがるセル](#spanning_rows_or_columns)  
  
- [テーブルとコードのバインディング](#building_a_table_with_code)  
  
- 関連トピック
  
<a name="table_basics"></a>
## <a name="table-basics"></a>テーブルの基本  
  
<a name="table_vs_Grid"></a>
### <a name="how-is-table-different-then-grid"></a>テーブルとグリッドの相違点  
 <xref:System.Windows.Documents.Table> と <xref:System.Windows.Controls.Grid> には共通の機能がいくつかありますが、それぞれが最も適している状況は異なります。 <xref:System.Windows.Documents.Table> は、フロー コンテンツ内で使用するために設計されています (フロー コンテンツの詳細については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください)。 グリッドは、フォーム内で最適に使用される (基本的に任意の場所以外のフロー コンテンツ)。 <xref:System.Windows.Documents.FlowDocument> 内の場合、<xref:System.Windows.Documents.Table> では改ページ位置の自動修正、列のリフロー、コンテンツの選択がサポートされますが、<xref:System.Windows.Controls.Grid> ではサポートされません。 一方、<xref:System.Windows.Controls.Grid> は、さまざまな理由から <xref:System.Windows.Documents.FlowDocument> の外で使用するのに適しています。たとえば、<xref:System.Windows.Controls.Grid> では行と列のインデックスに基づいて要素が追加されますが、<xref:System.Windows.Documents.Table> では追加されません。 <xref:System.Windows.Controls.Grid> 要素により、子のコンテンツのレイヤーが可能になり、1 つの "セル" 内に複数の要素を含むことができます。 <xref:System.Windows.Documents.Table> では、レイヤーはサポートされていません。 <xref:System.Windows.Controls.Grid> の子要素は、"セル" 境界の領域に対して絶対位置で配置できます。 <xref:System.Windows.Documents.Table> では、この機能はサポートされていません。 最後に、<xref:System.Windows.Controls.Grid> は <xref:System.Windows.Documents.Table> より必要なリソースの量が少ないため、パフォーマンスを向上させるには <xref:System.Windows.Controls.Grid> の使用をお勧めします。  
  
<a name="basic_table_structure"></a>
### <a name="basic-table-structure"></a>テーブルの基本構造  
 <xref:System.Windows.Documents.Table> では、列 (<xref:System.Windows.Documents.TableColumn> 要素で表されます) と 行 (<xref:System.Windows.Documents.TableRow> 要素で表されます) によって構成されるグリッドベースの表現が提供されます。 <xref:System.Windows.Documents.TableColumn> 要素ではコンテンツをホストされず、単に列と列の特性が定義されます。 <xref:System.Windows.Documents.TableRow> 要素は、テーブルの行のグループ化を定義する <xref:System.Windows.Documents.TableRowGroup> 要素でホストされる必要があります。 テーブルで表示される実際のコンテンツが格納される <xref:System.Windows.Documents.TableCell> 要素は、<xref:System.Windows.Documents.TableRow> 要素でホストする必要があります。 <xref:System.Windows.Documents.TableCell> には、<xref:System.Windows.Documents.Block> から派生した要素しか格納できません。  <xref:System.Windows.Documents.TableCell> に対する有効な子要素は次のとおりです。  
  
- <xref:System.Windows.Documents.BlockUIContainer>  
  
- <xref:System.Windows.Documents.List>  
  
- <xref:System.Windows.Documents.Paragraph>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.Table>  
  
> [!NOTE]
> <xref:System.Windows.Documents.TableCell> 要素では、テキスト コンテンツを直接ホストすることはできません。 <xref:System.Windows.Documents.TableCell> など、フロー コンテンツ要素の格納規則の詳細については、「[フロー ドキュメントの概要](flow-document-overview.md)」を参照してください。  
  
> [!NOTE]
> <xref:System.Windows.Documents.Table> は、<xref:System.Windows.Controls.Grid> 要素と似ていますが、より多くの機能を備えています。そのため、さらに多くのリソースのオーバーヘッドを必要とします。  
  
 次の例では、XAML を使用して単純な 2 × 3 のテーブルを定義しています。  
  
 [!code-xaml[TableSnippets2#_Table_BasicLayout](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_basiclayout)]  
  
 この例の表示結果を次の図に示します。  
  
 ![基本的なテーブルのレンダリング方法を示すスクリーンショット。](./media/table-overview/basic-table-render-example.png)  
  
<a name="table_containment"></a>
### <a name="table-containment"></a>テーブルの内容  
 <xref:System.Windows.Documents.Table> は <xref:System.Windows.Documents.Block> 要素から派生し、<xref:System.Windows.Documents.Block> レベル要素の共通規則に従います。  <xref:System.Windows.Documents.Table> 要素は、次の要素に含めることができます。  
  
- <xref:System.Windows.Documents.FlowDocument>  
  
- <xref:System.Windows.Documents.TableCell>  
  
- <xref:System.Windows.Controls.ListBoxItem>  
  
- <xref:System.Windows.Controls.ListViewItem>  
  
- <xref:System.Windows.Documents.Section>  
  
- <xref:System.Windows.Documents.Floater>  
  
- <xref:System.Windows.Documents.Figure>  
  
<a name="row_groupings"></a>
### <a name="row-groupings"></a>行グループ  
 <xref:System.Windows.Documents.TableRowGroup> 要素を使用すると、テーブル内の行を任意にグループ化できます。この場合、テーブル内のすべての行は行グループに属する必要があります。  多くの場合、行グループ内の行は共通の目的を共有しており、1 つのグループとしてスタイルを設定できます。  一般に、行のグループ化は、テーブルに格納された主要コンテンツから、特別な目的を持つ行 (タイトル行、ヘッダー行、フッター行など) を分離するために使用します。  
  
 次の例では XAML を使用して、スタイルが設定されたヘッダー行とフッター行を使用したテーブルを定義しています。  
  
 [!code-xaml[TableSnippets2#_Table_RowGroups](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_rowgroups)]  
  
 この例の表示結果を次の図に示します。  
  
 ![スクリーンショット: テーブル行グループ](./media/table-rowgroups.png "Table_RowGroups")  
  
<a name="rendering_precedence"></a>
### <a name="background-rendering-precedence"></a>背景のレンダリングの優先順位  
 テーブル要素は、次の順序でレンダリングされます (優先順位の低い項目から高い項目の z オーダー)。 この順序は変更できません。 たとえば、これらの要素には、確立された順序をオーバーライドするための "Z オーダー" プロパティは用意されていません。  
  
1. <xref:System.Windows.Documents.Table>  
  
2. <xref:System.Windows.Documents.TableColumn>  
  
3. <xref:System.Windows.Documents.TableRowGroup>  
  
4. <xref:System.Windows.Documents.TableRow>  
  
5. <xref:System.Windows.Documents.TableCell>  
  
 テーブル内のこれらの各要素に対して背景色を定義する例を次に示します。  
  
 [!code-xaml[TableSnippets2#_Table_ZOrder](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_zorder)]  
  
 次の図は、この例の表示結果 (背景色のみ表示) を示したものです。  
  
 ![スクリーンショット: テーブルの Z オーダー](./media/table-zorder.png "Table_ZOrder")  
  
<a name="spanning_rows_or_columns"></a>
### <a name="spanning-rows-or-columns"></a>複数の行または列にまたがるセル  
 テーブルのセルは、複数の行または列にまたがるように構成することができます。そのためには、それぞれ <xref:System.Windows.Documents.TableCell.RowSpan%2A> 属性または <xref:System.Windows.Documents.TableCell.ColumnSpan%2A> 属性を使用します。  
  
 3 つの列にまたがるセルの例を次に示します。  
  
 [!code-xaml[TableSnippets2#_Table_ColumnSpan](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml#_table_columnspan)]  
  
 この例の表示結果を次の図に示します。  
  
 ![スクリーンショット: 3 つの列すべてにまたがるセル](./media/table-columnspan.png "Table_ColumnSpan")  
  
<a name="building_a_table_with_code"></a>
## <a name="building-a-table-with-code"></a>テーブルとコードのバインディング  
 次の例は、プログラムで <xref:System.Windows.Documents.Table> を作成して内容を格納する方法を示しています。 テーブルの内容は 5 つの行 (<xref:System.Windows.Documents.Table.RowGroups%2A> オブジェクトに含まれる <xref:System.Windows.Documents.TableRow> オブジェクトにより表される) と 6 つの列 (<xref:System.Windows.Documents.TableColumn> オブジェクトにより表される) に配分されます。 たとえば、タイトル行はテーブル全体のタイトルの設定に使用され、ヘッダー行はテーブル内のデータ列の説明、フッター行は要約情報の格納に使用されます。  "タイトル"、"ヘッダー"、"フッター" 行の概念はテーブルに固有のものではなく、単純に異なる特性を持つ行です。 テーブルのセルには実際の内容が格納されます。テキスト、画像、またはその他のほとんどすべての [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 要素を格納できます。  
  
 まず、<xref:System.Windows.Documents.Table> をホストする <xref:System.Windows.Documents.FlowDocument> が作成され、新しい <xref:System.Windows.Documents.Table> が作成され、<xref:System.Windows.Documents.FlowDocument> の内容に追加されます。  
  
 [!code-csharp[TableSnippets#_TableCreate](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
 次に、6 つの <xref:System.Windows.Documents.TableColumn> オブジェクトが作成されてテーブルの <xref:System.Windows.Documents.Table.Columns%2A> に追加され、いくつかの書式設定が適用されます。  
  
> [!NOTE]
> テーブルの <xref:System.Windows.Documents.Table.Columns%2A> コレクションでは、0 から始まる標準インデックス作成が使用されることに注意してください。  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
 次に、タイトル行を作成してテーブルに追加し、書式を適用します。  タイトル行には、テーブルの 6 つの列にまたがる 1 つのセルが格納されます。  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
 次に、ヘッダー行を作成してテーブルに追加し、ヘッダー行のセルを作成してデータを格納します。  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
 次に、データ行を作成してテーブルに追加し、この行のセルを作成してデータを格納します。  この行の作成はヘッダー行の作成に似ていますが、適用する書式が少し異なります。  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
 最後に、フッター行を作成して追加し、書式を設定します。  タイトル行と同様に、フッター行にはテーブルの 6 つの列にまたがる 1 つのセルが格納されます。  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## <a name="see-also"></a>関連項目

- [フロー ドキュメントの概要](flow-document-overview.md)
- [XAML を使用してテーブルを定義する](how-to-define-a-table-with-xaml.md)
- [WPF のドキュメント](documents-in-wpf.md)
- [フロー コンテンツ要素を使用する](how-to-use-flow-content-elements.md)
