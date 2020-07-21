---
title: ワークフロー サービスのホストの概要
ms.date: 03/30/2017
ms.assetid: 19f3704f-06bf-4eeb-8724-5224e02d7ead
ms.openlocfilehash: 10ea35fc1988e1b3e6ceb44aca098e63bfc7d7e4
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84597294"
---
# <a name="hosting-workflow-services-overview"></a>ワークフロー サービスのホストの概要
ワークフロー サービスを実行するには、ホストされている必要があります。 <xref:System.ServiceModel.WorkflowServiceHost> は、複数のインスタンス、構成、および WCF メッセージングをサポートする標準ワークフロー ホストです (ワークフローはホストされるためにメッセージングを使用する必要はありません)。  また、一連のサービス動作を介して永続性、追跡、およびインスタンス コントロールを統合します。  WCF の <xref:System.ServiceModel.ServiceHost> と同様に、<xref:System.ServiceModel.WorkflowServiceHost> は任意のマネージド .NET アプリケーションでの自己ホスト、または IIS/WAS での Web ホスト (.xamlx ファイルとして) が可能です。  このセクションのトピックでは、ワークフロー サービスをホストする方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ワークフロー サービスのホスティング](hosting-workflow-services.md)  
 ワークフロー サービスのホスティングについて説明します。  
  
 [ワークフロー サービス ホストの内部](workflow-service-host-internals.md)  
 <xref:System.ServiceModel.WorkflowServiceHost> がどのように受信メッセージを処理するかについて説明します。  
  
 [ワークフロー サービス ホストの拡張機能](workflow-service-host-extensibility.md)  
 ワークフロー サービス ホストの機能を拡張する方法について説明します。  
  
 [ワークフロー コントロール エンドポイント](workflow-control-endpoint.md)  
 ワークフロー インスタンスを作成できるエンドポイントを定義する方法について説明します。
  
 [方法: Windows Server AppFabric を使用してワークフロー サービスをホストする](how-to-host-a-workflow-service-with-windows-server-app-fabric.md)  
 Windows Server AppFabric の既存のワークフロー サービスをホストする方法について説明します。  
  
 [WorkflowServiceHost の構成](configuring-workflowservicehost.md)  
 永続性、追跡、アイドル状態、および未処理の例外動作を制御する方法を説明します。  
  
## <a name="reference"></a>関連項目  
 <xref:System.ServiceModel.Activities.WorkflowServiceHost>  
  
 <xref:System.ServiceModel.Activities.WorkflowService>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactory>  
  
 <xref:System.ServiceModel.Activation.ServiceHostFactoryBase>  
  
 <xref:System.ServiceModel.Activation.WorkflowServiceHostFactory>  
  
## <a name="related-sections"></a>関連項目  
 [ワークフロー サービス](workflow-services.md)
