---
title: '方法: Columns プロパティによってテーブルの列を操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- documents [WPF], manipulating table columns
- properties [WPF], Columns [WPF], manipulating table columns
- tables [WPF], manipulating columns
- Columns property [WPF]
ms.assetid: 3f8884f4-7e1f-456b-be06-fbd3cf469bf3
ms.openlocfilehash: 18a26c76688ebf668293cb1254404d6d2cf15208
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913590"
---
# <a name="how-to-manipulate-a-tables-columns-through-the-columns-property"></a>方法: Columns プロパティによってテーブルの列を操作する
この例では、<xref:System.Windows.Documents.Table.Columns%2A> プロパティを使用して、テーブルの列に対して実行できる一般的な操作をいくつか示します。  
  
## <a name="example"></a>例  
 次の例では、新しいテーブルを作成し、<xref:System.Windows.Documents.TableColumnCollection.Add%2A> メソッドを使用して、テーブルの <xref:System.Windows.Documents.Table.Columns%2A> コレクションに列を追加します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Add](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_add)]
 [!code-vb[TableSnippets2#_Table_Columns_Add](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_add)]  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.TableColumn> を挿入します。  新しい列がインデックス位置 0 に挿入され、テーブル内の新しい最初の列になります。  
  
> [!NOTE]
> <xref:System.Windows.Documents.TableColumnCollection> コレクションでは、0 から始まる標準インデックス作成を使用します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Insert](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_insert)]
 [!code-vb[TableSnippets2#_Table_Columns_Insert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_insert)]  
  
## <a name="example"></a>例  
 次の例では、インデックスによって特定の列を参照して、<xref:System.Windows.Documents.TableColumnCollection> コレクション内の列にある任意のプロパティにアクセスします。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Manip](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_manip)]
 [!code-vb[TableSnippets2#_Table_Columns_Manip](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_manip)]  
  
## <a name="example"></a>例  
 次の例では、テーブルによって現在ホストされている列の数を取得します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Count](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_count)]
 [!code-vb[TableSnippets2#_Table_Columns_Count](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_count)]  
  
## <a name="example"></a>例  
 次の例では、参照によって特定の列を削除します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_DelRef](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_delref)]
 [!code-vb[TableSnippets2#_Table_Columns_DelRef](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_delref)]  
  
## <a name="example"></a>例  
 次の例では、インデックスによって特定の列を削除します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_DelIndex](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_delindex)]
 [!code-vb[TableSnippets2#_Table_Columns_DelIndex](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_delindex)]  
  
## <a name="example"></a>例  
 次の例では、テーブルの列コレクションからすべての列を削除します。  
  
 [!code-csharp[TableSnippets2#_Table_Columns_Clear](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_columns_clear)]
 [!code-vb[TableSnippets2#_Table_Columns_Clear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_columns_clear)]  
  
## <a name="see-also"></a>関連項目

- [テーブルの概要](table-overview.md)
- [XAML を使用してテーブルを定義する](how-to-define-a-table-with-xaml.md)
- [プログラムによってテーブルをビルドする](how-to-build-a-table-programmatically.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Blocks プロパティを介して FlowDocument を操作する](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [RowGroups プロパティを介してテーブルの行グループを操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
