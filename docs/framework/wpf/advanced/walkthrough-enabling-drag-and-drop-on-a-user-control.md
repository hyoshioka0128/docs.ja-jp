---
title: 'チュートリアル: ユーザー コントロールでのドラッグ アンド ドロップの有効化'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthrough [WPF], drag-and-drop
- drag-and-drop [WPF], walkthrough
ms.assetid: cc844419-1a77-4906-95d9-060d79107fc7
ms.openlocfilehash: 172e49c2c255db4d24d2180f919b1305326b5e82
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991809"
---
# <a name="walkthrough-enabling-drag-and-drop-on-a-user-control"></a>チュートリアル: ユーザー コントロールでのドラッグ アンド ドロップの有効化

このチュートリアルでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でドラッグ アンド ドロップのデータ転送 (受信) に参加できるカスタム ユーザー コントロールを作成する方法について説明します。

このチュートリアルでは、円の図形を表すカスタムの WPF <xref:System.Windows.Controls.UserControl> を作成します。 また、ドラッグ アンド ドロップによるデータ転送を有効にする機能をコントロールに実装します。 たとえば、ある円コントロールから別の円コントロールにドラッグすると、塗りつぶし色のデータがソースの円からターゲットの円にコピーされます。 円コントロールから <xref:System.Windows.Controls.TextBox> にドラッグすると、塗りつぶし色の文字列表現が <xref:System.Windows.Controls.TextBox> にコピーされます。 さらに、2 つのパネル コントロールと <xref:System.Windows.Controls.TextBox> を含む小さなアプリケーションを作成して、ドラッグ アンド ドロップ機能をテストします。 ドロップされた円データをパネルで処理できるようにするコードを作成します。これにより、ユーザーはあるパネルの子コレクションから別のパネルに円を移動またはコピーできるようになります。

このチュートリアルでは、次の作業について説明します。

- カスタム ユーザー コントロールを作成する。

- ユーザー コントロールをドラッグ ソースとして有効にする。

- ユーザー コントロールをドラッグ ターゲットとして有効にする。

- ユーザー コントロールからドロップされたデータをパネルで受信できるようにする。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを完了するには Visual Studio が必要です。

## <a name="create-the-application-project"></a>アプリケーション プロジェクトを作成する
 このセクションでは、2 つのパネルと <xref:System.Windows.Controls.TextBox> で構成されるメイン ページを含むアプリケーション インフラストラクチャを作成します。

1. Visual Basic または Visual C# で、`DragDropExample` という名前の WPF アプリケーション プロジェクトを作成します。 詳細については、「[チュートリアル:初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。

2. MainWindow.xaml を開きます。

