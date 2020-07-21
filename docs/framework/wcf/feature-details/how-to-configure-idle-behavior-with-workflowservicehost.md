---
title: '方法: WorkflowServiceHost を使用してアイドル動作を構成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1bb93652-d687-46ff-bff6-69ecdcf97437
ms.openlocfilehash: 8b9fa36408d5f2bc5445ebeccba61f71417935e7
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84599127"
---
# <a name="how-to-configure-idle-behavior-with-workflowservicehost"></a>方法: WorkflowServiceHost を使用してアイドル動作を構成する
ワークフローは、外部からの働きかけによって再開される必要があるブックマークに遭遇すると、アイドル状態になります。たとえば、 <xref:System.ServiceModel.Activities.Receive> アクティビティを使用して配信されるメッセージをワークフローが待機している場合などです。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> は、サービス インスタンスがアイドル状態になってから、インスタンスが永続化またはアンロードされるまでの時間を指定できる動作です。 これには、これらの時間の範囲を設定する 2 つのプロパティがあります。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> は、ワークフロー サービス インスタンスがアイドル状態になってから、そのワークフロー サービス インスタンスが永続化されるまでの時間の範囲を指定します。 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> は、ワークフロー サービス インスタンスがアイドル状態になってから、そのワークフロー サービス インスタンスがアンロードされるまでの時間の範囲を指定します。アンロードとは、インスタンスをインスタンス ストアに永続化し、メモリから削除することを意味します。 このトピックでは、 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> を構成ファイルで構成する方法について説明します。  
  
### <a name="to-configure-workflowidlebehavior"></a>WorkflowIdleBehavior を構成するには  
  
1. `workflowIdle` `behavior` 次の例に示すように、<> 要素内の <> 要素に <> 要素を追加し `serviceBehaviors` ます。  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="">  
          <workflowIdle timeToUnload="0:05:0" timeToPersist="0:04:0"/>
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
     `timeToUnload` 属性は、ワークフロー サービス インスタンスがアイドル状態になってから、そのワークフロー サービス インスタンスがアンロードされるまでの時間の範囲を指定します。 `timeToPersist` 属性は、ワークフロー サービス インスタンスがアイドル状態になってから、そのワークフロー サービス インスタンスが永続化されるまでの時間の範囲を指定します。 `timeToUnload` の既定値は 1 分です。 `timeToPersist` の既定値は <xref:System.TimeSpan.MaxValue> です。 インスタンスをメモリ内でアイドル状態を保ちながら信頼性を保持する場合、 `timeToPersist` < `timeToUnload`です。 アイドル状態のインスタンスがアンロードされないようにするには、 `timeToUnload` を <xref:System.TimeSpan.MaxValue>に設定します。 の詳細について <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> は、「[ワークフローサービスホストの機能拡張](workflow-service-host-extensibility.md)」を参照してください。  
  
    > [!NOTE]
    > 前の構成サンプルでは、簡略化された構成を使用しています。 詳細については、「簡略化された[構成](../simplified-configuration.md)」を参照してください。  
  
### <a name="to-change-idle-behavior-in-code"></a>コードのアイドル動作を変更するには  
  
- 次の例では、プログラムによって永続化とアンロードを行う前に待機する時間を変更します。  
  
     [!code-csharp[Wf_SvcHost_Idle_persist#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/wf_svchost_idle_persist/cs/source.cs#1)]
     [!code-vb[Wf_SvcHost_Idle_persist#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/wf_svchost_idle_persist/vb/source.vb#1)]  
  
## <a name="see-also"></a>関連項目

- [ワークフロー サービス ホストの拡張機能](workflow-service-host-extensibility.md)
- [簡略化された構成](../simplified-configuration.md)
- [ワークフロー サービス](workflow-services.md)
