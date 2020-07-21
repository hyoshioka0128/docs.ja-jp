---
title: データ グリッド コントロールの書式設定
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- columns [Windows Forms], DataGrid control
- colors [Windows Forms], applying to DataGrid controls
- DataGrid control [Windows Forms], formatting
- columns [Windows Forms], formatting in DataGrid control
- DataGrid control [Windows Forms], default styles
- tables [Windows Forms], formatting in DataGrid control
- formatting [Windows Forms]
ms.assetid: a50fcc3b-8abf-47ec-9029-7f268af4ddb1
ms.openlocfilehash: 180f837c7d60f49af880faefc05da262be061d12
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182148"
---
# <a name="how-to-format-the-windows-forms-datagrid-control"></a>方法 : Windows フォーム DataGrid コントロールの書式を設定する
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> コントロールは、<xref:System.Windows.Forms.DataGrid> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.DataGrid> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。 詳細については、「[Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)」を参照してください。  
  
 コントロールのさまざまな部分に異なる色を<xref:System.Windows.Forms.DataGrid>適用すると、その中の情報を読みやすく、解釈しやすくなります。 行と列に色を適用できます。 行と列は、ユーザーの裁量で非表示にしたり、表示したりすることもできます。  
  
 コントロールの書式設定には、3 つの<xref:System.Windows.Forms.DataGrid>基本的な側面があります。 プロパティを設定して、データが表示される既定のスタイルを設定できます。 そのベースから、実行時に特定のテーブルを表示する方法をカスタマイズできます。 最後に、データ グリッドに表示する列、および表示される色やその他の書式設定を変更できます。  
  
 データ グリッドの書式設定の最初の手順として、それ自体のプロパティを<xref:System.Windows.Forms.DataGrid>設定できます。 これらの色と書式の選択肢は、表示されるデータ テーブルと列に応じて変更を加えることができるベースを形成します。  
  
### <a name="to-establish-a-default-style-for-the-datagrid-control"></a>コントロールの既定のスタイルを設定するには  
  
1. 必要に応じて、次のプロパティを設定します。  
  
    |プロパティ|説明|  
    |--------------|-----------------|  
    |<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>|この<xref:System.Windows.Forms.DataGrid.BackColor%2A>プロパティは、グリッドの偶数行の色を定義します。 プロパティを<xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>異なる色に設定すると、他のすべての行がこの新しい色 (行 1、3、5 など) に設定されます。|  
    |<xref:System.Windows.Forms.DataGrid.BackColor%2A>|グリッドの偶数行の背景色 (行 0、2、4、6 など)。|  
    |<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>|プロパティと<xref:System.Windows.Forms.DataGrid.BackColor%2A><xref:System.Windows.Forms.DataGrid.AlternatingBackColor%2A>プロパティによってグリッド内の行の色が決まります<xref:System.Windows.Forms.DataGrid.BackgroundColor%2A>が、グリッドが下にスクロールされたとき、またはグリッドに含まれている行が数行しかない場合にのみ表示される非行領域の色がプロパティによって決まります。|  
    |<xref:System.Windows.Forms.DataGrid.BorderStyle%2A>|グリッドの境界線スタイル (列挙値の<xref:System.Windows.Forms.BorderStyle>1 つ)。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionBackColor%2A>|グリッドのすぐ上に表示される、グリッドのウィンドウ キャプションの背景色。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionFont%2A>|グリッドの上部にあるキャプションのフォント。|  
    |<xref:System.Windows.Forms.DataGrid.CaptionForeColor%2A>|グリッドのウィンドウ キャプションの背景色。|  
    |<xref:System.Windows.Forms.Control.Font%2A>|グリッド内のテキストを表示するために使用するフォント。|  
    |<xref:System.Windows.Forms.DataGrid.ForeColor%2A>|データ グリッドの行のデータによって表示されるフォントの色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineColor%2A>|データ グリッドのグリッド線の色。|  
    |<xref:System.Windows.Forms.DataGrid.GridLineStyle%2A>|グリッドのセルを区切る線のスタイル(<xref:System.Windows.Forms.DataGridLineStyle>列挙値の 1 つ)。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderBackColor%2A>|行ヘッダーと列ヘッダーの背景色。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderFont%2A>|列ヘッダーに使用されるフォント。|  
    |<xref:System.Windows.Forms.DataGrid.HeaderForeColor%2A>|列ヘッダーテキストとプラス/マイナスグリフ (複数の関連テーブルが表示されている場合に行を展開する) を含む、グリッドの列ヘッダーの前景色。|  
    |<xref:System.Windows.Forms.DataGrid.LinkColor%2A>|子テーブルへのリンク、リレーション名など、データ グリッド内のすべてのリンクのテキストの色。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsBackColor%2A>|子テーブルでは、親行の背景色です。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsForeColor%2A>|子テーブルでは、親行の前景色です。|  
    |<xref:System.Windows.Forms.DataGrid.ParentRowsLabelStyle%2A>|列挙体を使用して、テーブル名と列名を親の行に表示するかどうかを<xref:System.Windows.Forms.DataGridParentRowsLabelStyle>決定します。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredColumnWidth%2A>|グリッドの列の既定の幅 (ピクセル単位)。 プロパティを<xref:System.Windows.Forms.DataGrid.DataSource%2A><xref:System.Windows.Forms.DataGrid.DataMember%2A>リセットする前にこのプロパティを設定するか (個別に、<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>またはメソッドを使用して)、プロパティは無効になります。<br /><br /> このプロパティは 0 未満の値に設定できません。|  
    |<xref:System.Windows.Forms.DataGrid.PreferredRowHeight%2A>|グリッド内の行の行の高さ (ピクセル単位)。 プロパティを<xref:System.Windows.Forms.DataGrid.DataSource%2A><xref:System.Windows.Forms.DataGrid.DataMember%2A>リセットする前にこのプロパティを設定するか (個別に、<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>またはメソッドを使用して)、プロパティは無効になります。<br /><br /> このプロパティは 0 未満の値に設定できません。|  
    |<xref:System.Windows.Forms.DataGrid.RowHeaderWidth%2A>|グリッドの行ヘッダーの幅。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionBackColor%2A>|行またはセルが選択されている場合、背景色になります。|  
    |<xref:System.Windows.Forms.DataGrid.SelectionForeColor%2A>|行またはセルが選択されている場合、これは前景色です。|  
  
    > [!NOTE]
    > コントロールの色をカスタマイズする場合は、色の選択が不十分なため(赤や緑など)、コントロールにアクセスできなくなることを覚えておいてください。 この問題を回避するには、[**システム カラー** ] パレットで使用できる色を使用します。  
  
     次の手順では、フォームにデータ<xref:System.Windows.Forms.DataGrid>テーブルにバインドされたコントロールが含まれます。 詳細については、「 [Windows フォーム のデータ グリッド コントロールをデータ ソースにバインドする](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)」を参照してください。  
  
