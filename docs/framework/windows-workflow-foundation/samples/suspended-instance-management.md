---
title: 中断されたインスタンスの管理
ms.date: 03/30/2017
ms.assetid: f5ca3faa-ba1f-4857-b92c-d927e4b29598
ms.openlocfilehash: 784ec3cdda8eedb188c3c776ed412ea40baf37ea
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182790"
---
# <a name="suspended-instance-management"></a>中断されたインスタンスの管理
このサンプルでは、中断されているワークフロー インスタンスを管理する方法を示します。  <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior> の既定のアクションは `AbandonAndSuspend` です。 つまり、既定では、<xref:System.ServiceModel.WorkflowServiceHost> でホストされるワークフロー インスタンスからスローされた未処理の例外により、インスタンスがメモリから破棄され、インスタンスの永続バージョンが中断状態としてマークされることになります。 中断されたワークフロー インスタンスは、中断が解除されるまで実行できません。

 このサンプルでは、コマンド ライン ユーティリティを実装して、中断されたインスタンスについてクエリを実行する方法、およびユーザーがインスタンスを再開または終了できるようにする方法を示します。 このサンプルでは、ワークフロー サービスから例外が意図的にスローされ、中断状態になります。 その後、コマンド ライン ユーティリティを使用してインスタンスについてクエリを実行し、さらに、インスタンスを再開または終了できます。

## <a name="demonstrates"></a>対象
 <xref:System.ServiceModel.WorkflowServiceHost><xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>と<xref:System.ServiceModel.Activities.WorkflowControlEndpoint>Windows ワークフローファウンデーション (WF) での使用。

## <a name="discussion"></a>ディスカッション
 このサンプルに実装されているコマンド ライン ユーティリティは、[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] に用意されている SQL インスタンス ストアの実装に固有のものです。 インスタンス ストアのカスタム実装がある場合は、サンプルの `WorkflowInstanceCommand` の実装を、使用しているインスタンス ストアに固有の実装に置き換えることで、このユーティリティを調整できます。

 用意されている実装では、SQL インスタンス ストアに対して SQL コマンドを直接実行して、中断されたインスタンスのリストを取得し、<xref:System.ServiceModel.Activities.WorkflowControlEndpoint> に追加された <xref:System.ServiceModel.WorkflowServiceHost> を使用して、インスタンスを再開または終了できるようにします。

#### <a name="to-set-up-build-and-run-the-sample"></a>サンプルをセットアップ、ビルド、および実行するには

1. このサンプルでは、次の Windows コンポーネントが有効になっている必要があります。

    1. Microsoft メッセージ キュー (MSMQ) サーバー

    2. SQL Server Express

2. SQL Server データベースを設定します。

    1. Visual Studio 2010 コマンド プロンプトから、次の操作を行う中断インスタンス管理サンプル ディレクトリから "setup.cmd" を実行します。

        1. SQL Server Express を使用して永続性データベースを作成します。 永続性データベースが既に存在する場合、データベースは削除され、再作成されます。

        2. 永続化のためにデータベースを設定します。

        3. IIS APPPOOL\DefaultAppPool および NT AUTHORITY\Network Service を、永続化のためにデータベースを設定するときに定義された InstanceStoreUsers ロールに追加します。

3. サービス キューを設定します。

    1. Visual Studio 2010 で **、SampleWorkflowApp**プロジェクトを右クリックし、[**スタートアップ プロジェクトとして設定**] をクリックします。

    2. **F5**キーを押してサンプルワークフローアプリをコンパイルして実行します。 これにより、必要なキューが作成されます。

    3. **Enter**キーを押して、サンプルワークフローアプリを停止します。

    4. コマンド プロンプトから Compmgmt.msc を実行して、[コンピューターの管理] コンソールを開きます。

    5. [**サービスとアプリケーション]、[****メッセージ キュー**]、[**プライベート キュー**] の順に展開します。

    6. **ReceiveTx**キューを右クリックし、[**プロパティ]** をクリックします。

    7. [**セキュリティ**] タブを選択し **、Everyone**に対して **[メッセージの受信**]、[**メッセージのピーク**]、および [**メッセージの送信**] のアクセス許可を与えます。

4. サンプルを実行します。

    1. Visual Studio 2010 では **、Ctrl キーを押しながら F5**キーを押して、デバッグせずに SampleWorkflowApp プロジェクトを再度実行します。 2 つのエンドポイント アドレスがコンソール ウィンドウに出力されます。1 つはアプリケーション エンドポイントのアドレスで、もう 1 つは <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> のアドレスです。 その後、ワークフロー インスタンスが作成され、そのインスタンスの追跡レコードがコンソール ウィンドウに表示されます。 ワークフロー インスタンスから例外がスローされ、インスタンスは中断されて中止されます。

    2. 次に、コマンド ライン ユーティリティを使用して、これらのインスタンスに対してさらに操作を実行できます。 コマンド ライン引数の構文は次のとおりです。

         `SuspendedInstanceManagement -Command:[CommandName] -Server:[ServerName] -Database:[DatabaseName] -InstanceId:[InstanceId]`

         サポートされるコマンドは、`Query`、`Resume`、および `Terminate` です。  InstanceId スイッチを指定する必要があるのは、`Resume` 操作および `Terminate` 操作だけです。

#### <a name="to-cleanup-optional"></a>クリーンアップするには (省略可能)

1. `vs2010` コマンド プロンプトから Compmgmt.msc を実行して、[コンピューターの管理] コンソールを開きます。

2. [**サービスとアプリケーション]、[****メッセージ キュー**]、[**プライベート キュー**] の順に展開します。

3. 受信**Tx**キューを削除します。

4. 永続性データベースを削除するには、cleanup.cmd を実行します。

> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\SuspendedInstanceManagement`
