---
title: ComboBox または ListBox コントロールをデータにバインドする
description: Windows フォーム ComboBox と ListBox をデータにバインドして、データベース内のデータの参照、新しいデータの入力、既存のデータの編集などのタスクを実行する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data [Windows Forms], binding to controls
- list boxes [Windows Forms], data binding
- ComboBox control [Windows Forms], data binding
- data binding [Windows Forms], combo boxes
- ListBox control [Windows Forms], data binding
- combo boxes [Windows Forms], data binding
- bound controls [Windows Forms], combo boxes
- Windows Forms controls, data binding
- data-bound controls [Windows Forms], Windows Forms
ms.assetid: dfd7f081-8bea-4a41-86a3-86a1934828ef
ms.openlocfilehash: 0c07dc90ddc91061c5f34b5a237082cb444e89d9
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85324067"
---
# <a name="how-to-bind-a-windows-forms-combobox-or-listbox-control-to-data"></a>方法: Windows フォームの ComboBox または ListBox コントロールをデータにバインドする
<xref:System.Windows.Forms.ComboBox>とをデータにバインドすると、 <xref:System.Windows.Forms.ListBox> データベース内のデータの参照、新しいデータの入力、既存のデータの編集などのタスクを実行できます。  
  
### <a name="to-bind-a-combobox-or-listbox-control"></a>ComboBox または ListBox コントロールをバインドするには  
  
1. プロパティを `DataSource` データソースオブジェクトに設定します。 使用できるデータソースには、 <xref:System.Windows.Forms.BindingSource> データへのバインド、データテーブル、データビュー、データセット、データビューマネージャー、配列、またはインターフェイスを実装する任意のクラスが含ま <xref:System.Collections.IList> れます。 詳細については、「 [Windows フォームでサポートされるデータソース](../data-sources-supported-by-windows-forms.md)」を参照してください。  
  
2. テーブルにバインドする場合は、 `DisplayMember` プロパティをデータソース内の列の名前に設定します。  
  
     \- または  
  
     にバインドする場合は <xref:System.Collections.IList> 、表示メンバーをリスト内の型のパブリックプロパティに設定します。  
  
    ```vb  
    Private Sub BindComboBox()  
      ComboBox1.DataSource = DataSet1.Tables("Suppliers")  
      ComboBox1.DisplayMember = "ProductName"  
    End Sub  
    ```  
  
    ```csharp  
    private void BindComboBox()  
    {  
      comboBox1.DataSource = dataSet1.Tables["Suppliers"];  
      comboBox1.DisplayMember = "ProductName";  
    }  
    ```  
  
    > [!NOTE]
    > など、インターフェイスを実装していないデータソースにバインドされている場合、 <xref:System.ComponentModel.IBindingList> <xref:System.Collections.ArrayList> データソースの更新時にバインドされたコントロールのデータは更新されません。 たとえば、にバインドされたコンボボックスがあり、にデータが追加されている場合、 <xref:System.Collections.ArrayList> <xref:System.Collections.ArrayList> これらの新しい項目はコンボボックスに表示されません。 ただし、 <xref:System.Windows.Forms.BindingManagerBase.SuspendBinding%2A> <xref:System.Windows.Forms.BindingManagerBase.ResumeBinding%2A> コントロールがバインドされているクラスのインスタンスでメソッドとメソッドを呼び出すことにより、コンボボックスを強制的に更新でき <xref:System.Windows.Forms.BindingContext> ます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ComboBox>
- <xref:System.Windows.Forms.ListBox>
- [Windows フォームでのデータ バインディング](../windows-forms-data-binding.md)
- [データ連結と Windows フォーム](../data-binding-and-windows-forms.md)
- [オプションのリストを表示するための Windows フォーム コントロール](windows-forms-controls-used-to-list-options.md)
