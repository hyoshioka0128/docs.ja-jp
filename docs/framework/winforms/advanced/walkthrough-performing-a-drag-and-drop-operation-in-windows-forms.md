---
title: 'チュートリアル: ドラッグアンドドロップ操作の実行'
description: Windows フォームでドラッグアンドドロップ操作を実行する方法について説明します。これには、一連のイベント (特に、DragEnter、System.windows.dragdrop.dragleave>、System.windows.dragdrop.drop> イベント) を処理します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows Forms, drag and drop operations
- drag and drop [Windows Forms], Windows Forms
ms.assetid: eb66f6bf-4a7d-4c2d-b276-40fefb2d3b6c
ms.openlocfilehash: 83bfda875e2fdec3981bbcb8f8f7be00db342440
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325821"
---
# <a name="walkthrough-performing-a-drag-and-drop-operation-in-windows-forms"></a>チュートリアル: Windows フォームにおけるドラッグ アンド ドロップ操作の実行
Windows ベースのアプリケーション内でドラッグアンドドロップ操作を実行するには、一連のイベント (特に、、、およびイベント) を処理する必要があり <xref:System.Windows.Forms.Control.DragEnter> <xref:System.Windows.Forms.Control.DragLeave> <xref:System.Windows.Forms.Control.DragDrop> ます。 これらのイベントのイベント引数で使用できる情報を操作することにより、ドラッグアンドドロップ操作を容易に行うことができます。  
  
## <a name="dragging-data"></a>データのドラッグ  
 ドラッグアンドドロップ操作はすべて、ドラッグで開始されます。 ドラッグの開始時に収集されるデータを有効にする機能は、メソッドで実装され <xref:System.Windows.Forms.Control.DoDragDrop%2A> ます。  
  
 次の例では、 <xref:System.Windows.Forms.Control.MouseDown> イベントを使用してドラッグ操作を開始しています。これは最も直観的です (ドラッグアンドドロップ操作のほとんどは、押されているマウスボタンで開始されます)。 ただし、すべてのイベントを使用してドラッグアンドドロッププロシージャを開始できることに注意してください。  
  
> [!NOTE]
> 特定のコントロールには、ドラッグ固有のカスタムイベントがあります。 <xref:System.Windows.Forms.ListView> <xref:System.Windows.Forms.TreeView> たとえば、コントロールとコントロールには、イベントがあり <xref:System.Windows.Forms.TreeView.ItemDrag> ます。  
  
#### <a name="to-start-a-drag-operation"></a>ドラッグ操作を開始するには  
  
1. ドラッグを開始するコントロールのイベントでは、メソッドを使用して、ドラッグする <xref:System.Windows.Forms.Control.MouseDown> `DoDragDrop` データを設定します。ドラッグすると、ドラッグが許可されます。 詳細については、次のトピックを参照してください。 <xref:System.Windows.Forms.DragEventArgs.Data%2A> および <xref:System.Windows.Forms.DragEventArgs.AllowedEffect%2A>  
  
     次の例は、ドラッグ操作を開始する方法を示しています。 ドラッグが開始するコントロールはコントロール <xref:System.Windows.Forms.Button> で、ドラッグされるデータはコントロールのプロパティを表す文字列であり、許可されて <xref:System.Windows.Forms.Control.Text%2A> <xref:System.Windows.Forms.Button> いる効果はコピーまたは移動のいずれかになります。  
  
    ```vb  
    Private Sub Button1_MouseDown(ByVal sender As Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles Button1.MouseDown  
       Button1.DoDragDrop(Button1.Text, DragDropEffects.Copy Or DragDropEffects.Move)  
    End Sub  
    ```  
  
    ```csharp  
    private void button1_MouseDown(object sender,
    System.Windows.Forms.MouseEventArgs e)  
    {  
       button1.DoDragDrop(button1.Text, DragDropEffects.Copy |
          DragDropEffects.Move);  
    }  
    ```  
  
    > [!NOTE]
    > 任意のデータをメソッドのパラメーターとして使用でき `DoDragDrop` ます。上記の例では、 <xref:System.Windows.Forms.Control.Text%2A> <xref:System.Windows.Forms.Button> プロパティはドラッグ元 (コントロール) に関連付けられていたため、値をハードコーディングしたり、データセットからデータを取得したりする代わりに、コントロールのプロパティが使用されていました。 <xref:System.Windows.Forms.Button> ドラッグアンドドロップ操作を Windows ベースのアプリケーションに組み込むときは、この点に注意してください。  
  
 ドラッグ操作が有効になっている間は、イベントを処理して、 <xref:System.Windows.Forms.Control.QueryContinueDrag> ドラッグ操作を続行するためにシステムの "アクセス許可" を要求します。 このメソッドを処理する場合は、ドラッグ操作に影響を与えるメソッドを呼び出すための適切なポイントでもあります。たとえば、 <xref:System.Windows.Forms.TreeNode> <xref:System.Windows.Forms.TreeView> カーソルがコントロールの上に置かれたときにコントロールのを展開する場合などです。  
  
