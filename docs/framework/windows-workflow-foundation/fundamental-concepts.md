---
title: Windows Workflow の基本概念
description: この記事では、一部の開発者にとってなじみのない .NET Framework 4.6.1 のワークフロー開発における概念の一部について説明します。
ms.date: 03/30/2017
ms.assetid: 0e930e80-5060-45d2-8a7a-95c0690105d4
ms.openlocfilehash: 07498241280191fb62a35a559a3391f7148c05b9
ms.sourcegitcommit: 9a4488a3625866335e83a20da5e9c5286b1f034c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2020
ms.locfileid: "83419890"
---
# <a name="fundamental-windows-workflow-concepts"></a>Windows Workflow の基本概念
[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] のワークフロー開発で使用される概念は、一部の開発者には不慣れなことも考えられます。 ここでは、そのいくつかの概念について、内容と実装方法を説明します。  
  
## <a name="workflows-and-activities"></a>ワークフローとアクティビティ  
 ワークフローは、プロセスをモデル化するアクションの構造化されたコレクションです。 ワークフローの各アクションは、アクティビティとしてモデル化されます。 ホストがワークフローとのやり取りを行う場合、メソッドと同じようにワークフローを呼び出すときは <xref:System.Activities.WorkflowInvoker> が、1 つのワークフロー インスタンスの実行を明示的に制御するときは <xref:System.Activities.WorkflowApplication> が、インスタンスが複数のシナリオでメッセージ ベースのやり取りを行うときは <xref:System.ServiceModel.WorkflowServiceHost> が使用されます。 ワークフローの手順はアクティビティの階層として定義されるため、階層の最上位のアクティビティはワークフローそのものを定義すると言えます。 この階層モデルは、前のバージョンの明示的な `SequentialWorkflow` クラスおよび `StateMachineWorkflow` クラスの代わりになります。 アクティビティ自体は、他のアクティビティの集まりとして (ベースとして <xref:System.Activities.Activity> クラスを使用。通常は XAML を使用して定義されます)、データ アクセスにランタイムを使用できる <xref:System.Activities.CodeActivity> クラスを使用して作成されるカスタムとして、またはワークフロー ランタイムの範囲をアクティビティの作成者に提示する <xref:System.Activities.NativeActivity> クラスを使用して開発されます。 <xref:System.Activities.CodeActivity> クラスおよび <xref:System.Activities.NativeActivity> クラスを使用して開発されるアクティビティは、C# などの CLR 準拠の言語を使用して作成されます。  
  
## <a name="activity-data-model"></a>アクティビティ データ モデル  
 アクティビティは、次の表に示すタイプを使用してデータを格納および共有します。  
  
|||  
|-|-|  
|変数|データをアクティビティに格納します。|  
|引数|データをアクティビティに移動したり、アクティビティから移動したりします。|  
|正規表現|引数のバインディングで使用される、昇格された戻り値を持つアクティビティです。|  
  
## <a name="workflow-runtime"></a>ワークフロー ランタイム  
 ワークフロー ランタイムはワークフローが実行される環境です。 <xref:System.Activities.WorkflowInvoker> はワークフローを実行する最も単純な方法です。 ホストは、次の処理に <xref:System.Activities.WorkflowInvoker> を使用します。  
  
- ワークフローの同期呼び出しを実行する。  
  
- ワークフローに入力を行ったり、ワークフローから出力を取り出したりする。  
  
- アクティビティによって使用される拡張機能を追加する。  
  
 <xref:System.Activities.ActivityInstance> は、ホストがランタイムとのやり取りに使用できるスレッドセーフなプロキシです。 ホストは、次の処理に <xref:System.Activities.ActivityInstance> を使用します。  
  
- インスタンスを作成するか、インスタンス ストアから読み込んで、インスタンスを取得する。  
  
- インスタンスのライフサイクル イベントが通知されるようにする。  
  
- ワークフローの実行を制御する。  
  
- ワークフローに入力を行ったり、ワークフローから出力を取り出したりする。  
  
- ワークフローの継続を通知し、値をワークフローに渡す。  
  
- ワークフローのデータを永続化する。  
  
- アクティビティによって使用される拡張機能を追加する。  
  
 アクティビティは、<xref:System.Activities.ActivityContext> または <xref:System.Activities.NativeActivityContext> などの、適切な <xref:System.Activities.CodeActivityContext> 派生クラスを使用してワーク フローのランタイム環境にアクセスできます。 これらの要素がこのクラスを使用する目的は、引数や変数の解決や子アクティビティのスケジュール設定など、多岐にわたります。  
  
## <a name="services"></a>サービス  
 ワークフローは、メッセージング アクティビティを使用して疎結合サービスの実装およびアクセスを行う、無理のない方法です。 メッセージングアクティビティは WCF 上に構築されており、ワークフローとの間でデータを取得するために使用される主要なメカニズムです。 任意の種類のメッセージ交換パターンをモデル化するため、複数のメッセージング アクティビティを共に作成できます。 詳細については、「[メッセージングアクティビティ](../wcf/feature-details/messaging-activities.md)」を参照してください。 ワークフロー サービスは <xref:System.ServiceModel.Activities.WorkflowServiceHost> クラスを使用してホストされます。 詳細については、「[ワークフローサービスのホスティングの概要](../wcf/feature-details/hosting-workflow-services-overview.md)」を参照してください。 ワークフローサービスの詳細については、「[ワークフローサービス](../wcf/feature-details/workflow-services.md)」を参照してください。  
  
## <a name="persistence-unloading-and-long-running-workflows"></a>永続性、アンロード、実行時間の長いワークフロー  
 Windows Workflow は次の機能により、実行時間の長いリアクティブなプログラムの作成を簡素化しています。  
  
- 外部入力にアクセスするアクティビティ  
  
- ホストのリスナーが再開できる <xref:System.Activities.Bookmark> オブジェクトを作成する機能  
  
- ワークフローのデータを永続化してワークフローをアンロードした後、特定のワークフローでの <xref:System.Activities.Bookmark> オブジェクトの再開に反応してワークフローを再読み込みおよび再アクティブ化する機能  
  
 ワークフローは、実行するアクティビティがなくなるか、現在の実行中のすべてのアクティビティが入力を待機するまで、アクティビティを継続して実行します。 後者の場合、ワークフローはアイドル状態になります。 ホストでは、アイドル状態になったワークフローをアンロードし、メッセージが到着したときに実行を継続するためのワークフローを再読み込みすることは一般的です。 <xref:System.ServiceModel.Activities.WorkflowServiceHost> によって、この機能が実現されるほか、拡張可能なアンロード ポリシーを使用できます。 揮発性状態のデータまたは永続化できない他のデータを使用する実行ブロックの場合、アクティビティは <xref:System.Activities.NoPersistHandle> を使用して永続化すべきではないホストを指定できます。 また、ワークフローは <xref:System.Activities.Statements.Persist> アクティビティを使用して、そのデータを永続ストレージ メディアに永続化することもできます。
