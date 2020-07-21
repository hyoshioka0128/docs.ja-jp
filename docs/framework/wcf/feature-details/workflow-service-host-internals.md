---
title: ワークフロー サービス ホストの内部
ms.date: 03/30/2017
ms.assetid: af44596f-bf6a-4149-9f04-08d8e8f45250
ms.openlocfilehash: 7b47293211ee8143b1ce713c64ff1d5b22161b45
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84594882"
---
# <a name="workflow-service-host-internals"></a>ワークフロー サービス ホストの内部
<xref:System.ServiceModel.WorkflowServiceHost> では、ワークフロー サービスのホストが提供されます。 これにより、受信メッセージをリッスンして、該当するワークフロー サービス インスタンスにルーティングし、アイドル状態のワークフローのアンロードおよび永続化を制御できます。 このトピックでは、WorkflowServiceHost がどのように受信メッセージを処理するかについて説明します。  
  
## <a name="workflowservicehost-overview"></a>WorkflowServiceHost の概要  

<xref:System.ServiceModel.WorkflowServiceHost> クラスは、ワークフロー サービスをホストするために使用されます。 このクラスは、受信メッセージをリッスンして、該当するサービス インスタンスにルーティングし、必要に応じて、新しいインスタンスを作成するか、永続ストレージから既存のインスタンスを読み込みます。 次の図は、の機能の概要を示してい <xref:System.ServiceModel.WorkflowServiceHost> ます。
  
 ![ワークフローサービスホストの概要を示す図。](./media/workflow-service-host-internals/workflow-service-host-high-level-overview.gif)  
  
 この図では、<xref:System.ServiceModel.WorkflowServiceHost> は .xamlx ファイルからワークフロー サービス定義を読み込み、構成ファイルから構成情報を読み込みます。 また、追跡プロファイルから追跡構成を読み込みます。 <xref:System.ServiceModel.WorkflowServiceHost> によって、ワークフロー インスタンスへの制御操作の送信を可能にするワークフロー コントロール エンドポイントが公開されます。  詳細については、「[ワークフローコントロールエンドポイントのサンプル](workflow-control-endpoint.md)」を参照してください。  
  
 <xref:System.ServiceModel.WorkflowServiceHost> によって、受信アプリケーション メッセージをリッスンするアプリケーション エンドポイントも公開されます。 受信メッセージが到着すると、該当するワークフロー サービス インスタンスに送られます (現在読み込み中の場合)。 必要に応じて、新しいワークフロー インスタンスが作成されます。 既存のインスタンスが永続化されている場合は、永続ストアから読み込まれます。  
  
