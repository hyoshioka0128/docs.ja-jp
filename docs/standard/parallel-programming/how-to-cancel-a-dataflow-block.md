---
title: '方法: データフロー ブロックをキャンセルする'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Task Parallel Library, dataflows
- dataflow blocks, canceling in TPL
- TPL dataflow library,canceling dataflow blocks
ms.assetid: fbddda0d-da3b-4ec8-a1d6-67ab8573fcd7
ms.openlocfilehash: 530c231deeaba007975849ab6dc41f4da6a859ea
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/02/2020
ms.locfileid: "84285548"
---
# <a name="how-to-cancel-a-dataflow-block"></a>方法: データフロー ブロックをキャンセルする
このドキュメントでは、アプリケーションでキャンセルを有効にする方法を示します。 この例では、Windows フォームを使用して、データフロー パイプラインで作業項目がアクティブである場所と、キャンセルの影響を示します。  

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]
  
## <a name="to-create-the-windows-forms-application"></a>Windows フォーム アプリケーションを作成するには  
  
1. C# または Visual Basic の **Windows フォーム アプリケーション** プロジェクトを作成します。 以降の手順では、プロジェクトの名前は `CancellationWinForms` とします。  
  
2. メイン フォーム Form1.cs (Visual Basic の Form1.vb) のフォーム デザイナーで、<xref:System.Windows.Forms.ToolStrip> コントロールを追加します。  
  
3. <xref:System.Windows.Forms.ToolStrip> コントロールに <xref:System.Windows.Forms.ToolStripButton> コントロールを追加します。 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> プロパティを <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text> に設定し、<xref:System.Windows.Forms.ToolStripItem.Text%2A> プロパティを「**作業項目の追加**」に設定します。  
  
4. <xref:System.Windows.Forms.ToolStrip> コントロールに 2 つ目の <xref:System.Windows.Forms.ToolStripButton> コントロールを追加します。 <xref:System.Windows.Forms.ToolStripItem.DisplayStyle%2A> プロパティを <xref:System.Windows.Forms.ToolStripItemDisplayStyle.Text> に、<xref:System.Windows.Forms.ToolStripItem.Text%2A> プロパティを「**キャンセル**」に、<xref:System.Windows.Forms.ToolStripItem.Enabled%2A> プロパティを `False` に設定します。  
  
5. 4 つの <xref:System.Windows.Forms.ToolStripProgressBar> コントロールを <xref:System.Windows.Forms.ToolStrip> コントロールに追加します。  
  
## <a name="creating-the-dataflow-pipeline"></a>データフロー パイプラインの作成  
 このセクションでは、作業項目を処理して進行状況バーを更新するデータフロー パイプラインを作成する方法を示します。  
  
### <a name="to-create-the-dataflow-pipeline"></a>データフロー パイプラインを作成するには  
  
1. プロジェクトで、System.Threading.Tasks.Dataflow.dll への参照を追加します。  
  
2. Form1.cs (Visual Basic の Form1.vb) に次の `using` ステートメント (Visual Basic では `Imports`) が含まれていることを確認します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#1)]
     [!code-vb[TPLDataflow_CancellationWinForms#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#1)]  
  
3. `Form1` クラスの内部の型として `WorkItem` クラスを追加します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#2)]
     [!code-vb[TPLDataflow_CancellationWinForms#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#2)]  
  
4. `Form1` クラスに次のデータ メンバーを追加します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#3)]
     [!code-vb[TPLDataflow_CancellationWinForms#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#3)]  
  
5. 次の `CreatePipeline` メソッドを `Form1` クラスに追加します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#4)]
     [!code-vb[TPLDataflow_CancellationWinForms#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#4)]  
  
 `incrementProgress` と `decrementProgress` のデータフロー ブロックはユーザー インターフェイスで機能するので、これらの操作をユーザー インターフェイス スレッドで実行することが重要です。 これを実現するため、構築時にこれらのオブジェクトは <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.TaskScheduler%2A> プロパティが <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> に設定された <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions> オブジェクトを提供します。 <xref:System.Threading.Tasks.TaskScheduler.FromCurrentSynchronizationContext%2A?displayProperty=nameWithType> メソッドは、現行の同期コンテキストで作業を実行する <xref:System.Threading.Tasks.TaskScheduler> オブジェクトを作成します。 `Form1` コンストラクターはユーザー インターフェイス スレッドから呼び出されるので、`incrementProgress` および `decrementProgress` データフロー ブロックに対するアクションも、ユーザー インターフェイス スレッドで実行されます。  
  
 この例では、パイプラインのメンバーを構築するときに <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> プロパティを設定します。 <xref:System.Threading.Tasks.Dataflow.DataflowBlockOptions.CancellationToken%2A> プロパティはデータフロー ブロックの実行を完全にキャンセルするので、ユーザーが操作をキャンセルした後にパイプラインにさらに作業項目を追加する場合は、すべてのパイプラインを作り直す必要があります。 操作をキャンセルした後も他の作業を実行できるようにデータフロー ブロックをキャンセルする方法もあります。例については、「[チュートリアル: Windows フォーム アプリケーションでのデータフローの使用](walkthrough-using-dataflow-in-a-windows-forms-application.md)」を参照してください。  
  
## <a name="connecting-the-dataflow-pipeline-to-the-user-interface"></a>ユーザー インターフェイスへのデータフロー パイプラインの接続  
 このセクションでは、ユーザー インターフェイスにデータフロー パイプラインを接続する方法を説明します。 パイプラインの作成とパイプラインへの作業項目の追加は、どちらも **[作業項目の追加]** ボタンのインベント ハンドラーによって制御されます。 キャンセルは **[キャンセル]** ボタンによって開始されます。 ユーザーがこのいずれかのボタンをクリックすると、適切な操作が非同期的に開始されます。  
  
### <a name="to-connect-the-dataflow-pipeline-to-the-user-interface"></a>ユーザー インターフェイスにデータフロー パイプラインを接続するには  
  
1. メイン フォームのフォーム デザイナーで、**[作業項目の追加]** ボタンの <xref:System.Windows.Forms.ToolStripItem.Click> イベントのイベント ハンドラーを作成します。  
  
2. **[作業項目の追加]** ボタンの <xref:System.Windows.Forms.ToolStripItem.Click> イベントを実装します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#5)]
     [!code-vb[TPLDataflow_CancellationWinForms#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#5)]  
  
3. メイン フォームのフォーム デザイナーで、**[キャンセル]** ボタンの <xref:System.Windows.Forms.ToolStripItem.Click> イベント ハンドラーのイベント ハンドラーを作成します。  
  
4. **[キャンセル]** ボタンの <xref:System.Windows.Forms.ToolStripItem.Click> イベント ハンドラーを実装します。  
  
     [!code-csharp[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#6)]
     [!code-vb[TPLDataflow_CancellationWinForms#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#6)]  
  
## <a name="example"></a>例  
 次の例は、Form1.cs (Visual Basic の Form1.vb) のコード全体を示しています。  
  
 [!code-csharp[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_cancellationwinforms/cs/cancellationwinforms/form1.cs#100)]
 [!code-vb[TPLDataflow_CancellationWinForms#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_cancellationwinforms/vb/cancellationwinforms/form1.vb#100)]  
  
 次の図は、実行中のアプリケーションを示しています。  
  
 ![Windows フォーム アプリケーション](media/tpldataflow-cancellation.png "TPLDataflow_Cancellation")  

## <a name="see-also"></a>参照

- [データフロー](dataflow-task-parallel-library.md)
