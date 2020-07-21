---
title: BindingNavigator コントロールに [Load]、[Save]、[Cancel] の各ボタンを追加する
description: Windows フォーム BindingNavigator コントロールに [Load]、[Save]、[Cancel] の各ボタンを追加する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], manipulating
- BindingNavigator control [Windows Forms], adding buttons
ms.assetid: faa33042-186e-4bb2-8798-17ceb987ec62
ms.openlocfilehash: d4db91b8cfaf2df253d0c4cf5d8a66e9157d4986
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86173420"
---
# <a name="how-to-add-load-save-and-cancel-buttons-to-the-windows-forms-bindingnavigator-control"></a>方法: Windows フォーム BindingNavigator コントロールに [Load]、[Save]、[Cancel] の各ボタンを追加する

コントロールは、 <xref:System.Windows.Forms.BindingNavigator> <xref:System.Windows.Forms.ToolStrip> データにバインドされているフォーム上のコントロールを移動および操作するための特殊な用途のコントロールです。

コントロールであるため、コンポーネントを簡単に変更して、 <xref:System.Windows.Forms.ToolStrip> <xref:System.Windows.Forms.BindingNavigator> ユーザーの追加または別のコマンドを含めることができます。

次の手順では、 <xref:System.Windows.Forms.TextBox> コントロールがデータにバインドされ、 <xref:System.Windows.Forms.ToolStrip> フォームに追加されたコントロールが、[読み込み]、[保存]、および [キャンセル] の各ボタンを含むように変更されます。

## <a name="add-load-save-and-cancel-buttons-to-the-bindingnavigator-component"></a>[Load]、[save]、[cancel] の各ボタンを BindingNavigator コンポーネントに追加します。

1. Visual Studio で、 <xref:System.Windows.Forms.TextBox> フォームにコントロールを追加します。

2. <xref:System.Windows.Forms.BindingSource>データソースにバインドされているにバインドします。 この例では、 <xref:System.Windows.Forms.BindingSource> がデータベースにバインドされています。

3. データセットとテーブルアダプターが生成されたら、 <xref:System.Windows.Forms.BindingNavigator> コントロールをフォームにドラッグします。

4. コントロール <xref:System.Windows.Forms.BindingNavigator> のプロパティを <xref:System.Windows.Forms.BindingNavigator.BindingSource%2A> 、 <xref:System.Windows.Forms.BindingSource> コントロールにバインドされているフォーム上のに設定します。

5. <xref:System.Windows.Forms.BindingNavigator> コントロールを選択します。

6. [デザイナーアクション] グリフ ( ![ 小さい黒い矢印) をクリックして [ ](./media/designer-actions-glyph.gif) **BindingNavigator タスク**] ダイアログを表示し、[**アイテムの編集**] を選択します。

     **項目コレクションエディター**が表示されます。

7. **Items コレクションエディター**で、次の手順を実行します。

    1. <xref:System.Windows.Forms.ToolStripSeparator> <xref:System.Windows.Forms.ToolStripButton> 適切な種類のを選択 <xref:System.Windows.Forms.ToolStripItem> し、[**追加**] ボタンをクリックして、3つの項目を追加します。

    2. <xref:System.Windows.Forms.ToolStripItem.Name%2A>ボタンのプロパティを**loadbutton**、 **Savebutton**、および**cancelbutton**にそれぞれ設定します。

    3. [ <xref:System.Windows.Forms.ToolStripItem.Text%2A> **読み込み**]、[**保存**]、 **[キャンセル]** の各ボタンのプロパティを設定します。

    4. <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A>各ボタンのプロパティを [**テキスト**] に設定します。 または、このプロパティを**image**または**imageandtext**に設定し、プロパティに表示されるようにイメージを設定することもでき <xref:System.Windows.Forms.ToolStripItem.Image%2A> ます。

    5. **[OK]** をクリックしてダイアログ ボックスを閉じます。 ボタンがに追加され <xref:System.Windows.Forms.ToolStrip> ます。

8. フォームを右クリックし、[**コードの表示**] を選択します。

9. コードエディターで、テーブルアダプターにデータを読み込むコード行を見つけます。 このコードは、手順 2. でデータバインディングを設定したときに生成されました。 コードは次のようになり `TableAdapterName.Fill(DataSetName.TableName)` ます。 通常、フォームのイベントに含まれ <xref:System.Windows.Forms.Form.Load> ます。

10. 前に作成した読み込みのイベントのイベントハンドラーを作成 <xref:System.Windows.Forms.ToolStripItem.Click> し、 **Load** <xref:System.Windows.Forms.ToolStripButton> このデータ読み込みコードをそのイベントに移動します。

     これで、コードは次のようになります。

    ```vb
    Private Sub LoadButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles LoadButton.Click
        TableAdapterName.Fill(DataSetName.TableName)
    End Sub
    ```

    ```csharp
    private void LoadButton_Click(System.Object sender,
        System.EventArgs e)
    {
        TableAdapterName.Fill(DataSetName.TableName);
    }
    ```

11. 前の手順で作成した保存のイベントのイベントハンドラーを作成 <xref:System.Windows.Forms.ToolStripItem.Click> **Save** <xref:System.Windows.Forms.ToolStripButton> し、コントロールがバインドされているテーブル内のデータを更新するコードを記述します。

    ```vb
    Private Sub SaveButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles SaveButton.Click
        TableAdapterName.Update(DataSetName.TableName)
    End Sub
    ```

    ```csharp
    private void SaveButton_Click(System.Object sender,
        System.EventArgs e)
    {
        TableAdapterName.Update(DataSetName.TableName);
    }
    ```

    > [!NOTE]
    > 場合によっては、コンポーネントに [保存] ボタンが既に存在してい <xref:System.Windows.Forms.BindingNavigator> ても、Windows フォームデザイナーによってコードが生成されていないことがあります。 **Save** この場合は、 <xref:System.Windows.Forms.ToolStripItem.Click> 上にまったく新しいボタンを作成するのではなく、そのボタンのイベントハンドラーに上記のコードを配置でき <xref:System.Windows.Forms.ToolStrip> ます。 ただし、ボタンは既定で無効になっているので、ボタンのプロパティをに設定して、 <xref:System.Windows.Forms.ToolBarButton.Enabled%2A> ボタンが正しく機能するようにする必要があり `true` ます。

12. 前に作成したキャンセルのイベントのイベントハンドラーを作成 <xref:System.Windows.Forms.ToolStripItem.Click> **Cancel** <xref:System.Windows.Forms.ToolStripButton> し、表示されるデータレコードに対する変更を取り消すコードを記述します。

    ```vb
    Private Sub CancelButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles CancelButton.Click
        BindingSourceName.CancelEdit()
    End Sub
    ```

    ```csharp
    private void CancelButton_Click(System.Object sender, System.EventArgs e)
    {
        BindingSourceName.CancelEdit();
    }
    ```

    > [!NOTE]
    > <xref:System.Windows.Forms.BindingSource.CancelEdit%2A>メソッドのスコープは、データの行です。 次のレコードに移動する前に、個々のレコードを表示しているときに行ったすべての変更を保存します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.BindingNavigator>
- <xref:System.Windows.Forms.BindingSource>
- <xref:System.Windows.Forms.ToolStrip>
- [BindingNavigator コントロール](bindingnavigator-control-windows-forms.md)
- [BindingSource コンポーネントの概要](bindingsource-component-overview.md)
