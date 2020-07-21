---
title: デジタル インク - Windows フォームおよび COM と WPF
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- enabling ink [WPF]
- InkCanvas control [WPF]
- ink object model [WPF]
- tablet pen [WPF], events [WPF]
- ink [WPF], enabling
- events [WPF], tablet pen
ms.assetid: 577835be-b145-4226-8570-1d309e9b3901
ms.openlocfilehash: 4a183bba2c5cfb2d12a9cf435ae1f92b4cf63948
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76737286"
---
# <a name="the-ink-object-model-windows-forms-and-com-versus-wpf"></a>インク オブジェクト モデル:Windows フォームおよび COM と WPF の比較

基本的に、デジタル インクをサポートするプラットフォームは 3 つあります。TabletPC Windows フォーム プラットフォーム、Tablet PC COM プラットフォーム、および Windows Presentation Foundation (WPF) プラットフォームです。  Windows フォームと COM プラットフォームは同様のオブジェクト モデルを共有しますが、WPF プラットフォームのオブジェクト モデルは大きく異なります。  このトピックでは、あるオブジェクト モデルを使用して作業した開発者が他のオブジェクト モデルを理解しやすくなるように、違いを大まかに説明します。  
  
## <a name="enabling-ink-in-an-application"></a>アプリケーションでのインクの有効化  
 すべての 3 つのプラットフォームには、アプリケーションでタブレット ペンからの入力を受け取るができるようにするオブジェクトとコントロールが含まれています。  Windows フォームと COM プラットフォームには、[Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90))、[Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90))、[Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90))、および [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) クラスが含まれています。  [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) と [Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90)) は、インクを収集するためにアプリケーションに追加できるコントロールです。  [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) と [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) を既存のウィンドウに添付して、ウィンドウとカスタム コントロールをインク対応にすることができます。  
  
 WPF プラットフォームには <xref:System.Windows.Controls.InkCanvas> コントロールが含まれています。  アプリケーションに <xref:System.Windows.Controls.InkCanvas> を追加して、すぐにインクの収集を開始できます。 <xref:System.Windows.Controls.InkCanvas> を使用すると、ユーザーはインクのコピー、選択、およびサイズ変更を行うことができます。  他のコントロールを <xref:System.Windows.Controls.InkCanvas> に追加することができます。ユーザーはそれらのコントロールに手書きすることもできます。  <xref:System.Windows.Controls.InkPresenter> を追加してそのスタイラス ポイントを収集することにより、インク対応のカスタム コントロールを作成できます。  
  
 アプリケーションでインクを有効にする方法の詳細を次の表に示します。  
  
|目的|WPF プラットフォームの場合|Windows フォーム または COM プラットフォームの場合|  
|-----------------|--------------------------|------------------------------------------|  
|アプリケーションにインク対応コントロールを追加する|[インクの概要](getting-started-with-ink.md)に関するページを参照してください。|「[自動要求フォーム サンプル](/windows/desktop/tablet/auto-claims-form-sample)」を参照してください|  
|カスタム コントロールでインクを有効にする|「[インク入力コントロールの作成](creating-an-ink-input-control.md)」を参照してください。|「[インク クリップボードのサンプル](/windows/desktop/tablet/ink-clipboard-sample)」を参照してください。|  
  
