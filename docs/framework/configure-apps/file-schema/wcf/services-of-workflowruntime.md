---
title: <services> の <workflowRuntime>
ms.date: 03/30/2017
ms.assetid: 219a05b1-f573-45c9-849b-e86bc373b62f
ms.openlocfilehash: 1106a9c62f4b57a2a695343c26879b2adf0934de
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2020
ms.locfileid: "61758172"
---
# <a name="services-of-workflowruntime"></a>\<services> の \<workflowRuntime>
<xref:System.Workflow.Runtime.WorkflowRuntime> エンジンに追加されるサービスのコレクションを表します。 要素は、<xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement> 型です。  コレクションで指定されたサービスはワークフロー ランタイム エンジンによって初期化され、適切な <xref:System.Workflow.Runtime.WorkflowRuntime> コンストラクターが呼び出されるとワークフロー ランタイム エンジンのサービスに追加されます。 したがって、コレクションで指定されたサービスは、そのコンストラクターのシグネチャに関して一定の規則に従う必要があります。 詳細については、「<xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Workflow.Runtime.WorkflowRuntime>
- <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>
- <xref:System.Workflow.Runtime.WorkflowRuntime>
- [ワークフロー構成ファイル](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms732240(v=vs.90))
