---
title: アプリ データをキャッシュする
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- walkthroughs [WPF], caching
- caching [.NET Framework]
- caching [WPF]
ms.assetid: dac2c9ce-042b-4d23-91eb-28f584415cef
ms.openlocfilehash: b7d999f94e2f2ae410a16e537d51c0f890def4e1
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76728060"
---
# <a name="walkthrough-caching-application-data-in-a-wpf-application"></a>チュートリアル: WPF アプリケーション内のアプリケーション データのキャッシュ
キャッシュを使用すると、メモリにデータを格納して高速にアクセスできます。 アプリケーションからそのデータに再アクセスするときに、元のソースからではなく、キャッシュからデータを取得できます。 そのため、パフォーマンスとスケーラビリティが向上します。 また、データ ソースが一時的に使用できない場合でも、キャッシュのデータを使用できます。

 .NET Framework には、.NET Framework アプリケーションでキャッシュを使用できるようになるクラスが用意されています。 これらのクラスは <xref:System.Runtime.Caching> 名前空間にあります。

> [!NOTE]
> <xref:System.Runtime.Caching> 名前空間は、.NET Framework 4 で新しく追加されました。 この名前空間により、すべての .NET Framework アプリケーションでキャッシュを使用できるようになります。 .NET Framework の以前のバージョンでは、キャッシュは <xref:System.Web> 名前空間でのみ使用可能だったため、ASP.NET クラスへの依存が必要でした。

 このチュートリアルでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションの一部として .NET Framework で使用できるキャッシュ機能を使用する方法を示します。 このチュートリアルでは、テキスト ファイルのコンテンツをキャッシュします。

 このチュートリアルでは、以下のタスクを行います。

- WPF アプリケーション プロジェクトを作成する。

- .NET Framework 4 への参照を追加する。

- キャッシュを初期化する。

- テキスト ファイルのコンテンツを含むキャッシュ エントリを追加する。

- キャッシュ エントリの削除ポリシーを指定する。

- キャッシュされたファイルのパスを監視し、監視対象の項目に対する変更についてキャッシュ インスタンスに通知する。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを完了するための要件は次のとおりです。

- Visual Studio 2010。

- 少量のテキストを含むテキスト ファイル (テキスト ファイルのコンテンツをメッセージ ボックスに表示します)。このチュートリアルで示すコードは、次のファイルで作業していることを前提としています。

     `c:\cache\cacheText.txt`

     ただし、任意のテキスト ファイルを使用して、このチュートリアルのコードに小さな変更を加えることができます。

## <a name="creating-a-wpf-application-project"></a>WPF アプリケーション プロジェクトを作成する
 まず、WPF アプリケーション プロジェクトを作成します。

#### <a name="to-create-a-wpf-application"></a>WPF アプリケーションを作成するには

1. Visual Studio を起動します。

2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[新しいプロジェクト]** をクリックします。

     **[新しいプロジェクト]** ダイアログ ボックスが表示されます。

