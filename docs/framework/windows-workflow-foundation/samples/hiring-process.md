---
title: 雇用プロセス
ms.date: 03/30/2017
ms.assetid: d5fcacbb-c884-4b37-a5d6-02b1b8eec7b4
ms.openlocfilehash: ade72422d29d170e9c80f602f151ce765a1a00f7
ms.sourcegitcommit: e48a54ebe62e874500a7043f6ee0b77a744d55b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80291695"
---
# <a name="hiring-process"></a>雇用プロセス
このサンプルでは、メッセージング アクティビティ、およびワークフロー サービスとしてホストされる 2 つのワークフローを使用して、ビジネス プロセスを実装する方法を示します。 この 2 つのワークフローは、Contoso, Inc という架空の会社の IT インフラストラクチャの一部です。  
  
 `HiringRequest` ワークフロー プロセス (<xref:System.Activities.Statements.Flowchart> として実装) は、組織の複数のマネージャーの承認が必要です。 この目標を達成するために、ワークフローは組織内の他の既存のサービス (この場合は受信トレイ サービスと、プレーンな Windows コミュニケーション ファウンデーション (WCF) サービスとして実装された組織データ サービス) を使用します。  
  
 `ResumeRequest` ワークフロー (<xref:System.Activities.Statements.Sequence> として実装) は、Contoso 社の外部 Careers Web サイトに求人情報を発行し、履歴書の受け取りを管理します。 求人情報は、指定した期間 (タイムアウトになるまで) または Contoso の従業員が削除を決定するまで、外部 Web サイトに掲載されます。  
  
 このサンプルでは、次の [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] の機能について説明します。  
  
- ビジネス プロセスをモデル化する <xref:System.Activities.Statements.Flowchart> および <xref:System.Activities.Statements.Sequence> ワークフロー。  
  
- ワークフロー サービス。  
  
- メッセージング アクティビティ。  
  
- コンテンツ ベースの相関関係。  
  
- カスタム アクティビティ (宣言型およびコードベース)。  
  
- システムで指定された SQL サーバー永続性。  
  
- カスタム <xref:System.Activities.Persistence.PersistenceParticipant>。  
  
- カスタム追跡  
  
- Event Tracking for Windows (ETW) 追跡。  
  
- アクティビティの構成。  
  
- <xref:System.Activities.Statements.Parallel> アクティビティ。  
  
- <xref:System.Activities.Statements.CancellationScope> アクティビティ。  
  
- 永続的なタイマー (<xref:System.Activities.Statements.Delay> アクティビティ)。  
  
- トランザクション。  
  
