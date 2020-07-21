---
title: 'チュートリアル: ハイブリッド アプリケーションでのデータへのバインディング'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- data binding [WPF interoperability]
ms.assetid: 18997e71-745a-4425-9c69-2cbce1d8669e
ms.openlocfilehash: 0d1e66a1277e6a04d2f49ac91691160f70fb56e4
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095074"
---
# <a name="walkthrough-binding-to-data-in-hybrid-applications"></a>チュートリアル: ハイブリッド アプリケーションでのデータへのバインディング

データ ソースをコントロールにバインドすることは、Windows フォームを使用しているか [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用しているかに関係なく、基になるデータへのアクセスをユーザーに提供するために不可欠です。 このチュートリアルでは、Windows フォームと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールの両方を含むハイブリッド アプリケーションでデータ バインディングを使用する方法について説明します。

このチュートリアルでは、以下のタスクを行います。

- プロジェクトの作成。

- データ テンプレートの定義。

- フォームのレイアウトの指定。

- データ バインディングの指定。

- 相互運用を使用したデータの表示。

- データ ソースのプロジェクトへの追加。

- データ ソースへのバインド。

このチュートリアルで説明するタスクの完全なコード リストについては、[ハイブリッド アプリケーションのデータ バインディングのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFWithWFAndDatabinding)を参照してください。

完了すると、ハイブリッド アプリケーションのデータ バインディング機能について理解できます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio

- Microsoft SQL Server で実行されている Northwind サンプル データベースへのアクセス。

## <a name="creating-the-project"></a>プロジェクトの作成

### <a name="to-create-and-set-up-the-project"></a>プロジェクトを作成し、設定するには

1. `WPFWithWFAndDatabinding` という名前の WPF アプリケーション プロジェクトを作成します。

2. ソリューション エクスプローラーで、次のアセンブリへの参照を追加します。

    - WindowsFormsIntegration

    - System.Windows.Forms

3. WPF デザイナーで MainWindow.xaml を開きます。

4. <xref:System.Windows.Window> 要素に、次の Windows フォーム名前空間マップを追加します。

    ```xaml
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"
    ```

5. <xref:System.Windows.FrameworkElement.Name%2A> プロパティを割り当てて、既定の <xref:System.Windows.Controls.Grid> 要素に `mainGrid` という名前を付けます。

     [!code-xaml[WPFWithWFAndDatabinding#8](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#8)]

## <a name="defining-the-data-template"></a>データ テンプレートの定義

<xref:System.Windows.Controls.ListBox> コントロールには顧客のマスター リストが表示されます。 次のコード例では、<xref:System.Windows.Controls.ListBox> コントロールのビジュアル ツリーを制御する `ListItemsTemplate` という名前の <xref:System.Windows.DataTemplate> オブジェクトを定義します。 この <xref:System.Windows.DataTemplate> は、<xref:System.Windows.Controls.ListBox> コントロールの <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A> プロパティに割り当てられています。

### <a name="to-define-the-data-template"></a>データ テンプレートを定義するには

- 次の XAML を <xref:System.Windows.Controls.Grid> 要素の宣言にコピーします。

     [!code-xaml[WPFWithWFAndDatabinding#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#3)]

## <a name="specifying-the-form-layout"></a>フォーム レイアウトの指定

フォーム レイアウトは、3 つの行と 3 つの列を持つグリッドによって定義されます。 <xref:System.Windows.Controls.Label> コントロールは、Customers テーブルの各列を識別するために用意されています。

### <a name="to-set-up-the-grid-layout"></a>グリッド レイアウトを設定するには

- 次の XAML を <xref:System.Windows.Controls.Grid> 要素の宣言にコピーします。

     [!code-xaml[WPFWithWFAndDatabinding#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#4)]

### <a name="to-set-up-the-label-controls"></a>ラベル コントロールを設定するには

- 次の XAML を <xref:System.Windows.Controls.Grid> 要素の宣言にコピーします。

     [!code-xaml[WPFWithWFAndDatabinding#5](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#5)]

## <a name="specifying-data-bindings"></a>データ バインディングの指定

<xref:System.Windows.Controls.ListBox> コントロールには顧客のマスター リストが表示されます。 アタッチされた `ListItemsTemplate` によって、<xref:System.Windows.Controls.TextBlock> コントロールはデータベースの `ContactName` フィールドにバインドされます。

各顧客レコードの詳細は、いくつかの <xref:System.Windows.Controls.TextBox> コントロールに表示されます。

### <a name="to-specify-data-bindings"></a>データ バインディングを指定するには

- 次の XAML を <xref:System.Windows.Controls.Grid> 要素の宣言にコピーします。

     <xref:System.Windows.Data.Binding> クラスによって、<xref:System.Windows.Controls.TextBox> コントロールはデータベースの適切なフィールドにバインドされます。

     [!code-xaml[WPFWithWFAndDatabinding#6](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#6)]

## <a name="displaying-data-by-using-interoperation"></a>相互運用を使用したデータの表示

選択した顧客に対応する注文は、`dataGridView1` という名前の <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> コントロールに表示されます。 `dataGridView1` コントロールは、分離コード ファイルのデータ ソースにバインドされています。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールは、この Windows フォーム コントロールの親です。

### <a name="to-display-data-in-the-datagridview-control"></a>DataGridView コントロールにデータを表示するには

- 次の XAML を <xref:System.Windows.Controls.Grid> 要素の宣言にコピーします。

     [!code-xaml[WPFWithWFAndDatabinding#7](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml#7)]

## <a name="adding-the-data-source-to-the-project"></a>データ ソースのプロジェクトへの追加

Visual Studio を使用すると、プロジェクトにデータ ソースを簡単に追加できます。 この手順では、厳密に型指定されたデータ セットをプロジェクトに追加します。 選択した各テーブルのテーブル アダプターなど、他のいくつかのサポート クラスも追加されます。

### <a name="to-add-the-data-source"></a>データ ソースを追加するには

1. **[データ]** メニューの **[新しいデータ ソースの追加]** をクリックします。

2. **データ ソース構成ウィザード**で、データセットを使用して Northwind データベースへの接続を作成します。 詳細については、[方法: データベース内のデータに接続する](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/fxk9yw1t(v=vs.120))」を参照してください。

3. **データ ソース構成ウィザード**で確認メッセージが表示されたら、接続文字列を `NorthwindConnectionString` という名前で保存します。

4. データベース オブジェクトを選択するように求められたら、`Customers` および `Orders` テーブルを選択し、生成されたデータセットに `NorthwindDataSet` と名前を付けます。

## <a name="binding-to-the-data-source"></a>データ ソースへのバインド

<xref:System.Windows.Forms.BindingSource?displayProperty=nameWithType> コンポーネントには、アプリケーションのデータ ソース用の統一されたインターフェイスが用意されています。 データ ソースへのバインドは、分離コード ファイルに実装されています。

### <a name="to-bind-to-the-data-source"></a>データ ソースにバインドするには

1. MainWindow.xaml.vb または MainWindow.xaml.cs という名前の分離コード ファイルを開きます。

2. 次のコードを `MainWindow` クラス定義にコピーします。

     このコードでは、データベースに接続する <xref:System.Windows.Forms.BindingSource> コンポーネントと関連するヘルパー クラスを宣言します。

     [!code-csharp[WPFWithWFAndDatabinding#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#11)]
     [!code-vb[WPFWithWFAndDatabinding#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#11)]

3. 次のコードをコンストラクターにコピーします。

     このコードでは、<xref:System.Windows.Forms.BindingSource> コンポーネントを作成して初期化します。

     [!code-csharp[WPFWithWFAndDatabinding#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#12)]
     [!code-vb[WPFWithWFAndDatabinding#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#12)]

4. MainWindow.xaml を開きます。

5. デザイン ビューまたは XAML ビューで、<xref:System.Windows.Window> 要素を選択します。

6. プロパティ ウィンドウの **[イベント]** タブをクリックします。

7. <xref:System.Windows.FrameworkElement.Loaded> イベントをダブルクリックします。

8. 次のコードを <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーにコピーします。

     このコードでは、<xref:System.Windows.Forms.BindingSource> コンポーネントをデータ コンテキストとして割り当て、`Customers` および `Orders` アダプター オブジェクトを設定します。

     [!code-csharp[WPFWithWFAndDatabinding#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#13)]
     [!code-vb[WPFWithWFAndDatabinding#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#13)]

9. 次のコードを `MainWindow` クラス定義にコピーします。

     このメソッドを使用して <xref:System.Windows.Data.CollectionView.CurrentChanged> イベントを処理し、データ バインディングの現在の項目を更新します。

     [!code-csharp[WPFWithWFAndDatabinding#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFWithWFAndDatabinding/CSharp/WPFWithWFAndDatabinding/Window1.xaml.cs#14)]
     [!code-vb[WPFWithWFAndDatabinding#14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFWithWFAndDatabinding/VisualBasic/WPFWithWFAndDatabinding/Window1.xaml.vb#14)]

10. F5 キーを押してアプリケーションをビルドし、実行します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [ハイブリッド アプリケーションのデータ バインディングのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFWithWFAndDatabinding)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
