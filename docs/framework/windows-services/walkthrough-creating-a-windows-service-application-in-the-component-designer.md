---
title: 'チュートリアル: Windows サービス アプリを作成する'
ms.date: 03/27/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Windows service applications, walkthroughs
- Windows service applications, creating
ms.assetid: e24d8a3d-edc6-485c-b6e0-5672d91fb607
author: ghogen
ms.openlocfilehash: e5ff40d8413acf64e7a8a129a7b268f58780d591
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71053480"
---
# <a name="tutorial-create-a-windows-service-app"></a>チュートリアル: Windows サービス アプリを作成する

この記事では、イベント ログにメッセージを書き込む Windows サービス アプリを Visual Studio で作成する方法を示します。

## <a name="create-a-service"></a>サービスを作成する

最初に、プロジェクトを作成し、サービスが正しく機能するために必要な値を設定します。

1. Visual Studio の **[ファイル]** メニューで **[新規]**  >  **[プロジェクト]** を選択して (または **Ctrl**+**Shift**+**N** キーを押して)、 **[新しいプロジェクト]** ウィンドウを開きます。

2. **[Windows サービス (.NET Framework)]** プロジェクト テンプレートに移動して選択します。 これを見つけるには、 **[インストール済み]** の **[Visual C#]** または **[Visual Basic]** を展開し、 **[Windows デスクトップ]** を選択します。 または、右上の検索ボックスに「*Windows サービス*」と入力して **Enter** キーを押します。

   ![Visual Studio の [新しいプロジェクト] ダイアログの Windows サービス アプリ テンプレート](./media/new-project-dialog.png)

   > [!NOTE]
   > **[Windows サービス]** テンプレートが表示されない場合は、 **.NET デスクトップ開発**ワークロードのインストールが必要である可能性があります。
   >
   > **[新しいプロジェクト]** ダイアログの左側にある **[Visual Studio インストーラーを開く]** を選択します。 **[.NET デスクトップ開発]** ワークロードを選択し、 **[変更]** を選択します。

3. **[名前]** に「*MyNewService*」と入力し、 **[OK]** を選択します。

   **[デザイン]** タブが表示されます ( **[Service1.cs [デザイン]]** または **[Service1.vb [デザイン]]** )。

   プロジェクト テンプレートには、<xref:System.ServiceProcess.ServiceBase?displayProperty=nameWithType> から継承される `Service1` という名前のコンポーネント クラスが含まれます。 それは、サービスを開始するコードなどの多数の基本的なサービス コードを含んでいます。

## <a name="rename-the-service"></a>サービスの名前を変更する

サービスの名前を **Service1** から **MyNewService** に変更します。

1. **ソリューション エクスプローラー**で **Service1.cs** または **Service1.vb** を選択し、ショートカット メニューから **[名前の変更]** を選択します。 ファイルの名前を **MyNewService.cs** または **MyNewService.vb** に変更し、**Enter** キーを押します

    コード要素 *Service1* に対するすべての参照名を変更するかどうかを確認するポップアップ ウィンドウが表示されます。

2. ポップアップ ウィンドウで **[はい]** を選択します。

    ![名前の変更のプロンプト](./media/windows-service-rename.png "Windows サービスの名前の変更のプロンプト")

3. **[デザイン]** タブで、ショートカット メニューから **[プロパティ]** を選択します。 **[プロパティ]** ウィンドウで **ServiceName** の値を *MyNewService* に変更します。

    ![サービスのプロパティ](./media/windows-service-properties.png "Windows サービスのプロパティ")

4. **[ファイル]** メニューから **[すべて保存]** を選択します。

## <a name="add-features-to-the-service"></a>サービスに機能を追加する

このセクションでは、Windows サービスにカスタム イベント ログを追加します。 Windows サービスに追加できるコンポーネントの種類の例として、<xref:System.Diagnostics.EventLog> コンポーネントを使用しています。

### <a name="add-custom-event-log-functionality"></a>サービスにカスタム イベント ログ機能を追加する

1. **ソリューション エクスプローラー**で、**MyNewService.cs** または **MyNewService.vb** のショートカット メニューから **[デザイナーの表示]** を選択します。

2. **[ツールボックス]** で **[コンポーネント]** を展開し、**EventLog** コンポーネントを **[Service1.cs [デザイン]]** タブまたは **[Service1.vb [デザイン]]** タブにドラッグします。

3. **ソリューション エクスプローラー**で、**MyNewService.cs** または **MyNewService.vb** のショートカット メニューから **[コードの表示]** を選択します。

4. カスタム イベント ログを定義します。 C# の場合は、既存の `MyNewService()` コンストラクターを編集します。Visual Basic の場合は、`New()` コンストラクターを追加します。

   [!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#2)]
   [!code-vb[VbRadconService#2](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#2)]

5. <xref:System.Diagnostics?displayProperty=nameWithType> 名前空間について、**MyNewService.cs** には `using` ステートメントを追加し (まだ存在しない場合)、**MyNewService.vb** には `Imports` ステートメントを追加します。

    ```csharp
    using System.Diagnostics;
    ```

    ```vb
    Imports System.Diagnostics
    ```

6. **[ファイル]** メニューから **[すべて保存]** を選択します。

### <a name="define-what-occurs-when-the-service-starts"></a>サービスの開始時の処理を定義する

**MyNewService.cs** または **MyNewService.vb** のコード エディターで、<xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドを見つけます (プロジェクトの作成時に、Visual Studio によって空のメソッド定義が自動的に作成されます)。 サービスの開始時にイベント ログに対するエントリを記述するコードを追加します。

[!code-csharp[VbRadconService#3](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#3)]
[!code-vb[VbRadconService#3](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#3)]

#### <a name="polling"></a>ポーリング

サービス アプリケーションは長期間実行するように設計されているため、通常は、(<xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドの設定に従って) システムをポーリングまたは監視しています。 `OnStart` メソッドは、サービスの操作が開始された後にオペレーティング システムに戻る必要があります。そのため、システムはブロックされません。

単純なポーリング メカニズムを設定するには、<xref:System.Timers.Timer?displayProperty=nameWithType> コンポーネントを使用します。 このタイマーによって、定期的な間隔で <xref:System.Timers.Timer.Elapsed> イベントが発生します。サービスは、イベントが発生するごとに監視を実行できます。 <xref:System.Timers.Timer> コンポーネントは次のように使用します。

- `MyNewService.OnStart` メソッドで <xref:System.Timers.Timer> コンポーネントのプロパティを設定します。
- <xref:System.Timers.Timer.Start%2A> メソッドを呼び出して、タイマーを開始します。

##### <a name="set-up-the-polling-mechanism"></a>ポーリング メカニズムを設定します。

1. `MyNewService.OnStart` イベントに次のコードを追加して、ポーリング メカニズムを設定します。

   ```csharp
   // Set up a timer that triggers every minute.
   Timer timer = new Timer();
   timer.Interval = 60000; // 60 seconds
   timer.Elapsed += new ElapsedEventHandler(this.OnTimer);
   timer.Start();
   ```

   ```vb
   ' Set up a timer that triggers every minute.
   Dim timer As Timer = New Timer()
   timer.Interval = 60000 ' 60 seconds
   AddHandler timer.Elapsed, AddressOf Me.OnTimer
   timer.Start()
   ```

2. <xref:System.Timers?displayProperty=nameWithType> 名前空間について、**MyNewService.cs** には `using` ステートメントを追加し、**MyNewService.vb** には `Imports` ステートメントを追加します。

   ```csharp
   using System.Timers;
   ```

   ```vb
   Imports System.Timers
   ```

3. `MyNewService` クラスに <xref:System.Timers.Timer.Elapsed?displayProperty=nameWithType> イベントを処理する `OnTimer` メソッドを追加します。

   ```csharp
   public void OnTimer(object sender, ElapsedEventArgs args)
   {
       // TODO: Insert monitoring activities here.
       eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId++);
   }
   ```

   ```vb
   Private Sub OnTimer(sender As Object, e As Timers.ElapsedEventArgs)
      ' TODO: Insert monitoring activities here.
      eventLog1.WriteEntry("Monitoring the System", EventLogEntryType.Information, eventId)
      eventId = eventId + 1
   End Sub
   ```

4. `MyNewService` クラスにメンバー変数を追加します。 それには、イベント ログに書き込まれる次のイベントの識別子が含まれます。

   ```csharp
   private int eventId = 1;
   ```

   ```vb
   Private eventId As Integer = 1
   ```

すべての作業をメイン スレッド上で実行する代わりに、バックグラウンド ワーカー スレッドを使用してタスクを実行できます。 詳細については、「<xref:System.ComponentModel.BackgroundWorker?displayProperty=fullName>」を参照してください。

### <a name="define-what-occurs-when-the-service-is-stopped"></a>サービスの停止時の処理を定義する

サービスの停止時にイベント ログに対するエントリを追加するコード行を <xref:System.ServiceProcess.ServiceBase.OnStop%2A> に挿入します。

[!code-csharp[VbRadconService#2](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#4)]
[!code-vb[VbRadconService#4](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#4)]

### <a name="define-other-actions-for-the-service"></a>サービスに対して他の処理を定義する

<xref:System.ServiceProcess.ServiceBase.OnPause%2A>、<xref:System.ServiceProcess.ServiceBase.OnContinue%2A>、および <xref:System.ServiceProcess.ServiceBase.OnShutdown%2A> の各メソッドをオーバーライドして、コンポーネントの処理をさらに定義できます。

次のコードは、`MyNewService` クラスで <xref:System.ServiceProcess.ServiceBase.OnContinue%2A> メソッドをオーバーライドする方法を示しています。

[!code-csharp[VbRadconService#5](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/MyNewService.cs#5)]
[!code-vb[VbRadconService#5](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.vb#5)]

## <a name="set-service-status"></a>サービスの状態を設定する

サービスは、その状態を[サービス コントロール マネージャー](/windows/desktop/Services/service-control-manager)に報告します。これによりユーザーは、サービスが正常に機能しているかどうかを確認することができます。 既定では、<xref:System.ServiceProcess.ServiceBase> から継承したサービスは、SERVICE_STOPPED、SERVICE_PAUSED、および SERVICE_RUNNING など、限られたセットの状態設定を報告します。 サービスの開始に時間がかかる場合は、SERVICE_START_PENDING 状態を報告すると便利です。

Windows [SetServiceStatus](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus) 関数を呼び出すコードを追加することで、SERVICE_START_PENDING および SERVICE_STOP_PENDING 状態設定を実装できます。

### <a name="implement-service-pending-status"></a>サービス保留の状態を実装する

1. <xref:System.Runtime.InteropServices?displayProperty=nameWithType> 名前空間について、**MyNewService.cs** には `using` ステートメントを追加し、**MyNewService.vb** には `Imports` ステートメントを追加します。

    ```csharp
    using System.Runtime.InteropServices;
    ```

    ```vb
    Imports System.Runtime.InteropServices
    ```

2. **MyNewService.cs** または **MyNewService.vb** に次のコードを追加して、`ServiceState` の値を宣言し、プラットフォーム呼び出しで使用する状態の構造を追加します。

    ```csharp
    public enum ServiceState
    {
        SERVICE_STOPPED = 0x00000001,
        SERVICE_START_PENDING = 0x00000002,
        SERVICE_STOP_PENDING = 0x00000003,
        SERVICE_RUNNING = 0x00000004,
        SERVICE_CONTINUE_PENDING = 0x00000005,
        SERVICE_PAUSE_PENDING = 0x00000006,
        SERVICE_PAUSED = 0x00000007,
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct ServiceStatus
    {
        public int dwServiceType;
        public ServiceState dwCurrentState;
        public int dwControlsAccepted;
        public int dwWin32ExitCode;
        public int dwServiceSpecificExitCode;
        public int dwCheckPoint;
        public int dwWaitHint;
    };
    ```

    ```vb
    Public Enum ServiceState
        SERVICE_STOPPED = 1
        SERVICE_START_PENDING = 2
        SERVICE_STOP_PENDING = 3
        SERVICE_RUNNING = 4
        SERVICE_CONTINUE_PENDING = 5
        SERVICE_PAUSE_PENDING = 6
        SERVICE_PAUSED = 7
    End Enum

    <StructLayout(LayoutKind.Sequential)>
    Public Structure ServiceStatus
        Public dwServiceType As Long
        Public dwCurrentState As ServiceState
        Public dwControlsAccepted As Long
        Public dwWin32ExitCode As Long
        Public dwServiceSpecificExitCode As Long
        Public dwCheckPoint As Long
        Public dwWaitHint As Long
    End Structure
    ```

    > [!NOTE]
    > サービス コントロール マネージャーは、[SERVICE_STATUS 構造体](/windows/win32/api/winsvc/ns-winsvc-service_status)の `dwWaitHint` メンバーと `dwCheckpoint` メンバーを使って、Windows サービスの開始やシャットダウンまでの待機時間を判断します。 `OnStart` メソッドと `OnStop` メソッドが長時間実行している場合、サービスは、インクリメントした `dwCheckPoint` 値で `SetServiceStatus` をもう一度呼び出すことによって、追加の時間を要求できます。

3. `MyNewService` クラスで、[プラットフォーム呼び出し](../interop/consuming-unmanaged-dll-functions.md)を使用して、[SetServiceStatus 関数](/windows/desktop/api/winsvc/nf-winsvc-setservicestatus)を宣言します。

    ```csharp
    [DllImport("advapi32.dll", SetLastError = true)]
    private static extern bool SetServiceStatus(System.IntPtr handle, ref ServiceStatus serviceStatus);
    ```

    ```vb
    Declare Auto Function SetServiceStatus Lib "advapi32.dll" (ByVal handle As IntPtr, ByRef serviceStatus As ServiceStatus) As Boolean
    ```

4. SERVICE_START_PENDING 状態を実装するには、<xref:System.ServiceProcess.ServiceBase.OnStart%2A> メソッドの先頭に次のコードを追加します。

    ```csharp
    // Update the service state to Start Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Start Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_START_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

5. `OnStart` メソッドの末尾に、状態を SERVICE_RUNNING に設定するコードを追加します。

    ```csharp
    // Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Running.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_RUNNING
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

6. (省略可能) <xref:System.ServiceProcess.ServiceBase.OnStop%2A> が長時間実行されるメソッドの場合は、`OnStop` メソッドでこの手順を繰り返します。 SERVICE_STOP_PENDING 状態を実装し、`OnStop` メソッドが終了する前に SERVICE_STOPPED 状態を返します。

   次に例を示します。

    ```csharp
    // Update the service state to Stop Pending.
    ServiceStatus serviceStatus = new ServiceStatus();
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING;
    serviceStatus.dwWaitHint = 100000;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);

    // Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED;
    SetServiceStatus(this.ServiceHandle, ref serviceStatus);
    ```

    ```vb
    ' Update the service state to Stop Pending.
    Dim serviceStatus As ServiceStatus = New ServiceStatus()
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOP_PENDING
    serviceStatus.dwWaitHint = 100000
    SetServiceStatus(Me.ServiceHandle, serviceStatus)

    ' Update the service state to Stopped.
    serviceStatus.dwCurrentState = ServiceState.SERVICE_STOPPED
    SetServiceStatus(Me.ServiceHandle, serviceStatus)
    ```

## <a name="add-installers-to-the-service"></a>サービスにインストーラーを追加する

Windows サービスを実行するには、まず、サービスをインストールする必要があります。これにより、サービスがサービス コントロール マネージャーに登録されます。 登録の詳細を処理するインストーラーをプロジェクトに追加します。

1. **ソリューション エクスプローラー**で、**MyNewService.cs** または **MyNewService.vb** のショートカット メニューから **[デザイナーの表示]** を選択します。

2. **[デザイン]** ビューでバックグラウンド領域を選択し、ショートカット メニューから **[インストーラーの追加]** を選択します。

     Visual Studio の既定では、2 つのインストーラーを含む `ProjectInstaller` というコンポーネント クラスがプロジェクトに追加されます。 これらのインストーラーはサービス用とサービスの関連プロセス用です。

3. **[ProjectInstaller]** の **[デザイン]** ビューで、 **[serviceInstaller1]** (Visual C# プロジェクトの場合) または **[ServiceInstaller1]** (Visual Basic プロジェクトの場合) を選択してから、ショートカット メニューから **[プロパティ]** を選択します。

4. **[プロパティ]** ウィンドウで、<xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> プロパティが **MyNewService** に設定されていることを確認します。

5. *サンプル サービス*などのテキストを <xref:System.ServiceProcess.ServiceInstaller.Description%2A> プロパティに追加します。

     このテキストは **[サービス]** ウィンドウの **[説明]** 列に表示され、サービスに関する説明をユーザーに示します。

    ![サービス ウィンドウのサービスの説明](./media/windows-service-description.png "サービスの説明")

6. <xref:System.ServiceProcess.ServiceInstaller.DisplayName%2A> プロパティにテキストを追加します。 たとえば、*MyNewService Display Name* です。

     このテキストは、 **[サービス]** ウィンドウの **[表示名]** 列に表示されます。 この名前は、システムによって使用される (たとえば、<xref:System.ServiceProcess.ServiceInstaller.ServiceName%2A> コマンドを使用してサービスを開始する場合) 名前である `net start` プロパティとは異なる名前にすることができます。

7. ドロップダウン リストから <xref:System.ServiceProcess.ServiceInstaller.StartType%2A> プロパティを <xref:System.ServiceProcess.ServiceStartMode.Automatic> に設定します。

8. 完了すると、 **[プロパティ]** ウィンドウは次の図のようになります。

     ![Windows サービスのインストーラー プロパティ](./media/windows-service-installer-properties.png "Windows サービスのインストーラー プロパティ")

9. **[ProjectInstaller]** の **[デザイン]** ビューで、 **[serviceProcessInstaller1]** (Visual C# プロジェクトの場合) または **[ServiceProcessInstaller1]** (Visual Basic プロジェクトの場合) を選択してから、ショートカット メニューから **[プロパティ]** を選択します。 ドロップダウン リストから <xref:System.ServiceProcess.ServiceProcessInstaller.Account%2A> プロパティを <xref:System.ServiceProcess.ServiceAccount.LocalSystem> に設定します。

     この設定で、ローカル システム アカウントを使用してサービスがインストールされ、実行されます。

    > [!IMPORTANT]
    > <xref:System.ServiceProcess.ServiceAccount.LocalSystem> アカウントには、イベント ログへの書き込みを含む、幅広いアクセス許可が設定されています。 このアカウントは悪意のあるソフトウェアから攻撃されるリスクが高いため、使用する場合は注意が必要です。 その他のタスクについては、ローカル コンピューターで非特権ユーザーとして機能し、リモート サーバーには匿名の資格情報を渡す <xref:System.ServiceProcess.ServiceAccount.LocalService> アカウントの使用を検討してください。 この例は、 <xref:System.ServiceProcess.ServiceAccount.LocalService> アカウントを使用しようとすると失敗します。これは、イベント ログに書き込むアクセス許可が必要になるためです。

インストーラーについて詳しくは、「[方法: サービス アプリケーションにインストーラーを追加する](how-to-add-installers-to-your-service-application.md)」を参照してください。

## <a name="optional-set-startup-parameters"></a>(省略可能) スタートアップ パラメーターを設定する

> [!NOTE]
> スタートアップ パラメーターを追加するよう決定する前に、これがサービスに情報を渡す最適な方法であるかどうかを検討してください。 使用や解析は簡単であり、ユーザーが簡単にオーバーライドできますが、ドキュメントなしでは検索や使用が困難である可能性があります。 一般的に、サービスに必要なスタートアップ パラメーターが複数ある場合は、代わりにレジストリまたは構成ファイルの使用することをお勧めします。

Windows サービスは、コマンド ライン引数 (スタートアップ パラメーター) を受け入れることができます。 スタートアップ パラメーターを処理するコードを追加すると、ユーザーは、サービス プロパティ ウィンドウでカスタムのスタートアップ パラメーターを使用してサービスを開始できます。 ただし、これらのスタートアップ パラメーターは、次回のサービスの開始時には保持されません。 スタートアップ パラメーターを永続的に設定するには、レジストリに設定します。

各 Windows サービスには、**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services** サブキー以下にレジストリ エントリがあります。 各サービスのサブキーで、**Parameters** サブキーを使用してサービスがアクセスできる情報を格納します。 その他の種類のプログラムの場合と同じ方法で、Windows サービスに対してアプリケーション構成ファイルを使用できます。 サンプル コードについては、「<xref:System.Configuration.ConfigurationManager.AppSettings?displayProperty=nameWithType>」を参照してください。

### <a name="to-add-startup-parameters"></a>スタートアップ パラメーターを追加するには

1. **Program.cs** または **MyNewService.Designer.vb** を選択してから、ショートカット メニューから **[コードの表示]** を選択します。 `Main` メソッドで、入力パラメーターを追加してサービス コンストラクターに渡すようにコードを変更します。

   [!code-csharp[VbRadconService](../../../samples/snippets/csharp/VS_Snippets_VBCSharp/VbRadconService/CS/Program-add-parameter.cs?highlight=1,6)]
   [!code-vb[VbRadconService](../../../samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbRadconService/VB/MyNewService.Designer-add-parameter.vb?highlight=1-2)]

2. **MyNewService.cs** または **MyNewService.vb** で、次のように入力パラメーターを処理するように `MyNewService` コンストラクターを変更します。

   ```csharp
   using System.Diagnostics;

   public MyNewService(string[] args)
   {
       InitializeComponent();

       string eventSourceName = "MySource";
       string logName = "MyNewLog";

       if (args.Length > 0)
       {
          eventSourceName = args[0];
       }

       if (args.Length > 1)
       {
           logName = args[1];
       }

       eventLog1 = new EventLog();

       if (!EventLog.SourceExists(eventSourceName))
       {
           EventLog.CreateEventSource(eventSourceName, logName);
       }

       eventLog1.Source = eventSourceName;
       eventLog1.Log = logName;
   }
   ```

   ```vb
   Imports System.Diagnostics

   Public Sub New(ByVal cmdArgs() As String)
       InitializeComponent()
       Dim eventSourceName As String = "MySource"
       Dim logName As String = "MyNewLog"
       If (cmdArgs.Count() > 0) Then
           eventSourceName = cmdArgs(0)
       End If
       If (cmdArgs.Count() > 1) Then
           logName = cmdArgs(1)
       End If
       eventLog1 = New EventLog()
       If (Not EventLog.SourceExists(eventSourceName)) Then
           EventLog.CreateEventSource(eventSourceName, logName)
       End If
       eventLog1.Source = eventSourceName
       eventLog1.Log = logName
   End Sub
   ```

   このコードでは、ユーザーが指定したスタートアップ パラメーターに従ってイベント ソースとログ名を設定します。 引数が指定されていない場合は、既定値が使用されます。

3. コマンド ライン引数を指定するには、**ProjectInstaller.cs** または **ProjectInstaller.vb** の `ProjectInstaller` クラスに次のコードを追加します。

   ```csharp
   protected override void OnBeforeInstall(IDictionary savedState)
   {
       string parameter = "MySource1\" \"MyLogFile1";
       Context.Parameters["assemblypath"] = "\"" + Context.Parameters["assemblypath"] + "\" \"" + parameter + "\"";
       base.OnBeforeInstall(savedState);
   }
   ```

   ```vb
   Protected Overrides Sub OnBeforeInstall(ByVal savedState As IDictionary)
       Dim parameter As String = "MySource1"" ""MyLogFile1"
       Context.Parameters("assemblypath") = """" + Context.Parameters("assemblypath") + """ """ + parameter + """"
       MyBase.OnBeforeInstall(savedState)
   End Sub
   ```

   通常、この値には Windows サービスの実行可能ファイルの完全なパスが含まれています。 サービスが正しく開始されるには、ユーザーはパスと各パラメーターに引用符を付ける必要があります。 ユーザーは **ImagePath** レジストリ エントリのパラメーターを変更して、Windows サービスのスタートアップ パラメーターを変更できます。 ただし、管理や構成のユーティリティを使用するなどして、プログラムで値を変更し、わかりやすい方法で機能を公開することをお勧めします。

## <a name="build-the-service"></a>サービスをビルドする

1. **ソリューション エクスプローラー**で、**MyNewService** プロジェクトのショートカット メニューから **[プロパティ]** を選択します。

   プロジェクトのプロパティ ページが表示されます。

2. **[アプリケーション]** タブの **[スタートアップ オブジェクト]** 一覧で **MyNewService.Program** (Visual Basic プロジェクトの場合は **Sub Main**) を選択します。

3. プロジェクトをビルドするには、**ソリューション エクスプローラー**で、プロジェクトのショートカット メニューから **[ビルド]** を選択します (または **Ctrl**+**Shift**+**B** キーを押します)。

## <a name="install-the-service"></a>サービスをインストールする

Windows サービスを構築済みであるため、サービスをインストールできます。 Windows サービスをインストールするには、インストール先のコンピューター上の管理者資格情報が必要です。

1. 管理者資格情報を使用して、[Visual Studio 用開発者コマンド プロンプト](https://docs.microsoft.com/dotnet/framework/tools/developer-command-prompt-for-vs)を開きます。 Windows の**スタート** メニューから、Visual Studio フォルダーの **[開発者コマンド プロンプト for VS 2017]** を選択し、ショートカット メニューから **[その他]**  >  **[管理者として実行]** を選択します。

2. **[開発者コマンド プロンプト for Visual Studio]** ウィンドウで、プロジェクトの出力を含むフォルダーに移動します (既定では、プロジェクトの *\bin\Debug* サブディレクトリです)。

3. 次のコマンドを入力します。

    ```shell
    installutil MyNewService.exe
    ```

    サービスが正常にインストールされると、正常に実行されたことが報告されます。

    システムで *installutil.exe* を見付けることができない場合は、コンピューター上に存在することを確認してください。 このツールは、.NET Framework と共に *%windir%\Microsoft.NET\Framework[64]\\&lt;framework version&gt;* フォルダーにインストールされます。 たとえば、64 ビット バージョンでの既定のパスは *%windir%\Microsoft.NET\Framework64\v4.0.30319\InstallUtil.exe* です。

    **installutil.exe** プロセスが失敗する場合は、インストール ログを調べて理由を確認します。 既定で、ログはサービスの実行可能ファイルと同じフォルダーにあります。 インストールは次の場合に失敗することがあります。
    - <xref:System.ComponentModel.RunInstallerAttribute> クラスが `ProjectInstaller` クラスに存在しない。
    - 属性が `true` に設定されていない。
    - `ProjectInstaller` クラスが `public` として定義されていない。

詳細については、[サービスをインストールおよびアンインストールする](how-to-install-and-uninstall-services.md)」を参照してください。

## <a name="start-and-run-the-service"></a>サービスを開始して実行する

1. Windows で、 **[サービス]** デスクトップ アプリを開きます。 **Windows**+**R** キーを押して **[ファイル名を指定して実行]** ボックスを開き、「*services.msc*」と入力して、**Enter** キーを押すか **[OK]** を選択します。

     **[サービス]** 内にサービスが一覧表示されます。サービスは、サービスに対して設定した表示名でアルファベット順に表示されます。

     ![[サービス] ウィンドウの MyNewService。](./media/windowsservices-serviceswindow.PNG)

2. サービスを開始するには、サービスのショートカット メニューから **[開始]** を選択します。

3. サービスを停止するには、サービスのショートカット メニューから **[停止]** を選択します。

4. (省略可能) コマンド ラインから、コマンド **net start &lt;service name&gt;** と **net stop &lt;service name&gt;** を使用して、サービスを開始または停止します。

### <a name="verify-the-event-log-output-of-your-service"></a>サービスのイベント ログ出力を確認する

1. Windows で、 **[イベント ビューアー]** デスクトップ アプリを開きます。 Windows 検索バーに「*イベント ビューアー*」と入力し、検索結果から **[イベント ビューアー]** を選択します。

   > [!TIP]
   > Visual Studio でイベント ログにアクセスするには、 **[表示]** メニューから**サーバー エクスプローラー**を開き (または **Ctrl**+**Alt**+**S** キーを押し)、ローカル コンピューターの **[イベント ログ]** ノードを展開します。

2. **[イベント ビューアー]** で、 **[アプリケーションとサービス ログ]** を展開します。

3. **MyNewLog** (または、手順に従ってコマンド ライン引数を追加した場合は **MyLogFile1**) の一覧を見つけて展開します。 サービスが実行した 2 つの操作 (開始および停止) のエントリが表示されます。

     ![イベント ビューアーを使用してイベント ログの項目を表示する](./media/windows-service-event-viewer.png)

## <a name="clean-up-resources"></a>リソースをクリーンアップする

Windows サービス アプリが不要になったら、削除することができます。

1. 管理者資格情報を使用して、**Visual Studio 用開発者コマンド プロンプト**を開きます。

2. **[開発者コマンド プロンプト for Visual Studio]** ウィンドウで、プロジェクトの出力を含むフォルダーに移動します。

3. 次のコマンドを入力します。

    ```shell
    installutil.exe /u MyNewService.exe
    ```

   サービスが正常にアンインストールされると、サービスが正常に削除されたことが報告されます。 詳細については、[サービスをインストールおよびアンインストールする](how-to-install-and-uninstall-services.md)」を参照してください。

## <a name="next-steps"></a>次の手順

サービスを作成したので、以下を実行できます。

- 他のユーザーが Windows サービスのインストールに使用できるスタンドアロン セットアップ プログラムを作成します。 [WiX ツールセット](https://wixtoolset.org/)を使用して、Windows サービスのインストーラーを作成します。 その他のアイデアについては、[インストーラー パッケージの作成](/visualstudio/deployment/deploying-applications-services-and-components#create-an-installer-package-windows-desktop)に関する記事を参照してください。

- インストールしたサービスにコマンドを送信できる <xref:System.ServiceProcess.ServiceController> コンポーネントの使用法を調べます。

- アプリケーションの実行時にイベント ログを作成するのではなく、アプリケーションのインストール時にインストーラーを使用してイベント ログを作成します。 アプリケーションをアンインストールすると、イベント ログはインストーラーによって削除されます。 詳細については、「<xref:System.Diagnostics.EventLogInstaller>」を参照してください。

## <a name="see-also"></a>関連項目

- [Windows サービス アプリケーション](index.md)
- [Windows サービス アプリケーションの概要](introduction-to-windows-service-applications.md)
- [方法: Windows サービス アプリケーションをデバッグする](how-to-debug-windows-service-applications.md)
- [サービス (Windows)](/windows/desktop/Services/services)
