---
ms.openlocfilehash: daf09748e69e70ad982bcee14461b66579f3bb87
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614863"
---
### <a name="avoiding-endless-recursion-for-iworkflowinstancemanagementtransactedcancel-and-iworkflowinstancemanagementtransactedterminate"></a>IWorkflowInstanceManagement.TransactedCancel および IWorkflowInstanceManagement.TransactedTerminate の無限再帰の回避

#### <a name="details"></a>説明

<xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedCancel%2A?displayProperty=nameWithType> または <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement.TransactedTerminate%2A?displayProperty=nameWithType> API を使用してワークフロー サービス インスタンスを取り消すか終了するとき、状況によっては、`Workflow` ランタイムが要求の処理の一部としてサービス インスタンスの永続化を試みるときの無限再帰のために、ワークフロー インスタンスでスタック オーバーフローが発生する可能性があります。 問題は、別のサービスに対する他の未処理 WCF 要求が完了するのをワークフロー インスタンスが待機している状態の場合に発生します。 `TransactedCancel` および `TransactedTerminate` 操作により、ワークフロー サービス インスタンスのキューに登録される作業項目が作成されます。 これらの作業項目は、`TransactedCancel/TransactedTerminate` 要求の処理の一部としては実行されません。 ワークフロー サービス インスタンスは他の未処理 WCF 要求が完了するのを待ってビジー状態であるため、作成された作業項目はキューに残ります。 `TransactedCancel/TransactedTerminate` 操作が完了して、クライアントに制御が返されます。 `TransactedCancel/TransactedTerminate` 操作に関連付けられているトランザクションは、コミットしようとした場合、ワークフロー サービス インスタンスの状態を永続化する必要があります。 しかし、インスタンスには未処理の `WCF` 要求があるため、ワークフロー ランタイムはワークフロー サービス インスタンスを永続化できず、無限再帰ループによってスタックがオーバーフローします。`TransactedCancel` と `TransactedTerminate` はメモリ内にのみ作業項目を作成するので、トランザクションが存在してもまったく影響ありません。 トランザクションのロールバックは作業項目を破棄しません。この問題に対処するため、.NET Framework 4.7.2 以降では、ワークフロー サービスの `web.config/app.config` に追加できる `AppSetting` が導入されています。これは、`TransactedCancel` および `TransactedTerminate` のトランザクションを無視するようにサービスに指示します。 これにより、ワークフロー インスタンスの永続化を待たずにトランザクションをコミットできます。 この機能の AppSetting には、`microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate` という名前が付けられています。 値 `true` はトランザクションを無視することを示し、したがってスタック オーバーフローが回避されます。 この AppSetting の既定値は `false` なので、既存のワークフロー サービス インスタンスに影響はありません。

#### <a name="suggestion"></a>提案される解決策

AppFabric または別の <xref:System.ServiceModel.Activities.IWorkflowInstanceManagement> クライアントを使っていて、ワークフロー インスタンスを取り消すか終了しようとするとワークフロー サービス インスタンスでスタック オーバーフローが発生する場合は、ワークフロー サービスの web.config/app.config ファイルの `<appSettings>` セクションに以下を追加できます。

<pre><code class="lang-xml">&lt;add key=&quot;microsoft:WorkflowServices:IgnoreTransactionsForTransactedCancelAndTransactedTerminate&quot; value=&quot;true&quot;/&gt;&#13;&#10;</code></pre>

この問題が発生しない場合は、これを行う必要はありません。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
