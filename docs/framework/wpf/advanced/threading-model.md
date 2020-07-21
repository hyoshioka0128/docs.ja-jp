---
title: スレッド モデル
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- text on buttons [WPF], updating
- message processing [WPF], nested
- blocking operations [WPF]
- Common Language Runtime (CLR), locking mechanism
- locking mechanism of Common Language Runtime (CLR)
- threading model [WPF]
- Word [WPF], spelling checking
- button text [WPF], updating
- spelling checking in Word [WPF]
- asynchronous behavior [WPF], exposing
- nested message processing [WPF]
- reentrancy [WPF]
ms.assetid: 02d8fd00-8d7c-4604-874c-58e40786770b
ms.openlocfilehash: 87dcfa22bcce730c5a9b61721c3a846a08146475
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77094502"
---
# <a name="threading-model"></a>スレッド モデル
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、スレッド処理の難しさから開発者を救うように設計されています。 その結果、大部分の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 開発者は、複数のスレッドを使用するインターフェイスを作成する必要がなくなります。 マルチスレッド プログラムは複雑でデバッグが困難なため、シングルスレッド ソリューションが存在する場合は回避することが推奨されます。

 ただし、どれほど適切に設計したとしても、あらゆる種類の問題に対してシングルスレッドのソリューションを [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] フレームワークで提供することはできません。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] はもう一歩のところですが、複数のスレッドで [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] の応答性またはアプリケーションのパフォーマンスが向上する状況がまだあります。 この記事では、いくつかの背景資料について説明した後、このような状況の一部について探り、最後にいくつかの下位レベルの詳細について説明します。

> [!NOTE]
> このトピックでは、非同期呼び出しに <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> メソッドを使用したスレッド処理について説明します。 また、<xref:System.Action> または <xref:System.Func%601> をパラメーターとして受け取る <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A> メソッドを呼び出して、非同期呼び出しを行うこともできます。  <xref:System.Windows.Threading.Dispatcher.InvokeAsync%2A> メソッドからは、<xref:System.Windows.Threading.DispatcherOperation.Task%2A> プロパティを持つ <xref:System.Windows.Threading.DispatcherOperation> または <xref:System.Windows.Threading.DispatcherOperation%601> が返されます。 `await` キーワードは、<xref:System.Windows.Threading.DispatcherOperation> または関連する <xref:System.Threading.Tasks.Task> のいずれかと共に使用できます。 <xref:System.Threading.Tasks.Task> または <xref:System.Windows.Threading.DispatcherOperation> によって返される <xref:System.Windows.Threading.DispatcherOperation%601> を同期的に待機する必要がある場合、<xref:System.Windows.Threading.TaskExtensions.DispatcherOperationWait%2A> 拡張メソッドを呼び出します。  <xref:System.Threading.Tasks.Task.Wait%2A?displayProperty=nameWithType> を呼び出すと、デッドロックが発生します。 <xref:System.Threading.Tasks.Task> を使用して非同期操作を実行する方法の詳細については、「タスクの並列化」を参照してください。  <xref:System.Windows.Threading.Dispatcher.Invoke%2A> メソッドには、<xref:System.Action> または <xref:System.Func%601> をパラメーターとして受け取るオーバーロードもあります。  <xref:System.Windows.Threading.Dispatcher.Invoke%2A> メソッドを使用すると、デリゲートで <xref:System.Action> または <xref:System.Func%601> を渡すことにより、同期呼び出しを行うことができます。

