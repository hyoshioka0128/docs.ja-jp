---
title: WorkflowInstanceId の取得
ms.date: 03/30/2017
ms.assetid: bd7eea3b-1c28-4b84-9a67-003bc553aa81
ms.openlocfilehash: 8cb83fcf15b814b0ca6f7f95f1a9b8eec70185cb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79142733"
---
# <a name="get-workflowinstanceid"></a>WorkflowInstanceId の取得
このサンプルでは、カスタム アクティビティ `GetWorkflowInstanceId` を使用して、ワークフロー インスタンス ID を返す方法を示します。  
  
## <a name="demonstrates"></a>対象  
 カスタム アクティビティの開発、ワークフロー インスタンスにアクセスする方法。  
  
## <a name="discussion"></a>ディスカッション  
 実行中のワークフローのインスタンス ID を取得するには、コードを記述する必要があります。 完全な宣言型のワークフローを記述する場合は、ワークフロー インスタンス ID を返すことができるアクティビティが必要です。そのアクティビティをワークフローで参照することで、完全な宣言型のワークフローを作成できるようになります。 多くのシナリオで、インスタンス ID へのアクセスが必要になります。例としては、ログ記録または監査のためや、後で連携できるようにインスタンス ID をクライアントに返送する (たとえば、SendReply アクティビティ内でこのアクティビティを使用する) ことでアプリケーション レベルの関連付けを行うためなどが挙げられます。  
  
 `GetWorkflowInstanceId` は、<xref:System.Activities.CodeActivity%601> 型の値を返す必要があり、ワークフローのインスタンス ID を取得するために <xref:System.Guid> にアクセスできる必要があるので、<xref:System.Activities.CodeActivityContext> として実装されます。 この実装は非常に基本的なものです。  
  
```csharp  
public sealed class GetWorkflowInstanceId : CodeActivity<Guid>  
{  
    protected override Guid Execute(CodeActivityContext context)  
    {  
        return context.WorkflowInstanceId;  
    }  
}
```  
  
> [!IMPORTANT]
> サンプルは、既にコンピューターにインストールされている場合があります。 続行する前に、次の (既定の) ディレクトリを確認してください。  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> このディレクトリが存在しない場合は[、.NET Framework 4 の Windows コミュニケーション ファウンデーション (WCF) および Windows ワークフローファウンデーション (WF) サンプル](https://www.microsoft.com/download/details.aspx?id=21459)に移動して、すべての Windows 通信基盤 (WCF) とサンプルを[!INCLUDE[wf1](../../../../includes/wf1-md.md)]ダウンロードします。 このサンプルは、次のディレクトリに格納されます。  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\GetWorkflowInstanceId`