- 同一ソリューションの複数のワークフロー。  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\HiringProcess`  
  
## <a name="description-of-the-process"></a>プロセスの説明  
 Contoso 社は、各部門の人数を綿密に管理しようとしています。 このため、従業員が新しい雇用プロセスを開始する場合、求人を実際に開始する前に雇用要件プロセスの承認を受ける必要があります。 このプロセスは、雇用プロセス要求 (HiringRequestService プロジェクトで定義) と呼ばれ、次の手順で構成されます。  
  
1. 従業員 (要求者) は雇用プロセス要求を開始します。  
  
2. 依頼者のマネージャーは、要求を承認する必要があります。  
  
    1. マネージャーは要求を拒否できます。  
  
    2. マネージャーは、追加情報が必要な場合、要求者に要求を戻すことができます。  
  
        1. 要求者は要求をレビューし、マネージャーに再承認を求めることができます。  
  
    3. マネージャーはこれを承認します。  
  
3. 依頼者のマネージャーが承認した後、部門の所有者は要求を承認する必要があります。  
  
    1. 部門の責任者は要求を拒否できます。  
  
    2. 部門の責任者は要求を承認できます。  
  
4. 部門の責任者の承認後は、HR (人事部) の 2名のマネージャーまたは CEO (最高経営責任者) の承認を受ける必要があります。  
  
    1. プロセスは承認状態または拒否状態のいずれかになります。  
  
    2. プロセスが [承諾済み] になると、`ResumeRequest` ワークフローの新しいインスタンスが開始されます (`ResumeRequest` はサービス参照を使用して HiringRequest.csproj にリンクされます)。  
  
 マネージャーが新しい従業員の雇用を承認すると、HR は適切な応募者を採用する必要があります。 このプロセスは、2 番目のワークフロー (`ResumeRequest`。ResumeRequestService.csproj で定義。) で実行されます。 このワークフローによって、Contoso 社の外部 Careers Web サイトに求人情報を送信するプロセスが定義され、応募者から履歴書を受信し、募集の状況が監視されます。 求人は、指定した期間 (有効期間が過ぎるまで) または Contoso の従業員が削除を指定するまで有効です。 `ResumeRequest` ワークフローは、次のステップから構成されています。  
  
1. Contoso 社の従業員は、求人およびタイムアウト期間に関する情報を入力します。 従業員がこの情報を入力すると、Careers Web サイトに求人情報が掲載されます。  
  
2. この情報が発行されると、この情報に興味を持った人が自分の履歴書を送信します。 履歴書は、送信後、求人にリンクされたレコードに保存されます。  
  
3. 応募者は、タイムアウトになるまで、または Contoso 社の HR 部でプロセスを停止して求人を削除することを明示的に決定するまでは履歴書を送信することができます。  
  
## <a name="projects-in-the-sample"></a>サンプルのプロジェクト  
 サンプル ソリューションのプロジェクトを次の表に示します。  
  
|Project|説明|  
|-------------|-----------------|  
|ContosoHR|データ コントラクト、ビジネス オブジェクト、およびリポジトリ クラスが含まれます。|  
|HiringRequestService|Hiring Request Process ワークフローの定義を含んでいます。<br /><br /> このプロジェクトは、サービスとしてワークフロー (xaml ファイル) を自己ホストするコンソール アプリケーションとして実装されます。|  
|ResumeRequestService|タイムアウトとなるかプロセス終了が決定するまで応募者からの履歴書を収集するワークフロー サービス。<br /><br /> このプロジェクトは、宣言型ワークフロー サービス (xamlx) として実装されます。|  
|OrgService|組織情報 (Employees、Positions、PositionTypes、および Departments) を公開するサービス。 このサービスは、Enterprise Resource Plan (ERP) の Company Organization モジュールと考えることができます。<br /><br /> このプロジェクトは、Windows 通信基盤 (WCF) サービスを公開するコンソール アプリケーションとして実装されます。|  
|InboxService|従業員のアクション可能なタスクを含んでいる受信トレイです。<br /><br /> このプロジェクトは、WCF サービスを公開するコンソール アプリケーションとして実装されます。|  
|InternalClient|プロセスと対話するための Web アプリケーション。 ユーザーは、HiringProcess ワークフローを開始して、参加し、表示できます。 このアプリケーションを使用すると、ResumeRequest プロセスを開始および監視することもできます。<br /><br /> このサイトは、Contoso のイントラネット内のサイトとして実装されます。 このプロジェクトは ASP.NET Web サイトとして実装されます。|  
|CareersWebSite|Contoso 社で募集中の求人を公開する外部 Web サイト。 興味を持った応募者は、このサイトに移動して、履歴書を送信します。|  
  
## <a name="feature-summary"></a>機能の概要  
 このサンプルでの各機能の使用方法を次の表に示します。  
  
|機能|説明|Project|  
|-------------|-----------------|-------------|  
|フローチャート|ビジネス プロセスがフローチャートとして表されます。 このフローチャートの説明では、業務時にプロセスがホワイトボードに描画されるのと同じ方法でプロセスが表されます。|HiringRequestService|  
|ワークフロー サービス|プロセスの定義を持つフローチャートは、サービスでホストされます (この例では、サービスはコンソール アプリケーションでホストされます)。|HiringRequestService|  
|メッセージング アクティビティ|フローチャートでは、次の 2 つの方法でメッセージング アクティビティが使用されます。<br /><br /> - ユーザーから情報を取得する(各承認ステップで決定と関連情報を受け取る)。<br />- 他の既存のサービス (受信トレイサービスおよび OrgDataService、サービス参照を通じて使用) と対話する。|HiringRequestService|  
|コンテンツ・ベースの相関|雇用要求の ID プロパティにおける承認メッセージ相関関係は次のとおりです。<br /><br /> - プロセスが開始されると、相関ハンドルは要求の ID で初期化されます。<br />- 受信承認メッセージは、その ID に関連付けられます (各承認メッセージの最初のパラメーターは、要求の ID です)。|HiringRequestService / ResumeRequestService|  
|カスタム アクティビティ (宣言型およびコード ベース)|このサンプルには、次の複数のカスタム アクティビティがあります。<br /><br /> -   `SaveActionTracking`: このアクティビティはカスタム<xref:System.Activities.Tracking.TrackingRecord>を出力します<xref:System.Activities.NativeActivityContext.Track%2A>(を使用)。 このアクティビティは、<xref:System.Activities.NativeActivity> を拡張する命令型コードを使用して作成されています。<br />-   `GetEmployeesByPositionTypes`: このアクティビティは、位置タイプ ID のリストを受け取り、Contoso でその職位を持つ人物のリストを返します。 このアクティビティは、宣言的に作成されています (アクティビティ デザイナーを使用)。<br />-   `SaveHiringRequestInfo`: このアクティビティは、 の`HiringRequest`情報を`HiringRequestRepository.Save`保存します ( を使用します)。 このアクティビティは、<xref:System.Activities.CodeActivity> を拡張する命令型コードを使用して作成されています。|HiringRequestService|  
|システムで指定された SQL サーバー永続性|Flowchart プロセス定義をホストする<xref:System.ServiceModel.Activities.WorkflowServiceHost> インスタンスは、システムで指定された SQL サーバー永続性を使用するように構成されています。|HiringRequestService / ResumeRequestService|  
|カスタム追跡|このサンプルには、`HiringRequestProcess` の履歴を保存するカスタム追跡参加要素が含まれています (これによって、アクションの内容、実行者、および時期が記録されます)。 ソース コードは、HiringRequestService の Tracking フォルダーにあります。|HiringRequestService|  
|ETW 追跡|システムで指定された ETW 追跡は、HiringRequestService サービスの App.config ファイルで設定されます。|HiringRequestService|  
|アクティビティの構成|プロセス定義では、<xref:System.Activities.Activity> のフリー コンポジションが使用されます。 Flowchart には、その他のアクティビティなどを同時に含んでいる複数の Sequence アクティビティと Parallel アクティビティが含まれています。|HiringRequestService|  
|並列アクティビティ|-   <xref:System.Activities.Statements.ParallelForEach%601>は、CEO と人事部長の受信ボックスに同時に登録するために使用されます (2 人の人事マネージャーの承認ステップを待機しています)。<br />-   <xref:System.Activities.Statements.Parallel>は、完了および却下されたステップでクリーンアップタスクを実行するために使用されます。|HiringRequestService|  
|モデルの取り消し|フローチャートでは、<xref:System.Activities.Statements.CancellationScope> を使用して、取り消し動作を作成します (この場合、一部のクリーンアップが実行されます)。|HiringRequestService|  
|カスタマー永続参加要素|`HiringRequestPersistenceParticipant` は、ワークフロー変数のデータを Contoso HR データベースに保存されているテーブルに保存します。|HiringRequestService|  
|ワークフロー サービス|`ResumeRequestService` は、ワークフロー サービスを使用して実装されます。 ワークフロー定義とサービス情報は、ResumeRequestService.xamlx に含まれています。 サービスは、永続性と追跡を使用するように構成されます。|ResumeRequestService|  
|永続的なタイマー|`ResumeRequestService` は、永続的なタイマーを使用して、求人の期間を定義します (タイムアウトになると、求人は終了します)。|ResumeRequestService|  
|トランザクション|<xref:System.Activities.Statements.TransactionScope> は、複数のアクティビティの実行時にデータの一貫性を保つために使用されます (新しい履歴書の受信時)。|ResumeRequestService|  
|トランザクション|カスタムの永続参加要素 (`HiringRequestPersistenceParticipant`) とカスタムの追跡参加要素 (`HistoryFileTrackingParticipant`) では、同じトランザクションを使用します。|HiringRequestService|  
|ASP.NET[!INCLUDE[wf1](../../../../includes/wf1-md.md)]アプリケーションでの使用。|ワークフローには、2 つのASP.NETアプリケーションからアクセスできます。|InternalClient / CareersWebSite|  
  
## <a name="data-storage"></a>データ ストレージ  
 データは、`ContosoHR` という名前の SQL Server データベースに保存されます (このデータベースを作成するためのスクリプトは `DbSetup` フォルダーにあります)。 ワークフロー インスタンスは `InstanceStore` という名前の SQL Server データベースに保存されます (インスタンス ストアを作成するためのスクリプトは [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] の配布に含まれています)。  
  
 どちらのデータベースも、Visual Studio の開発者コマンド プロンプトから Setup.cmd スクリプトを実行して作成します。  
  
## <a name="running-the-sample"></a>サンプルの実行  
  
#### <a name="to-create-the-databases"></a>データベースを作成するには  
  
1. Visual Studio の開発者コマンド プロンプトを開きます。  
  
2. サンプル フォルダーに移動します。  
  
3. Setup.cmd を実行します。  
  
4. 2 つのデータベース (`ContosoHR` と `InstanceStore`) が SQL Express に作成されたことを確認します。  
  
#### <a name="to-set-up-the-solution-for-execution"></a>ソリューションの実行を設定するには  
  
1. Visual Studio を管理者として実行します。 HiringRequest.sln を開きます。  
  
2. **ソリューション エクスプローラ**でソリューションを右クリックし、[**プロパティ]** を選択します。  
  
3. **オプションの複数のスタートアップ プロジェクト**を選択し、キャリア Web**サイト**、**内部クライアント**、**雇用要求サービス**、および**再開要求サービス**を**開始**に設定します。 **ContosoHR**、**受信トレイサービス**、および**組織サービス**を [なし] のままにします。  
  
4. Ctrl キーと Shift キーを押しながら B キーを押して、ソリューションをビルドします。 ビルドが成功したことを確認します。  
  
#### <a name="to-run-the-solution"></a>ソリューションを実行するには  
  
1. デバッグを行わない場合は、ソリューションのビルド後、Ctrl キーを押しながら F5 キーを押してソリューションを実行します。 すべてのサービスが開始されたことを確認します。  
  
2. ソリューションの**内部クライアント**を右クリックし、[**ブラウザーで表示**] を選択します。 `InternalClient` の既定のページが表示されます。 サービスが実行中であることを確認し、リンクをクリックします。  
  
3. **採用依頼モジュール**が表示されます。 詳細については、以下のシナリオを参照してください。  
  
4. `HiringRequest` が完了すると、`ResumeRequest` を開始できます。 詳細については、以下のシナリオを参照してください。  
  
5. `ResumeRequest` は、投稿されると、パブリック Web サイト (Contoso Careers Web サイト) で使用可能になります。 求人を確認するには (さらに、応募するには)、Careers Web サイトに移動します。  
  
6. ソリューションで **[キャリア Web サイト**] を右クリックし、[**ブラウザーで表示]** を選択します。  
  
7. に戻るには、`InternalClient`ソリューションで**InternalClient**を右クリックし、[**ブラウザで表示]** を選択します。  
  
8. [受信トレイ] トップ メニューの [**求人情報**] リンクをクリックして、[**求**人情報] セクションに移動します。 詳細については、以下のシナリオを参照してください。  
  
## <a name="scenarios"></a>シナリオ  
  
### <a name="hiring-request"></a>雇用要求  
  
1. Michael Alexander (ソフトウェア エンジニア) は、エンジニアリング部において、C# の分野で 3 年以上の実務経験を持つ SDET (Software Engineer in Test) を採用するための新たな求人を要求します。  
  
2. 作成後、リクエストはマイケルの受信トレイに表示されます (要求が表示されない場合は **[更新**] をクリックします)。  
  
3. ピーターはマイケルの要求に基づいて行動したいと考えています。 Peter は、この職種で要求される C# の実務経験は 3 年ではなく 5 年であると考え、その旨を知らせるコメントを送信します。  
  
4. マイケルは上司からの受信トレイにメッセージを見て行動したいと考えています。マイケルはポジションリクエストの歴史を見て、ピーターに同意します。 Michael は、求人要求の C# の実務経験に関する説明を 5 年に変更し、その変更を受け入れます。  
  
5. ピーターはマイケルの変更された要求に基づいて行動し、それを受け入れます。 ここで、要求は、エンジニアリング部長 Tsvi Reiter の承認が必要になります。  
  
6. Tsvi Reiter は、要求に多くの時間をかけることができないため、要求が緊急であることと、この要求を受け入れることをコメントします。  
  
7. ここで、要求は、2 人の HR マネージャーまたは CEO の承認が必要になります。 CEO である Brian Richard Goldstein は Tsvi による緊急要求を確認します。 Brian Richard Goldstein は、これを受け入れ、2 人の HR マネージャーによる承認を省略して、要求に対応します。  
  
8. リクエストはマイケルの受信トレイから削除され、SDETを雇うプロセスが開始されました。  
  
### <a name="start-resume-request"></a>履歴書の要求の開始  
  
1. これで、仕事の位置は、ユーザーが応募できる外部 Web サイトに転記されるのを待機しています **([求人情報**] リンクをクリックして表示されます)。 現在、この求人は、求人を決定して掲載する HR 担当者の最終判断を待っている状態です。  
  
2. HR は、60 分のタイムアウト (実際の場合は数日または数週間) を設定して、(**編集**リンクをクリックして)このジョブポジションを編集したいと考えています。 タイムアウトによって、求人は指定時間に従い外部 Web サイトに掲載されます。  
  
3. 編集したジョブの位置を保存すると、[**受信再開**] タブに表示されます (Web ページを更新して新しいジョブの位置を表示します)。  
  
### <a name="collecting-resumes"></a>履歴書の収集  
  
1. 求人は外部の Web サイトに提示されています。 求人の応募に興味がある人は、この求人に応募するために履歴書を送信することができます。  
  
2. 求人情報一覧サービスに戻ると、これまでに収集した「履歴書を表示」することができます。  
  
3. また、HR は履歴書の募集を停止することもできます (適切な応募者が見つかった場合など)。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
  
1. 管理者特権で Visual Studio を実行していることを確認します。  
  
2. ソリューションをビルドできない場合は、次の項目を確認してください。  
  
    - または`CareersWebSite`プロジェクト`ContosoHR`からの`InternalClient`参照が見つかりません。  
  
3. ソフトウェアを実行できない場合は、次の項目を確認してください。  
  
    1. すべてのサービスが実行中である。  
  
    2. サービス参照が更新されている。  
  
        1. App_WebReferences フォルダーを開きます。  
  
        2. **[Contoso]** を右クリックし **、[Web/サービス参照の更新**] を選択します。  
  
        3. Visual Studio で Ctrl キーを押しながら Shift キーを押しながら B キーを押してソリューションを再構築します。  
  
## <a name="uninstalling"></a>アンインストール  
  
1. DbSetup フォルダーにある Cleanup.bat を実行して SQL Server インスタンス ストアを削除します。  
  
2. ハード ドライブからソース コードを削除します。