## <a name="workflowservicehost-details"></a>WorkflowServiceHost の詳細  
 次の図は、がメッセージを少し詳しく処理する方法を示してい <xref:System.ServiceModel.WorkflowServiceHost> ます。  
  
 ![ワークフローサービスホストのメッセージフローを示す図。](./media/workflow-service-host-internals/workflow-service-host-message-flow.gif)  
  
 この図には、3 つの異なるエンドポイント (アプリケーション エンドポイント、ワークフロー コントロール エンドポイント、およびワークフローをホストするエンドポイント) が示されています。 アプリケーション エンドポイントは、特定のワークフロー インスタンスにバインドされたメッセージを受信します。 ワークフロー コントロール エンドポイントは、制御操作をリッスンします。 ワークフローをホストするエンドポイントは、<xref:System.ServiceModel.WorkflowServiceHost> がサービス以外のワークフローを読み込んで実行するためのメッセージをリッスンします。 この図が示すように、すべてのメッセージは、WCF ランタイム中に処理されます。  ワークフロー サービス インスタンスの調整は、<xref:System.ServiceModel.Description.ServiceThrottlingBehavior.MaxConcurrentInstances%2A> プロパティを使用して実現されます。 このプロパティは、同時ワークフロー サービス インスタンスの数を制限します。 この調整を超過すると、新しいワークフロー サービス インスタンスの追加要求または永続化されたワークフロー インスタンスのアクティブ化の要求がキューに置かれます。 キューに置かれた要求は、新規インスタンスと実行中の永続化されたインスタンスのどちらに対するものであるかにかかわらず、FIFO 順で処理されます。 未処理の例外の処理方法およびアイドル状態のワークフロー サービスのアンロードおよび永続化方法を指定するホスト ポリシー情報が読み込まれます。 これらのトピックの詳細については、「[方法: workflowservicehost を使用してワークフローの未処理の例外動作を構成する](config-workflow-unhandled-exception-workflowservicehost.md)」および「[方法: workflowservicehost を使用してアイドル動作を構成](how-to-configure-idle-behavior-with-workflowservicehost.md)する」を参照してください。 ワークフロー インスタンスは、ホスト ポリシーに従って永続化され、必要に応じて再度読み込まれます。 ワークフローの永続化の詳細については、「[方法: WorkflowServiceHost を使用](how-to-configure-persistence-with-workflowservicehost.md)して永続化を構成する」、「[実行時間の長いワークフローサービスの作成](creating-a-long-running-workflow-service.md)」、および「[ワークフローの永続](../../windows-workflow-foundation/workflow-persistence.md)化」を参照してください。  
  
 次の図は、WorkflowServiceHost が呼び出されたときのフローを示しています。  
  
 ![WorkflowServiceHost が呼び出されたときのフローを示す図。](./media/workflow-service-host-internals/workflow-service-host-open.gif)  
  
 ワークフローが XAML から読み込まれ、アクティビティ ツリーが作成されます。 <xref:System.ServiceModel.WorkflowServiceHost> は、アクティビティ ツリーに従い、サービスの記述を作成します。 構成がホストに適用されます。 最後に、ホストは受信メッセージのリッスンを開始します。  
  
 次の図は、 <xref:System.ServiceModel.WorkflowServiceHost> CanCreateInstance がに設定されている Receive アクティビティにバインドされたメッセージを受信したときの動作を示してい `true` ます。  
  
 ![WFS ホストがメッセージを受信し、CanCreateInstance が true の場合に使用されるデシジョンツリー。](./media/workflow-service-host-internals/workflow-service-host-receive-message-cancreateinstance.gif)  
  
 メッセージが到着し、WCF チャネル スタックによって処理されます。 スロットルがチェックされ、関連付けクエリが実行されます。 既存のインスタンスにバインドされているメッセージは配信されます。 新しいインスタンスを作成する必要がある場合は、Receive アクティビティの CanCreateInstance プロパティが確認されます。 true に設定されている場合、新しいインスタンスが作成され、メッセージが配信されます。  
  
 次の図は、CanCreateInstance が false に設定された場合の Receive アクティビティにバインドされたメッセージを受信したときの <xref:System.ServiceModel.WorkflowServiceHost> の動作を示しています。  
  
 ![WFS ホストがメッセージを受信し、CanCreateInstance が false の場合に使用されるデシジョンツリー。](./media/workflow-service-host-internals/workflow-service-host-receive-message.gif)  
  
 メッセージが到着し、WCF チャネル スタックによって処理されます。 スロットルがチェックされ、関連付けクエリが実行されます。 メッセージが既存のインスタンスにバインドされている場合は (CanCreateInstance が false に設定されているため) インスタンスが永続ストアから読み込まれ、ブックマークが再開され、ワークフローが実行されます。  
  
> [!WARNING]
> SQL Server が NamedPipe プロトコルでのみリッスンするように設定されている場合、ワークフロー サービス ホストは開きません。  
  
## <a name="see-also"></a>関連項目

- [ワークフロー サービス](workflow-services.md)
- [ワークフロー サービスのホスティング](hosting-workflow-services.md)
- [ワークフロー コントロール エンドポイント](workflow-control-endpoint.md)
- [方法: WorkflowServiceHost を使用してワークフロー サービスの未処理の例外動作を構成する](config-workflow-unhandled-exception-workflowservicehost.md)
- [長時間のワークフロー サービスの作成](creating-a-long-running-workflow-service.md)
- [ワークフローの永続性](../../windows-workflow-foundation/workflow-persistence.md)
