---
title: 'チュートリアル: デザイナーを使用した、ListView コントロールと TreeView コントロールを含むエクスプローラー スタイルのインターフェイスの作成'
description: デザイナーを使用して Windows フォーム ListView コントロールと TreeView コントロールを含むエクスプローラースタイルのインターフェイスを作成する方法について説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Explorer-style applications [Windows Forms], walkthroughs
- TreeView control [Windows Forms], ListView controls used with
- ListView control [Windows Forms], TreeView controls used with
- Explorer-style applications
- TreeView control [Windows Forms], using for explorer-style interface
- ListView control [Windows Forms], explorer style interface
- ListView control [Windows Forms], explorer-style interface
ms.assetid: 9e5e7721-19e2-4890-b273-a43589fe99ff
ms.openlocfilehash: 44d4db1ef3da85dbf411498f486882b86a05c140
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174628"
---
# <a name="walkthrough-creating-an-explorer-style-interface-with-the-listview-and-treeview-controls-using-the-designer"></a>チュートリアル: デザイナーを使用した、ListView コントロールと TreeView コントロールを含むエクスプローラー スタイルのインターフェイスの作成

Visual Studio の利点の1つは、プロフェッショナルな外観の Windows フォームアプリケーションを短時間で作成できることです。 一般的なシナリオでは、 <xref:System.Windows.Forms.ListView> <xref:System.Windows.Forms.TreeView> windows オペレーティングシステムの windows エクスプローラー機能に似たコントロールとコントロールを使用して、ユーザーインターフェイス (UI) を作成します。 エクスプローラーには、ユーザーのコンピューター上のファイルとフォルダーの階層構造が表示されます。