3. <xref:System.Windows.Controls.Grid> の開始タグと終了タグの間に次のマークアップを追加します。

     このマークアップは、テスト アプリケーションのユーザー インターフェイスを作成します。

     [!code-xaml[DragDropWalkthrough#PanelsStep1XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep1xaml)]

## <a name="add-a-new-user-control-to-the-project"></a>新しいユーザー コントロールをプロジェクトに追加する
 このセクションでは、新しいユーザー コントロールをプロジェクトに追加します。

1. [プロジェクト] メニューで、 **[ユーザー コントロールの追加]** を選択します。

2. **[新しい項目の追加]** ダイアログ ボックスで、名前を `Circle.xaml` に変更し、 **[追加]** をクリックします。

     Circle.xaml とその分離コードがプロジェクトに追加されます。

3. Circle.xaml を開きます。

     このファイルには、ユーザー コントロールのユーザー インターフェイス要素が含まれています。

4. 次のマークアップをルート <xref:System.Windows.Controls.Grid> に追加し、UI として青色の円を含む単純なユーザー コントロールを作成します。

     [!code-xaml[DragDropWalkthrough#EllipseXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#ellipsexaml)]

5. Circle.xaml.cs または Circle.xaml.vb を開きます。

6. C# で、パラメーターなしのコンストラクターの後に次のコードを追加して、コピー コンストラクターを作成します。 Visual Basic で、次のコードを追加して、パラメーターなしのコンストラクターとコピー コンストラクターの両方を作成します。

     ユーザー コントロールをコピーできるようにするために、分離コード ファイルにコピー コンストラクター メソッドを追加します。 単純な円形のユーザー コントロールの場合、ユーザー コントロールの塗りつぶしとサイズのみをコピーします。

     [!code-csharp[DragDropWalkthrough#CopyCtor](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#copyctor)]
     [!code-vb[DragDropWalkthrough#CopyCtor](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#copyctor)]

## <a name="add-the-user-control-to-the-main-window"></a>ユーザー コントロールをメイン ウィンドウに追加する

1. MainWindow.xaml を開きます。

2. <xref:System.Windows.Window> の開始タグで、次の XAML を追加して、現在のアプリケーションへの XML 名前空間参照を作成します。

    ```xaml
    xmlns:local="clr-namespace:DragDropExample"
    ```

3. 最初の <xref:System.Windows.Controls.StackPanel>で、次の XAML を追加して、最初のパネルの円ユーザー コントロールの 2 つのインスタンスを作成します。

     [!code-xaml[DragDropWalkthrough#CirclesXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#circlesxaml)]

     パネルの完全な XAML は、次のようになります。

     [!code-xaml[DragDropWalkthrough#PanelsStep2XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/SnippetWindow.xaml#panelsstep2xaml)]

## <a name="implement-drag-source-events-in-the-user-control"></a>ユーザー コントロールでドラッグ ソース イベントを実装する
 このセクションでは、<xref:System.Windows.UIElement.OnMouseMove%2A> メソッドをオーバーライドして、ドラッグ アンド ドロップ操作を開始します。

 ドラッグが開始されたら (マウス ボタンが押されて、マウスが移動されたら)、<xref:System.Windows.DataObject>に転送されるデータをパッケージ化します。 この場合、円コントロールは、3 つのデータ項目 (塗りつぶし色の文字列表現、高さの double 表現、それ自体のコピー) をパッケージ化します。

### <a name="to-initiate-a-drag-and-drop-operation"></a>ドラッグ アンド ドロップ操作を開始する手順

1. Circle.xaml.cs または Circle.xaml.vb を開きます。

2. 次の <xref:System.Windows.UIElement.OnMouseMove%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.MouseMove> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnMouseMove](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#onmousemove)]
     [!code-vb[DragDropWalkthrough#OnMouseMove](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#onmousemove)]

     この <xref:System.Windows.UIElement.OnMouseMove%2A> オーバーライドは、次のタスクを実行します。

    - マウスの移動中にマウスの左ボタンが押されたかどうかを確認します。

    - 円データを <xref:System.Windows.DataObject> にパッケージ化します。 この場合、円コントロールは、3 つのデータ項目 (塗りつぶし色の文字列表現、高さの double 表現、それ自体のコピー) をパッケージ化します。

    - 静的 <xref:System.Windows.DragDrop.DoDragDrop%2A?displayProperty=nameWithType> メソッドを呼び出して、ドラッグ アンド ドロップ操作を開始します。 次の 3 つのパラメーターを <xref:System.Windows.DragDrop.DoDragDrop%2A> メソッドに渡します。

        - `dragSource` - このコントロールへの参照。

        - `data` - 前のコードで作成された <xref:System.Windows.DataObject>。

        - `allowedEffects` - 許可されたドラッグ アンド ドロップ操作。これは、<xref:System.Windows.DragDropEffects.Copy> または <xref:System.Windows.DragDropEffects.Move> です。

3. **F5** キーを押してアプリケーションをビルドし、実行します。

4. いずれかの円コントロールをクリックしてパネル、もう一方の円、<xref:System.Windows.Controls.TextBox> にドラッグします。 <xref:System.Windows.Controls.TextBox>にドラッグすると、カーソルが変化して移動を示すようになります。

5. 円を <xref:System.Windows.Controls.TextBox>にドラッグしながら、**Ctrl** キーを押します。 カーソルが変化してコピーを示すようになる方法にご注意ください。

6. 円を <xref:System.Windows.Controls.TextBox> にドラッグ アンド ドロップします。 円の塗りつぶし色の文字列表現が <xref:System.Windows.Controls.TextBox> に追加されます。

     ![円の塗りつぶし色の文字列表現](./media/dragdrop-colorstring.png "DragDrop_ColorString")

既定では、カーソルは、ドラッグ アンド ドロップ操作中に変化して、データのドロップによる効果を示します。 <xref:System.Windows.UIElement.GiveFeedback> イベントを処理して、別のカーソルを設定することによって、ユーザーに表示するフィードバックをカスタマイズできます。

## <a name="give-feedback-to-the-user"></a>ユーザーにフィードバックを表示する

1. Circle.xaml.cs または Circle.xaml.vb を開きます。

2. 次の <xref:System.Windows.UIElement.OnGiveFeedback%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.GiveFeedback> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ongivefeedback)]
     [!code-vb[DragDropWalkthrough#OnGiveFeedback](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ongivefeedback)]

     この <xref:System.Windows.UIElement.OnGiveFeedback%2A> オーバーライドは、次のタスクを実行します。

    - ドロップ ターゲットの <xref:System.Windows.UIElement.DragOver> イベント ハンドラーで設定されている <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> 値を確認します。

    - <xref:System.Windows.GiveFeedbackEventArgs.Effects%2A> 値に基づいてカスタム カーソルを設定します。 カーソルは、データのドロップによる効果について視覚的フィードバックをユーザーに表示することを目的としています。

3. **F5** キーを押してアプリケーションをビルドし、実行します。

4. いずれかの円コントロールをパネル、もう一方の円、<xref:System.Windows.Controls.TextBox> にドラッグします。 今度は、カーソルが、<xref:System.Windows.UIElement.OnGiveFeedback%2A> で指定したカスタム カーソルになることにご注意ください。

     ![カスタム カーソルによるドラッグ アンド ドロップ](./media/dragdrop-customcursor.png "DragDrop_CustomCursor")

5. <xref:System.Windows.Controls.TextBox> からテキスト `green` を選択します。

6. テキスト `green` を円コントロールにドラッグします。 既定のカーソルは、ドラッグ アンド ドロップ操作の効果を示すために表示されていることにご注意ください。 フィードバック カーソルは、常にドラッグ ソースによって設定されます。

## <a name="implement-drop-target-events-in-the-user-control"></a>ユーザー コントロールにドロップ ターゲット イベントを実装する
 このセクションでは、ユーザー コントロールがドロップ ターゲットであり、ユーザー コントロールをドロップ ターゲットとして有効にするメソッドをオーバーライドし、ドロップされたデータを処理することを指定します。

### <a name="to-enable-the-user-control-to-be-a-drop-target"></a>ユーザー コントロールをドロップ ターゲットとして有効にする手順

1. Circle.xaml を開きます。

2. <xref:System.Windows.Controls.UserControl> の開始タグで、<xref:System.Windows.UIElement.AllowDrop%2A> プロパティを追加し、それを `true` に設定します。

     [!code-xaml[DragDropWalkthrough#UCTagXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml#uctagxaml)]

<xref:System.Windows.UIElement.AllowDrop%2A> が `true` に設定され、ドラッグ ソースのデータが円ユーザー コントロールにドロップされると、<xref:System.Windows.UIElement.OnDrop%2A> メソッドが呼び出されます。 このメソッドでは、ドロップされたデータを処理し、データを円に適用します。

### <a name="to-process-the-dropped-data"></a>ドロップされたデータを処理する手順

1. Circle.xaml.cs または Circle.xaml.vb を開きます。

2. 次の <xref:System.Windows.UIElement.OnDrop%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.Drop> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondrop)]
     [!code-vb[DragDropWalkthrough#OnDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondrop)]

     この <xref:System.Windows.UIElement.OnDrop%2A> オーバーライドは、次のタスクを実行します。

    - <xref:System.Windows.DataObject.GetDataPresent%2A> メソッドを使用して、ドラッグされたデータに文字列オブジェクトが含まれているかどうかを確認します。

    - 文字列データがある場合、<xref:System.Windows.DataObject.GetData%2A> メソッドを使用して、それを抽出します。

    - <xref:System.Windows.Media.BrushConverter> を使用して、文字列の <xref:System.Windows.Media.Brush> への変換を試みます。

    - 変換が成功した場合、円コントロールの UI を表示する <xref:System.Windows.Shapes.Ellipse> の <xref:System.Windows.Shapes.Shape.Fill%2A> にブラシを適用します。

    - <xref:System.Windows.UIElement.Drop> イベントを処理済みとしてマークします。 このイベントを受信する他の要素に、イベントが円ユーザー コントロールで処理されたことを認識させるために、ドロップ イベントを処理済みとしてマークする必要があります。

3. **F5** キーを押してアプリケーションをビルドし、実行します。

4. <xref:System.Windows.Controls.TextBox> で、テキスト `green` を選択します。

5. そのテキストを円コントロールにドラッグしてドロップします。 円が青色から緑色に変化します。

     ![文字列をブラシに変換する](./media/dragdrop-dropgreentext.png "DragDrop_DropGreenText")

6. <xref:System.Windows.Controls.TextBox> にテキスト `green` を入力します。

7. <xref:System.Windows.Controls.TextBox>で、テキスト `gre` を選択します。

8. それを円コントロールにドラッグしてドロップします。 カーソルが変化して、ドロップが許可されていることを示しますが、円の色は変化していないことに注目してください。これは、`gre` が有効な色ではないためです。

9. 緑色の円コントロールをドラッグして青色の円コントロールにドロップします。 円が青色から緑色に変化します。 表示されるカーソルが、<xref:System.Windows.Controls.TextBox> または円のどちらがドラッグ ソースであるかによって異なることにご注意ください。

要素をドロップ ターゲットとして有効にするために必要な手順は、<xref:System.Windows.UIElement.AllowDrop%2A> プロパティを `true` に設定して、ドロップされたデータを処理することだけです。 しかし、より優れたユーザー エクスペリエンスを提供するには、<xref:System.Windows.UIElement.DragEnter>、<xref:System.Windows.UIElement.DragLeave>、<xref:System.Windows.UIElement.DragOver> の各イベントも処理する必要があります。 これらのイベントでは、データがドロップされる前に、チェックを実行して、ユーザーに追加のフィードバックを表示することができます。

データが円ユーザー コントロールにドラッグされると、コントロールは、ドラッグされているデータを処理できるかどうかをドラッグ ソースに通知する必要があります。 コントロールがデータの処理方法を認識していない場合、ドロップを拒否する必要があります。 このためには、<xref:System.Windows.UIElement.DragOver> イベントを処理して、<xref:System.Windows.DragEventArgs.Effects%2A> プロパティを設定します。

### <a name="to-verify-that-the-data-drop-is-allowed"></a>データのドロップが許可されていることを確認する手順

1. Circle.xaml.cs または Circle.xaml.vb を開きます。

2. 次の <xref:System.Windows.UIElement.OnDragOver%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.DragOver> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragover)]
     [!code-vb[DragDropWalkthrough#OnDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragover)]

     この <xref:System.Windows.UIElement.OnDragOver%2A> オーバーライドは、次のタスクを実行します。

    - <xref:System.Windows.DragEventArgs.Effects%2A> プロパティを <xref:System.Windows.DragDropEffects.None> に設定します。

    - <xref:System.Windows.UIElement.OnDrop%2A> メソッドで実行したチェックと同じチェックを実行して、円ユーザー コントロールがドラッグされたデータを処理できるかどうかを判断します。

    - ユーザー コントロールがデータを処理できる場合、<xref:System.Windows.DragEventArgs.Effects%2A> プロパティを <xref:System.Windows.DragDropEffects.Copy> または <xref:System.Windows.DragDropEffects.Move> に設定します。

3. **F5** キーを押してアプリケーションをビルドし、実行します。

4. <xref:System.Windows.Controls.TextBox>で、テキスト `gre` を選択します。

5. テキストを円コントロールにドラッグします。 今度は、カーソルがドロップを許可しないことを示すように変化することに注目してください。これは、`gre` が有効な色ではないためです。

 さらに、ドロップ操作のプレビューを適用して、ユーザー エクスペリエンスを向上させることができます。 この円ユーザー コントロールの場合、<xref:System.Windows.UIElement.OnDragEnter%2A> メソッドと <xref:System.Windows.UIElement.OnDragLeave%2A> メソッドをオーバーライドします。 データがコントロールにドラッグされると、現在の背景 <xref:System.Windows.Shapes.Shape.Fill%2A> はプレースホルダー変数に保存されます。 次に、文字列がブラシに変換されて、円の UI を表示する <xref:System.Windows.Shapes.Ellipse> に適用されます。 データがドロップされずに円からドラッグされると、元の <xref:System.Windows.Shapes.Shape.Fill%2A> 値が円に再度適用されます。

### <a name="to-preview-the-effects-of-the-drag-and-drop-operation"></a>ドラッグ アンド ドロップ操作の効果をプレビューする手順

1. Circle.xaml.cs または Circle.xaml.vb を開きます。

2. Circle クラスで、`_previousFill` という名前の <xref:System.Windows.Media.Brush> プライベート変数を宣言し、それを `null` に初期化します。

     [!code-csharp[DragDropWalkthrough#Brush](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#brush)]
     [!code-vb[DragDropWalkthrough#Brush](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#brush)]

3. 次の <xref:System.Windows.UIElement.OnDragEnter%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.DragEnter> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnDragEnter](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragenter)]
     [!code-vb[DragDropWalkthrough#OnDragEnter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragenter)]

     この <xref:System.Windows.UIElement.OnDragEnter%2A> オーバーライドは、次のタスクを実行します。

    - <xref:System.Windows.Shapes.Ellipse> の <xref:System.Windows.Shapes.Shape.Fill%2A> プロパティを `_previousFill` 変数に保存します。

    - <xref:System.Windows.UIElement.OnDrop%2A> メソッドで実行したチェックと同じチェックを実行して、データを <xref:System.Windows.Media.Brush> に変換できるかどうかを判断します。

    - データが有効な <xref:System.Windows.Media.Brush>に変換されると、それを<xref:System.Windows.Shapes.Ellipse>の <xref:System.Windows.Shapes.Shape.Fill%2A> に適用します。

4. 次の <xref:System.Windows.UIElement.OnDragLeave%2A> オーバーライドを追加して、<xref:System.Windows.UIElement.DragLeave> イベントのクラス処理を提供します。

     [!code-csharp[DragDropWalkthrough#OnDragLeave](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/Circle.xaml.cs#ondragleave)]
     [!code-vb[DragDropWalkthrough#OnDragLeave](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/Circle.xaml.vb#ondragleave)]

     この <xref:System.Windows.UIElement.OnDragLeave%2A> オーバーライドは、次のタスクを実行します。

    - `_previousFill` 変数に保存された <xref:System.Windows.Media.Brush> を、円ユーザー コントロールの UI を表示する <xref:System.Windows.Shapes.Ellipse> の <xref:System.Windows.Shapes.Shape.Fill%2A> に適用します。

5. **F5** キーを押してアプリケーションをビルドし、実行します。

6. <xref:System.Windows.Controls.TextBox> で、テキスト `green` を選択します。

7. テキストを円コントロールにドラッグします。ドロップはしません。 円が青色から緑色に変化します。

     ![ドラッグの効果をプレビューする&#45;and&#45;drop operation](./media/dragdrop-previeweffects.png "DragDrop_PreviewEffects")

8. テキストを円コントロールからドラッグします。 円が緑色から青色に戻ります。

## <a name="enable-a-panel-to-receive-dropped-data"></a>ドロップされたデータをパネルで受信できるようにする

このセクションでは、円ユーザー コントロールをホストするパネルが、ドラッグされた円データのドラッグ ターゲットとして機能できるようにします。 円を一方のパネルからもう一方のパネルに移動できるようにする、または**Ctrl** キーを押したまま円をドラッグ アンド ドロップして円コントロールのコピーを作成できるようにするコードを実装します。

1. MainWindow.xaml を開きます。

2. 次の XAML に示すように、各 <xref:System.Windows.Controls.StackPanel> で、<xref:System.Windows.UIElement.DragOver> イベントと <xref:System.Windows.UIElement.Drop> イベントのハンドラーを追加します。 <xref:System.Windows.UIElement.DragOver> イベント ハンドラーに `panel_DragOver` という名前を指定し、<xref:System.Windows.UIElement.Drop> イベント ハンドラーには `panel_Drop` という名前を指定します。

     [!code-xaml[DragDropWalkthrough#PanelsXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml#panelsxaml)]

3. MainWindows.xaml.cs または MainWindow.xaml.vb を開きます。

4. <xref:System.Windows.UIElement.DragOver> イベント ハンドラーに次のコードを追加します。

     [!code-csharp[DragDropWalkthrough#PanelDragOver](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldragover)]
     [!code-vb[DragDropWalkthrough#PanelDragOver](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldragover)]

     この <xref:System.Windows.UIElement.DragOver> イベント ハンドラーは、次のタスクを実行します。

    - ドラッグされたデータに、円ユーザー コントロールによって <xref:System.Windows.DataObject> にパッケージ化され、<xref:System.Windows.DragDrop.DoDragDrop%2A>の呼び出しで渡された "Object" データが含まれていることを確認します。

    - "Object" データがある場合、**Ctrl** キーが押されたかどうかを確認します。

    - **Ctrl** キーが押されていた場合、<xref:System.Windows.DragEventArgs.Effects%2A> プロパティを <xref:System.Windows.DragDropEffects.Copy> に設定します。 それ以外の場合は、<xref:System.Windows.DragEventArgs.Effects%2A> プロパティを <xref:System.Windows.DragDropEffects.Move> に設定します。

5. <xref:System.Windows.UIElement.Drop> イベント ハンドラーに次のコードを追加します。

     [!code-csharp[DragDropWalkthrough#PanelDrop](~/samples/snippets/csharp/VS_Snippets_Wpf/DragDropWalkthrough/CS/MainWindow.xaml.cs#paneldrop)]
     [!code-vb[DragDropWalkthrough#PanelDrop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DragDropWalkthrough/VB/MainWindow.xaml.vb#paneldrop)]

     この <xref:System.Windows.UIElement.Drop> イベント ハンドラーは、次のタスクを実行します。

    - <xref:System.Windows.UIElement.Drop> イベントが既に処理されたかどうかを確認します。 たとえば、円が別の円にドロップされ、その円で <xref:System.Windows.UIElement.Drop> イベントが処理される場合、円を含むパネルにそれを処理させる必要はありません。

    - <xref:System.Windows.UIElement.Drop> イベントが処理されていない場合、**Ctrl** キーが押されたかどうかを確認します。

    - <xref:System.Windows.UIElement.Drop> が発生したときに **Ctrl** キーが押されていた場合、円コントロールのコピーを作成し、それを <xref:System.Windows.Controls.StackPanel> の <xref:System.Windows.Controls.Panel.Children%2A> コレクションに追加します。

    - **Ctrl** キーが押されていない場合、円をその親パネルの <xref:System.Windows.Controls.Panel.Children%2A> コレクションから、ドロップされたパネルの <xref:System.Windows.Controls.Panel.Children%2A> コレクションに移動します。

    - 移動操作またはコピー操作のどちらが実行されたかを <xref:System.Windows.DragDrop.DoDragDrop%2A> メソッドに通知するように <xref:System.Windows.DragEventArgs.Effects%2A> プロパティを設定します。

6. **F5** キーを押してアプリケーションをビルドし、実行します。

7. <xref:System.Windows.Controls.TextBox> からテキスト `green` を選択します。

8. そのテキストを円コントロールにドラッグしてドロップします。

9. 円コントロールを左側のパネルから右側のパネルにドラッグしてドロップします。 円は、左側のパネルの <xref:System.Windows.Controls.Panel.Children%2A> コレクションから削除され、右側のパネルの Children コレクションに追加されます。

10. **Ctrl** キーを押したまま、円コントロールを、現在表示されているパネルからもう一方のパネルにドラッグしてドロップします。 円がコピーされ、そのコピーが、受け取り側のパネルの <xref:System.Windows.Controls.Panel.Children%2A> コレクションに追加されます。

     ![CTRL キーを押したまま円をドラッグする](./media/dragdrop-paneldrop.png "DragDrop_PanelDrop")

## <a name="see-also"></a>関連項目

- [ドラッグ アンド ドロップの概要](drag-and-drop-overview.md)
