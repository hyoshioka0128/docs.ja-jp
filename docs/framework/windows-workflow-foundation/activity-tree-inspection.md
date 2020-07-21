---
title: アクティビティ ツリー検査
ms.date: 03/30/2017
ms.assetid: 100d00e4-8c1d-4233-8fbb-dd443a01155d
ms.openlocfilehash: 692f36d993c3f9c27839122b388a24d0698a2b59
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79183036"
---
# <a name="activity-tree-inspection"></a>アクティビティ ツリー検査
アクティビティ ツリー検査は、アプリケーションによってホストされるワークフローを検査するためにワークフロー アプリケーションの作成者によって使用されます。 <xref:System.Activities.WorkflowInspectionServices> を使用することによって、特定の子アクティビティを対象としてワークフローを検索したり、個々のアクティビティとそのプロパティを列挙したりできるほか、アクティビティのランタイム メタデータを特定の時点でキャッシュできます。 ここでは、<xref:System.Activities.WorkflowInspectionServices> の概要を説明します。また、これを使用してアクティビティ ツリーを検査する方法も説明します。  
  
## <a name="using-workflowinspectionservices"></a>WorkflowInspectionServices の使用  
 <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> メソッドは、指定したアクティビティ ツリーのアクティビティをすべて列挙するために使用されます。 <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> は、子、デリゲート ハンドラー、変数の既定値、引数の式を含む、ツリー内のすべてのアクティビティに接触する列挙可能なアクティビティを返します。 次の例では、ワークフロー定義は <xref:System.Activities.Statements.Sequence>、<xref:System.Activities.Statements.While>、<xref:System.Activities.Statements.ForEach%601>、<xref:System.Activities.Statements.WriteLine>、および式を使用して作成されます。 ワークフロー定義が作成されると、このワークフロー定義が呼び出されて、`InspectActivity` メソッドが呼び出されます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#45](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#45)]  
  
 アクティビティを列挙するために、<xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> がルート アクティビティで呼び出され、返される各アクティビティでもう一度再帰的に呼び出されます。 次の例では、アクティビティ ツリーのそれぞれのアクティビティと式の <xref:System.Activities.Activity.DisplayName%2A> がコンソールに書き込まれます。  
  
 [!code-csharp[CFX_WorkflowApplicationExample#46](~/samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#46)]  
  
 このサンプル コードから次の出力が得られます。  
  
 **リスト項目 1**  
**リスト アイテム 2**
**リスト アイテム 3**
**リスト アイテム 4**
**リスト アイテム 5**
**アイテムをコレクションに追加しました。**
**シーケンス****リテラル<リスト\<文字列>>**  
 **しばらくの間**  
 **コレクション文字列\<>**  
 **変数値<\<I コレクション文字列>>**  
 **ラムダ\<値文字列>**  
 **場所参照値<リスト\<文字列>>**  
 **ラムダ\<値ブール値>**  
 **場所参照値<リスト\<文字列>>**  
 **各\<文字列>**  
 **可変値<IEnumerable\<文字列>>**  
 **WriteLine**  
 **\<文字列>**  
 **シーケンス**  
 **WriteLine**  
 **リテラル\<文字列>** すべてのアクティビティを列挙するのではなく、<xref:System.Activities.WorkflowInspectionServices.Resolve%2A>特定のアクティビティを取得するために使用されます。 <xref:System.Activities.WorkflowInspectionServices.Resolve%2A> と <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> はいずれも、`WorkflowInspectionServices.CacheMetadata` が前に呼び出されていない場合にメタデータのキャッシュ処理を実行します。 <xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> が呼び出されている場合、<xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> は既存のメタデータに基づいています。 このため、<xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> を最後に呼び出した後でツリーが変更されていると、予期しない結果が <xref:System.Activities.WorkflowInspectionServices.GetActivities%2A> で生じることがあります。 呼び出し<xref:System.Activities.WorkflowInspectionServices.GetActivities%2A>後にワークフローに変更が加えられた場合は、メソッドを呼び出してメタデータ<xref:System.Activities.Validation.ActivityValidationServices><xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>を再キャッシュできます。 メタデータのキャッシュ処理については、次のセクションで説明します。  
  
### <a name="caching-metadata"></a>メタデータのキャッシュ処理  
 アクティビティのメタデータをキャッシュすると、アクティビティの引数、変数、子アクティビティ、アクティビティ デリゲートの記述が構築および検証されます。 既定では、メタデータはアクティビティが実行用に準備されるときにランタイムによってキャッシュされます。 ワークフロー ホストの作成者が、それよりも前 (すべてのコストを先に取得する場合など) にアクティビティまたはアクティビティ ツリーのメタデータをキャッシュする場合は、<xref:System.Activities.WorkflowInspectionServices.CacheMetadata%2A> を使用して目的の時点でメタデータをキャッシュできます。
