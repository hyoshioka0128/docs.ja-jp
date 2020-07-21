---
title: '方法: 現在、印刷ジョブが印刷可能であるかどうかを検出する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- print queues [WPF], timing
- printers [WPF], availability
- print jobs [WPF], timing
ms.assetid: 7e9c8ec1-abf6-4b3d-b1c6-33b35d3c4063
ms.openlocfilehash: 859dc75169e443d07361951692a428507886fa2e
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69947811"
---
# <a name="how-to-discover-whether-a-print-job-can-be-printed-at-this-time-of-day"></a>方法: 現在、印刷ジョブが印刷可能であるかどうかを検出する
印刷キューは、1 日 24 時間利用できるとは限りません。 開始時刻と終了時刻のプロパティがあり、特定の時間帯に使用できないように設定できます。 この機能を使用すると、たとえば、午後 5 時以降は特定の部署が排他的に使用するようにプリンターを予約することができます。 この部署では、他の部署が使用しているのとは異なるキューを使用します。 他の部署のキューは、午後 5 時以降は使用不可になるように設定されるのに対し、優先される部署のキューは常に使用可能になるように設定できます。  
  
 さらに、印刷ジョブ自体を、指定された期間内にのみ印刷できるように設定できます。  
  
 Microsoft .NET Framework の API で公開されている <xref:System.Printing.PrintQueue> クラスと <xref:System.Printing.PrintSystemJobInfo> クラスにより、特定の印刷ジョブが現在の時刻に特定のキューで印刷できるかどうかをリモートで確認する手段が提供されます。  
  
## <a name="example"></a>例  
 次の例は、印刷ジョブに関する問題を診断できるサンプルです。  
  
 この種の関数には、次の 2 つの主要な手順があります。  
  
1. <xref:System.Printing.PrintQueue> の <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> プロパティと <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> プロパティを読み取って、現在の時刻が両者の間にあるかどうかを判断します。  
  
2. <xref:System.Printing.PrintSystemJobInfo> の <xref:System.Printing.PrintSystemJobInfo.StartTimeOfDay%2A> プロパティと <xref:System.Printing.PrintSystemJobInfo.UntilTimeOfDay%2A> プロパティを読み取って、現在の時刻が両者の間にあるかどうかを判断します。  
  
 しかし、これらのプロパティが <xref:System.DateTime> オブジェクトではないという事実から、複雑な問題が発生します。 これらは、時刻を午前 0 時からの分数として表す <xref:System.Int32> オブジェクトです。 さらに、現在のタイム ゾーンの午前 0 時ではなく、UTC (世界協定時) の午前 0 時です。  
  
 最初のコード例は、静的メソッド **ReportQueueAndJobAvailability** を示しています。これは、<xref:System.Printing.PrintSystemJobInfo> に渡され、ヘルパー メソッドを呼び出して、現在の時刻にジョブが印刷できるかどうか、できない場合はいつ印刷できるかを判断します。 <xref:System.Printing.PrintQueue> はメソッドに渡されないことにご注意ください。 これは、<xref:System.Printing.PrintSystemJobInfo> にはその <xref:System.Printing.PrintSystemJobInfo.HostingPrintQueue%2A> プロパティのキューへの参照が含まれているためです。  
  
 下位メソッドには、オーバーロードされた **ReportAvailabilityAtThisTime** メソッドが含まれています。このメソッドは、パラメーターとして <xref:System.Printing.PrintQueue> または <xref:System.Printing.PrintSystemJobInfo> を受け取ることができます。 **TimeConverter.ConvertToLocalHumanReadableTime** もあります。 これらのメソッドについては、すべて以下で説明します。  
  
 **ReportQueueAndJobAvailability** メソッドは、最初に、キューまたは印刷ジョブが現時点で使用できないかどうかを確認します。 これらのいずれかが使用できない場合は、次にキューが使用できないかどうかを確認します。 使用できない場合、このメソッドは、この事実と、キューが再び使用可能になる時刻を報告します。 次にジョブを確認し、使用できない場合は、次に印刷できる時間帯を報告します。 最後に、このメソッドは、ジョブが印刷できる最も早い時刻を報告します。 これは、次の 2 つの時刻の遅い方です。  
  
- 印刷キューが次に使用可能になる時刻。  
  
