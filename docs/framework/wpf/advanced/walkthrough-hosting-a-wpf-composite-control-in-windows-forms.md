---
title: Windows フォームで WPF 複合コントロールをホストする
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- hosting WPF content in Windows Forms [WPF]
ms.assetid: 0ac41286-4c1b-4b17-9196-d985cb844ce1
ms.openlocfilehash: 88efab8adf36989938ba5aa887a28b41eb8820f3
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291619"
---
# <a name="walkthrough-hosting-a-wpf-composite-control-in-windows-forms"></a>チュートリアル: Windows フォームでの WPF 複合コントロールのホスト
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、アプリケーションの作成に適した環境を提供します。 ただし、Windows フォームのコードに多大な手間と時間をかけた場合は、それを最初から書き直すよりも、既存の Windows フォーム アプリケーションを [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で拡張する方が効率的な場合もあります。 一般的なシナリオとして、Windows フォーム アプリケーションに、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用して実装したコントロールを埋め込む場合が挙げられます。 WPF コントロールのカスタマイズの詳細については、「[コントロールのカスタマイズ](../controls/control-customization.md)」を参照してください。  
  
 このチュートリアルでは、Windows フォーム アプリケーション内で [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールをホストしてデータ エントリを実行するアプリケーションについて、順を追って説明します。 複合コントロールは DLL にパッケージ化されています。 この一般的な手順は、より複雑なアプリケーションやコントロールに拡張することができます。 このチュートリアルは、外観および機能が「[チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)」とほぼ同じ構成になっています。 主な違いは、ホストする側とされる側が逆であることです。  
  
 このチュートリアルは、2 つのセクションに分かれています。 最初のセクションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールの実装について簡単に説明します。 2 番目のセクションでは、Windows フォーム アプリケーションで複合コントロールをホストし、コントロールからイベントを受け取って、コントロールのプロパティの一部にアクセスする方法について詳しく説明します。  
  
 このチュートリアルでは、以下のタスクを行います。  
  
- WPF 複合コントロールを実装する。  
  
- Windows フォーム ホスト アプリケーションを実装する。  
  
 このチュートリアルで示すタスクの完全なコード一覧については、[Windows フォームでの WPF 複合コントロールのホストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WindowsFormsHostingWpfControl)に関するページを参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  

このチュートリアルを完了するには Visual Studio が必要です。  
  
## <a name="implementing-the-wpf-composite-control"></a>WPF 複合コントロールの実装  
 この例で使用される [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールは、ユーザーの名前とアドレスを受け取る単純なデータ入力フォームです。 ユーザーが 2 つのボタンのいずれかをクリックして入力操作が終了したことを示すと、コントロールはカスタム イベントを発生させて入力情報をホストに返します。 次の図はレンダリングされたコントロールを示しています。

 次の図は WPF 複合コントロールを示したものです。

 ![シンプルな WPF コントロールを示すスクリーンショット。](./media/walkthrough-hosting-a-wpf-composite-control-in-windows-forms/windows-presentation-foundation-composite-control.png)  
  
### <a name="creating-the-project"></a>プロジェクトの作成  
 プロジェクトを開始するには  
  
1. Visual Studio を起動し、 **[新しいプロジェクト]** ダイアログ ボックスを開きます。  
  
2. Visual C# および Windows のカテゴリで、 **[WPF ユーザー コントロール ライブラリ]** テンプレートを選択します。  
  
3. 新しいプロジェクトに `MyControls` という名前を付けます。  
  
4. 配置場所として、`WindowsFormsHostingWpfControl` など、わかりやすい名前を付けた最上位フォルダーを指定します。 このフォルダーには後でホスト アプリケーションも配置します。  
  
5. **[OK]** をクリックして、プロジェクトを作成します。 既定のプロジェクトには、`UserControl1` という名前の 1 つのコントロールが含まれます。  
  
6. ソリューション エクスプローラーで、`UserControl1` を `MyControl1` という名前に変更します。  
  
 プロジェクトは、以下のシステム DLL を参照している必要があります。 これらの DLL のいずれかが既定で含まれていない場合は、プロジェクトに追加します。  
  
- PresentationCore  
  
- PresentationFramework  
  
- システム  
  
- WindowsBase  
  
### <a name="creating-the-user-interface"></a>ユーザー インターフェイスの作成  
 複合コントロールの[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用して実装されます。 複合コントロールの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] は、5 つの <xref:System.Windows.Controls.TextBox> 要素で構成されています。 各 <xref:System.Windows.Controls.TextBox> 要素には、ラベルとして使用される <xref:System.Windows.Controls.TextBlock> 要素が関連付けられています。 さらに下部には **[OK]** と **[Cancel]** という 2 つの <xref:System.Windows.Controls.Button> 要素があります。 ユーザーがいずれかのボタンをクリックすると、コントロールは情報をホストに返すカスタム イベントを発生させます。  
  
#### <a name="basic-layout"></a>基本的なレイアウト  
 <xref:System.Windows.Controls.Grid> 要素には、さまざまな [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素が格納されます。 <xref:System.Windows.Controls.Grid> を使用して、HTML で `Table` 要素を使用する場合とほぼ同じ方法で、複合コントロールのコンテンツを配置できます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には <xref:System.Windows.Documents.Table> 要素もありますが、<xref:System.Windows.Controls.Grid> の方が軽量で、単純なレイアウト タスクに適しています。  
  
 次の XAML に基本的なレイアウトを示します。 この XAML では、<xref:System.Windows.Controls.Grid> 要素に列および行の数を指定することにより、コントロールの全体的な構造が定義されています。  
  
 MyControl1.xaml で、で、既存の XAML を次の XAML で置き換えます。  
  
 [!code-xaml[WindowsFormsHostingWpfControl#101](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#101)]  
[!code-xaml[WindowsFormsHostingWpfControl#102](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#102)]  
  
#### <a name="adding-textblock-and-textbox-elements-to-the-grid"></a>TextBlock および TextBox 要素のグリッドへの追加  
 グリッドに [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素を配置するには、その要素の <xref:System.Windows.Controls.Grid.RowProperty> および <xref:System.Windows.Controls.Grid.ColumnProperty> 属性を適切な行番号と列番号に設定します。 行と列の番号付けは 0 から始まることに注意してください。 <xref:System.Windows.Controls.Grid.ColumnSpanProperty> 属性を設定することによって、1 つの要素を複数の列にまたがって表示することができます。 <xref:System.Windows.Controls.Grid> 要素の詳細については、「[グリッド要素を作成する](../controls/how-to-create-a-grid-element.md)」を参照してください。  
  
 次の XAML では、複合コントロールの <xref:System.Windows.Controls.TextBox> 要素と <xref:System.Windows.Controls.TextBlock> 要素およびそれらの <xref:System.Windows.Controls.Grid.RowProperty> 属性と <xref:System.Windows.Controls.Grid.ColumnProperty> 属性が示されており、要素をグリッドに適切に配置するために属性が設定されています。  
  
 MyControl1.xaml で、次の XAML を <xref:System.Windows.Controls.Grid> 要素内に追加します。  
  
 [!code-xaml[WindowsFormsHostingWpfControl#103](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#103)]  
  
#### <a name="styling-the-ui-elements"></a>UI 要素のスタイル設定  
 データ入力フォームの多くの要素は外観が似ていますが、それは、そのいくつかのプロパティの設定が同一であることを意味しています。 前の XAML では、各要素の属性を個別に設定するのではなく、<xref:System.Windows.Style> 要素を使用して、複数要素のクラスの標準プロパティ設定を定義しています。 この方法だと、コントロールの複雑さが軽減され、1 つのスタイル属性を使用して複数要素の外観を変更することができます。  
  
 <xref:System.Windows.Style> 要素は <xref:System.Windows.Controls.Grid> 要素の <xref:System.Windows.FrameworkElement.Resources%2A> プロパティに含まれるため、コントロール内のすべての要素で使用できます。 スタイルに名前が付いている場合は、そのスタイルの名前に設定された <xref:System.Windows.Style> 要素を追加することによって、そのスタイルを要素に適用します。 名前が付いていないスタイルは、その要素の既定のスタイルになります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のスタイルの詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。  
  
 次の XAML では、複合コントロールの <xref:System.Windows.Style> 要素が示されています。 スタイルがどのように要素に適用されるかについては、前の XAML を参照してください。 たとえば、最後の <xref:System.Windows.Controls.TextBlock> 要素では `inlineText` スタイルが使用され、最後の <xref:System.Windows.Controls.TextBox> 要素では既定のスタイルが使用されています。  
  
 MyControl1.xaml で、次の XAML を <xref:System.Windows.Controls.Grid> 開始要素の直後に追加します。  
  
 [!code-xaml[WindowsFormsHostingWpfControl#104](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#104)]  
  
#### <a name="adding-the-ok-and-cancel-buttons"></a>[OK] ボタンと [キャンセル] ボタンの追加  
 複合コントロール上の最後の要素は **[OK]** と **[Cancel]** の <xref:System.Windows.Controls.Button> 要素で、これらは <xref:System.Windows.Controls.Grid> の最後の行の最初の 2 つの列を専有します。 これらの要素では、共通のイベント ハンドラーである `ButtonClicked` と、前の XAML で定義されている既定の <xref:System.Windows.Controls.Button> スタイルが使用されています。  
  
 MyControl1.xaml で、次の XAML を最後の <xref:System.Windows.Controls.TextBox> 要素の後に追加します。 複合コントロールの [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 部分はこれで完成しました。  
  
 [!code-xaml[WindowsFormsHostingWpfControl#105](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml#105)]  
  
### <a name="implementing-the-code-behind-file"></a>分離コード ファイルの実装  
 分離コード ファイル MyControl1.xaml.cs では、次の 3 つの基本的なタスクが実装されます。
  
1. ユーザーがいずれかのボタンをクリックしたときに発生するイベントを処理します。  
  
2. <xref:System.Windows.Controls.TextBox> 要素からデータを取得し、それをカスタム イベント引数オブジェクトにパッケージ化します。  
  
3. カスタム `OnButtonClick` イベントを発生させて、ユーザーが操作終了したことをホストに通知し、入力データをホストに渡します。  
  
 コントロールは、外観を変更するための色とフォントの多くのプロパティも公開します。 Windows フォーム コントロールをホストするために使用される <xref:System.Windows.Forms.Integration.WindowsFormsHost> クラスとは異なり、<xref:System.Windows.Forms.Integration.ElementHost> クラスでは、コントロールの <xref:System.Windows.Controls.Panel.Background%2A> プロパティのみが公開されます。 このコード例と「[チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)」で説明されている例の類似性を保持するために、このコントロールでは残りのプロパティが直接公開されます。  
  
#### <a name="the-basic-structure-of-the-code-behind-file"></a>分離コード ファイルの基本構造  
 分離コード ファイルは、`MyControl1` と `MyControlEventArgs` という 2 つのクラスを格納する単一の名前空間である `MyControls` で構成されています。  
  
```csharp  
namespace MyControls  
{  
  public partial class MyControl1 : Grid  
  {  
    //...  
  }  
  public class MyControlEventArgs : EventArgs  
  {  
    //...  
  }  
}  
```  
  
 最初のクラスである `MyControl1` は、MyControl1.xaml で定義された [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 機能を実装するコードを格納する部分クラスです。 MyControl1.xaml が解析されると、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] は同じ部分クラスに変換され、2 つの部分クラスがマージされて、コンパイルされたコントロールを形成します。 このため、分離コード ファイル内のクラス名は MyControl1.xaml に割り当てられたクラス名と一致する必要があり、コントロールのルート要素から継承する必要があります。 2 番目のクラスである `MyControlEventArgs` はホストにデータを返送するために使用されるイベント引数クラスです。  
  
 MyControl1.xaml.cs を開きます。 既存のクラス宣言を以下の名前に合わせて変更し、<xref:System.Windows.Controls.Grid> を継承するようにします。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#21](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#21)]  
  
#### <a name="initializing-the-control"></a>コントロールの初期化  
 このコードでは、次の基本タスクを実装します。  
  
- プライベート イベント `OnButtonClick` と、それに関連付けられたデリゲート `MyControlEventHandler` を宣言します。  
  
- ユーザーのデータを格納するいくつかのプライベート グローバル変数を作成します。 このデータは、対応するプロパティを通じて公開されます。  
  
- コントロールの <xref:System.Windows.FrameworkElement.Loaded> イベントのハンドラー `Init` を実装します。 このハンドラーは、MyControl1.xaml で定義された値をグローバル変数に割り当てることで、グローバル変数を初期化します。 これを行うには、標準的な <xref:System.Windows.Controls.TextBlock> 要素である `nameLabel` に割り当てられた <xref:System.Windows.FrameworkElement.Name%2A> を使用して、その要素のプロパティ設定にアクセスします。  
  
 既存のコンストラクターを削除し、次のコードを `MyControl1` クラスに追加します。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#11](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#11)]  
  
#### <a name="handling-the-buttons-click-events"></a>ボタンのクリック イベントの処理  
 ユーザーは **[OK]** ボタンまたは **[Cancel]** ボタンをクリックすることによって、データ入力タスクが完了したことを示します。 どちらのボタンでも、同じ <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント ハンドラーである `ButtonClicked` が使用されています。 これらのボタンにはそれぞれ `btnOK` または `btnCancel` という名前が付けられているので、ハンドラーでは `sender` 引数の値を調べることによって、どちらのボタンがクリックされたかを判断することができます。 ハンドラーは次の処理を行います。  
  
- <xref:System.Windows.Controls.TextBox> 要素からのデータを格納する `MyControlEventArgs` オブジェクトを作成します。  
  
- ユーザーが **[Cancel]** ボタンをクリックした場合は、`MyControlEventArgs` オブジェクトの `IsOK` プロパティを `false` に設定します。  
  
- ユーザーが操作を終了したことをホストに示す `OnButtonClick` イベントを発生させ、収集したデータを渡します。  
  
 次のコードを、`MyControl1` クラスの `Init` メソッドの後に追加します。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#12](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#12)]  
  
#### <a name="creating-properties"></a>プロパティの作成  
 クラスの残りの部分では単に、前に説明したグローバル変数に対応するプロパティを公開します。 プロパティが変更されると、set アクセサーは、対応する要素のプロパティを変更し、基になるグローバル変数を更新することによって、コントロールの外観を変更します。  
  
 `MyControl1` クラスに次のコードを追加します。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#13](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#13)]  
  
#### <a name="sending-the-data-back-to-the-host"></a>ホストへのデータの返送  
 ファイルの最後のコンポーネントは、収集されたデータをホストに返送するために使用される `MyControlEventArgs` クラスです。  
  
 `MyControls` 名前空間に次のコードを追加します。 この実装は簡単なので、これ以上の説明はしません。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#14](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/MyControls/Page1.xaml.cs#14)]  
  
 ソリューションをビルドします。 ビルドでは、MyControls.dll という名前の DLL が生成されます。  
  
<a name="winforms_host_section"></a>
## <a name="implementing-the-windows-forms-host-application"></a>Windows フォーム ホスト アプリケーションの実装  
 Windows フォーム ホスト アプリケーションでは、<xref:System.Windows.Forms.Integration.ElementHost> オブジェクトを使用して [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールがホストされます。 アプリケーションでは `OnButtonClick` イベントを処理して、複合コントロールからデータを受け取ります。 アプリケーションにはオプションのボタンのセットもあり、それを使用してコントロールの外観を変更することができます。 次の図は、アプリケーションを示しています。  

次の図では、Windows フォーム アプリケーションでホストされる WPF 複合コントロールを示します。  

 ![Avalon コントロールをホストする Windows フォームを示すスクリーンショット。](./media/walkthrough-hosting-a-wpf-composite-control-in-windows-forms/windows-form-hosting-avalon-control.png)  
  
### <a name="creating-the-project"></a>プロジェクトの作成  
 プロジェクトを開始するには  
  
1. Visual Studio を起動し、 **[新しいプロジェクト]** ダイアログ ボックスを開きます。  
  
2. Visual C# および Windows のカテゴリで、 **[Windows フォーム アプリケーション]** テンプレートを選択します。  
  
3. 新しいプロジェクトに `WFHost` という名前を付けます。  
  
4. 配置場所として、MyControls の配置先と同じ最上位フォルダーを指定します。  
  
5. **[OK]** をクリックして、プロジェクトを作成します。  
  
 `MyControl1` および他のアセンブリを含む DLL への参照も追加する必要があります。  
  
1. ソリューション エクスプローラーで、プロジェクト名を右クリックし、 **[参照の追加]** を選択します。  
  
2. **[参照]** タブをクリックし、MyControls.dll が格納されているフォルダーに移動します。 このチュートリアルの場合は、MyControls\bin\Debug フォルダーです。  
  
3. MyControls.dll を選択し、 **[OK]** をクリックします。  
  
4. 次のアセンブリへの参照を追加します。  
  
    - PresentationCore  
  
    - PresentationFramework  
  
    - System.Xaml  
  
    - WindowsBase  
  
    - WindowsFormsIntegration  
  
### <a name="implementing-the-user-interface-for-the-application"></a>アプリケーションのユーザー インターフェイスの実装  
 Windows フォーム アプリケーションの UI には、WPF 複合コントロールを操作するいくつかのコントロールが含まれています。  
  
1. Windows フォーム デザイナーで、Form1 を開きます。  
  
2. コントロールを配置するためにフォームを拡大します。  
  
3. フォームの右上隅に、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールを保持するための <xref:System.Windows.Forms.Panel?displayProperty=nameWithType> コントロールを追加します。  
  
4. 次の <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType> コントロールをフォームに追加します。  
  
    |名前|テキスト|  
    |----------|----------|  
    |groupBox1|背景色|  
    |groupBox2|前景色|  
    |groupBox3|フォント サイズ|  
    |groupBox4|フォント ファミリ|  
    |groupBox5|[スタイル]|  
    |groupBox6|フォントの太さ|  
    |groupBox7|コントロールからのデータ|  
  
5. 次の <xref:System.Windows.Forms.RadioButton?displayProperty=nameWithType> コントロールを <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType> コントロールに追加します。  
  
    |GroupBox|名前|テキスト|  
    |--------------|----------|----------|  
    |groupBox1|radioBackgroundOriginal|元|  
    |groupBox1|radioBackgroundLightGreen|ライトグリーン|  
    |groupBox1|radioBackgroundLightSalmon|ライトサーモン|  
    |groupBox2|radioForegroundOriginal|元|  
    |groupBox2|radioForegroundRed|赤|  
    |groupBox2|radioForegroundYellow|黄|  
    |groupBox3|radioSizeOriginal|元|  
    |groupBox3|radioSizeTen|10|  
    |groupBox3|radioSizeTwelve|12|  
    |groupBox4|radioFamilyOriginal|元|  
    |groupBox4|radioFamilyTimes|ＭＳ Ｐゴシック|  
    |groupBox4|radioFamilyWingDings|WingDings|  
    |groupBox5|radioStyleOriginal|標準|  
    |groupBox5|radioStyleItalic|[斜体]|  
    |groupBox6|radioWeightOriginal|元|  
    |groupBox6|radioWeightBold|[太字]|  
  
6. 次の <xref:System.Windows.Forms.Label?displayProperty=nameWithType> コントロールを最後の <xref:System.Windows.Forms.GroupBox?displayProperty=nameWithType> に追加します。 これらのコントロールでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールから返されたデータが表示されます。  
  
    |GroupBox|名前|テキスト|  
    |--------------|----------|----------|  
    |groupBox7|lblName|名前:|  
    |groupBox7|lblAddress|番地:|  
    |groupBox7|lblCity|市区町村:|  
    |groupBox7|lblState|都道府県:|  
    |groupBox7|lblZip|郵便番号:|  
  
### <a name="initializing-the-form"></a>フォームの初期化  
 通常は、フォームの <xref:System.Windows.Forms.Form.Load> イベント ハンドラー内にホスティング コードを実装します。 次のコードでは、<xref:System.Windows.Forms.Form.Load> イベント ハンドラー、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールの <xref:System.Windows.FrameworkElement.Loaded> イベントのハンドラー、および後で使用するいくつかのグローバル変数の宣言を示します。  
  
 Windows フォーム デザイナーで、フォームをダブルクリックして <xref:System.Windows.Forms.Form.Load> イベント ハンドラーを作成します。 Form1.cs の先頭に、次の `using` ステートメントを追加します。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#10](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#10)]  
  
 既存の `Form1` クラスの内容を次のコードに置き換えます。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#2](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#2)]  
  
 前のコードの `Form1_Load` メソッドでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールをホストするための一般的な手順が示されています。  
  
1. 新しい <xref:System.Windows.Forms.Integration.ElementHost> オブジェクトを作成します。  
  
2. コントロールの <xref:System.Windows.Forms.Control.Dock%2A> プロパティを <xref:System.Windows.Forms.DockStyle.Fill?displayProperty=nameWithType> に設定します。  
  
3. <xref:System.Windows.Forms.Integration.ElementHost> コントロールを <xref:System.Windows.Forms.Panel> コントロールの <xref:System.Windows.Forms.Control.Controls%2A> コレクションに追加します。  
  
4. [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールのインスタンスを作成します。  
  
5. <xref:System.Windows.Forms.Integration.ElementHost> コントロールの <xref:System.Windows.Forms.Integration.ElementHost.Child%2A> プロパティにコントロールを割り当てることによって、フォーム上で複合コントロールをホストします。  
  
 `Form1_Load` メソッドの残りの 2 行では、2 つのコントロール イベントにハンドラーをアタッチします。  
  
- `OnButtonClick` は、ユーザーが **[OK]** または **[Cancel]** ボタンをクリックしたときに複合コントロールで生成されるカスタム イベントです。 このイベントを処理してユーザーの応答を取得し、ユーザーが指定したデータをすべて収集します。  
  
- <xref:System.Windows.FrameworkElement.Loaded> は、完全に読み込まれた [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロールによって生成される標準のイベントです。 ここでこのイベントを使用するのは、この例ではこのコントロールからのプロパティを使用して複数のグローバル変数を初期化する必要があるからです。 フォームの <xref:System.Windows.Forms.Form.Load> イベントの時点では、コントロールは完全には読み込まれておらず、これらの値はまだ `null` に設定されています。 それらのプロパティにアクセスするには、コントロールの <xref:System.Windows.FrameworkElement.Loaded> イベントが発生するまで待つ必要があります。  
  
 <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーは、前のコードで示されています。 `OnButtonClick` ハンドラーについては次のセクションで説明します。  
  
### <a name="handling-onbuttonclick"></a>OnButtonClick の処理  
 `OnButtonClick` イベントは、ユーザーが **[OK]** または **[Cancel]** ボタンをクリックしたときに発生します。  
  
 イベント ハンドラーでは、イベント引数の `IsOK` フィールドがチェックされて、どちらのボタンがクリックされたかが特定されます。 `lbl`*data* 変数は、前に説明した <xref:System.Windows.Forms.Label> コントロールに対応します。 ユーザーが **[OK]** ボタンをクリックすると、コントロールの <xref:System.Windows.Controls.TextBox> コントロールからのデータは、対応する <xref:System.Windows.Forms.Label> コントロールに割り当てられます。 ユーザーが **[Cancel]** をクリックすると、<xref:System.Windows.Forms.Label.Text%2A> の値は既定の文字列に設定されます。  
  
 次のボタン クリック イベント ハンドラーのコードを `Form1` クラスに追加します。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#3](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#3)]  
  
 アプリケーションをビルドして実行します。 WPF 複合コントロールに任意のテキストを追加し、 **[OK]** をクリックします。 そのテキストがラベルに表示されます。 この時点で、オプション ボタンを処理するコードは追加されていません。  
  
### <a name="modifying-the-appearance-of-the-control"></a>コントロールの外観の変更  
 フォームの <xref:System.Windows.Forms.RadioButton> コントロールを使用すると、ユーザーは [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールの前景と背景の色、およびいくつかのフォント プロパティを変更できます。 背景色は <xref:System.Windows.Forms.Integration.ElementHost> オブジェクトによって公開されます。 残りのプロパティは、コントロールのカスタム プロパティとして公開されます。  
  
 フォーム上の各 <xref:System.Windows.Forms.RadioButton> コントロールをダブルクリックして、<xref:System.Windows.Forms.RadioButton.CheckedChanged> イベント ハンドラーを作成します。 <xref:System.Windows.Forms.RadioButton.CheckedChanged> イベント ハンドラーを次のコードに置き換えます。  
  
 [!code-csharp[WindowsFormsHostingWpfControl#4](~/samples/snippets/csharp/VS_Snippets_Wpf/WindowsFormsHostingWpfControl/CSharp/WFHost/Form1.cs#4)]  
  
 アプリケーションをビルドして実行します。 別のオプション ボタンをクリックして、WPF 複合コントロール上の影響を確認します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの 3D WPF 複合コントロールのホスト](walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)
