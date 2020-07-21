---
title: データ グリッド コントロールをデータ ソースにバインドする
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- datasets [Windows Forms], binding to DataGrid control
- data binding [Windows Forms], DataGrid control
- DataGrid control [Windows Forms], data binding
- bound controls [Windows Forms], DataGrid control
- Windows Forms controls, data binding
- bound controls [Windows Forms]
- data-bound controls [Windows Forms], DataGrid
ms.assetid: 128cdb07-dfd3-4d60-9d6a-902847667c36
ms.openlocfilehash: 42514c6a0ab9cf912a32b13675a069976632ece5
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182240"
---
# <a name="how-to-bind-the-windows-forms-datagrid-control-to-a-data-source"></a>方法 : データ ソースに Windows フォーム DataGrid コントロールをバインドする
> [!NOTE]
> <xref:System.Windows.Forms.DataGridView> コントロールは、<xref:System.Windows.Forms.DataGrid> コントロールに代わると共に追加の機能を提供します。ただし、<xref:System.Windows.Forms.DataGrid> コントロールは、下位互換性を保つ目的および将来使用する目的で保持されます。 詳細については、「[Windows フォームの DataGridView コントロールと DataGrid コントロールの違いについて](differences-between-the-windows-forms-datagridview-and-datagrid-controls.md)」を参照してください。  
  
 Windows フォーム<xref:System.Windows.Forms.DataGrid>コントロールは、データ ソースからの情報を表示するように特別に設計されています。 実行時にメソッドを呼び出してコントロールを<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>バインドします。 さまざまなデータ ソースのデータを表示できますが、最も一般的なソースはデータセットとデータ ビューです。  
  
### <a name="to-data-bind-the-datagrid-control-programmatically"></a>プログラムによって DataGrid コントロールをデータバインドするには  
  
1. データセットにデータを格納するコードを記述します。  
  
     データ ソースがデータセット テーブルに基づくデータセットまたはデータ ビューの場合は、データセットにデータを格納するコードをフォームに追加します。  
  
     使用する正確なコードは、データセットがデータを取得する場所によって異なります。 データセットがデータベースから直接設定されている場合は、通常、データアダプタの`Fill`メソッドを呼び出します。 `DsCategories1`  
  
    ```vb  
    sqlDataAdapter1.Fill(DsCategories1)  
    ```  
  
    ```csharp  
    sqlDataAdapter1.Fill(DsCategories1);  
    ```  
  
    ```cpp  
    sqlDataAdapter1->Fill(dsCategories1);  
    ```  
  
     データセットが XML Web サービスから取得される場合は、通常、コード内にサービスのインスタンスを作成し、そのメソッドの 1 つを呼び出してデータセットを返します。 次に、XML Web サービスからローカル データセットにデータセットをマージします。 XML Web サービスのインスタンス`CategoriesService`を作成する方法を次の例に示します。 `GetCategories` `DsCategories1`  
  
    ```vb  
    Dim ws As New MyProject.localhost.CategoriesService()  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials  
    DsCategories1.Merge(ws.GetCategories())  
    ```  
  
    ```csharp  
    MyProject.localhost.CategoriesService ws = new MyProject.localhost.CategoriesService();  
    ws.Credentials = System.Net.CredentialCache.DefaultCredentials;  
    DsCategories1.Merge(ws.GetCategories());  
    ```  
  
    ```cpp  
    MyProject::localhost::CategoriesService^ ws =
       new MyProject::localhost::CategoriesService();  
    ws->Credentials = System::Net::CredentialCache::DefaultCredentials;  
    dsCategories1->Merge(ws->GetCategories());  
    ```  
  
2. コントロールの<xref:System.Windows.Forms.DataGrid><xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>メソッドを呼び出して、データ ソースとデータ メンバーを渡します。 データ メンバーを明示的に渡す必要がない場合は、空の文字列を渡します。  
  
    > [!NOTE]
    > グリッドを初めてバインドする場合は、コントロール<xref:System.Windows.Forms.DataGrid.DataSource%2A>と<xref:System.Windows.Forms.DataGrid.DataMember%2A>プロパティを設定できます。 ただし、いったん設定したプロパティはリセットできません。 したがって、常に<xref:System.Windows.Forms.DataGrid.SetDataBinding%2A>この方法を使用することをお勧めします。  
  
     次の例は、プログラムによって、`DsCustomers1`というデータセットの Customers テーブルにバインドする方法を示しています。  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers")  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "Customers");  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "Customers");  
    ```  
  
     データセット内の唯一のテーブルが Customers テーブルの場合は、グリッドを次の方法でバインドすることもできます。  
  
    ```vb  
    DataGrid1.SetDataBinding(DsCustomers1, "")  
    ```  
  
    ```csharp  
    DataGrid1.SetDataBinding(DsCustomers1, "");  
    ```  
  
    ```cpp  
    dataGrid1->SetDataBinding(dsCustomers1, "");  
    ```  
  
3. (オプション)グリッドに適切な表スタイルと列スタイルを追加します。 表スタイルがない場合は、表が表示されますが、最小限の書式とすべての列が表示されます。  
  
## <a name="see-also"></a>関連項目

- [DataGrid コントロールの概要](datagrid-control-overview-windows-forms.md)
- [方法 : Windows フォーム DataGrid コントロールにテーブルと列を追加する](how-to-add-tables-and-columns-to-the-windows-forms-datagrid-control.md)
- [DataGrid コントロール](datagrid-control-windows-forms.md)
- [Windows フォームでのデータ バインディング](../windows-forms-data-binding.md)