### <a name="to-set-the-table-and-column-style-of-a-data-table-programmatically"></a>データ テーブルのテーブルスタイルと列スタイルをプログラムで設定するには  
  
1. 新しい表スタイルを作成し、そのプロパティを設定します。  
  
2. 列スタイルを作成し、そのプロパティを設定します。  
  
3. 表スタイルの列スタイルコレクションに列スタイルを追加します。  
  
4. データ グリッドのテーブル スタイル コレクションにテーブル スタイルを追加します。  
  
5. 次の例では、新しい<xref:System.Windows.Forms.DataGridTableStyle>インスタンスを作成し、そのプロパティ<xref:System.Windows.Forms.DataGridTableStyle.MappingName%2A>を設定します。  
  
6. **GridColumnStyle**の新しいインスタンスを作成し、その**マッピング名**(およびその他のレイアウトと表示プロパティ) を設定します。  
  
7. 作成する列スタイルごとに、手順 2 から 6 を繰り返します。  
  
     次の例は、 の<xref:System.Windows.Forms.DataGridTextBoxColumn>列に名前が表示されるため、a が作成される方法を示しています。 さらに、列スタイルをテーブル スタイルの<xref:System.Windows.Forms.GridColumnStylesCollection>に追加し、データ グリッドの に<xref:System.Windows.Forms.GridTableStylesCollection>テーブル スタイルを追加します。  
  
    ```vb  
    Private Sub CreateAuthorFirstNameColumn()  
       ' Add a GridTableStyle and set the MappingName
       ' to the name of the DataTable.  
       Dim TSAuthors As New DataGridTableStyle()  
       TSAuthors.MappingName = "Authors"  
  
       ' Add a GridColumnStyle and set the MappingName
       ' to the name of a DataColumn in the DataTable.
       ' Set the HeaderText and Width properties.
       Dim TCFirstName As New DataGridTextBoxColumn()  
       TCFirstName.MappingName = "AV_FName"  
       TCFirstName.HeaderText = "First Name"  
       TCFirstName.Width = 75  
       TSAuthors.GridColumnStyles.Add(TCFirstName)  
  
       ' Add the DataGridTableStyle instance to
       ' the GridTableStylesCollection.
       myDataGrid.TableStyles.Add(TSAuthors)  
    End Sub  
    ```  
  
    ```csharp  
    private void addCustomDataTableStyle()  
    {  
       // Add a GridTableStyle and set the MappingName
       // to the name of the DataTable.  
       DataGridTableStyle TSAuthors = new DataGridTableStyle();  
       TSAuthors.MappingName = "Authors";  
  
       // Add a GridColumnStyle and set the MappingName
       // to the name of a DataColumn in the DataTable.
       // Set the HeaderText and Width properties.
       DataGridColumnStyle TCFirstName = new DataGridTextBoxColumn();  
       TCFirstName.MappingName = " AV_FName";  
       TCFirstName.HeaderText = "First Name";  
       TCFirstName.Width = 75;  
       TSAuthors.GridColumnStyles.Add(TCFirstName);  
  
       // Add the DataGridTableStyle instance to
       // the GridTableStylesCollection.
       dataGrid1.TableStyles.Add(TSAuthors);  
    }  
    ```  
  
    ```cpp  
    private:  
       void addCustomDataTableStyle()  
       {  
          // Add a GridTableStyle and set the MappingName
          // to the name of the DataTable.  
          DataGridTableStyle^ TSAuthors = new DataGridTableStyle();  
          TSAuthors->MappingName = "Authors";  
  
          // Add a GridColumnStyle and set the MappingName
          // to the name of a DataColumn in the DataTable.
          // Set the HeaderText and Width properties.
          DataGridColumnStyle^ TCFirstName = gcnew DataGridTextBoxColumn();  
          TCFirstName->MappingName = "AV_FName";  
          TCFirstName->HeaderText = "First Name";  
          TCFirstName->Width = 75;  
          TSAuthors->GridColumnStyles->Add(TCFirstName);  
  
          // Add the DataGridTableStyle instance to
          // the GridTableStylesCollection.
          dataGrid1->TableStyles->Add(TSAuthors);  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.GridTableStylesCollection>
- <xref:System.Windows.Forms.GridColumnStylesCollection>
- <xref:System.Windows.Forms.DataGrid>
- [方法 : Windows フォーム DataGrid コントロールの列を削除するまたは非表示にする](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [DataGrid コントロール](datagrid-control-windows-forms.md)
