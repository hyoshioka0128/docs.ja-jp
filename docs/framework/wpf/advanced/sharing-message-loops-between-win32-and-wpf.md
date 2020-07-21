---
title: Win32 と WPF 間でのメッセージ ループの共有
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- Win32 code [WPF], sharing message loops
- message loops [WPF]
- sharing message loops [WPF]
- interoperability [WPF], Win32
ms.assetid: 39ee888c-e5ec-41c8-b11f-7b851a554442
ms.openlocfilehash: e1b96284d69645876d3e383beb03a2cc540d8b7b
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76731711"
---
# <a name="sharing-message-loops-between-win32-and-wpf"></a>Win32 と WPF 間でのメッセージ ループの共有
このトピックでは、<xref:System.Windows.Threading.Dispatcher> の既存のメッセージ ループの公開を使用するか、相互運用コードの Win32 側に別のメッセージ ループを作成することにより、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] との相互運用のためのメッセージ ループを実装する方法について説明します。  
  
## <a name="componentdispatcher-and-the-message-loop"></a>ComponentDispatcher とメッセージ ループ  
 相互運用とキーボード イベント サポートの通常のシナリオとして、<xref:System.Windows.Interop.IKeyboardInputSink> を実装する方法、または <xref:System.Windows.Interop.HwndSource> や <xref:System.Windows.Interop.HwndHost> など、既に <xref:System.Windows.Interop.IKeyboardInputSink> を実装しているクラスからサブクラスを作成する方法があります。 ただし、キーボード シンクのサポートでは、相互運用の境界を越えてメッセージを送受信するときに発生する可能性があるすべてのメッセージ ループのニーズに対応できるわけではありません。 アプリケーション メッセージ ループ アーキテクチャを形式化するために、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には <xref:System.Windows.Interop.ComponentDispatcher> クラスが用意されています。これには、メッセージ ループが従う単純なプロトコルが定義されています。  
  
 <xref:System.Windows.Interop.ComponentDispatcher> は、いくつかのメンバーが公開されている静的クラスです。 各メソッドのスコープは、呼び出しスレッドに暗黙的に関連付けられています。 メッセージ ループでは、これらの API の一部をクリティカルなタイミングで呼び出す必要があります (次のセクションで定義します)。  
  
 <xref:System.Windows.Interop.ComponentDispatcher> には、他のコンポーネント (キーボード シンクなど) からリッスンできるイベントが用意されています。 <xref:System.Windows.Threading.Dispatcher> クラスを使用すると、適切なすべての <xref:System.Windows.Interop.ComponentDispatcher> メソッドを適切なシーケンスで呼び出すことができます。 独自のメッセージ ループを実装している場合、コードでは同様の方法で <xref:System.Windows.Interop.ComponentDispatcher> メソッドを呼び出す必要があります。  
  
 スレッドに対して <xref:System.Windows.Interop.ComponentDispatcher> メソッドを呼び出すと、そのスレッドに登録されていたイベント ハンドラーのみが呼び出されます。  
  
## <a name="writing-message-loops"></a>メッセージ ループの作成  
 独自のメッセージ ループを作成する場合に使用する <xref:System.Windows.Interop.ComponentDispatcher> メンバーのチェックリストを次に示します。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A>: スレッドがモーダルであることを示すには、メッセージ ループでこれを呼び出す必要があります。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A>: スレッドが非モーダルに戻ったことを示すには、メッセージ ループでこれを呼び出す必要があります。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A>: <xref:System.Windows.Interop.ComponentDispatcher> で <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> イベントを発生させる必要があることを示すには、メッセージ ループでこれを呼び出す必要があります。 <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A> が `true` の場合、<xref:System.Windows.Interop.ComponentDispatcher> によって <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> が発生することはありませんが、モーダル状態のときに <xref:System.Windows.Interop.ComponentDispatcher> が応答できない場合でも、メッセージ ループでは <xref:System.Windows.Interop.ComponentDispatcher.RaiseIdle%2A> の呼び出しを選択できます。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A>: 新しいメッセージが使用可能であることを示すには、メッセージ ループでこれを呼び出す必要があります。 戻り値は、<xref:System.Windows.Interop.ComponentDispatcher> イベントのリスナーによってメッセージが処理されたかどうかを示します。 <xref:System.Windows.Interop.ComponentDispatcher.RaiseThreadMessage%2A> から `true` (処理済み) が返される場合、ディスパッチャーではメッセージに対してそれ以上何もする必要はありません。 戻り値が `false` の場合、ディスパッチャーでは Win32 関数 `TranslateMessage` を呼び出し、次に `DispatchMessage` を呼び出すことが期待されます。  
  
