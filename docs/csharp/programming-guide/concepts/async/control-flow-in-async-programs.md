---
title: 非同期プログラムにおける制御フロー (C#)
ms.date: 07/20/2015
ms.assetid: fc92b08b-fe1d-4d07-84ab-5192fafe06bb
ms.openlocfilehash: 99f80a86f14179c5f270064a9f96e35f8611ef13
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "70204446"
---
# <a name="control-flow-in-async-programs-c"></a>非同期プログラムにおける制御フロー (C#)

`async` キーワードと `await` キーワードを使用すると、非同期のプログラムの作成と保守をより簡単に行えます。 ただし、プログラムがどのように動作するかを理解しないと、その結果は予想に反するものになる場合があります。 このトピックでは、簡単な非同期プログラムによる制御フローをトレースして、制御があるメソッドから別のメソッドに移るタイミングと、その都度転送される情報について説明します。

一般に、[async (C#)](../../../language-reference/keywords/async.md) 修飾子を使用した非同期コードを含むメソッドをマークします。 async 修飾子でマークされたメソッドでは、[await (C#)](../../../language-reference/operators/await.md) 演算子を使用して、呼び出される非同期処理の終了をメソッドが待機する場所を指定できます。 詳細については、「[Async および Await を使用した非同期プログラミング (C#)](./index.md)」を参照してください。

次の例では、非同期メソッドを使用して、指定した Web サイトのコンテンツを文字列としてダウンロードし、その文字列の長さを表示します。 この例には、次の 2 つのメソッドが含まれています。

- `startButton_Click` を呼び出して結果を表示する `AccessTheWebAsync`。

- Web サイトのコンテンツを文字列としてダウンロードして、その文字列の長さを返す `AccessTheWebAsync`。 `AccessTheWebAsync` は、非同期 <xref:System.Net.Http.HttpClient> メソッドである <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> を使用してコンテンツをダウンロードします。

番号付き表示行はプログラム全体で重要なポイントを示し、プログラムがどのように実行され、マークされている各ポイントで何が発生するかを理解するために役立ちます。 表示行には「1」から「6」までのラベルが付けられています。 このラベルは、プログラムがこれらのコード行に到達する順序を表します。

次のコードは、プログラムの概要を示します。

```csharp
public partial class MainWindow : Window
{
    // . . .
    private async void startButton_Click(object sender, RoutedEventArgs e)
    {
        // ONE
        Task<int> getLengthTask = AccessTheWebAsync();

        // FOUR
        int contentLength = await getLengthTask;

        // SIX
        resultsTextBox.Text +=
            $"\r\nLength of the downloaded string: {contentLength}.\r\n";
    }

    async Task<int> AccessTheWebAsync()
    {
        // TWO
        HttpClient client = new HttpClient();
        Task<string> getStringTask =
            client.GetStringAsync("https://msdn.microsoft.com");

        // THREE
        string urlContents = await getStringTask;

        // FIVE
        return urlContents.Length;
    }
}
```

「1」から「6」までのそれぞれのラベルの位置は、プログラムの現在の状態に関する情報を表示します。 次の出力が生成されます。

```output
ONE:   Entering startButton_Click.
           Calling AccessTheWebAsync.

TWO:   Entering AccessTheWebAsync.
           Calling HttpClient.GetStringAsync.

THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.

FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.

FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.

SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.

Length of the downloaded string: 33946.
```

## <a name="set-up-the-program"></a>プログラムをセットアップする

このトピックで使用するコードは、MSDN からダウンロードするか、または自分でビルドできます。

> [!NOTE]
> この例を実行するには、Visual Studio 2012 以降と .NET Framework 4.5 以降が、コンピューターにインストールされている必要があります。

### <a name="download-the-program"></a>プログラムをダウンロードする

このトピックのアプリケーションは、「[非同期のサンプル:非同期プログラムにおける制御フロー](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)」からダウンロードできます。 次の手順でプログラムを開いて実行します。

1. ダウンロードしたファイルを解凍し、Visual Studio を開始します。

2. メニュー バーで、 **[ファイル]**  >  **[開く]**  >  **[プロジェクト/ソリューション]** を選択します。

3. 解凍したサンプル コードが含まれるフォルダーに移動し、ソリューション (.sln) ファイルを開き、**F5** キーを押してプロジェクトをビルドし、実行します。

### <a name="create-the-program-yourself"></a>プログラムを自分で作成する

次の Windows Presentation Foundation (WPF) プロジェクトには、このトピックのコード例が含まれています。

このプロジェクトを実行するには、次の手順を実行します。

1. Visual Studio を起動します。

2. メニュー バーで、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** を選択します。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. **[インストール済み]**  >  **[Visual C#]**  >  **[Windows Desktop]** カテゴリを選択し、プロジェクト テンプレートの一覧から **[WPF アプリ]** を選択します。

4. プロジェクトの名前として「`AsyncTracer`」と入力し、 **[OK]** をクリックします。

     **ソリューション エクスプローラー**に新しいプロジェクトが表示されます。

5. Visual Studio コード エディターで、 **[MainWindow.xaml]** タブをクリックします。

     タブが表示されない場合は、**ソリューション エクスプローラー**で MainWindow.xaml のショートカット メニューを開き、 **[コードの表示]** を選択します。

6. MainWindow.xaml の **XAML** ビューで、コードを次のコードに置き換えます。

    ```csharp
    <Window
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008" xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" mc:Ignorable="d" x:Class="AsyncTracer.MainWindow"
            Title="Control Flow Trace" Height="350" Width="592">
        <Grid>
            <Button x:Name="startButton" Content="Start
    " HorizontalAlignment="Left" Margin="250,10,0,0" VerticalAlignment="Top" Width="75" Height="24"  Click="startButton_Click" d:LayoutOverrides="GridBox"/>
            <TextBox x:Name="resultsTextBox" HorizontalAlignment="Left" TextWrapping="Wrap" VerticalAlignment="Bottom" Width="576" Height="265" FontFamily="Lucida Console" FontSize="10" VerticalScrollBarVisibility="Visible" Grid.ColumnSpan="3"/>
        </Grid>
    </Window>
    ```

     テキスト ボックスとボタンを含む簡単なウィンドウが、MainWindow.xaml の**デザイン** ビューに表示されます。

7. <xref:System.Net.Http> への参照を追加します。

8. **ソリューション エクスプローラー**で MainWindow.xaml.cs のショートカット メニューを開き、 **[コードの表示]** を選択します。

9. MainWindow.xaml.cs のコードを次のコードに置き換えます。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;

    // Add a using directive and a reference for System.Net.Http;
    using System.Net.Http;

    namespace AsyncTracer
    {
        public partial class MainWindow : Window
        {
            public MainWindow()
            {
                InitializeComponent();
            }

            private async void startButton_Click(object sender, RoutedEventArgs e)
            {
                // The display lines in the example lead you through the control shifts.
                resultsTextBox.Text += "ONE:   Entering startButton_Click.\r\n" +
                    "           Calling AccessTheWebAsync.\r\n";

                Task<int> getLengthTask = AccessTheWebAsync();

                resultsTextBox.Text += "\r\nFOUR:  Back in startButton_Click.\r\n" +
                    "           Task getLengthTask is started.\r\n" +
                    "           About to await getLengthTask -- no caller to return to.\r\n";

                int contentLength = await getLengthTask;

                resultsTextBox.Text += "\r\nSIX:   Back in startButton_Click.\r\n" +
                    "           Task getLengthTask is finished.\r\n" +
                    "           Result from AccessTheWebAsync is stored in contentLength.\r\n" +
                    "           About to display contentLength and exit.\r\n";

                resultsTextBox.Text +=
                    $"\r\nLength of the downloaded string: {contentLength}.\r\n";
            }

            async Task<int> AccessTheWebAsync()
            {
                resultsTextBox.Text += "\r\nTWO:   Entering AccessTheWebAsync.";

                // Declare an HttpClient object.
                HttpClient client = new HttpClient();

                resultsTextBox.Text += "\r\n           Calling HttpClient.GetStringAsync.\r\n";

                // GetStringAsync returns a Task<string>.
                Task<string> getStringTask = client.GetStringAsync("https://msdn.microsoft.com");

                resultsTextBox.Text += "\r\nTHREE: Back in AccessTheWebAsync.\r\n" +
                    "           Task getStringTask is started.";

                // AccessTheWebAsync can continue to work until getStringTask is awaited.

                resultsTextBox.Text +=
                    "\r\n           About to await getStringTask and return a Task<int> to startButton_Click.\r\n";

                // Retrieve the website contents when task is complete.
                string urlContents = await getStringTask;

                resultsTextBox.Text += "\r\nFIVE:  Back in AccessTheWebAsync." +
                    "\r\n           Task getStringTask is complete." +
                    "\r\n           Processing the return statement." +
                    "\r\n           Exiting from AccessTheWebAsync.\r\n";

                return urlContents.Length;
            }
        }
    }
    ```

10. **F5** キーを押してプログラムを実行し、 **[スタート]** を複数回クリックします。

    次の出力が表示されます。

    ```output
    ONE:   Entering startButton_Click.
               Calling AccessTheWebAsync.

    TWO:   Entering AccessTheWebAsync.
               Calling HttpClient.GetStringAsync.

    THREE: Back in AccessTheWebAsync.
               Task getStringTask is started.
               About to await getStringTask & return a Task<int> to startButton_Click.

    FOUR:  Back in startButton_Click.
               Task getLengthTask is started.
               About to await getLengthTask -- no caller to return to.

    FIVE:  Back in AccessTheWebAsync.
               Task getStringTask is complete.
               Processing the return statement.
               Exiting from AccessTheWebAsync.

    SIX:   Back in startButton_Click.
               Task getLengthTask is finished.
               Result from AccessTheWebAsync is stored in contentLength.
               About to display contentLength and exit.

    Length of the downloaded string: 33946.
    ```

## <a name="trace-the-program"></a>プログラムをトレースする

### <a name="steps-one-and-two"></a>手順 1. および 2.

`startButton_Click` が `AccessTheWebAsync` を呼び出し、`AccessTheWebAsync` が非同期 <xref:System.Net.Http.HttpClient> メソッド <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> を呼び出すと、最初の 2 行の表示行がパスをトレースします。 次の図は、メソッドからメソッドへの呼び出しを示しています。

![手順 1. および 2.](./media/asynctrace-onetwo.png "AsyncTrace-ONETWO")

`AccessTheWebAsync` と `client.GetStringAsync` の戻り値の型はどちらも <xref:System.Threading.Tasks.Task%601> です。 `AccessTheWebAsync` では、TResult は整数です。 `GetStringAsync` では、TResult は文字列です。 非同期メソッドの戻り値の型について詳しくは、「[非同期の戻り値の型 (C#)](./async-return-types.md)」を参照してください。

タスクを返す非同期のメソッドは、制御が呼び出し元に戻ると、タスク インスタンスを返します。 `await` 演算子が呼び出されたメソッドで実行されるか、または呼び出されたメソッドが終了すると、非同期メソッドから呼び出し元に制御が戻ります。 「3」から「6」のラベルの付いた表示行はこのプロセスの部分をトレースします。

### <a name="step-three"></a>手順 3.

`AccessTheWebAsync` で非同期メソッド <xref:System.Net.Http.HttpClient.GetStringAsync%28System.String%29> が呼び出され、ターゲットの Web ページのコンテンツがダウンロードされます。 `client.GetStringAsync` が制御を返すと、`AccessTheWebAsync` から `client.GetStringAsync` に制御が戻ります。

 `client.GetStringAsync` メソッドは、`getStringTask` の `AccessTheWebAsync` 変数に割り当てる文字列のタスクを返します。 プログラム例の次の行は、`client.GetStringAsync` の呼び出しと割り当てを示しています。

```csharp
Task<string> getStringTask = client.GetStringAsync("https://msdn.microsoft.com");
```

 このタスクは `client.GetStringAsync` により実際の文字列が最終的に生成される約束と見なすことができます。 `AccessTheWebAsync` には `client.GetStringAsync` から約束された文字列に依存しない処理がある場合、その処理は `client.GetStringAsync` を待機している間は、続行できます。 この例では、"THREE" のラベルの付いた行の出力は、独立した処理を行う機会を表します。

```output
THREE: Back in AccessTheWebAsync.
           Task getStringTask is started.
           About to await getStringTask & return a Task<int> to startButton_Click.
```

 次のステートメントは `AccessTheWebAsync` が待機中の場合 `getStringTask` の進行を中断します。

```csharp
string urlContents = await getStringTask;
```

 次の図は `client.GetStringAsync` から `getStringTask` への割り当てへの制御フロー、および `getStringTask` の作成から await 演算子のアプリケーションへの制御フローを示しています。

 ![手順 3.](./media/asynctrace-three.png "AsyncTrace-Three")

 await 式は `AccessTheWebAsync` が制御を返すまで `client.GetStringAsync` を中断します。 その間、コントロールは `AccessTheWebAsync` の呼び出し元である `startButton_Click` に戻されます。

> [!NOTE]
> 通常、直ちに非同期メソッドへの呼び出しの待機状態となります。 たとえば、次の割り当てで、`getStringTask` を作成してそれを待機する前のコードを置き換えることができます: `string urlContents = await client.GetStringAsync("https://msdn.microsoft.com");`
>
> このトピックでは、await 演算子が後で適用され、プログラムでの制御フローを示す出力行を格納します。

### <a name="step-four"></a>手順 4.

`AccessTheWebAsync` の宣言された戻り値の型は、`Task<int>` です。 したがって、`AccessTheWebAsync` が中断されると、`startButton_Click` に整数のタスクを返します。 返されたタスクは `getStringTask` ではないことに注意する必要があります。 返されたタスクは、中断されたメソッド `AccessTheWebAsync` での未処理を表す、整数の新しいタスクです。 これにより、タスクが完了したときに `AccessTheWebAsync` が整数を生成することが保証されます。

次のステートメントはこのタスクを `getLengthTask` 変数に割り当てます。

```csharp
Task<int> getLengthTask = AccessTheWebAsync();
```

 `AccessTheWebAsync` と同様に、`startButton_Click` は、非同期タスク (`getLengthTask`) の結果に依存しない処理を、タスクが待機するまで続行できます。 次の出力行はその処理を表します。

```output
FOUR:  Back in startButton_Click.
           Task getLengthTask is started.
           About to await getLengthTask -- no caller to return to.
```

 `startButton_Click` が待機すると、`getLengthTask` の進行は中断します。 次の代入ステートメントは、`startButton_Click` が完了するまで `AccessTheWebAsync` を中断します。

```csharp
int contentLength = await getLengthTask;
```

 次の図で、矢印は `AccessTheWebAsync` の await 式から `getLengthTask` への値の割り当てへの制御のフロー、および `startButton_Click` が待機するまでの `getLengthTask` の通常の処理を示しています。

 ![手順 4.](./media/asynctrace-four.png "AsyncTrace-FOUR")

### <a name="step-five"></a>手順 5.

`client.GetStringAsync` が終了を通知すると、`AccessTheWebAsync` の処理は中断から解放され、await ステートメントを越えて続行できます。 次の出力行は、処理の再開を表します。

```output
FIVE:  Back in AccessTheWebAsync.
           Task getStringTask is complete.
           Processing the return statement.
           Exiting from AccessTheWebAsync.
```

 return ステートメントのオペランド `urlContents.Length` は `AccessTheWebAsync` が返すタスクに格納されます。 await 式はその値を `getLengthTask` の `startButton_Click` から取得します。

 次の図は、`client.GetStringAsync` (および `getStringTask`) が完了した後の制御の移動を示します。

 ![手順 5.](./media/asynctrace-five.png "AsyncTrace-FIVE")

 `AccessTheWebAsync` は完了するまで実行され、完了を待機していた `startButton_Click` に制御が戻ります。

### <a name="step-six"></a>手順 6.

`AccessTheWebAsync` が終了を通知すると、処理は `startButton_Async` の await ステートメントを越えて続行できます。 実際、プログラムはそれ以上行うことがありません。

次の出力行は、`startButton_Async` の処理の再開を表します。

```output
SIX:   Back in startButton_Click.
           Task getLengthTask is finished.
           Result from AccessTheWebAsync is stored in contentLength.
           About to display contentLength and exit.
```

 await 式は `getLengthTask` から `AccessTheWebAsync` の return ステートメントのオペランドである整数値を取得します。 次のステートメントはその値を `contentLength` 変数に割り当てます。

```csharp
int contentLength = await getLengthTask;
```

 次の図は `AccessTheWebAsync` から `startButton_Click` に制御が戻ることを示しています。

 ![手順 6.](./media/asynctrace-six.png "AsyncTrace-SIX")

## <a name="see-also"></a>関連項目

- [Async および Await を使用した非同期プログラミング (C#)](./index.md)
- [非同期の戻り値の型 (C#)](./async-return-types.md)
- [チュートリアル: Async と Await を使用した Web へのアクセス (C#)](./walkthrough-accessing-the-web-by-using-async-and-await.md)
- [Async Sample:非同期プログラムにおける制御フロー (C# および Visual Basic)](https://code.msdn.microsoft.com/Async-Sample-Control-Flow-5c804fc0)
