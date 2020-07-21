---
title: アクティビティ ライブラリ
ms.date: 03/30/2017
ms.assetid: 5323e9d4-71d6-47eb-bfa6-31feac62044d
ms.openlocfilehash: fae2a94b5e5e776625aa7f26700980640b66afd4
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142902"
---
# <a name="activity-library"></a>アクティビティ ライブラリ
このセクションには、Windows ワークフローファンデーション (WF) の高度なカスタム アクティビティを示すサンプルが含まれています。  
  
## <a name="in-this-section"></a>このセクションの内容

 [SendMail カスタム アクティビティ](sendmail-custom-activity.md)  
 <xref:System.Activities.AsyncCodeActivity> から派生するカスタム アクティビティを作成して、SMTP を使用して電子メールを送信し、ワークフロー アプリケーション内で使用する方法を示します。  
  
 [制限された並列 ForEach](throttled-parallel-foreach.md)  
 ph x="1" /&gt; アクティビティは、実行するコンカレンシー分岐の数を制限するためのコンカレンシー要因を設定できるという 1 つの例外を除き、<xref:System.Activities.Statements.ParallelForEach%601> アクティビティと似ていることについて示します。
  
 [データベース アクセス アクティビティ](database-access-activities.md)  
 データベースへのアクセスを許可するアクティビティを作成して、情報の取得や変更を行い[、ADO.NET](../../data/adonet/index.md)を使用してデータベースにアクセスできるようにする方法について説明します。  
  
 [.NET Framework 4.5 の外部化されたポリシー アクティビティ](externalized-policy-activity-in-net-framework-4-5.md)  
 外部化された Policy4 アクティビティにより、WF 3.5 に付属するルール エンジンを使用して、Windows ワークフロー<xref:System.Workflow.Activities.Rules.RuleSet>ファウンデーション[!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)](WF 4.5) の .NET Framework 3.5 (WF 3.5) オブジェクトで既存の Windows ワークフロー基盤を直接実行する方法を示します。
  
 [非ジェネリックの ForEach](non-generic-foreach.md)  
 <xref:System.Activities.Statements.ForEach%601> アクティビティの非ジェネリック バージョンを作成する方法を示します。  
  
 [非ジェネリックの ParallelForEach](non-generic-parallelforeach.md)  
 <xref:System.Activities.Statements.ParallelForEach%601> アクティビティの非ジェネリック バージョンを作成する方法を示します。  
  
 [WorkflowInstanceId の取得](get-workflowinstanceid.md)  
 カスタム アクティビティ `GetWorkflowInstanceId` を使用して、ワークフロー インスタンス ID を返す方法を示します。
