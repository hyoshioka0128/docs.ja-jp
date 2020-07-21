---
title: '方法: プリンターのステータスをリモート操作で調査する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- surveying printer status remotely [WPF]
- printer status [WPF], surveying remotely
- remotely surveying printer status [WPF]
- status [WPF], printers [WPF], surveying remotely
ms.assetid: d6324759-8292-4c23-9584-9c708887dc94
ms.openlocfilehash: 859ccb703c6c54c66d6ea7b433c67d156627e25b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187034"
---
# <a name="how-to-remotely-survey-the-status-of-printers"></a>方法: プリンターのステータスをリモート操作で調査する
中企業および大企業では、任意の時点において、紙詰まりや用紙切れなどの問題が発生したために動作していないプリンターが複数存在する場合があります。 Microsoft .NET Framework の API で公開されているさまざまなプリンター プロパティには、プリンターの状態を迅速に調査する手段が用意されています。  
  
## <a name="example"></a>例  
 このようなユーティリティを作成する主な手順は次のとおりです。  
  
1. プリント サーバーの一覧を取得します。  
  
2. サーバーをループして、印刷キューを照会します。  
  
3. サーバー ループの各パス内で、すべてのサーバーのキューをループして、キューが現在動作していないことを示している各プロパティを読み取ります。  
  
 以下のコードは、一連のスニペットを示しています。 この例では、説明を簡単にするために、CRLF で区切られたプリント サーバー リストがあることを想定しています。 変数 `fileOfPrintServers` は、このファイル用の <xref:System.IO.StreamReader> オブジェクトです。 各サーバー名はそれぞれ独自の行に含まれているため、<xref:System.IO.StreamReader.ReadLine%2A> を呼び出すと、次のサーバーの名前が取得され、<xref:System.IO.StreamReader> のカーソルは次の行の先頭に移動ｓれます。  
  
 外側のループ内のコードでは、最新のプリント サーバーの <xref:System.Printing.PrintServer> オブジェクトを作成し、サーバーに対する管理権限をアプリケーションが持つように指定します。  
  
> [!NOTE]
> サーバーが多数存在する場合は、必要になるプロパティのみを初期化する <xref:System.Printing.PrintServer.%23ctor%28System.String%2CSystem.String%5B%5D%2CSystem.Printing.PrintSystemDesiredAccess%29> コンストラクターを使用することで、パフォーマンスを向上させることができます。  
  
 この例では、次に <xref:System.Printing.PrintServer.GetPrintQueues%2A> を使用して、サーバーのすべてのキューのコレクションを作成し、そのキューのループを開始します。 この内側のループは分岐構造になっており、プリンターの状態を確認する 2 つの方法に対応しています。  
  
- <xref:System.Printing.PrintQueueStatus> 型の <xref:System.Printing.PrintQueue.QueueStatus%2A> プロパティのフラグを読み取ることができます。  
  
- <xref:System.Printing.PrintQueue.IsOutOfPaper%2A> や <xref:System.Printing.PrintQueue.IsPaperJammed%2A> など、関連する各プロパティを読み取ることができます。  
  
 この例では両方の方法が示されています。したがって、<xref:System.Printing.PrintQueue.QueueStatus%2A> プロパティのフラグを使用するユーザーは、以前に使用する方法に関する指定を求められたときに、"y" と応答しました。 2 つの方法の詳細については、以下を参照してください。  
  
 最後に、結果がユーザーに表示されます。  
  
 [!code-cpp[PrinterStatusSurvey#SurveyQueues](~/samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#surveyqueues)]
 [!code-csharp[PrinterStatusSurvey#SurveyQueues](~/samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#surveyqueues)]
 [!code-vb[PrinterStatusSurvey#SurveyQueues](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#surveyqueues)]  
  
 <xref:System.Printing.PrintQueue.QueueStatus%2A> プロパティのフラグを使用して、プリンターの状態を確認するには、各関連フラグが設定されているかどうかを確認します。 1 ビットがビット フラグ セットで設定されているかどうかを確認するには、通常、フラグ セットを 1 つのオペランドとし、フラグ自体をもう 1 つのオペランドとして、論理 AND 演算を行います。 フラグ自体には 1 ビットのみが設定されているため、論理 AND の結果は、その同じビットが上限となります。 それが該当するかどうかを確認するには、論理 AND の結果とフラグ自体を比較します。 詳細については、「<xref:System.Printing.PrintQueueStatus>」、「[& 演算子 (C# リファレンス)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)」、および「<xref:System.FlagsAttribute>」を参照してください。  
  
 次のコードでは、ビットが設定されている属性ごとに、ユーザーに表示される最終レポートに警告を追加します (コードの最後で呼び出している **ReportAvailabilityAtThisTime** メソッドについては以下で説明します)。  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](~/samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueattributes)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](~/samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueattributes)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueAttributes](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueattributes)]  
  
 各プロパティを使用してプリンターの状態を確認するには、各プロパティを読み取り、プロパティが `true` の場合にユーザーに表示される最終レポートに警告を追加するだけです (コードの最後で呼び出している **ReportAvailabilityAtThisTime** メソッドについては以下で説明します)。  
  
 [!code-cpp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](~/samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#spottroubleusingqueueproperties)]
 [!code-csharp[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](~/samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#spottroubleusingqueueproperties)]
 [!code-vb[PrinterStatusSurvey#SpotTroubleUsingQueueProperties](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#spottroubleusingqueueproperties)]  
  
 **ReportAvailabilityAtThisTime** メソッドは、現在の時刻にキューが使用可能かどうかを確認する必要がある場合に備えて作成されたものです。  
  
 <xref:System.Printing.PrintQueue.StartTimeOfDay%2A> プロパティと <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> プロパティが等しい場合、プリンターは常に使用可能であるため、このメソッドでは何も行われません。 異なる場合は、このメソッドで現在の時刻が取得されます。この時刻は、後で、午前 0 時からの合計分数に変換する必要があります。これは、<xref:System.Printing.PrintQueue.StartTimeOfDay%2A> プロパティと <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A> プロパティが、<xref:System.DateTime> オブジェクトではなく、午前 0 時からの分数を表す <xref:System.Int32> であるためです。 最後に、このメソッドは、現在の時刻が、開始時刻と終了時刻の間にあるかどうかを確認します。  
  
 [!code-cpp[PrinterStatusSurvey#UsingStartAndUntilTimes](~/samples/snippets/cpp/VS_Snippets_Wpf/PrinterStatusSurvey/CPP/Program.cpp#usingstartanduntiltimes)]
 [!code-csharp[PrinterStatusSurvey#UsingStartAndUntilTimes](~/samples/snippets/csharp/VS_Snippets_Wpf/PrinterStatusSurvey/CSharp/Program.cs#usingstartanduntiltimes)]
 [!code-vb[PrinterStatusSurvey#UsingStartAndUntilTimes](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PrinterStatusSurvey/visualbasic/program.vb#usingstartanduntiltimes)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintQueue.StartTimeOfDay%2A>
- <xref:System.Printing.PrintQueue.UntilTimeOfDay%2A>
- <xref:System.DateTime>
- <xref:System.Printing.PrintQueueStatus>
- <xref:System.FlagsAttribute>
- <xref:System.Printing.PrintServer.GetPrintQueues%2A>
- <xref:System.Printing.PrintServer>
- <xref:System.Printing.LocalPrintServer>
- <xref:System.Printing.EnumeratedPrintQueueTypes>
- <xref:System.Printing.PrintQueue>
- [& 演算子 (C# リファレンス)](../../../csharp/language-reference/operators/bitwise-and-shift-operators.md#logical-and-operator-)
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