3. **[インストール済みのテンプレート]** で使用するプログラミング言語を選択します ( **[Visual Basic]** または **[Visual C#]** )。

4. **[新しいプロジェクト]** ダイアログ ボックスで **[WPF アプリケーション]** を選択します。

    > [!NOTE]
    > **WPF アプリケーション** テンプレートが表示されない場合は、WPF をサポートする .NET Framework のバージョンをターゲットにしていることを確認します。 **[新しいプロジェクト]** ダイアログ ボックスで、一覧から [.NET Framework 4] を選択します。

5. **[プロジェクト名]** テキスト ボックスにプロジェクトの名前を入力します。 たとえば、「**WPFCaching**」と入力できます。

6. **[ソリューションのディレクトリを作成]** チェック ボックスをオンにします。

7. **[OK]** をクリックします。

     WPF デザイナーが **[デザイン]** ビューで開き、MainWindow.xaml ファイルが表示されます。 Visual Studio によって**マイ プロジェクト** フォルダー、Application.xaml ファイル、および MainWindow.xaml ファイルが作成されます。

## <a name="targeting-the-net-framework-and-adding-a-reference-to-the-caching-assemblies"></a>.NET Framework のターゲット設定とキャッシュ アセンブリへの参照の追加
 既定で、WPF アプリケーションでは .NET Framework 4 クライアント プロファイルをターゲットとしています。 WPF アプリケーションで <xref:System.Runtime.Caching> 名前空間を使用するには、アプリケーションで (.NET Framework 4 クライアント プロファイルではなく).NET Framework 4 をターゲットとし、名前空間への参照を含める必要があります。

 そのため、次の手順は、.NET Framework のターゲットを変更し、<xref:System.Runtime.Caching> 名前空間への参照を追加することです。

> [!NOTE]
> .NET Framework のターゲットを変更する手順は、Visual Basic プロジェクトと Visual C# プロジェクトとで異なります。

#### <a name="to-change-the-target-net-framework-in-visual-basic"></a>Visual Basic でターゲットの .NET Framework を変更するには

1. **ソリューション エクスプローラー**で、プロジェクト名を右クリックし、 **[プロパティ]** をクリックします。

     アプリケーションの [プロパティ] ウィンドウが表示されます。

2. **[コンパイル]** タブをクリックします。

3. ウィンドウの下部にある **[詳細コンパイル オプション]** をクリックします。

     **[コンパイラの詳細設定]** ダイアログ ボックスが表示されます。

4. **[ターゲット フレームワーク (すべての構成)]** 一覧で [.NET Framework 4] を選択します ([.NET Framework 4 Client Profile] は選択しないでください)。

5. **[OK]** をクリックします。

     **[ターゲット フレームワークの変更]** ダイアログ ボックスが表示されます。

6. **[ターゲット フレームワークの変更]** ダイアログ ボックスで **[はい]** をクリックします。

     プロジェクトが閉じられ、再び開かれます。

7. 次の手順に従って、キャッシュ アセンブリへの参照を追加します。

    1. **ソリューション エクスプローラー**で、プロジェクトの名前を右クリックし、 **[参照の追加]** をクリックします。

    2. **[.NET]** タブを選択し、`System.Runtime.Caching` を選択し、 **[OK]** をクリックします。

#### <a name="to-change-the-target-net-framework-in-a-visual-c-project"></a>Visual C# プロジェクトでターゲットの .NET Framework を変更するには

1. **ソリューション エクスプローラー**でプロジェクト名を右クリックし、 **[プロパティ]** をクリックします。

     アプリケーションの [プロパティ] ウィンドウが表示されます。

2. **[アプリケーション]** タブをクリックします。

3. **[ターゲット フレームワーク]** 一覧で [.NET Framework 4] を選択します ( **[.NET Framework 4 Client Profile]** は選択しないでください)。

4. 次の手順に従って、キャッシュ アセンブリへの参照を追加します。

    1. **[参照]** フォルダーを右クリックし、 **[参照の追加]** をクリックします。

    2. **[.NET]** タブを選択し、`System.Runtime.Caching` を選択し、 **[OK]** をクリックします。

## <a name="adding-a-button-to-the-wpf-window"></a>WPF ウィンドウへのボタンの追加
 次に、ボタン コントロールを追加し、ボタンの `Click` イベントのイベント ハンドラーを作成します。 後でコードを追加して、ボタンをクリックするとテキスト ファイルのコンテンツがキャッシュされ、表示されるようにします。

#### <a name="to-add-a-button-control"></a>ボタン コントロールを追加するには

1. **ソリューション エクスプローラー**で MainWindow.xaml ファイルをダブルクリックして開きます。

2. **[ツールボックス]** の **[コモン WPF コントロール]** で、`Button` コントロールを `MainWindow` ウィンドウにドラッグします。

3. **[プロパティ]** ウィンドウで、`Button` コントロールの `Content` プロパティを **[Get Cache]\(キャッシュの取得\)** に設定します。

## <a name="initializing-the-cache-and-caching-an-entry"></a>キャッシュの初期化とエントリのキャッシュ
 次に、次のタスクを実行するコードを追加します。

- キャッシュ クラスのインスタンスを作成します。つまり、新しい <xref:System.Runtime.Caching.MemoryCache> オブジェクトをインスタンス化します。

- キャッシュで <xref:System.Runtime.Caching.HostFileChangeMonitor> オブジェクトを使用してテキスト ファイルの変更を監視するように指定します。

- テキスト ファイルを読み取り、そのコンテンツをキャッシュ エントリとしてキャッシュします。

- キャッシュされたテキスト ファイルのコンテンツを表示します。

#### <a name="to-create-the-cache-object"></a>キャッシュ オブジェクトを作成するには

1. MainWindow.xaml.cs ファイルまたは MainWindow.Xaml.vb ファイルにイベント ハンドラーを作成するために、追加したボタンをダブルクリックします。

2. ファイルの先頭 (クラス宣言の前) に、次の `Imports` (Visual Basic) または `using` (C#) ステートメントを追加します。

    ```csharp
    using System.Runtime.Caching;
    using System.IO;
    ```

    ```vb
    Imports System.Runtime.Caching
    Imports System.IO
    ```

3. イベント ハンドラーで、次のコードを追加してキャッシュ オブジェクトをインスタンス化します。

    ```csharp
    ObjectCache cache = MemoryCache.Default;
    ```

    ```vb
    Dim cache As ObjectCache = MemoryCache.Default
    ```

     <xref:System.Runtime.Caching.ObjectCache> クラスは、メモリ内オブジェクト キャッシュを提供する組み込みクラスです。

4. 次のコードを追加して、`filecontents` というキャッシュ エントリのコンテンツを読み取ります。

    ```vb
    Dim fileContents As String = TryCast(cache("filecontents"), String)
    ```

    ```csharp
    string fileContents = cache["filecontents"] as string;
    ```

5. 次のコードを追加して、`filecontents` というキャッシュ エントリが存在するかどうかを確認します。

    ```vb
    If fileContents Is Nothing Then

    End If
    ```

    ```csharp
    if (fileContents == null)
    {

    }
    ```

     指定したキャッシュ エントリが存在しない場合は、テキスト ファイルを読み取り、それをキャッシュ エントリとしてキャッシュに追加する必要があります。

6. `if/then` ブロックで、次のコードを追加して、キャッシュ エントリが 10 秒後に期限切れになることを指定する新しい <xref:System.Runtime.Caching.CacheItemPolicy> オブジェクトを作成します。

    ```vb
    Dim policy As New CacheItemPolicy()
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0)
    ```

    ```csharp
    CacheItemPolicy policy = new CacheItemPolicy();
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0);
    ```

     削除または有効期限の情報が提供されていない場合、既定値は <xref:System.Runtime.Caching.ObjectCache.InfiniteAbsoluteExpiration> です。これは、キャッシュ エントリが絶対時間のみに基づいて期限切れになることはないことを意味します。 代わりに、メモリが不足している場合にのみ、キャッシュ エントリが期限切れになります。 ベスト プラクティスとして、絶対またはスライド式の有効期限を常に明示的に指定することをお勧めします。

7. `if/then` ブロック内で、前の手順で追加したコードの後に、次のコードを追加し、監視するファイル パスのコレクションを作成し、テキスト ファイルのパスをコレクションに追加します。

    ```vb
    Dim filePaths As New List(Of String)()
    filePaths.Add("c:\cache\cacheText.txt")
    ```

    ```csharp
    List<string> filePaths = new List<string>();
    filePaths.Add("c:\\cache\\cacheText.txt");
    ```

    > [!NOTE]
    > 使用するテキスト ファイルが `c:\cache\cacheText.txt` でない場合は、使用するテキスト ファイルのパスを指定します。

8. 前の手順で追加したコードの後に、次のコードを追加し、新しい <xref:System.Runtime.Caching.HostFileChangeMonitor> オブジェクトをキャッシュ エントリの変更モニターのコレクションに追加します。

    ```vb
    policy.ChangeMonitors.Add(New HostFileChangeMonitor(filePaths))
    ```

    ```csharp
    policy.ChangeMonitors.Add(new HostFileChangeMonitor(filePaths));
    ```

     <xref:System.Runtime.Caching.HostFileChangeMonitor> オブジェクトを使用すると、テキスト ファイルのパスを監視し、変更が発生した場合はキャッシュに通知することができます。 この例では、ファイルのコンテンツが変更されると、キャッシュ エントリが期限切れになります。

9. 前の手順で追加したコードの後に次のコードを追加し、テキスト ファイルのコンテンツを読み取ります。

    ```vb
    fileContents = File.ReadAllText("c:\cache\cacheText.txt") & vbCrLf & DateTime.Now.ToString()
    ```

    ```csharp
    fileContents = File.ReadAllText("c:\\cache\\cacheText.txt") + "\n" + DateTime.Now;
    ```

     日付と時刻のタイムスタンプが追加されるので、キャッシュ エントリの有効期限がいつ切れるかを確認できます。

10. 前の手順で追加したコードの後に次のコードを追加し、ファイルのコンテンツを <xref:System.Runtime.Caching.CacheItem> インスタンスとしてキャッシュ オブジェクトに挿入します。

    ```vb
    cache.Set("filecontents", fileContents, policy)
    ```

    ```csharp
    cache.Set("filecontents", fileContents, policy);
    ```

     前の手順で作成した <xref:System.Runtime.Caching.CacheItemPolicy> オブジェクトをパラメーターとして渡すことにより、キャッシュ エントリを削除する方法に関する情報を指定します。

11. `if/then` ブロックの後に次のコードを追加し、キャッシュされたファイルのコンテンツをメッセージ ボックスに表示します。

    ```vb
    MessageBox.Show(fileContents)
    ```

    ```csharp
    MessageBox.Show(fileContents);
    ```

12. **[ビルド]** メニューで、 **[WPFCaching のビルド]** をクリックしてプロジェクトをビルドします。

## <a name="testing-caching-in-the-wpf-application"></a>WPF アプリケーションでのキャッシュのテスト
 これで、アプリケーションをテストすることができます。

#### <a name="to-test-caching-in-the-wpf-application"></a>WPF アプリケーションでキャッシュをテストするには

1. Ctrl キーを押しながら F5 キーを押してアプリケーションを実行します。

     `MainWindow`  ウィンドウが表示されます。

2. **[Get Cache]\(キャッシュの取得\)** をクリックします。

     テキスト ファイルからキャッシュされたコンテンツがメッセージ ボックスに表示されます。 ファイルのタイムスタンプに注意してください。

3. メッセージ ボックスを閉じ、 **[Get Cache]\(キャッシュの取得\)** をクリックします。

     タイムスタンプは変更されません。 これは、キャッシュされたコンテンツが表示されることを示します。

4. 10 秒以上待ってから、 **[Get Cache]\(キャッシュの取得\)** をクリックします。

     今回は、新しいタイムスタンプが表示されます。 これは、ポリシーによってキャッシュ エントリの有効期限が切れ、新しいキャッシュされたコンテンツが表示されることを示しています。

5. テキスト エディターで、作成したテキスト ファイルを開きます。 まだ変更を加えないでください。

6. メッセージ ボックスを閉じ、 **[Get Cache]\(キャッシュの取得\)** をクリックします。

     タイムスタンプに再び注目してください。

7. テキスト ファイルに変更を加え、ファイルを保存します。

8. メッセージ ボックスを閉じ、 **[Get Cache]\(キャッシュの取得\)** をクリックします。

     このメッセージ ボックスには、テキスト ファイルの更新されたコンテンツと新しいタイムスタンプが含まれています。 これは、絶対タイムアウト期間が経過していなくても、ファイルを変更した直後にホスト ファイル変更モニターによってキャッシュ エントリが削除されたことを示しています。

    > [!NOTE]
    > 削除時間を 20 秒以上に増やして、ファイルに変更を加える時間を増やすことができます。

## <a name="code-example"></a>コード例
 このチュートリアルを完了すると、作成したプロジェクトのコードは次の例のようになります。

 [!code-csharp[CachingWPFApplications#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CachingWPFApplications/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[CachingWPFApplications#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CachingWPFApplications/VisualBasic/MainWindow.xaml.vb#1)]

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.Caching.MemoryCache>
- <xref:System.Runtime.Caching.ObjectCache>
- <xref:System.Runtime.Caching>
- [.NET Framework アプリケーションでのキャッシュ](../../performance/caching-in-net-framework-applications.md)