<a name="threading_overview"></a>
## <a name="overview-and-the-dispatcher"></a>概要とディスパッチャー
 通常、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションは 2 つのスレッドから始まります。1 つはレンダリングを処理するもの、もう 1 つは [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を管理するものです。 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで入力を受け取り、イベントを処理し、画面を描画し、アプリケーション コードを実行する間、レンダリング スレッドは表示されずにバックグラウンドで効果的に実行されます。 ほとんどのアプリケーションでは 1 つの [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドが使用されますが、複数のスレッドを使用することが最適な状況もあります。 これについては後で例を使って説明します。

 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドにより、<xref:System.Windows.Threading.Dispatcher> というオブジェクト内の作業項目がキューに格納されます。 <xref:System.Windows.Threading.Dispatcher> は作業項目を優先順位に従って選択し、それぞれを最後まで実行します。  すべての [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドには少なくとも 1 つの <xref:System.Windows.Threading.Dispatcher> が必要であり、各 <xref:System.Windows.Threading.Dispatcher> では 1 つのスレッドで作業項目を実行できます。

 応答性の高いユーザー フレンドリなアプリケーションを構築する秘訣は、作業項目を小さく保って <xref:System.Windows.Threading.Dispatcher> のスループットを最大化することです。 このようにすると、処理の待機中に <xref:System.Windows.Threading.Dispatcher> キューに格納されている項目が古くなることはなくなります。 入力と応答の間に知覚可能な遅延があると、ユーザーに不満が生じる可能性があります。

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは、どのような方法で大規模な操作を処理することが想定されているでしょうか。 コードに大規模な計算が含まれる場合や、リモート サーバー上のデータベースに対してクエリを実行する必要がある場合は、どうすればよいでしょうか。 通常、その答えは、大規模な操作は別のスレッドで処理し、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで <xref:System.Windows.Threading.Dispatcher> キュー内の項目を処理できる余地を残すことです。 大規模な操作が完了すると、結果が [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドに報告され、表示できるようになります。

 従来、Windows では、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素へのアクセスは、それらを作成したスレッドにのみ許可されています。 つまり、実行時間が長いタスクを担当するバックグラウンド スレッドでは、終了時にテキスト ボックスを更新できないことがあります。 Windows では、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] コンポーネントの整合性を確保するためにこれを行っています。 コンテンツが描画中にバックグラウンド スレッドによって更新された場合、リスト ボックスが適切に表示されない可能性があります。

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、この調整を強制する組み込みの相互排他メカニズムがあります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のほとんどのクラスは <xref:System.Windows.Threading.DispatcherObject> から派生しています。 構築時に、現在実行中のスレッドにリンクされた <xref:System.Windows.Threading.Dispatcher> への参照が <xref:System.Windows.Threading.DispatcherObject> に格納されます。 実際には、<xref:System.Windows.Threading.DispatcherObject> は、それを作成したスレッドに関連付けられます。 プログラムの実行中に、<xref:System.Windows.Threading.DispatcherObject> を使用してそのパブリック <xref:System.Windows.Threading.DispatcherObject.VerifyAccess%2A> メソッドを呼び出すことができます。 <xref:System.Windows.Threading.DispatcherObject.VerifyAccess%2A> では、現在のスレッドに関連付けられている <xref:System.Windows.Threading.Dispatcher> が確認され、構築中に格納された <xref:System.Windows.Threading.Dispatcher> 参照と比較されます。 一致しない場合、<xref:System.Windows.Threading.DispatcherObject.VerifyAccess%2A> からは例外がスローされます。 <xref:System.Windows.Threading.DispatcherObject.VerifyAccess%2A> は、<xref:System.Windows.Threading.DispatcherObject> に属するすべてのメソッドの最初に呼び出されることが想定されています。

 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を変更できるのが 1 つのスレッドのみである場合、バックグラウンド スレッドはユーザーとどのように対話するでしょうか。 バックグラウンド スレッドからは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドに対して、代理で操作を実行するように要求することができます。 これを行うには、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドの <xref:System.Windows.Threading.Dispatcher> に作業項目を登録します。 <xref:System.Windows.Threading.Dispatcher> クラスには、作業項目を登録するための 2 つのメソッド <xref:System.Windows.Threading.Dispatcher.Invoke%2A> と <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> が用意されています。 どちらのメソッドでも、デリゲートの実行がスケジュールされます。 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> は同期呼び出しです。つまり、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドでデリゲートの実行が実際に完了するまで戻りません。 <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> は非同期であり、すぐに戻ります。

 <xref:System.Windows.Threading.Dispatcher> によって、キュー内の要素が優先度順に並べ替えられます。 要素を <xref:System.Windows.Threading.Dispatcher> キューに追加するときに指定できるレベルは 10 個あります。 これらの優先度は、<xref:System.Windows.Threading.DispatcherPriority> 列挙体に維持されます。 <xref:System.Windows.Threading.DispatcherPriority> レベルの詳細については、Windows SDK のドキュメントを参照してください。

<a name="samples"></a>
## <a name="threads-in-action-the-samples"></a>動作中のスレッド:サンプル

<a name="prime_number"></a>
### <a name="a-single-threaded-application-with-a-long-running-calculation"></a>実行時間の長い計算を使用するシングルスレッド アプリケーション
 ほとんどのグラフィカル ユーザー インターフェイス (GUI) では、ユーザーの操作に応じて生成されるイベントを待機する間、アイドルの状態で大部分の時間が費やされます。 慎重にプログラミングすると、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の応答性に影響を与えることなく、このアイドル時間を建設的に使用できます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] スレッド モデルでは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで発生する操作を中断する入力は許可されていません。 つまり、保留中の入力イベントが古くなる前に処理できるように、定期的に <xref:System.Windows.Threading.Dispatcher> に戻る必要があります。

 次に例を示します。

 ![素数のスレッド処理を示すスクリーンショット。](./media/threading-model/threading-prime-numbers.png)

 このシンプルなアプリケーションでは、素数を検索して、3 から数え上げます。 ユーザーが **[Start]\(開始\)** ボタンをクリックすると、検索が開始されます。 プログラムによって素数が検出されると、その検出によってユーザー インターフェイスが更新されます。 ユーザーはいつでも検索を停止できます。

 とてもシンプルですが、素数検索は永遠に続く可能性があり、いくつかの困難を伴います。  ボタンのクリック イベント ハンドラー内で検索全体を処理した場合、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドに他のイベントを処理する機会を与えないことになります。 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] では、入力に応答することや、メッセージを処理することができません。 再描画もボタンのクリックに対する応答も行われません。

 別のスレッドで素数検索を行うこともできますが、その場合は同期の問題に対処する必要があります。 シングルスレッド方式では、ラベルを直接更新し、見つかった最大の素数を列挙することができます。

 計算のタスクを扱いやすいチャンクに分割すると、定期的に <xref:System.Windows.Threading.Dispatcher> に戻ってイベントを処理できます。 入力を再描画して処理する機会を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に与えることができます。

 計算とイベント処理の間で処理時間を分割する最善の方法は、<xref:System.Windows.Threading.Dispatcher> から計算を管理することです。 <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> メソッドを使用することで、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] イベントが取得される同じキューで素数チェックをスケジュールできます。 この例では、一度に 1 つの素数チェックのみをスケジュールします。 素数チェックが完了したら、次のチェックをすぐにスケジュールします。 このチェックは、保留中の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] イベントが処理された後にのみ実行されます。

 ![ディスパッチャー キューを示すスクリーンショット。](./media/threading-model/threading-dispatcher-queue.png)

 Microsoft Word では、このメカニズムを使用してスペル チェックが実行されます。 スペル チェックは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドのアイドル時間を使用してバックグラウンドで行われます。 コードを見てみましょう。

 次の例は、ユーザー インターフェイスを作成する XAML を示しています。

 [!code-xaml[ThreadingPrimeNumbers#ThreadingPrimeNumberXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingPrimeNumbers/CSharp/Window1.xaml#threadingprimenumberxaml)]

 コードビハインドの例を次に示します。

 [!code-csharp[ThreadingPrimeNumbers#ThreadingPrimeNumberCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingPrimeNumbers/CSharp/Window1.xaml.cs#threadingprimenumbercodebehind)]
 [!code-vb[ThreadingPrimeNumbers#ThreadingPrimeNumberCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingPrimeNumbers/visualbasic/mainwindow.xaml.vb#threadingprimenumbercodebehind)]

 <xref:System.Windows.Controls.Button> のイベント ハンドラーの例を次に示します。

 [!code-csharp[ThreadingPrimeNumbers#ThreadingPrimeNumberStartOrStop](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingPrimeNumbers/CSharp/Window1.xaml.cs#threadingprimenumberstartorstop)]
 [!code-vb[ThreadingPrimeNumbers#ThreadingPrimeNumberStartOrStop](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingPrimeNumbers/visualbasic/mainwindow.xaml.vb#threadingprimenumberstartorstop)]

 このハンドラーは、<xref:System.Windows.Controls.Button> のテキストの更新だけでなく、<xref:System.Windows.Threading.Dispatcher> キューにデリゲートを追加して最初の素数チェックのスケジュールを設定することを担当しています。 このイベント ハンドラーの処理が完了すると、<xref:System.Windows.Threading.Dispatcher> によってこのデリゲートが選択され、実行されます。

 前述のとおり、<xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> はデリゲートの実行をスケジュールするために使用される <xref:System.Windows.Threading.Dispatcher> メンバーです。 この場合、<xref:System.Windows.Threading.DispatcherPriority.SystemIdle> の優先度を選択します。 <xref:System.Windows.Threading.Dispatcher> では、処理する重要なイベントがない場合にのみ、このデリゲートが実行されます。 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の応答性は、数値チェックよりも重要です。 また、数値チェック ルーチンを表す新しいデリゲートも渡します。

 [!code-csharp[ThreadingPrimeNumbers#ThreadingPrimeNumberCheckNextNumber](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingPrimeNumbers/CSharp/Window1.xaml.cs#threadingprimenumberchecknextnumber)]
 [!code-vb[ThreadingPrimeNumbers#ThreadingPrimeNumberCheckNextNumber](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingPrimeNumbers/visualbasic/mainwindow.xaml.vb#threadingprimenumberchecknextnumber)]

 このメソッドでは、次の奇数が素数かどうかがチェックされます。 素数の場合、メソッドによって `bigPrime`<xref:System.Windows.Controls.TextBlock> が直接更新され、その検出が反映されます。 これを実行できるのは、コンポーネントの作成に使用されたものと同じスレッドで計算が行われているためです。 計算に別のスレッドを使用することを選択した場合、より複雑な同期メカニズムを使用して、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで更新を実行する必要があります。 この状況を次に示します。

 このサンプルの完全なソース コードについては、[実行時間が長い計算があるシングルスレッド アプリケーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Threading/SingleThreadedApplication)に関するページを参照してください。

<a name="weather_sim"></a>
### <a name="handling-a-blocking-operation-with-a-background-thread"></a>バックグラウンド スレッドを使用したブロック操作の処理
 グラフィカル アプリケーションでのブロック操作の処理は困難な場合があります。 イベント ハンドラーからはブロック メソッドを呼び出したくありません。これは、アプリケーションがフリーズしたように見えるためです。 別のスレッドを使用してこれらの操作を処理できますが、ワーカー スレッドからは GUI を直接変更できないため、完了したら、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドと同期する必要があります。 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> または <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> を使用して、デリゲートを [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドの <xref:System.Windows.Threading.Dispatcher> に挿入できます。 最終的に、これらのデリゲートは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] 要素を変更するアクセス許可を使用して実行されます。

 この例では、天気予報を取得するリモート プロシージャ コールを模倣しています。 別のワーカー スレッドを使用してこの呼び出しを実行し、完了したら [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドの <xref:System.Windows.Threading.Dispatcher> で更新メソッドをスケジュールします。

 ![天気予報 UI を示すスクリーンショット。](./media/threading-model/threading-weather-ui.png)

 [!code-csharp[ThreadingWeatherForecast#ThreadingWeatherCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingWeatherForecast/CSharp/Window1.xaml.cs#threadingweathercodebehind)]
 [!code-vb[ThreadingWeatherForecast#ThreadingWeatherCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingWeatherForecast/visualbasic/window1.xaml.vb#threadingweathercodebehind)]

 注意する必要がある詳細の一部を次に示します。

- ボタン ハンドラーの作成

     [!code-csharp[ThreadingWeatherForecast#ThreadingWeatherButtonHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingWeatherForecast/CSharp/Window1.xaml.cs#threadingweatherbuttonhandler)]
     [!code-vb[ThreadingWeatherForecast#ThreadingWeatherButtonHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingWeatherForecast/visualbasic/window1.xaml.vb#threadingweatherbuttonhandler)]

 ボタンをクリックすると、時計の描画が表示され、アニメーションが開始されます。 このボタンを無効にします。 新しいスレッドで `FetchWeatherFromServer` メソッドを呼び出してから、戻って、天気予報の収集を待機している間に <xref:System.Windows.Threading.Dispatcher> でイベントを処理できるようにします。

- 天気のフェッチ

     [!code-csharp[ThreadingWeatherForecast#ThreadingWeatherFetchWeather](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingWeatherForecast/CSharp/Window1.xaml.cs#threadingweatherfetchweather)]
     [!code-vb[ThreadingWeatherForecast#ThreadingWeatherFetchWeather](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingWeatherForecast/visualbasic/window1.xaml.vb#threadingweatherfetchweather)]

 簡単にするために、この例にはネットワーク コードを含めていません。 代わりに、ネットワーク アクセスの待機時間をシミュレートするために、新しいスレッドを 4 秒間スリープさせます。 このとき、元の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドはまだ実行中であり、イベントに応答しています。 これを示すために、アニメーションを実行したままにしました。最小化と最大化のボタンも引き続き機能します。

 待機時間が完了し、天気予報をランダムに選択したら、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドに報告します。 これを行うには、そのスレッドの <xref:System.Windows.Threading.Dispatcher> を使用して、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで `UpdateUserInterface` の呼び出しをスケジュールします。 天気を説明する文字列を、このスケジュールされたメソッド呼び出しに渡します。

- [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] の更新

     [!code-csharp[ThreadingWeatherForecast#ThreadingWeatherUpdateUI](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingWeatherForecast/CSharp/Window1.xaml.cs#threadingweatherupdateui)]
     [!code-vb[ThreadingWeatherForecast#ThreadingWeatherUpdateUI](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingWeatherForecast/visualbasic/window1.xaml.vb#threadingweatherupdateui)]

 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッド内の <xref:System.Windows.Threading.Dispatcher> に時間がある場合、スケジュールされた `UpdateUserInterface` の呼び出しが実行されます。 このメソッドによって、時計のアニメーションが停止され、天気を説明する画像が選択されます。 この画像が表示され、"天気予報のフェッチ" ボタンが復元されます。

<a name="multi_browser"></a>
### <a name="multiple-windows-multiple-threads"></a>複数のウィンドウ、複数のスレッド
 一部の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションには、複数の最上位ウィンドウが必要です。 1 つのスレッドと <xref:System.Windows.Threading.Dispatcher> の組み合わせで複数のウィンドウを管理することは完全に許容されていますが、複数のスレッドの方が適切にジョブを実行できる場合もあります。 これは、ウィンドウの 1 つがスレッドを独占する可能性がある場合に特に当てはまります。

 Windows エクスプローラーはこの方法で動作します。 新しいエクスプローラー ウィンドウはそれぞれ元のプロセスに属しますが、独立したスレッドの制御下で作成されます。

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]<xref:System.Windows.Controls.Frame> コントロールを使用して、Web ページを表示できます。 Internet Explorer のシンプルな代替品を簡単に作成できます。 まず重要な機能から始めます。新しいエクスプローラー ウィンドウを開く機能です。 ユーザーが [新しいウィンドウ] ボタンをクリックすると、ウィンドウのコピーが別のスレッドで起動されます。 このように、いずれかのウィンドウで長時間実行またはブロックする操作によって、他のすべてのウィンドウがロックされることはありません。

 実際、Web ブラウザー モデルには独自の複雑なスレッド モデルがあります。 これを選択した理由は、ほとんどの読者にとってなじみ深いものだからです。

 次の例でそのコードを示します。

 [!code-xaml[ThreadingMultipleBrowsers#ThreadingMultiBrowserXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingMultipleBrowsers/CSharp/Window1.xaml#threadingmultibrowserxaml)]

 [!code-csharp[ThreadingMultipleBrowsers#ThreadingMultiBrowserCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingMultipleBrowsers/CSharp/Window1.xaml.cs#threadingmultibrowsercodebehind)]
 [!code-vb[ThreadingMultipleBrowsers#ThreadingMultiBrowserCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingMultipleBrowsers/VisualBasic/Window1.xaml.vb#threadingmultibrowsercodebehind)]

 このコードの次のスレッド セグメントは、このコンテキストで最も興味深いものです。

 [!code-csharp[ThreadingMultipleBrowsers#ThreadingMultiBrowserNewWindow](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingMultipleBrowsers/CSharp/Window1.xaml.cs#threadingmultibrowsernewwindow)]
 [!code-vb[ThreadingMultipleBrowsers#ThreadingMultiBrowserNewWindow](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingMultipleBrowsers/VisualBasic/Window1.xaml.vb#threadingmultibrowsernewwindow)]

 このメソッドは、[新しいウィンドウ] ボタンがクリックされたときに呼び出されます。 新しいスレッドが作成され、非同期に開始されます。

 [!code-csharp[ThreadingMultipleBrowsers#ThreadingMultiBrowserThreadStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ThreadingMultipleBrowsers/CSharp/Window1.xaml.cs#threadingmultibrowserthreadstart)]
 [!code-vb[ThreadingMultipleBrowsers#ThreadingMultiBrowserThreadStart](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ThreadingMultipleBrowsers/VisualBasic/Window1.xaml.vb#threadingmultibrowserthreadstart)]

 このメソッドは、新しいスレッドの始点です。 このスレッドの制御下で新しいウィンドウを作成します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって自動的に新しい <xref:System.Windows.Threading.Dispatcher> が作成され、新しいスレッドが管理されます。 ウィンドウを機能させるために必要なことは、<xref:System.Windows.Threading.Dispatcher> の開始のみです。

<a name="stumbling_points"></a>
## <a name="technical-details-and-stumbling-points"></a>技術的な詳細とつまずくポイント

### <a name="writing-components-using-threading"></a>スレッド処理を使用したコンポーネントの作成
 Microsoft .NET Framework 開発者ガイドでは、コンポーネントでクライアントに非同期動作を公開する方法のパターンが説明されています (「[イベントベースの非同期パターンの概要](../../../standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)」を参照してください)。 たとえば、`FetchWeatherFromServer` メソッドを再利用可能な非グラフィカル コンポーネントにパッケージ化するとします。 標準の Microsoft .NET Framework パターンに従うと、これは次のようになります。

 [!code-csharp[CommandingOverviewSnippets#ThreadingArticleWeatherComponent1](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#threadingarticleweathercomponent1)]
 [!code-vb[CommandingOverviewSnippets#ThreadingArticleWeatherComponent1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#threadingarticleweathercomponent1)]

 `GetWeatherAsync` では、バックグラウンド スレッドの作成など、前述の手法のいずれかを使用して、呼び出しスレッドをブロックせずに非同期で作業を行います。

 このパターンの最も重要な部分の 1 つは、最初に *MethodName*`Async` メソッドを呼び出したものと同じスレッドで *MethodName*`Completed` メソッドを呼び出すことです。 これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用して <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A> を格納することで、とても簡単に実行できます。ただし、この非グラフィカル コンポーネントは、Windows フォームや ASP.NET プログラムではなく、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでのみ使用できます。

 <xref:System.Windows.Threading.DispatcherSynchronizationContext> クラスを使用すると、このニーズに対応できます。これを他の [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] フレームワークでも機能する <xref:System.Windows.Threading.Dispatcher> の簡略化されたバージョンとして考えてください。

 [!code-csharp[CommandingOverviewSnippets#ThreadingArticleWeatherComponent2](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#threadingarticleweathercomponent2)]
 [!code-vb[CommandingOverviewSnippets#ThreadingArticleWeatherComponent2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#threadingarticleweathercomponent2)]

### <a name="nested-pumping"></a>入れ子になったポンプ
 [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドを完全にロックすることができない場合があります。 <xref:System.Windows.MessageBox> クラスの <xref:System.Windows.MessageBox.Show%2A> メソッドについて考えてみましょう。 ユーザーが [OK] ボタンをクリックするまで <xref:System.Windows.MessageBox.Show%2A> は戻りません。 ただし、対話型にするためにメッセージ ループが必要なウィンドウが作成されます。 ユーザーが [OK] をクリックするまで待機している間に、元のアプリケーション ウインドウではユーザー入力に応答しません。 ただし、描画メッセージの処理は続行されます。 元のウィンドウは、隠れたときと、見えるようになったときに再描画されます。

 ![[OK] ボタンのある MessageBox を示すスクリーンショット](./media/threading-model/threading-message-loop.png)

 何らかのスレッドがメッセージ ボックス ウィンドウを担当する必要があります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用して、メッセージ ボックス ウィンドウ専用の新しいスレッドを作成できますが、このスレッドでは元のウィンドウで無効な要素を描画できません (相互排他に関する前述の説明を思い出してください)。 代わりに、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で入れ子になったメッセージ処理システムを使用します。 <xref:System.Windows.Threading.Dispatcher> クラスには、<xref:System.Windows.Threading.Dispatcher.PushFrame%2A> という特殊なメソッドが含まれています。これを使用すると、アプリケーションの現在の実行ポイントを格納してから、新しいメッセージ ループを開始できます。 入れ子になったメッセージ ループが完了すると、元の <xref:System.Windows.Threading.Dispatcher.PushFrame%2A> 呼び出しの後に実行が再開されます。

 この場合、<xref:System.Windows.MessageBox.Show%2A?displayProperty=nameWithType> の呼び出し時にプログラム コンテキストが <xref:System.Windows.Threading.Dispatcher.PushFrame%2A> に保持され、新しいメッセージ ループが開始され、背景ウィンドウが再描画され、メッセージ ボックス ウィンドウへの入力が処理されます。 ユーザーが [OK] をクリックしてポップアップ ウィンドウをクリアすると、入れ子になったループが終了し、<xref:System.Windows.MessageBox.Show%2A> の呼び出し後に制御が再開されます。

### <a name="stale-routed-events"></a>古いルーティング イベント
 イベントが発生すると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のルーティング イベント システムによってツリー全体に通知されます。

 [!code-xaml[InputOvw#ThreadingArticleStaticRoutedEvent](~/samples/snippets/csharp/VS_Snippets_Wpf/InputOvw/CSharp/Page1.xaml#threadingarticlestaticroutedevent)]

 マウスの左ボタンで楕円を押すと、`handler2` が実行されます。 `handler2` が完了すると、イベントは <xref:System.Windows.Controls.Canvas> オブジェクトに渡され、そこで処理に `handler1` が使用されます。 これは、`handler2` によってイベント オブジェクトが処理済みと明示的にマークされない場合にのみ発生します。

 `handler2` でこのイベントを処理するためにかなりの時間がかかる可能性があります。 `handler2` では、<xref:System.Windows.Threading.Dispatcher.PushFrame%2A> を使用して入れ子になったメッセージ ループが開始され、何時間も戻らなくなることがあります。 このメッセージ ループの完了時に `handler2` によってイベントが処理済みとマークされない場合、イベントは、非常に古くても、ツリーの上位に渡されます。

### <a name="reentrancy-and-locking"></a>再入とロック
 共通言語ランタイム (CLR) のロック メカニズムは、想像どおりに動作しません。ロックを要求した場合、スレッドによる操作が完全に停止することを予想するのではないでしょうか。 実際には、スレッドでは引き続き優先度の高いメッセージが受信され、処理されます。 これにより、デッドロックを防止し、インターフェイスの応答性を最小限に抑えることができますが、軽度のバグが発生する可能性があります。  ほとんどの場合、この点について理解する必要はありません。ただし、まれな状況ではありますが (通常は Win32 ウィンドウ メッセージまたは COM STA コンポーネントが関係しています)、この点を理解しておくことが重要な場合があります。

 ほとんどのインターフェイスは、スレッド セーフを考慮して構築されていません。開発者は、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] が複数のスレッドからアクセスされることはないと想定して作業しているためです。 この場合、その 1 つのスレッドで予期しないタイミングで環境が変化し、本来は <xref:System.Windows.Threading.DispatcherObject> 相互排他メカニズムで解決されるはずの悪影響を生じる可能性があります。 次の擬似コードを考えてみましょう。

 ![スレッド処理の再入を示す図。](./media/threading-model/threading-reentrancy.png "ThreadingReentrancy")

 ほとんどの場合は適切ですが、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、このような予期しない再入によって問題を発生する場合があります。 そのため、特定のキー時刻で、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって <xref:System.Windows.Threading.Dispatcher.DisableProcessing%2A> が呼び出されます。これにより、通常の CLR ロックではなく、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 再入可能なロックを使用するように、そのスレッドのロック命令が変更されます。

 では、CLR チームがこの動作を選択したのはなぜでしょうか。 COM STA オブジェクトと終了処理スレッドに対応する必要がありました。 オブジェクトのガベージ コレクションが実行されると、その `Finalize` メソッドは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドではなく、専用のファイナライザー スレッドで実行されます。 ここに問題があります。これは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドで作成された COM STA オブジェクトは、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドでのみ破棄できるためです。 CLR では、(この場合は Win32 の `SendMessage` を使用して) <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> に相当する処理が実行されます。 ただし、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] スレッドがビジーの場合、ファイナライザー スレッドは停止し、COM STA オブジェクトを破棄できないため、重大なメモリ リークが発生します。 そのため、CLR チームは、ロックを適切に機能させるために難しい判断を下しました。

 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のタスクは、メモリ リークを再発生させることなく、予期しない再入を回避することです。そのため、ここでは、あらゆる場所で再入をブロックしていません。

## <a name="see-also"></a>関連項目

- [実行時間の長い計算を使用するシングルスレッド アプリケーションのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Threading/SingleThreadedApplication)