### <a name="to-create-the-form-containing-a-listview-and-treeview-control"></a>ListView コントロールと TreeView コントロールを含むフォームを作成するには

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. **[新しいプロジェクト]** ダイアログ ボックスで、次の操作を行います。

    1. [カテゴリ] で、[ **Visual Basic** ] または [ **Visual C#**] を選択します。

    2. テンプレートの一覧で、[ **Windows フォームアプリケーション**] を選択します。

3. **[OK]** をクリックします。 新しい Windows フォームプロジェクトが作成されます。

4. <xref:System.Windows.Forms.SplitContainer>フォームにコントロールを追加し、その <xref:System.Windows.Forms.SplitContainer.Dock%2A> プロパティをに設定し <xref:System.Windows.Forms.DockStyle.Fill> ます。

5. <xref:System.Windows.Forms.ImageList>という名前 `imageList1` のをフォームに追加し、プロパティウィンドウを使用して2つのイメージ (フォルダーイメージとドキュメントイメージ) をこの順序で追加します。

6. <xref:System.Windows.Forms.TreeView>という名前のコントロールを `treeview1` フォームに追加し、コントロールの左側に配置し <xref:System.Windows.Forms.SplitContainer> ます。 のプロパティウィンドウで、 `treeView1` 次の操作を行います。

    1. <xref:System.Windows.Forms.Control.Dock%2A> プロパティを <xref:System.Windows.Forms.DockStyle.Fill>に設定します。

    2. <xref:System.Windows.Forms.TreeView.ImageList%2A> プロパティを `imagelist1.` に設定します。

7. <xref:System.Windows.Forms.ListView>という名前のコントロールを `listView1` フォームに追加し、コントロールの右側に配置し <xref:System.Windows.Forms.SplitContainer> ます。 のプロパティウィンドウで、 `listview1` 次の操作を行います。

    1. <xref:System.Windows.Forms.Control.Dock%2A> プロパティを <xref:System.Windows.Forms.DockStyle.Fill>に設定します。

    2. <xref:System.Windows.Forms.ListView.View%2A> プロパティを <xref:System.Windows.Forms.View.Details>に設定します。

    3. [] プロパティの省略記号 ( ![ 省略記号ボタン ([...] プロパティウィンドウ) をクリックして、ColumnHeader コレクションエディターを ](./media/visual-studio-ellipsis-button.png) <xref:System.Windows.Forms.ListView.Columns%2A> **開きます**。 3つの列を追加し、 <xref:System.Windows.Forms.ColumnHeader.Text%2A> それぞれのプロパティを、、およびにそれぞれ設定し `Name` `Type` `Last Modified` ます。 **[OK]** をクリックしてダイアログ ボックスを閉じます。

    4. <xref:System.Windows.Forms.ListView.SmallImageList%2A> プロパティを `imageList1.` に設定します。

8. ノードとサブノードをに設定するコードを実装し <xref:System.Windows.Forms.TreeView> ます。 `Form1` クラスに次のコードを追加します。

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#1)]

9. 前のコードでは System.IO 名前空間を使用しているため、フォームの先頭に適切な using ステートメントまたは import ステートメントを追加します。

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#4)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#4)]

10. フォームのコンストラクターまたはイベント処理メソッドで、前の手順の設定メソッドを呼び出し <xref:System.Windows.Forms.Form.Load> ます。 このコードをフォームコンストラクターに追加します。

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#2)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#2)]

11. <xref:System.Windows.Forms.TreeView.NodeMouseClick>のイベントを処理 `treeview1` **,** し、 `listview1` ノードがクリックされたときにノードの内容を設定するコードを実装します。 `Form1` クラスに次のコードを追加します。

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#3)]
     [!code-vb[System.Windows.Forms.ExplorerStyleInterface#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/VB/Form1.vb#3)]

     C# を使用する場合は、イベント <xref:System.Windows.Forms.TreeView.NodeMouseClick> 処理メソッドにイベントが関連付けられていることを確認してください。 このコードをフォームコンストラクターに追加します。

     [!code-csharp[System.Windows.Forms.ExplorerStyleInterface#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ExplorerStyleInterface/CS/Form1.cs#5)]

## <a name="testing-the-application"></a>アプリケーションのテスト

フォームをテストして、期待どおりに動作することを確認します。

#### <a name="to-test-the-form"></a>フォームをテストするには

- F5 キーを押してアプリケーションを実行します。

     <xref:System.Windows.Forms.TreeView>左側にプロジェクトディレクトリを表示するコントロールと、右側に3つの列があるコントロールを含む分割フォームが表示され <xref:System.Windows.Forms.ListView> ます。 を走査するには、 <xref:System.Windows.Forms.TreeView> ディレクトリノードを選択し <xref:System.Windows.Forms.ListView> ます。には、選択したディレクトリの内容が設定されます。

## <a name="next-steps"></a>次の手順

このアプリケーションでは、を使用して制御する方法の例を示し <xref:System.Windows.Forms.TreeView> て <xref:System.Windows.Forms.ListView> います。 これらのコントロールの詳細については、次のトピックを参照してください。

- [方法: TreeView コントロールまたは ListView コントロール (Windows フォーム) にカスタム情報を追加する](add-custom-information-to-a-treeview-or-listview-control-wf.md)

- [方法: ListView コントロールに検索機能を追加する](how-to-add-search-capabilities-to-a-listview-control.md)

- [方法: ショートカット メニューを TreeView ノードに追加する](how-to-attach-a-shortcut-menu-to-a-treeview-node.md)

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.TreeView>
- [ListView コントロール](listview-control-windows-forms.md)
- [方法: Windows フォーム TreeView コントロールでノードを追加および削除する](how-to-add-and-remove-nodes-with-the-windows-forms-treeview-control.md)
- [方法: Windows フォーム ListView コントロールで項目を追加および削除する](how-to-add-and-remove-items-with-the-windows-forms-listview-control.md)
- [方法: Windows フォーム ListView コントロールに列を追加する](how-to-add-columns-to-the-windows-forms-listview-control.md)
