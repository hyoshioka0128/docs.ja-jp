---
title: '方法: RowGroups プロパティを介してテーブルの行グループを操作する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- row groups [WPF], manipulating through RowGroups property
- RowGroups property [WPF], manipulating row groups
- documents [WPF], manipulating row groups through RowGroups property
- properties [WPF], RowGroups [WPF], manipulating row groups
ms.assetid: ea61440f-08ae-44ed-b314-5716aaaae3ed
ms.openlocfilehash: 195920af64888bd3671b45befc0fe4cde463ae7b
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69913556"
---
# <a name="how-to-manipulate-a-tables-row-groups-through-the-rowgroups-property"></a>方法: RowGroups プロパティを介してテーブルの行グループを操作する
この例では、<xref:System.Windows.Documents.Table.RowGroups%2A> プロパティを使用して、テーブルの行グループに対して実行できる、より一般的な操作をいくつか示します。  
  
## <a name="example"></a>例  
 次の例では、新しいテーブルを作成し、<xref:System.Windows.Documents.TableRowGroupCollection.Add%2A> メソッドを使用して、テーブルの <xref:System.Windows.Documents.Table.RowGroups%2A> コレクションに列を追加します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Add](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_add)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Add](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_add)]  
  
## <a name="example"></a>例  
 次の例では、新しい <xref:System.Windows.Documents.TableRowGroup> を挿入します。  新しい列がインデックス位置 0 に挿入され、テーブル内の新しい最初の行グループになります。  
  
> [!NOTE]
> <xref:System.Windows.Documents.TableRowGroupCollection> コレクションでは、0 から始まる標準インデックス作成を使用します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Insert](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_insert)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Insert](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_insert)]  
  
## <a name="example"></a>例  
 次の例では、テーブル内の特定の <xref:System.Windows.Documents.TableRowGroup> (インデックスで指定) に複数の行を追加します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_AddRows](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_addrows)]
 [!code-vb[TableSnippets2#_Table_RowGroups_AddRows](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_addrows)]  
  
## <a name="example"></a>例  
 次の例では、テーブル内の最初の行グループの行にある任意のプロパティにアクセスします。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_ManipRows](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_maniprows)]
 [!code-vb[TableSnippets2#_Table_RowGroups_ManipRows](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_maniprows)]  
  
## <a name="example"></a>例  
 次の例では、テーブル内の特定の <xref:System.Windows.Documents.TableRow> (インデックスで指定) に複数のセルを追加します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_AddCells](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_addcells)]
 [!code-vb[TableSnippets2#_Table_RowGroups_AddCells](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_addcells)]  
  
## <a name="example"></a>例  
 次の例では、最初の行グループの最初の行のセルにある任意のメソッドとプロパティにアクセスします。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_ManipCells](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_manipcells)]
 [!code-vb[TableSnippets2#_Table_RowGroups_ManipCells](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_manipcells)]  
  
## <a name="example"></a>例  
 次の例では、テーブルによってホストされる <xref:System.Windows.Documents.TableRowGroup> 要素の数を返します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Count](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_count)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Count](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_count)]  
  
## <a name="example"></a>例  
 次の例では、参照によって特定の行グループを削除します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_DelRef](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_delref)]
 [!code-vb[TableSnippets2#_Table_RowGroups_DelRef](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_delref)]  
  
## <a name="example"></a>例  
 次の例では、インデックスによって特定の行グループを削除します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_DelIndex](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_delindex)]
 [!code-vb[TableSnippets2#_Table_RowGroups_DelIndex](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_delindex)]  
  
## <a name="example"></a>例  
 次の例では、テーブルの行グループ コレクションからすべての行グループを削除します。  
  
 [!code-csharp[TableSnippets2#_Table_RowGroups_Clear](~/samples/snippets/csharp/VS_Snippets_Wpf/TableSnippets2/CSharp/Window1.xaml.cs#_table_rowgroups_clear)]
 [!code-vb[TableSnippets2#_Table_RowGroups_Clear](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TableSnippets2/visualbasic/window1.xaml.vb#_table_rowgroups_clear)]  
  
## <a name="see-also"></a>関連項目

- [方法:Inlines プロパティを介してフロー コンテンツ要素を操作する](how-to-manipulate-table-row-groups-through-the-rowgroups-property.md)
- [Blocks プロパティを介して FlowDocument を操作する](how-to-manipulate-a-flowdocument-through-the-blocks-property.md)
- [Columns プロパティによってテーブルの列を操作する](how-to-manipulate-table-columns-through-the-columns-property.md)
