---
title: WPF で Windows フォーム複合コントロールをホストする
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
- composite controls [WPF], hosting in WPF
ms.assetid: 96fcd78d-1c77-4206-8928-3a0579476ef4
ms.openlocfilehash: 22eb323d1c1921832630d1d1b30463b4ecb7d1fd
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794228"
---
# <a name="walkthrough-hosting-a-windows-forms-composite-control-in-wpf"></a>チュートリアル: WPF での Windows フォーム複合コントロールのホスト
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、アプリケーションの作成に適した環境を提供します。 ただし、Windows フォーム コードに多大な投資をしている場合、コードを最初から書き直すよりも、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでそのコードの少なくとも一部を再利用する方が効率的な場合があります。 最も一般的なシナリオは、既存の Windows フォーム コントロールがある場合です。 場合によっては、これらのコントロールのソース コードにアクセスできないこともあります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでそのようなコントロールをホストするための簡単な手順が用意されています。 たとえば、特殊な <xref:System.Windows.Forms.DataGridView> コントロールをホストしながら、ほとんどのプログラミングに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用できます。  
  
 このチュートリアルでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション内で Windows フォーム複合コントロールをホストしてデータ エントリを実行するアプリケーションについて、順を追って説明します。 複合コントロールは DLL にパッケージ化されています。 この一般的な手順は、より複雑なアプリケーションやコントロールに拡張することができます。 このチュートリアルは、「[チュートリアル:Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)」とほぼ同じ外観と機能になるように設計されています。 主な違いは、ホストする側とされる側が逆であることです。  
  
 このチュートリアルは、2 つのセクションに分かれています。 最初のセクションでは、Windows フォーム複合コントロールの実装について簡単に説明します。 2 番目のセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションで複合コントロールをホストし、コントロールからイベントを受け取って、コントロールのプロパティの一部にアクセスする方法について詳しく説明します。  
  
 このチュートリアルでは、以下のタスクを行います。  
  
- Windows フォーム複合コントロールの実装。  
  
