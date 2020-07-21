---
title: データ グリッド コントロールで実行時に表示されるデータを変更する
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- DataGrid control [Windows Forms], dynamically changing at run time
- DataGrid control [Windows Forms], data binding
- cells [Windows Forms], changing DataGrid cell values
ms.assetid: 0c7a6d00-30de-416e-8223-0a81ddb4c1f8
ms.openlocfilehash: 6b788c10784082a0c74ee09f8cd85d540c670b84
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142382"
---
# <a name="how-to-change-displayed-data-at-run-time-in-the-windows-forms-datagrid-control"></a>方法 : Windows フォーム DataGrid コントロールに表示されるデータを実行時に変更する
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> コントロールは、<xref:System.Windows.Forms.DataGrid> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.DataGrid> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。 詳細については、「[Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)」を参照してください。  
  
 デザイン時機能を使用して<xref:System.Windows.Forms.DataGrid>Windows フォームを作成した後、実行時にグリッドのオブジェクトの要素を<xref:System.Data.DataSet>動的に変更することもできます。 これには、テーブルの個々の値に対する変更や、コントロールにバインドされているデータ ソース<xref:System.Windows.Forms.DataGrid>の変更が含まれます。 個々の値の変更は、コントロール<xref:System.Data.DataSet>ではなくオブジェクトを<xref:System.Windows.Forms.DataGrid>通じて行われます。  
  
### <a name="to-change-data-programmatically"></a>プログラムによってデータを変更するには  
  
1. オブジェクトから目的の<xref:System.Data.DataSet>テーブルを指定し、テーブルから目的の行とフィールドを指定し、セルを新しい値に設定します。  
  
    > [!NOTE]
    > テーブルの最初のテーブル<xref:System.Data.DataSet>またはテーブルの最初の行を指定するには、0 を使用します。  
  
     次の例は、 をクリック`Button1`して、データセットの最初のテーブルの最初の行の 2 番目のエントリを変更する方法を示しています。 <xref:System.Data.DataSet> (`ds`) とテーブル`0` `1`( と ) は以前に作成されています。  
  
    ```vb  
    Protected Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       ds.tables(0).rows(0)(1) = "NewEntry"  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)  
    {  
       ds.Tables[0].Rows[0][1]="NewEntry";  
    }  
    ```  
  
    ```cpp  
    private:
       void button1_Click(System::Object^ sender, System::EventArgs^ e)  
       {  
          dataSet1->Tables[0]->Rows[0][1] = "NewEntry";  
       }  
    ```  
  
     (ビジュアル C#、ビジュアル C++)フォームのコンストラクターに次のコードを配置して、イベント ハンドラーを登録します。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
    ```cpp  
    this->button1->Click +=  
       gcnew System::EventHandler(this, &Form1::button1_Click);  
    ```  
  
     実行時に、このメソッドを<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>使用して、コントロールを<xref:System.Windows.Forms.DataGrid>別のデータ ソースにバインドできます。 たとえば、複数のADO.NETデータ コントロールがあり、それぞれが異なるデータベースに接続されている場合があります。  
  
### <a name="to-change-the-datasource-programmatically"></a>プログラムでデータ ソースを変更するには  
  
1. メソッドを<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>、バインドするデータ ソースとテーブルの名前に設定します。  
  
     次の例は、<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>メソッドを使用して、Pubs データベースの Authors テーブルに接続されているADO.NET データ コントロール (adoPubsAuthors) に日付ソースを変更する方法を示しています。  
  
    ```vb  
    Private Sub ResetSource()  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors")  
    End Sub  
    ```  
  
    ```csharp  
    private void ResetSource()  
    {  
       DataGrid1.SetDataBinding(adoPubsAuthors, "Authors");  
    }  
    ```  
  
    ```cpp  
    private:  
       void ResetSource()  
       {  
          dataGrid1->SetDataBinding(adoPubsAuthors, "Authors");  
       }  
    ```  
  
## <a name="see-also"></a>関連項目

- [ADO.NET データセット](../../data/adonet/ado-net-datasets.md)
- [方法 : Windows フォーム DataGrid コントロールの列を削除するまたは非表示にする](how-to-delete-or-hide-columns-in-the-windows-forms-datagrid-control.md)
- [方法 : Windows フォーム DataGrid コントロールにテーブルと列を追加する](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [方法 : データ ソースに Windows フォーム DataGrid コントロールをバインドする](how-to-bind-the-windows-forms-datagrid-control-to-a-data-source.md)