- 印刷ジョブが次に使用可能になる時刻。  
  
 時刻を報告する場合に、<xref:System.DateTime.ToShortTimeString%2A> メソッドも呼び出されます。このメソッドは、出力に年、月、日が表示されないようにするからです。 印刷キューまたは印刷ジョブの可用性を、特定の年、月、または日に制限することはできません。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#reportqueueandjobavailability)]
 [!code-csharp[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#reportqueueandjobavailability)]
 [!code-vb[DiagnoseProblematicPrintJob#ReportQueueAndJobAvailability](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#reportqueueandjobavailability)]  
  
 **ReportAvailabilityAtThisTime** メソッドの 2 つのオーバーロードは、これらに渡される型を除いて同じです。そのため、<xref:System.Printing.PrintQueue> バージョンのみを以下に示します。  
  
> [!NOTE]
> メソッドは型を除き同一であるため、サンプルでは、なぜジェネリック メソッド **ReportAvailabilityAtThisTime\<T>** が作成されないのかという疑問が生じます。 その理由は、これらのメソッドは、メソッドによって呼び出される **StartTimeOfDay** および **UntilTimeOfDay** のプロパティを持つクラスに制限する必要がありますが、ジェネリック メソッドは 1 つのクラスにしか制限できず、継承ツリー内の <xref:System.Printing.PrintQueue> と <xref:System.Printing.PrintSystemJobInfo> の両方に共通する唯一のクラスは、こうしたプロパティを持たない <xref:System.Printing.PrintSystemObject> だからです。  
  
 (下記のコード例に示されている) **ReportAvailabilityAtThisTime** メソッドは、まず <xref:System.Boolean> sentinel 変数を `true`に初期化します。 キューが使用できない場合は、`false` にリセットされます。  
  
 次にこのメソッドは、開始時刻と "until" (終了) 時刻が同じかどうかを確認します。 同じ場合、キューは常に使用可能なので、メソッドは `true` を返します。  
  
 キューが常に利用できない場合、メソッドは静的 <xref:System.DateTime.UtcNow%2A> プロパティを使用して、<xref:System.DateTime> オブジェクトとして現在の時刻を取得します (<xref:System.Printing.PrintQueue.StartTimeOfDay%2A> プロパティと <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> プロパティは UTC 時刻であるため、現地時刻は必要ありません)。  
  
 ただし、これら 2 つのプロパティは <xref:System.DateTime> オブジェクトではありません。 これらは UTC の午前 0 時からの分数として時刻を表す <xref:System.Int32> です。 そのため、<xref:System.DateTime> オブジェクトを午前 0 時からの分数に変換する必要があります。 それが完了すると、メソッドでは "now" (現在の時刻) がキューの開始時刻と "until" (終了) 時刻の間にあるかどうかが確認され、"now" がこの 2 つの時刻の間にない場合は sentinel が false に設定されて、sentinel が返されます。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#printqueuestartuntil)]
 [!code-csharp[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#printqueuestartuntil)]
 [!code-vb[DiagnoseProblematicPrintJob#PrintQueueStartUntil](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#printqueuestartuntil)]  
  
 (下記のコード例に示されている) **TimeConverter.ConvertToLocalHumanReadableTime** メソッドは、Microsoft .NET Framework で導入されたメソッドを使用しないため、説明は簡単です。 このメソッドには、2 回の変換タスクがあります。これは、午前 0 時からの分数を表す整数値を取得し、それを人間が判読できる時刻に変換し、それを現地時刻に変換する必要があります。 これを実現するには、最初に UTC の午前 0 時に設定された <xref:System.DateTime> オブジェクトを作成し、次に <xref:System.DateTime.AddMinutes%2A> メソッドを使用して、メソッドに渡された分数を加算します。 これにより、メソッドに渡された元の時刻を表す新しい <xref:System.DateTime> が返されます。 その後、<xref:System.DateTime.ToLocalTime%2A> メソッドがこれを現地時刻に変換します。  
  
 [!code-cpp[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/cpp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CPP/Program.cpp#timeconverter)]
 [!code-csharp[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/csharp/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/CSharp/Program.cs#timeconverter)]
 [!code-vb[DiagnoseProblematicPrintJob#TimeConverter](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DiagnoseProblematicPrintJob/visualbasic/program.vb#timeconverter)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.DateTime>
- <xref:System.Printing.PrintSystemJobInfo>
- <xref:System.Printing.PrintQueue>
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