- WPF ホスト アプリケーションの実装。  
  
 このチュートリアルで示されているタスクの完全なコード一覧については、[WPF での Windows フォーム複合コントロールのホストのサンプル](https://go.microsoft.com/fwlink/?LinkID=159999)を参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  

このチュートリアルを完了するには Visual Studio が必要です。
  
## <a name="implementing-the-windows-forms-composite-control"></a>Windows フォーム複合コントロールの実装  
 この例で使用されている Windows フォーム複合コントロールは、簡単なデータ入力フォームです。 このフォームでは、ユーザーの名前とアドレスを受け取り、カスタム イベントを使用してその情報をホストに返します。 次の図はレンダリングされたコントロールを示しています。  

 次の図は Windows フォーム複合コントロールを示しています。  

 ![シンプルな Windows フォーム コントロールを示すスクリーンショット。](./media/walkthrough-hosting-a-windows-forms-composite-control-in-wpf/windows-forms-control.gif)  
  
### <a name="creating-the-project"></a>プロジェクトの作成  
 プロジェクトを開始するには  
  
1. Visual Studio を起動し、 **[新しいプロジェクト]** ダイアログ ボックスを開きます。  
  
2. [ウィンドウ] カテゴリで、 **[Windows フォーム コントロール ライブラリ]** テンプレートを選択します。  
  
3. 新しいプロジェクトに `MyControls` という名前を付けます。  
  
4. 配置場所として、`WpfHostingWindowsFormsControl` など、わかりやすい名前を付けた最上位フォルダーを指定します。 このフォルダーには後でホスト アプリケーションも配置します。  
  
5. **[OK]** をクリックして、プロジェクトを作成します。 既定のプロジェクトには、`UserControl1` という名前の 1 つのコントロールが含まれます。  
  
6. ソリューション エクスプローラーで、`UserControl1` を `MyControl1` という名前に変更します。  
  
 プロジェクトは、以下のシステム DLL を参照している必要があります。 これらの DLL のいずれかが既定で含まれていない場合は、プロジェクトに追加します。  
  
- システム  
  
- System.Data  
  
- System.Drawing  
  
- System.Windows.Forms  
  
- System.Xml  
  
### <a name="adding-controls-to-the-form"></a>フォームへのコントロールの追加  
 フォームにコントロールを追加するには  
  
- デザイナーで `MyControl1` を開きます。  
  
 5 つの <xref:System.Windows.Forms.Label> コントロールとそれに対応する<xref:System.Windows.Forms.TextBox> コントロールを、前の図と同じサイズと配置でフォームに追加します。 この例では、<xref:System.Windows.Forms.TextBox> コントロールに次の名前が付けられています。  
  
- `txtName`  
  
- `txtAddress`  
  
- `txtCity`  
  
- `txtState`  
  
- `txtZip`  
  
 **[OK]** と **[キャンセル]** というラベルの 2 つの <xref:System.Windows.Forms.Button> コントロールを追加します。 この例では、ボタン名はそれぞれ `btnOK` と `btnCancel` です。  
  
### <a name="implementing-the-supporting-code"></a>サポート コードの実装  
 コード ビューでフォームを開きます。 このコントロールでは、カスタム `OnButtonClick` イベントを発生させることによって収集されたデータをホストに返します。 データは、イベント引数オブジェクトに格納されます。 次のコードは、イベントとデリゲートの宣言を示しています。  
  
 `MyControl1` クラスに次のコードを追加します。  
  
 [!code-csharp[WpfHostingWindowsFormsControl#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#2)]
 [!code-vb[WpfHostingWindowsFormsControl#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#2)]

 `MyControlEventArgs` クラスには、ホストに返される情報が含まれています。

 次のクラスをフォームに追加します。

 [!code-csharp[WpfHostingWindowsFormsControl#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#3)]
 [!code-vb[WpfHostingWindowsFormsControl#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#3)]

 ユーザーが **[OK]** または **[キャンセル]** ボタンをクリックすると、<xref:System.Windows.Forms.Control.Click> イベント ハンドラーによってデータが格納された `MyControlEventArgs` オブジェクトが作成され、`OnButtonClick` イベントを発生します。 2 つのハンドラーの唯一の違いは、イベント引数の `IsOK` プロパティです。 このプロパティを使用すると、クリックされたボタンをホストで判別できるようになります。 **[OK]** ボタンの場合は `true`、 **[キャンセル]** ボタンの場合は `false` に設定されます。 次のコードは、2 つのボタン ハンドラーを示しています。

 `MyControl1` クラスに次のコードを追加します。

 [!code-csharp[WpfHostingWindowsFormsControl#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/MyControls/MyControl1.cs#4)]
 [!code-vb[WpfHostingWindowsFormsControl#4](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/MyControls/MyControl1.vb#4)]

### <a name="giving-the-assembly-a-strong-name-and-building-the-assembly"></a>アセンブリに厳密な名前を付け、アセンブリをビルドする
 このアセンブリを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションから参照するには、厳密な名前が必要です。 厳密な名前を作成するには、Sn.exe を使用してキー ファイルを作成し、プロジェクトに追加します。

1. Visual Studio のコマンド プロンプトを開きます。 これを行うには、 **[スタート]** メニューをクリックし、 **[すべてのプログラム]、[Microsoft Visual Studio 2010]、[Visual Studio Tools]、[Visual Studio コマンド プロンプト]** の順に選択します。 これにより、カスタマイズされた環境変数を使用してコンソール ウィンドウが起動します。

2. コマンド プロンプトで、`cd` コマンドを使用してプロジェクト フォルダーに移動します。

3. 次のコマンドを実行して、MyControls.snk という名前のキー ファイルを生成します。

    ```console
    Sn.exe -k MyControls.snk
    ```

4. プロジェクトにキー ファイルを含めるには、ソリューション エクスプローラーでプロジェクト名を右クリックし、 **[プロパティ]** をクリックします。 プロジェクト デザイナーで **[署名]** タブをクリックし、 **[アセンブリに署名する]** チェック ボックスをオンにして、キー ファイルを参照します。

5. ソリューションをビルドします。 ビルドでは、MyControls.dll という名前の DLL が生成されます。

## <a name="implementing-the-wpf-host-application"></a>WPF ホスト アプリケーションの実装
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ホスト アプリケーションでは、`MyControl1` をホストするために <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールを使用します。 アプリケーションでは `OnButtonClick`イベントを処理して複合コントロールからデータを受け取ります。 また、オプション ボタンのコレクションもあります。これらを使うと、コントロールのプロパティの一部を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションから変更できます。 完成したアプリケーションを次の図に示します。

次の図は、WPF アプリケーションに埋め込まれたコントロールを含む完全なアプリケーションを示しています。

 ![WPF ページに埋め込まれたコントロールを示すスクリーンショット。](./media/walkthrough-hosting-a-windows-forms-composite-control-in-wpf/windows-presentation-foundation-page-control.gif)

### <a name="creating-the-project"></a>プロジェクトの作成
 プロジェクトを開始するには

1. Visual Studio を開いて、 **[新しいプロジェクト]** をクリックします。

2. [ウィンドウ] カテゴリで、 **[WPF アプリケーション テンプレート]** を選択します。

3. 新しいプロジェクトに `WpfHost` という名前を付けます。

4. 配置場所として、MyControls の配置先と同じ最上位フォルダーを指定します。

5. **[OK]** をクリックして、プロジェクトを作成します。

 `MyControl1` および他のアセンブリを含む DLL への参照も追加する必要があります。

1. ソリューション エクスプローラーで、プロジェクト名を右クリックし、 **[参照の追加]** を選択します。

2. **[参照]** タブをクリックし、MyControls.dll を格納しているフォルダーに移動します。 このチュートリアルの場合は、MyControls\bin\Debug フォルダーです。

3. MyControls.dll を選択し、 **[OK]** をクリックします。

4. WindowsFormsIntegration.dll という名前の WindowsFormsIntegration アセンブリへの参照を追加します。

### <a name="implementing-the-basic-layout"></a>基本的なレイアウトの実装
 ホスト アプリケーションの [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] は MainWindow.xaml に実装されています。 このファイルには、レイアウトを定義し、Windows フォーム コントロールをホストする [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] マークアップが含まれています。 アプリケーションは 3 つの領域に分かれています。

- **[Control Properties]\(コントロールのプロパティ\)** パネル。ホストされているコントロールのさまざまなプロパティを変更するために使用できるオプション ボタンのコレクションが含まれています。

- **[Data from Control]\(コントロールのデータ\)** パネル。ホストされているコントロールから返されたデータを表示する <xref:System.Windows.Controls.TextBlock> 要素がいくつか含まれています。

- ホストされているコントロール自体。

 基本的なレイアウトを次の XAML に示します。 `MyControl1` をホストするために必要なマークアップはこの例では省略されていますが、後で説明します。

 MainWindow.xaml の XAML を次のように置き換えます。 Visual Basic を使用している場合は、クラスを `x:Class="MainWindow"` に変更します。

 [!code-xaml[WpfHostingWindowsFormsControl#100](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#100)]

 最初の <xref:System.Windows.Controls.StackPanel> 要素には、ホストされているコントロールのさまざまな既定プロパティを変更できる <xref:System.Windows.Controls.RadioButton> コントロールのセットがいくつか含まれています。 その後に `MyControl1` をホストする <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素が続きます。 最後の <xref:System.Windows.Controls.StackPanel> 要素には、ホストされたコントロールから返されるデータを表示するいくつかの <xref:System.Windows.Controls.TextBlock> 要素が含まれています。 要素の順序と、<xref:System.Windows.Controls.DockPanel.Dock%2A> および <xref:System.Windows.FrameworkElement.Height%2A> の属性設定により、ギャップやゆがみを生じることなく、ホストされているコントロールがウィンドウに埋め込まれます。

#### <a name="hosting-the-control"></a>コントロールのホスト
 前述の XAML を編集した以下のバージョンでは、`MyControl1` をホストするために必要な要素に焦点を当てています。

 [!code-xaml[WpfHostingWindowsFormsControl#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#101)]
[!code-xaml[WpfHostingWindowsFormsControl#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml#102)]

 `xmlns` 名前空間マッピング属性を使用すると、ホストされているコントロールを含む `MyControls` 名前空間への参照が作成されます。 このマッピングにより、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の `MyControl1` を `<mcl:MyControl1>` と表すことができます。

 XAML の 2 つの要素によってホスティングを処理します。

- `WindowsFormsHost` は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションで Windows フォーム コントロールをホストできるようにする <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を表します。

- `MyControl1` を表す `mcl:MyControl1` は、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の子コレクションに追加されます。 その結果、この Windows フォーム コントロールは [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ウィンドウの一部としてレンダリングされ、アプリケーションからそのコントロールと通信できるようになります。

### <a name="implementing-the-code-behind-file"></a>分離コード ファイルの実装
 分離コード ファイル MainWindow.xaml.vb または MainWindow.xaml.cs には、前のセクションで説明した [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の機能を実装する手続き型コードが含まれています。 主なタスクは次のとおりです。

- `MyControl1` の `OnButtonClick` イベントへのイベント ハンドラーのアタッチ。

- オプション ボタンのコレクションの設定方法に基づく `MyControl1` のさまざまなプロパティの変更。

- コントロールによって収集されたデータの表示。

#### <a name="initializing-the-application"></a>アプリケーションの初期化
 初期化コードは、ウィンドウの <xref:System.Windows.FrameworkElement.Loaded> イベントのイベント ハンドラーに含まれており、これを使用してコントロールの `OnButtonClick` イベントにイベント ハンドラーをアタッチすることができます。

 MainWindow.xaml.vb または MainWindow.xaml.cs で、次のコードを `MainWindow` クラスに追加します。

 [!code-csharp[WpfHostingWindowsFormsControl#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#11)]
 [!code-vb[WpfHostingWindowsFormsControl#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#11)]

 前述の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の子要素コレクションに `MyControl1` が追加されたため、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の <xref:System.Windows.Forms.Integration.WindowsFormsHost.Child%2A> をキャストして`MyControl1` への参照を取得できます。 これで、その参照を使用してイベント ハンドラーを `OnButtonClick` にアタッチできるようになります。

 <xref:System.Windows.Forms.Integration.WindowsFormsHost> では、コントロール自体に参照が提供されるだけでなく、アプリケーションから操作できるいくつかのコントロールのプロパティが公開されています。 初期化コードを使用してこれらの値をプライベート グローバル変数に割り当て、後でアプリケーションで使用できるようにします。

 `MyControls` DLL の型に簡単にアクセスできるように、次の `Imports` または `using` ステートメントをファイルの先頭に追加します。

```vb
Imports MyControls
```

```csharp
using MyControls;
```

#### <a name="handling-the-onbuttonclick-event"></a>OnButtonClick イベントの処理
 `MyControl1` を使用すると、ユーザーがコントロールのボタンのいずれかをクリックしたときに `OnButtonClick` イベントを発生させることができます。

 `MainWindow` クラスに次のコードを追加します。

 [!code-csharp[WpfHostingWindowsFormsControl#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#12)]
 [!code-vb[WpfHostingWindowsFormsControl#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#12)]

 テキスト ボックスのデータは `MyControlEventArgs` オブジェクトにパックされます。 ユーザーが **[OK]** ボタンをクリックすると、イベント ハンドラーによってデータが抽出され、そのデータがパネルの `MyControl1` の下に表示されます。

#### <a name="modifying-the-controls-properties"></a>コントロールのプロパティの変更
 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素では、ホストされているコントロールの既定プロパティの一部が公開されています。 その結果、アプリケーションのスタイルに合わせてコントロールの外観を変更することができます。 ユーザーは、左側のパネルにあるオプション ボタン セットを使用して、いくつかの色とフォントのプロパティを変更できます。 各ボタン セットには <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントのハンドラーがあります。これによってユーザーのオプション ボタンの選択が検出され、コントロールの対応するプロパティが変更されます。

 `MainWindow` クラスに次のコードを追加します。

 [!code-csharp[WpfHostingWindowsFormsControl#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/CSharp/WpfHost/Page1.xaml.cs#13)]
 [!code-vb[WpfHostingWindowsFormsControl#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WpfHostingWindowsFormsControl/VisualBasic/WpfHost/Page1.xaml.vb#13)]  
  
 アプリケーションをビルドして実行します。 Windows フォーム複合コントロールにテキストを追加し、 **[OK]** をクリックします。 そのテキストがラベルに表示されます。 さまざまなラジオ ボタンをクリックしてコントロールへの影響を確認します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: WPF での Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
