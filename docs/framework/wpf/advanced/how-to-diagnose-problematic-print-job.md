---
title: '方法: 問題のある印刷ジョブを診断する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- troubleshooting print job problems [WPF]
- print jobs [WPF], troubleshooting
- print jobs [WPF], diagnosing problems
ms.assetid: b081a170-84c6-48f9-a487-5766a8d58a82
ms.openlocfilehash: 15de5d9ec8dc4016753b9d4cbed6fb0c64571774
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186041"
---
# <a name="how-to-diagnose-problematic-print-job"></a>方法: 問題のある印刷ジョブを診断する
印刷ジョブで印刷を実行できない、印刷速度が遅い、などのユーザーからの苦情に、ネットワーク管理者が対処することはよくあります。 Microsoft .NET Framework の API で公開されているさまざまな印刷ジョブのプロパティには、印刷ジョブを迅速にリモート診断する手段が用意されています。  
  
## <a name="example"></a>例  
 このようなユーティリティを作成する主な手順は次のとおりです。  
  
1. ユーザーから苦情が出ている印刷ジョブを特定します。 ユーザーがそのジョブを正確に特定できないことはよくあります。 プリント サーバーやプリンターの名前がわからないのかもしれません。 プリンターの場所の記述に使用されている用語が、<xref:System.Printing.PrintQueue.Location%2A> プロパティの設定で使用されたものとは異なる可能性もあります。 そこで、ユーザーが現在送信しているジョブのリストを生成することをお勧めします。 ジョブが複数存在する場合は、ユーザーと印刷システム管理者の間の通信を使用して、問題のあるジョブを特定できます。 その手順を次に示します。  
  
    1. プリント サーバーの一覧を取得します。  
  
    2. サーバーをループして、印刷キューを照会します。  
  
    3. サーバー ループの各パス内で、すべてのサーバーのキューをループして、ジョブを照会します  
  
    4. キュー ループの各パス内で、ジョブをループし、苦情を訴えているユーザーが送信したジョブに関する識別情報を収集します。  
  