## <a name="ink-data"></a>インク データ  
 Windows フォームと COM プラットフォームでは、[Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90))、[Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90))、[Microsoft.Ink.InkEdit](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552265(v=vs.90))、および [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) のそれぞれによって [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトが公開されます。 [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトには、1 つ以上の [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) オブジェクトのデータが含まれ、それらのストロークを管理および操作するための一般的なメソッドとプロパティが公開されています。  [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトでは、含まれているストロークの有効期間を管理します。[Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトでは、所有するストロークを作成および削除します。  各 [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) には、親の [Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクト内で一意の識別子があります。  
  
 WPF プラットフォームでは、<xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> クラスには自身の有効期間が所有および管理されます。 <xref:System.Windows.Ink.Stroke> オブジェクトのグループは、<xref:System.Windows.Ink.StrokeCollection> でまとめて収集できます。これには、インクのヒット テスト、消去、変換、シリアル化などの一般的なインク データ管理操作のメソッドが用意されています。 <xref:System.Windows.Ink.Stroke> は、任意の時点で 0 個、1 個、または複数の <xref:System.Windows.Ink.StrokeCollection> オブジェクトに属する可能性があります。  <xref:System.Windows.Controls.InkCanvas> と <xref:System.Windows.Controls.InkPresenter> には、[Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトではなく <xref:System.Windows.Ink.StrokeCollection?displayProperty=nameWithType> が含まれています。  
  
 次の 2 つの図では、インク データ オブジェクト モデルを比較しています。  Windows フォームと COM プラットフォームでは、[Microsoft.Ink.Ink](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583670(v=vs.90)) オブジェクトによって [Microsoft.Ink.Stroke](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552692(v=vs.90)) オブジェクトの有効期間が制限され、スタイラス パケットは個々のストロークに属します。  次の図に示すように、複数のストロークから同じ [Microsoft.Ink.DrawingAttributes](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583636(v=vs.90)) オブジェクトを参照できます。  
  
 ![COM および Winforms のインク オブジェクト モデルの図。](./media/ink-inkownsstrokes.png "Ink_InkOwnsStrokes")  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、各 <xref:System.Windows.Ink.Stroke?displayProperty=nameWithType> は共通言語ランタイム オブジェクトです。これは、それを参照する何かがある限り存在します。  各 <xref:System.Windows.Ink.Stroke> は、共通言語ランタイム オブジェクトでもある <xref:System.Windows.Input.StylusPointCollection> および <xref:System.Windows.Ink.DrawingAttributes?displayProperty=nameWithType> オブジェクトを参照してください。  
  
 ![WPF のインク オブジェクト モデルの図。](./media/ink-wpfinkobjectmodel.png "Ink_WPFInkObjectModel")  
  
 次の表では、WPF プラットフォームと Windows フォームおよび COM プラットフォーム上でいくつかの一般的なタスクを実行する方法を比較しています。  
  
|タスク|Windows Presentation Foundation|Windows フォームと COM|  
|----------|-------------------------------------|---------------------------|  
|インクを保存する|<xref:System.Windows.Ink.StrokeCollection.Save%2A>|[Microsoft.Ink.Ink.Save](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571335(v=vs.90))|  
|インクを読み込む|<xref:System.Windows.Ink.StrokeCollection.%23ctor%2A> コンストラクターを使用して <xref:System.Windows.Ink.StrokeCollection> を作成します。|[Microsoft.Ink.Ink.Load](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms569609(v=vs.90))|  
|ヒット テスト|<xref:System.Windows.Ink.StrokeCollection.HitTest%2A>|[Microsoft.Ink.Ink.HitTest](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571330(v=vs.90))|  
|インクをコピーする|<xref:System.Windows.Controls.InkCanvas.CopySelection%2A>|[Microsoft.Ink.Ink.ClipboardCopy](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571316(v=vs.90))|  
|インクを貼り付ける|<xref:System.Windows.Controls.InkCanvas.Paste%2A>|[Microsoft.Ink.Ink.ClipboardPaste](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms571318(v=vs.90))|  
|ストロークのコレクションのカスタム プロパティにアクセスする|<xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A> (プロパティは内部的に格納され、<xref:System.Windows.Ink.StrokeCollection.AddPropertyData%2A>、<xref:System.Windows.Ink.StrokeCollection.RemovePropertyData%2A>、および <xref:System.Windows.Ink.StrokeCollection.ContainsPropertyData%2A> を介してアクセスされます)|[Microsoft.Ink.Ink.ExtendedProperties](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms582214(v=vs.90)) を使用します|  
  
### <a name="sharing-ink-between-platforms"></a>プラットフォーム間でインクを共有する  
 プラットフォームにはインク データ用のさまざまなオブジェクト モデルがありますが、プラットフォーム間でのデータの共有は非常に簡単です。 次の例では、Windows フォーム アプリケーションからインクを保存し、そのインクを Windows Presentation Foundation アプリケーションに読み込みます。  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#SaveWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewinforms)]
[!code-vb[WinFormWPFInk#SaveWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewinforms)]  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#LoadWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwpf)]
[!code-vb[WinFormWPFInk#LoadWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwpf)]  
  
 次の例では、Windows Presentation Foundation アプリケーションからインクを保存し、Windows フォーム アプリケーションにインクを読み込みます。  
  
 [!code-csharp[WinFormWPFInk#UsingWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwpf)]
 [!code-vb[WinFormWPFInk#UsingWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwpf)]  
[!code-csharp[WinFormWPFInk#SaveWPF](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#savewpf)]
[!code-vb[WinFormWPFInk#SaveWPF](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#savewpf)]  
  
 [!code-csharp[WinFormWPFInk#UsingWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#usingwinforms)]
 [!code-vb[WinFormWPFInk#UsingWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#usingwinforms)]  
[!code-csharp[WinFormWPFInk#LoadWinforms](~/samples/snippets/csharp/VS_Snippets_Wpf/WinformWPFInk/CSharp/Program.cs#loadwinforms)]
[!code-vb[WinFormWPFInk#LoadWinforms](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WinformWPFInk/VisualBasic/Module1.vb#loadwinforms)]
## <a name="events-from-the-tablet-pen"></a>タブレットペンからのイベント  

 Windows フォームおよび COM プラットフォーム上の [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90))、[Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90))、および [Microsoft.Ink.InkPicture](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583740(v=vs.90)) は、ユーザーがペン データを入力したときにイベントを受け取ります。 [Microsoft.Ink.InkOverlay](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms552322(v=vs.90)) または [Microsoft.Ink.InkCollector](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms583683(v=vs.90)) はウィンドウまたはコントロールに添付され、これを使用してタブレット入力データによって発生したイベントを登録できます。 これらのイベントが発生するスレッドは、イベントがペン、マウス、またはプログラムのいずれで発生したかによって変わります。 これらのイベントに関連するスレッドの詳細については、「[スレッドに関する一般的な考慮事項](/windows/desktop/tablet/general-threading-considerations)」と「[イベントが発生する可能性のあるスレッド](/windows/desktop/tablet/threads-on-which-an-event-can-fire)」を参照してください。  
  
 Windows Presentation Foundation プラットフォームでは、<xref:System.Windows.UIElement> クラスにはペン入力のイベントがあります。 これは、すべてのコントロールではスタイラス イベントの完全なセットが公開されていることを意味します。  スタイラス イベントにはトンネリングおよびバブリング イベントのペアがあり、常にアプリケーション スレッド上で発生します。  詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
 次の図では、スタイラス イベントを発生させるクラスのオブジェクト モデルを比較しています。 Windows Presentation Foundation オブジェクト モデルでは、バブリング イベントのみが表示され、対応するトンネル イベントは表示されません。  
  
 ![WPF と Winforms のスタイラス イベントのダイアグラム。](./media/ink-stylusevents.png "Ink_StylusEvents")  
  
## <a name="pen-data"></a>ペン データ  
 すべての 3 つのプラットフォームには、タブレット ペンからのデータを取得して操作する方法が用意されています。  Windows フォームと COM プラットフォームでは、これを実行するには、[Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)) を作成し、それにウィンドウまたはコントロールを添付し、[Microsoft.StylusInput.IStylusSyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575201(v=vs.90)) または [Microsoft.StylusInput.IStylusAsyncPlugin](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms575194(v=vs.90)) インターフェイスを実装するクラスを作成します。 これで、カスタム プラグインが [Microsoft.StylusInput.RealTimeStylus](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)) のプラグイン コレクションに追加されます。 このオブジェクト モデルの詳細については、「[StylusInput API のアーキテクチャ](/windows/desktop/tablet/architecture-of-the-stylusinput-apis)」を参照してください。  
  
 WPF プラットフォームでは、<xref:System.Windows.UIElement> クラスによって、設計が [ Microsoft.StylusInput.RealTimeStylus ](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms585724(v=vs.90)) と同様のプラグインのコレクションが公開されています。  ペン データを取得するには、<xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> から継承するクラスを作成し、そのオブジェクトを <xref:System.Windows.UIElement> の <xref:System.Windows.UIElement.StylusPlugIns%2A> コレクションに追加します。 この相互作用の詳細については、「[スタイラスからの入力のインターセプト](intercepting-input-from-the-stylus.md)」を参照してください。  
  
 すべてのプラットフォームで、スレッド プールではスタイラス イベントを介してインク データが受け取られ、それがアプリケーション スレッドに送信されます。  COM および Windows プラットフォームでのスレッド処理の詳細については、「[StylusInput API のスレッドに関する考慮事項](/windows/desktop/tablet/threading-considerations-for-the-stylusinput-apis)」を参照してください。  Windows プレゼンテーション ソフトウェアでのスレッドの詳細については、「[インク スレッド モデル](the-ink-threading-model.md)」を参照してください。  
  
 次の図では、ペン スレッド プールでペンデータを受け取るクラスのオブジェクト モデルを比較しています。  
  
 ![StylusPlugin モデル WPF と Winforms の図。](./media/ink-stylusplugins.png "Ink_StylusPlugins")