## <a name="dropping-data"></a>データの削除  
 Windows フォームまたはコントロール上の場所からデータのドラッグを開始した後は、どこかにデータをドロップすることをお勧めします。 カーソルは、データの削除用に正しく構成されているフォームまたはコントロールの領域と交差すると変更されます。 Windows フォームまたはコントロール内の領域は、プロパティを設定 <xref:System.Windows.Forms.Control.AllowDrop%2A> し、イベントおよびイベントを処理することによって、削除されたデータを受け入れることができ <xref:System.Windows.Forms.Control.DragEnter> <xref:System.Windows.Forms.Control.DragDrop> ます。  
  
#### <a name="to-perform-a-drop"></a>削除を実行するには  
  
1. <xref:System.Windows.Forms.Control.AllowDrop%2A>プロパティを true に設定します。  
  
2. ドロップが `DragEnter` 発生するコントロールのイベントで、ドラッグされるデータが許容される型 (この場合は) であることを確認し <xref:System.Windows.Forms.Control.Text%2A> ます。 次に、このコードは、ドロップが列挙体の値に対して発生した場合に発生する効果を設定し <xref:System.Windows.Forms.DragDropEffects> ます。 詳細については、「<xref:System.Windows.Forms.DragEventArgs.Effect%2A>」を参照してください。  
  
    ```vb  
    Private Sub TextBox1_DragEnter(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragEnter  
       If (e.Data.GetDataPresent(DataFormats.Text)) Then  
         e.Effect = DragDropEffects.Copy  
       Else  
         e.Effect = DragDropEffects.None  
       End If  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_DragEnter(object sender,
    System.Windows.Forms.DragEventArgs e)  
    {  
       if (e.Data.GetDataPresent(DataFormats.Text))
          e.Effect = DragDropEffects.Copy;  
       else  
          e.Effect = DragDropEffects.None;  
    }  
    ```  
  
    > [!NOTE]
    > 独自の <xref:System.Windows.Forms.DataFormats> オブジェクトをメソッドのパラメーターとして指定することで、独自のを定義でき <xref:System.Object> <xref:System.Windows.Forms.DataObject.SetData%2A> ます。 これを行うときは、指定されたオブジェクトがシリアル化可能であることを確認してください。 詳細については、「<xref:System.Runtime.Serialization.ISerializable>」を参照してください。  
  
3. ドロップが <xref:System.Windows.Forms.Control.DragDrop> 発生するコントロールのイベントで、メソッドを使用し <xref:System.Windows.Forms.DataObject.GetData%2A> て、ドラッグされているデータを取得します。 詳細については、「<xref:System.Security.Cryptography.Xml.DataObject.Data%2A>」を参照してください。  
  
     次の例では、 <xref:System.Windows.Forms.TextBox> コントロールはドラッグされているコントロールです (ドロップが発生します)。 このコードは、 <xref:System.Windows.Forms.Control.Text%2A> <xref:System.Windows.Forms.TextBox> ドラッグされているデータと同じコントロールのプロパティを設定します。  
  
    ```vb  
    Private Sub TextBox1_DragDrop(ByVal sender As Object, ByVal e As System.Windows.Forms.DragEventArgs) Handles TextBox1.DragDrop  
       TextBox1.Text = e.Data.GetData(DataFormats.Text).ToString  
    End Sub  
    ```  
  
    ```csharp  
    private void textBox1_DragDrop(object sender,
    System.Windows.Forms.DragEventArgs e)  
    {  
       textBox1.Text = e.Data.GetData(DataFormats.Text).ToString();  
    }  
    ```  
  
    > [!NOTE]
    > また、プロパティを操作することもできます <xref:System.Windows.Forms.DragEventArgs.KeyState%2A> 。これにより、ドラッグアンドドロップ操作中に押されたキーに応じて、特定の効果が発生します (たとえば、CTRL キーが押されたときに、ドラッグしたデータをコピーするのは標準です)。  
  
## <a name="see-also"></a>関連項目

- [方法: クリップボードにデータを追加する](how-to-add-data-to-the-clipboard.md)
- [方法: クリップボードからデータを取得する](how-to-retrieve-data-from-the-clipboard.md)
- [ドラッグ アンド ドロップ操作とクリップボードのサポート](drag-and-drop-operations-and-clipboard-support.md)