2. 問題のある印刷ジョブを特定したら、関連するプロパティを調べて、 ジョブがエラー状態になっていないか、キューにサービスを提供しているプリンターがジョブの印刷前にオフラインになっていないか、など、何が問題になっているかを確認します。  
  
 一連のコード例を以下に示します。 最初のコード例には、印刷キューのループが示されています (前の手順 1c. を参照)。変数 `myPrintQueues` は、現在のプリント サーバーに対する <xref:System.Printing.PrintQueueCollection> オブジェクトです。  
  
 このコード例では、まず現在の印刷キューのオブジェクトを <xref:System.Printing.PrintQueue.Refresh%2A?displayProperty=nameWithType> で更新します。 これにより、オブジェクトのプロパティが、オブジェクトに示される物理プリンターの状態を正確に表すようになります。 その後、アプリケーションで <xref:System.Printing.PrintQueue.GetPrintJobInfoCollection%2A> を使用して、現在印刷キューに存在する印刷ジョブのコレクションを取得します。  
  
 次に、アプリケーションで <xref:System.Printing.PrintSystemJobInfo> コレクションをループ処理し、各 <xref:System.Printing.PrintSystemJobInfo.Submitter%2A> プロパティと、苦情を訴えているユーザーのエイリアスを比較します。 一致した場合、アプリケーションは、ジョブに関する識別情報を、表示される文字列に追加します (`userName` 変数と `jobList` 変数は、前にアプリケーションで初期化されています)。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#enumeratejobsinqueues)]
 [!code-csharp[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#enumeratejobsinqueues)]
 [!code-vb[DiagnoseProblematicPrintJob#EnumerateJobsInQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#enumeratejobsinqueues)]  
  
 次のコード例では、手順 2. のアプリケーションを取り上げます (前の説明を参照)。問題のあるジョブが特定され、その問題に関する情報を入力するように求められます。 この情報から、<xref:System.Printing.PrintServer>、<xref:System.Printing.PrintQueue>、<xref:System.Printing.PrintSystemJobInfo> の各オブジェクトを作成します。  
  
 この時点で、アプリケーションは分岐構造になっており、印刷ジョブの状態を確認する 2 つの方法に対応しています。  
  
- <xref:System.Printing.PrintJobStatus> 型の <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> プロパティのフラグを読み取ることができます。  
  
- <xref:System.Printing.PrintSystemJobInfo.IsBlocked%2A> や <xref:System.Printing.PrintSystemJobInfo.IsInError%2A> など、関連する各プロパティを読み取ることができます。  
  
 この例では両方の方法が示されています。したがって、<xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> プロパティのフラグを使用するユーザーは、以前に使用する方法に関する指定を求められたときに、"Y" と応答しました。 2 つの方法の詳細については、以下を参照してください。 最後に、アプリケーションは **ReportQueueAndJobAvailability** というメソッドを使用して、現在ジョブを印刷できるかどうかを報告します。 このメソッドについては、「[方法: 現在、印刷ジョブが印刷可能であるかどうかを検出する](how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day.md)」で説明しています。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#identifyanddiagnoseproblematicjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#identifyanddiagnoseproblematicjob)]
 [!code-vb[DiagnoseProblematicPrintJob#IdentifyAndDiagnoseProblematicJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#identifyanddiagnoseproblematicjob)]  
  
 <xref:System.Printing.PrintSystemJobInfo.JobStatus%2A> プロパティのフラグを使用して、印刷ジョブの状態を確認するには、各関連フラグが設定されているかどうかを確認します。 1 ビットがビット フラグ セットで設定されているかどうかを確認するには、通常、フラグ セットを 1 つのオペランドとし、フラグ自体をもう 1 つのオペランドとして、論理 AND 演算を行います。 フラグ自体には 1 ビットのみが設定されているため、論理 AND の結果は、その同じビットが上限となります。 それが該当するかどうかを確認するには、論理 AND の結果とフラグ自体を比較します。 詳細については、<xref:System.Printing.PrintJobStatus>、[& 演算子 (C# リファレンス)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)、および <xref:System.FlagsAttribute> に関する記事を参照してください。  
  
 次のコードでは、ビットが設定されている属性ごとにこの報告をコンソール画面に表示し、場合によっては応答方法を示します (ジョブまたはキューが一時停止されている場合に呼び出される **HandlePausedJob** メソッドについては、後で説明します)。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobattributes)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobattributes)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobAttributes](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobattributes)]  
  
 個別のプロパティを使用して印刷ジョブの状態を確認するには、単に各プロパティを読み取り、プロパティが `true` の場合は報告をコンソール画面に表示し、場合によっては応答方法を示します (ジョブまたはキューが一時停止されている場合に呼び出される **HandlePausedJob** メソッドについては、後で説明します)。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#spottroubleusingjobproperties)]
 [!code-csharp[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#spottroubleusingjobproperties)]
 [!code-vb[DiagnoseProblematicPrintJob#SpotTroubleUsingJobProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#spottroubleusingjobproperties)]  
  
 **HandlePausedJob** メソッドを使用すると、アプリケーションのユーザーが、一時停止されているジョブをリモートで再開できます。 印刷キューが正当な理由で一時停止している可能性があるため、まず、印刷キューを再開するかどうかを確認するメッセージが表示されます。 "Y" と応答すると、<xref:System.Printing.PrintQueue.Resume%2A?displayProperty=nameWithType> メソッドが呼び出されます。  
  
 次に、ユーザーはジョブ自体を再開するかどうかを確認するよう求められます。これは、そのジョブが印、刷キューとは関係なく一時停止されている可能性もあるためです (<xref:System.Printing.PrintQueue.IsPaused%2A?displayProperty=nameWithType> と <xref:System.Printing.PrintSystemJobInfo.IsPaused%2A?displayProperty=nameWithType> を比較します)。"Y" と応答すると、<xref:System.Printing.PrintSystemJobInfo.Resume%2A?displayProperty=nameWithType> が呼び出されます。それ以外の場合は、<xref:System.Printing.PrintSystemJobInfo.Cancel%2A> が呼び出されます。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#handlepausedjob)]
 [!code-csharp[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#handlepausedjob)]
 [!code-vb[DiagnoseProblematicPrintJob#HandlePausedJob](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#handlepausedjob)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintJobStatus>
- <xref:System.Printing.PrintSystemJobInfo>
- <xref:System.FlagsAttribute>
- <xref:System.Printing.PrintQueue>
- [& 演算子 (C# リファレンス)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
