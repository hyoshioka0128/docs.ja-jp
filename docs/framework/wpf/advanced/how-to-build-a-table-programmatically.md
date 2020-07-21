---
title: '方法: プログラムによってテーブルをビルドする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tables [WPF], creating programmatically
ms.assetid: e3ca88f3-6e94-4b61-82fc-42104c10b761
ms.openlocfilehash: 9c9061d3c4d6b3de5e1ab42a6b98c20813835ba8
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69964157"
---
# <a name="how-to-build-a-table-programmatically"></a>方法: プログラムによってテーブルをビルドする
次の例は、プログラムで <xref:System.Windows.Documents.Table> を作成して内容を格納する方法を示しています。 テーブルの内容は 5 つの行 (<xref:System.Windows.Documents.Table.RowGroups%2A> オブジェクトに含まれる <xref:System.Windows.Documents.TableRow> オブジェクトにより表される) と 6 つの列 (<xref:System.Windows.Documents.TableColumn> オブジェクトにより表される) に配分されます。 たとえば、タイトル行はテーブル全体のタイトルの設定に使用され、ヘッダー行はテーブル内のデータ列の説明、フッター行は要約情報の格納に使用されます。  "タイトル"、"ヘッダー"、"フッター" 行の概念はテーブルに固有のものではなく、単純に異なる特性を持つ行です。 テーブルのセルには実際の内容が格納されます。テキスト、画像、またはその他のほとんどすべての [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] 要素を格納できます。  
  
## <a name="example"></a>例  
 まず、<xref:System.Windows.Documents.Table> をホストする <xref:System.Windows.Documents.FlowDocument> が作成され、新しい <xref:System.Windows.Documents.Table> が作成され、<xref:System.Windows.Documents.FlowDocument> の内容に追加されます。  
  
 [!code-csharp[TableSnippets#_TableCreate](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreate)]
 [!code-vb[TableSnippets#_TableCreate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreate)]  
  
## <a name="example"></a>例  
 次に、6 つの <xref:System.Windows.Documents.TableColumn> オブジェクトが作成されてテーブルの <xref:System.Windows.Documents.Table.Columns%2A> に追加され、いくつかの書式設定が適用されます。  
  
> [!NOTE]
> テーブルの <xref:System.Windows.Documents.Table.Columns%2A> コレクションでは、0 から始まる標準インデックス作成が使用されることに注意してください。  
  
 [!code-csharp[TableSnippets#_TableCreateColumns](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tablecreatecolumns)]
 [!code-vb[TableSnippets#_TableCreateColumns](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tablecreatecolumns)]  
  
## <a name="example"></a>例  
 次に、タイトル行が作成され、テーブルに追加されます。いくつかの書式設定が適用されます。  タイトル行には、テーブルの 6 つの列にまたがる 1 つのセルが格納されます。  
  
 [!code-csharp[TableSnippets#_TableAddTitleRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddtitlerow)]
 [!code-vb[TableSnippets#_TableAddTitleRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddtitlerow)]  
  
## <a name="example"></a>例  
 次に、ヘッダー行を作成してテーブルに追加し、ヘッダー行のセルを作成してデータを格納します。  
  
 [!code-csharp[TableSnippets#_TableAddHeaderRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddheaderrow)]
 [!code-vb[TableSnippets#_TableAddHeaderRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddheaderrow)]  
  
## <a name="example"></a>例  
 次に、データの行が作成され、テーブルに追加されます。この行のセルが作成され、内容が入力されます。  この行の作成はヘッダー行の作成に似ていますが、適用する書式が少し異なります。  
  
 [!code-csharp[TableSnippets#_TableAddDataRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableadddatarow)]
 [!code-vb[TableSnippets#_TableAddDataRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableadddatarow)]  
  
## <a name="example"></a>例  
 最後に、フッター行が作成され、追加され、書式設定されます。  タイトル行と同様に、フッター行にはテーブルの 6 つの列にまたがる 1 つのセルが格納されます。  
  
 [!code-csharp[TableSnippets#_TableAddFooterRow](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets/CSharp/Table.cs#_tableaddfooterrow)]
 [!code-vb[TableSnippets#_TableAddFooterRow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets/VisualBasic/Table.vb#_tableaddfooterrow)]  
  
## <a name="see-also"></a>関連項目

- [テーブルの概要](table-overview.md)