## <a name="using-componentdispatcher-and-existing-message-handling"></a>ComponentDispatcher と既存のメッセージ処理の使用  
 固有の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] メッセージ ループに依存する場合に使用する <xref:System.Windows.Interop.ComponentDispatcher> メンバーのチェックリストを次に示します。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.IsThreadModal%2A>: アプリケーションがモーダルになっているかどうかを返します (たとえば、モーダル メッセージ ループがプッシュされた、など)。 <xref:System.Windows.Interop.ComponentDispatcher> を使用すると、この状態を追跡できます。このクラスにはメッセージ ループからの <xref:System.Windows.Interop.ComponentDispatcher.PushModal%2A> および <xref:System.Windows.Interop.ComponentDispatcher.PopModal%2A> の呼び出し数が保持されるためです。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> および <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> イベントは、デリゲート呼び出しの標準規則に従います。 デリゲートは不特定の順序で呼び出され、最初のデリゲートでメッセージが処理済みとマークされた場合でも、すべてのデリゲートが呼び出されます。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle>: アイドル処理を実行するための適切かつ効率的な時間を示します (そのスレッドに対して保留中のメッセージは他にありません)。 スレッドがモーダルの場合、<xref:System.Windows.Interop.ComponentDispatcher.ThreadIdle> は発生しません。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage>: メッセージ ポンプで処理されるすべてのメッセージに対して発生します。  
  
- <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage>: <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> の間に処理されなかったすべてのメッセージに対して発生します。  
  
 <xref:System.Windows.Interop.ComponentDispatcher.ThreadFilterMessage> イベントまたは <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> イベントの後で、イベント データの参照によって渡された `handled` パラメーターが `true` の場合、メッセージは処理済みと見なされます。 `handled` が `true` の場合、イベント ハンドラーではメッセージを無視する必要があります。これは、別のハンドラーによって先にメッセージが処理されたことを意味するためです。 両方のイベントに対する複数のイベント ハンドラーによってメッセージが変更される場合があります。 ディスパッチャーでは、元の変更されていないメッセージではなく、変更されたメッセージをディスパッチする必要があります。 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> はすべてのリスナーに配信されますが、メッセージに応答してコードを呼び出す必要があるのは、メッセージの宛先に指定された HWND を含むトップレベル ウィンドウのみ、というのがアーキテクチャの目的です。  
  
## <a name="how-hwndsource-treats-componentdispatcher-events"></a>HwndSource で ComponentDispatcher イベントを処理する方法  
 <xref:System.Windows.Interop.HwndSource> がトップレベル ウィンドウ (親 HWND なし) の場合、<xref:System.Windows.Interop.ComponentDispatcher> に登録されます。 <xref:System.Windows.Interop.ComponentDispatcher.ThreadPreprocessMessage> が発生し、メッセージが <xref:System.Windows.Interop.HwndSource> または子ウィンドウを対象としている場合、<xref:System.Windows.Interop.HwndSource> からその <xref:System.Windows.Interop.HwndSource.System%23Windows%23Interop%23IKeyboardInputSink%23TranslateAccelerator%2A>、<xref:System.Windows.Interop.IKeyboardInputSink.TranslateChar%2A>、<xref:System.Windows.Interop.IKeyboardInputSink.OnMnemonic%2A> キーボード シンク シーケンスが呼び出されます。  
  
 <xref:System.Windows.Interop.HwndSource> がトップレベル ウィンドウではない (親 HWND がある) 場合、処理は行われません。 処理を行うのはトップレベル ウィンドウのみと想定されており、相互運用シナリオの一部としてキーボード シンクをサポートするトップ レベル ウィンドウであることが想定されています。  
  
 適切なキーボード シンク メソッドを最初に呼び出さずに <xref:System.Windows.Interop.HwndSource> に対して <xref:System.Windows.Interop.HwndHost.WndProc%2A> を呼び出すと、アプリケーションは <xref:System.Windows.UIElement.KeyDown> などの上位のキーボード イベントを受け取ります。 ただし、キーボード シンク メソッドは呼び出されません。これにより、アクセス キーのサポートなどの望ましいキーボード入力モデル機能は使用されません。 これは、メッセージ ループから <xref:System.Windows.Interop.ComponentDispatcher> の関連スレッドに適切に通知されなかったため、または親 HWND から適切なキーボード シンク応答が呼び出されなかったために発生することがあります。  
  
 <xref:System.Windows.Interop.HwndSource.AddHook%2A> メソッドを使用してそのメッセージのフックを追加した場合、キーボード シンクに送信されたメッセージが HWND に送信されない場合があります。 メッセージはメッセージ ポンプ レベルで直接処理され、`DispatchMessage` 関数に送信されていない可能性があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.ComponentDispatcher>
- <xref:System.Windows.Interop.IKeyboardInputSink>
- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
- [スレッド モデル](threading-model.md)
- [入力の概要](input-overview.md)
