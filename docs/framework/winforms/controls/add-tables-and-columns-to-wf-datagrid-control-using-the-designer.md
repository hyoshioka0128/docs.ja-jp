---
title: '方法: デザイナーを使って Windows フォーム DataGrid コントロールにテーブルと列を追加する'
ms.date: 03/30/2017
helpviewer_keywords:
- columns [Windows Forms], adding to DataGrid control
- tables [Windows Forms], adding to DataGrid control
- DataGrid control [Windows Forms], adding tables and columns
ms.assetid: 4a6d1b34-b696-476b-bf8a-57c6230aa9e1
ms.openlocfilehash: d11c4f7e4cdfb597477bb99f38612ed648849f20
ms.sourcegitcommit: cf9515122fce716bcfb6618ba366e39b5a2eb81e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69040049"
---
# <a name="how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control-using-the-designer"></a>方法: デザイナーを使って Windows フォーム DataGrid コントロールにテーブルと列を追加する

> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> コントロールは、<xref:System.Windows.Forms.DataGrid> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.DataGrid> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。 詳細については、「[Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)」を参照してください。

<xref:System.Windows.Forms.DataGrid>オブジェクトを作成<xref:System.Windows.Forms.DataGrid> <xref:System.Windows.Forms.GridTableStylesCollection> <xref:System.Windows.Forms.DataGrid.TableStyles%2A>し、コントロールのプロパティを使用してアクセスするオブジェクトに追加することにより、テーブルおよび列の Windows フォームコントロール<xref:System.Windows.Forms.DataGridTableStyle>にデータを表示できます。 各テーブルスタイルには、 <xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A> <xref:System.Windows.Forms.DataGridTableStyle>のプロパティで指定されているデータテーブルの内容が表示されます。 既定では、列スタイルが指定されていないテーブルスタイルでは、そのデータテーブル内のすべての列が表示されます。 にオブジェクトを追加<xref:System.Windows.Forms.DataGridColumnStyle>することで、テーブル内のどの列を表示するかを制限できます。この<xref:System.Windows.Forms.DataGridTableStyle>オブジェクトには、各のプロパティを<xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>通じてアクセスします。 <xref:System.Windows.Forms.GridColumnStylesCollection>

次の手順では、コントロールを<xref:System.Windows.Forms.DataGrid>含むフォームを含む**Windows アプリケーション**プロジェクトが必要です。 このようなプロジェクトを設定する方法については[、「方法:Windows フォームアプリケーションプロジェクト](/visualstudio/ide/step-1-create-a-windows-forms-application-project)を作成し[、次の操作を行います。Windows フォーム](how-to-add-controls-to-windows-forms.md)にコントロールを追加します。 既定では、Visual Studio 2005 <xref:System.Windows.Forms.DataGrid>では、コントロールは**ツールボックス**に含まれていません。 追加の詳細については[、「方法:ツールボックス](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ms165355(v=vs.100))に項目を追加します。

### <a name="to-add-a-table-to-the-datagrid-control-in-the-designer"></a>デザイナーで DataGrid コントロールにテーブルを追加するには

1. テーブルにデータを表示するには、最初に<xref:System.Windows.Forms.DataGrid>コントロールをデータセットにバインドする必要があります。 詳細については、「[方法 :デザイナー](bind-wf-datagrid-control-to-a-data-source-using-the-designer.md)を使用して、データソースに Windows フォーム DataGrid コントロールをバインドします。

2. プロパティウィンドウで<xref:System.Windows.Forms.DataGrid.TableStyles%2A> ![コントロールのプロパティを選択し、プロパティの横にある省略記号ボタン ([...] プロパティウィンドウ) をクリックして、次のように表示します。](./media/visual-studio-ellipsis-button.png) <xref:System.Windows.Forms.DataGrid>**DataGridTableStyle Collection エディター**。

3. コレクションエディターで、 **[追加]** をクリックしてテーブルのスタイルを挿入します。

4. **[OK]** をクリックしてコレクションエディターを閉じ、プロパティの<xref:System.Windows.Forms.DataGrid.TableStyles%2A>横にある省略記号ボタンをクリックして再度開きます。

     コレクションエディターを再度開くと、コントロールにバインドされているすべてのデータテーブルが、テーブルスタイルの<xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A>プロパティのドロップダウンリストに表示されます。

5. コレクションエディターの **[メンバー]** ボックスで、テーブルのスタイルをクリックします。

6. コレクションエディターの **[プロパティ]** ボックスで、表示する<xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A>テーブルの値を選択します。

### <a name="to-add-a-column-to-the-datagrid-control-in-the-designer"></a>デザイナーで DataGrid コントロールに列を追加するには

1. **DataGridTableStyle コレクションエディター**の **[メンバー]** ボックスで、適切なテーブルのスタイルを選択します。 コレクションエディターの **[プロパティ]** ボックスで<xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>コレクションを選択し、![プロパティの横にプロパティウィンドウある省略記号ボタン (省略記号ボタン ([...]) をクリック](./media/visual-studio-ellipsis-button.png)します。**System.windows.forms.datagridcolumnstyle> コレクションエディター**を表示します。

2. コレクションエディターで、 **[追加]** をクリックして列のスタイルを挿入するか、 **[追加]** の横にある下矢印をクリックして列の種類を指定します。

     ドロップダウンボックスで、または<xref:System.Windows.Forms.DataGridTextBoxColumn> <xref:System.Windows.Forms.DataGridBoolColumn>のいずれかの種類を選択できます。

3. [OK] をクリックして**system.windows.forms.datagridcolumnstyle> Collection エディター**を閉じ、プロパティの<xref:System.Windows.Forms.DataGridTableStyle.GridColumnStyles%2A>横にある省略記号ボタンをクリックして再度開きます。

     コレクションエディターを再度開くと、バインドされたデータテーブルのデータ列が、列スタイルの<xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A>プロパティのドロップダウンリストに表示されます。

4. コレクションエディターの **[メンバー]** ボックスで、列のスタイルをクリックします。

5. コレクションエディターの **[プロパティ]** ボックスで、表示する<xref:System.Windows.Forms.DataGridColumnStyle.MappingName%2A>列の値を選択します。

## <a name="see-also"></a>関連項目

- [DataGrid コントロール](datagrid-control-windows-forms.md)
- [方法: Windows フォーム DataGrid コントロールの列を削除または非表示にする](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
