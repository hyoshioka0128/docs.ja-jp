---
title: .NET Core の EventCounters
description: この記事では、EventCounters の概要とその実装方法および使用方法について学習します。
ms.date: 08/07/2020
ms.openlocfilehash: be273776b888f13893fc694a111093cca1fa8a5e
ms.sourcegitcommit: b59237ca4ec763969a0dd775a3f8f39f8c59fe24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91955318"
---
# <a name="eventcounters-in-net-core"></a>.NET Core の EventCounters

**この記事の対象: ✔️** .NET Core 3.0 SDK 以降のバージョン

EventCounters は、軽量でクロスプラットフォームであり、ほぼリアルタイムのパフォーマンス メトリックの収集に使用される .NET Core API です。 EventCounters は、Windows 上の .NET Framework の "パフォーマンス カウンター" に代わるクロスプラットフォームとして追加されました。 この記事では、EventCounters の概要とその実装方法および使用方法について学習します。

.NET Core ランタイムといくつかの .NET ライブラリにより、.NET Core 3.0 以降の EventCounters が使用され、基本的な診断情報が公開されます。 .NET ランタイムによって提供される EventCounters とは別に、独自の EventCounters を実装することもできます。 EventCounters を使用して、さまざまなメトリックを追跡できます。

EventCounters は <xref:System.Diagnostics.Tracing.EventSource> の一部として存在し、定期的にリスナー ツールに自動的にプッシュされます。 <xref:System.Diagnostics.Tracing.EventSource> の他のすべてのイベントと同様に、<xref:System.Diagnostics.Tracing.EventListener> と EventPipe を介してインプロセスとアウトプロセスの両方で使用できます。 この記事では、EventCounters のクロスプラットフォーム機能に焦点を当てています。PerfView と ETW (Event Trace for Windows) は意図的に除外していますが、両方とも EventCounters で使用できます。

![EventCounters のインプロセスとアウトプロセスの図のイメージ](media/event-counters.svg)

[!INCLUDE [available-counters](includes/available-counters.md)]

## <a name="eventcounter-api-overview"></a>EventCounter API の概要

カウンターには主に 2 つのカテゴリがあります。 一部のカウンターは、例外の合計数、GC の合計数、要求の合計数などの "比率" の値用です。 その他のカウンターは、ヒープ使用率、CPU 使用率、ワーキング セット サイズなどの "スナップショット" の値です。 これらのカウンターの各カテゴリ内には、値の取得方法によって異なる 2 種類のカウンターがあります。 ポーリング カウンターによって、コールバックを介して値が取得され、ポーリング以外のカウンターの値は、カウンター インスタンスで直接設定されます。

これらのカウンターは、次の実装によって表されます。

* <xref:System.Diagnostics.Tracing.EventCounter>
* <xref:System.Diagnostics.Tracing.IncrementingEventCounter>
* <xref:System.Diagnostics.Tracing.IncrementingPollingCounter>
* <xref:System.Diagnostics.Tracing.PollingCounter>

イベント リスナーによって、測定間隔の長さが指定されます。 各間隔の最後に、各カウンターのリスナーに値が送信されます。 カウンターの実装によって、各間隔の値を生成するために使用される API と計算が決まります。

1. <xref:System.Diagnostics.Tracing.EventCounter> によって、値のセットが記録されます。 <xref:System.Diagnostics.Tracing.EventCounter.WriteMetric%2A?displayProperty=nameWithType> メソッドによって、新しい値がセットに追加されます。 各間隔では、最小値、最大値、平均値など、セットの統計概要が計算されます。 [dotnet-counters](dotnet-counters.md) ツールによって、常に平均値が表示されます。 <xref:System.Diagnostics.Tracing.EventCounter> は、個別の操作セットを記述する場合に役立ちます。 一般的な用途には、最近の IO 操作の平均サイズ (バイト単位) や、金融取引セットの平均額の監視が含まれる場合があります。

1. <xref:System.Diagnostics.Tracing.IncrementingEventCounter> によって、各時間間隔の累計が記録されます。 <xref:System.Diagnostics.Tracing.IncrementingEventCounter.Increment%2A?displayProperty=nameWithType> メソッドによって、合計に加算されます。 たとえば、値が `1`、`2`、および `5` に指定され、1 つの間隔で `Increment()` が 3 回呼び出された場合、`8` の累計は、この間隔のカウンター値として報告されます。 [dotnet-counters](dotnet-counters.md) ツールにより、記録された合計/時間として比率が表示されます。 <xref:System.Diagnostics.Tracing.IncrementingEventCounter> は、1 秒あたりに処理された要求の数など、アクションの発生頻度を測定するのに役立ちます。

1. <xref:System.Diagnostics.Tracing.PollingCounter> によってコールバックが使用され、報告される値が決定されます。 各時間間隔で、ユーザーが指定したコールバック関数が呼び出され、戻り値がカウンター値として使用されます。 <xref:System.Diagnostics.Tracing.PollingCounter> を使用すると、ディスク上の現在の空きバイト数を取得するなど、外部ソースからのメトリックに対してクエリを実行できます。 また、アプリケーションで要求時に計算できるカスタム統計を報告するために使用できます。 たとえば、最近の要求待機時間の 95 パーセンタイルや、キャッシュの現在のヒットまたはミス率の報告などです。

1. <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> によってコールバックが使用され、報告される増分値が決定されます。 各時間間隔で、コールバックが呼び出され、現在の呼び出しと最後の呼び出しの差が報告される値となります。 [dotnet-counters](dotnet-counters.md) ツールにより、比率 (報告された値/時間) として常に差が表示されます。 このカウンターは、発生のたびに API を呼び出すことができない場合に便利ですが、発生の合計回数に対してクエリを実行することもできます。 たとえば、バイトが書き込まれるたびに通知しなくても、1 秒あたりにファイルに書き込まれたバイト数を報告することができます。

## <a name="implement-an-eventsource"></a>EventSource を実装する

次のコードにより、名前付きの `"Sample.EventCounter.Minimal"` プロバイダーとして公開されるサンプルの <xref:System.Diagnostics.Tracing.EventSource> が実装されます。 このソースには、要求の処理時間を表す <xref:System.Diagnostics.Tracing.EventCounter> が含まれています。 このようなカウンターには、名前 (つまり、ソースのその一意の ID) と表示名があり、両方とも [dotnet-counter](dotnet-counters.md) などのリスナー ツールで使用されます。

:::code language="csharp" source="snippets/EventCounters/MinimalEventCounterSource.cs":::

監視できる .NET プロセスの一覧を表示するには、`dotnet-counters ps` を使用します。

```console
dotnet-counters ps
   1398652 dotnet     C:\Program Files\dotnet\dotnet.exe
   1399072 dotnet     C:\Program Files\dotnet\dotnet.exe
   1399112 dotnet     C:\Program Files\dotnet\dotnet.exe
   1401880 dotnet     C:\Program Files\dotnet\dotnet.exe
   1400180 sample-counters C:\sample-counters\bin\Debug\netcoreapp3.1\sample-counters.exe
```

カウンターの監視を開始するには、<xref:System.Diagnostics.Tracing.EventSource> の名前を `counter_list` スイッチに渡します。

```console
dotnet-counters monitor --process-id 1400180 Sample.EventCounter.Minimal
```

次の例は監視出力を示しています。

```console
Press p to pause, r to resume, q to quit.
    Status: Running

[Samples-EventCounterDemos-Minimal]
    Request Processing Time (ms)                            0.445
```

監視コマンドを停止するには、<kbd>q</kbd> キーを押します。

#### <a name="conditional-counters"></a>条件付きカウンター

<xref:System.Diagnostics.Tracing.EventSource> を実装する場合、<xref:System.Diagnostics.Tracing.EventCommandEventArgs.Command> の値として `EventCommand.Enable` を指定して、<xref:System.Diagnostics.Tracing.EventSource.OnEventCommand%2A?displayProperty=nameWithType> メソッドが呼び出されると、格納先のカウンターを条件付きでインスタンス化できます。 `null` である場合にのみ、カウンター インスタンスを安全にインスタンス化するには、[null 合体代入演算子](../../csharp/language-reference/operators/null-coalescing-operator.md)を使用します。 さらに、カスタム メソッドで <xref:System.Diagnostics.DiagnosticSource.IsEnabled%2A> メソッドを評価して、現在のイベント ソースが有効になっているかどうかを判断できます。

:::code language="csharp" source="snippets/EventCounters/ConditionalEventCounterSource.cs":::

> [!TIP]
> 条件付きカウンターは、条件付きでインスタンス化 (マイクロ最適化) されるカウンターです。 ランタイムにより、わずかな時間を節約するために、通常はカウンターが使用されないシナリオでこのパターンが採用されます。

### <a name="net-core-runtime-example-counters"></a>.NET Core ランタイムのカウンター例

.NET Core ランタイムには、多くの優れた実装例があります。 アプリケーションのワーキング セット サイズを追跡するカウンターのランタイム実装を以下に示します。

```csharp
var workingSetCounter = new PollingCounter(
    "working-set",
    this,
    () => (double)(Environment.WorkingSet / 1_000_000))
{
    DisplayName = "Working Set",
    DisplayUnits = "MB"
};
```

<xref:System.Diagnostics.Tracing.PollingCounter> により、アプリのプロセス (ワーキング セット) にマップされる物理メモリの現在の量が報告されます。これは、ある時点のメトリックがキャプチャされるためです。 値をポーリングするためのコールバックは、指定されたラムダ式であり、単に <xref:System.Environment.WorkingSet?displayProperty=fullName> API の呼び出しです。 <xref:System.Diagnostics.Tracing.DiagnosticCounter.DisplayName> および <xref:System.Diagnostics.Tracing.DiagnosticCounter.DisplayUnits> は、カウンターのコンシューマー側でより明確に値を表示するのに役立つように設定できる省略可能なプロパティです。 たとえば、よりわかりやすいバージョンのカウンター名を表示するために、[dotnet-counters](dotnet-counters.md) によってこれらのプロパティが使用されます。

> [!IMPORTANT]
> `DisplayName` のプロパティはローカライズされません。

<xref:System.Diagnostics.Tracing.PollingCounter>、および <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> では、他に何も行う必要はありません。 いずれの場合も、コンシューマーによって要求された間隔で値自体がポーリングされます。

<xref:System.Diagnostics.Tracing.IncrementingPollingCounter> を使用して実装されたランタイム カウンターの例を以下に示します。

```csharp
var monitorContentionCounter = new IncrementingPollingCounter(
    "monitor-lock-contention-count",
    this,
    () => Monitor.LockContentionCount
)
{
    DisplayName = "Monitor Lock Contention Count",
    DisplayRateTimeScale = TimeSpan.FromSeconds(1)
};
```

ロック競合の合計数の増加を報告するために、<xref:System.Diagnostics.Tracing.IncrementingPollingCounter> によって <xref:System.Threading.Monitor.LockContentionCount?displayProperty=nameWithType> API が使用されます。 <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale> プロパティは省略可能ですが、これを使用すると、カウンターが最適に表示される時間間隔に関するヒントを提供できます。 たとえば、ロック競合数は、"_1 秒あたりの数_" として最適に表示されるので、その <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale> は 1 秒に設定されます。 表示率は、さまざまな種類の比率カウンターに合わせて調整できます。

> [!NOTE]
> <xref:System.Diagnostics.Tracing.IncrementingPollingCounter.DisplayRateTimeScale> は [dotnet-counters](dotnet-counters.md) によって使用 "_されません_"。また、それを使用するためにイベント リスナーは必要ありません。

[.NET ランタイム](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Private.CoreLib/src/System/Diagnostics/Tracing/RuntimeEventSource.cs) リポジトリで参照として使用するカウンター実装は他にもあります。

## <a name="concurrency"></a>コンカレンシー

> [!TIP]
> EventCounters API によるスレッド セーフは保証されません。 <xref:System.Diagnostics.Tracing.PollingCounter> または <xref:System.Diagnostics.Tracing.IncrementingPollingCounter> インスタンスに渡された委任が複数のスレッドによって呼び出された場合、委任のスレッドセーフを保証するのはお客様の責任となります。

たとえば、要求を追跡する以下の <xref:System.Diagnostics.Tracing.EventSource> について考えてみます。

:::code language="csharp" source="snippets/EventCounters/RequestEventSource.cs":::

`AddRequest()` メソッドは要求ハンドラーから呼び出すことができ、カウンターのコンシューマーによって指定された間隔で、`RequestRateCounter` により値がポーリングされます。 しかし、`AddRequest()` メソッドは、一度に複数のスレッドによって呼び出すことができ、`_requestCount` で競合状態が発生します。 `_requestCount` を増分させるスレッドセーフな別の方法は、<xref:System.Threading.Interlocked.Increment%2A?displayProperty=nameWithType> を使用することです。

```csharp
public void AddRequest() => Interlocked.Increment(ref _requestCount);
```

(32 ビット アーキテクチャでの) `long`-field `_requestCount` の読み取りの欠落を防ぐには、<xref:System.Threading.Interlocked.Read%2A?displayProperty=nameWithType> を使用します。

```csharp
_requestRateCounter = new IncrementingPollingCounter("request-rate", this, () => Interlocked.Read(ref _requestCount))
{
    DisplayName = "Request Rate",
    DisplayRateTimeScale = TimeSpan.FromSeconds(1)
};
```

## <a name="consume-eventcounters"></a>EventCounters を使用する

EventCounters を使用する場合、インプロセスとアウトプロセスという 2 つの主な方法があります。 EventCounters の使用は、さまざまな使用テクノロジの 3 つの層に分類できます。

- ETW または EventPipe を介した生のストリームでのイベントの転送:
  - ETW API は Windows OS に付属しています。EventPipe には [.NET API](https://github.com/dotnet/diagnostics/blob/master/documentation/design-docs/diagnostics-client-library.md#1-attaching-to-a-process-and-dumping-out-all-the-runtime-gc-events-in-real-time-to-the-console)、または診断 [IPC プロトコル](https://github.com/dotnet/diagnostics/blob/master/documentation/design-docs/ipc-protocol.md)としてアクセスできます。
- バイナリ イベント ストリームのイベントへのデコード:
  - [TraceEvent ライブラリ](https://www.nuget.org/packages/Microsoft.Diagnostics.Tracing.TraceEvent)により、ETW と EventPipe の両方のストリーム形式が処理されます。
- コマンド ラインと GUI ツール:
  - PerfView (ETW または EventPipe)、dotnet-counters (EventPipe のみ)、dotnet-monitor (EventPipe のみ) などのツール。

### <a name="consume-out-of-proc"></a>アウトプロセスで使用する

EventCounters をアウトプロセスで使用することは、非常に一般的な方法です。 [dotnet-counters](dotnet-counters.md) を使って、EventPipe を介してクロスプラットフォーム方式でそれらを使用することができます。 `dotnet-counters` ツールは、カウンターの値を監視するために使用できるクロスプラットフォームの dotnet CLI グローバル ツールです。 `dotnet-counters` を使用してカウンターを監視する方法を確認する場合は、「[dotnet-counters](dotnet-counters.md)」を参照するか、[EventCounters を使用するパフォーマンスの測定](event-counter-perf.md)に関するチュートリアルを実行してください。

#### <a name="dotnet-trace"></a>dotnet-トレース

`dotnet-trace` ツールを使って、EventPipe を介してカウンター データを使用することができます。 カウンター データを収集するために `dotnet-trace` を使用する例を以下に示します。

```console
dotnet-trace collect --process-id <pid> Sample.EventCounter.Minimal:0:0:EventCounterIntervalSec=1
```

経時的なカウンター値を収集する方法の詳細については、[dotnet-trace](dotnet-trace.md#use-dotnet-trace-to-collect-counter-values-over-time) に関するドキュメントを参照してください。

#### <a name="azure-application-insights"></a>Azure Application Insights

EventCounters は Azure Monitor、つまり、Azure Application Insights で使用できます。 カウンターを追加したり、削除したりすることができます。また、カスタム カウンターや既知のカウンターを自由に指定することができます。 詳細については、「[収集されるカウンターのカスタマイズ](/azure/azure-monitor/app/eventcounters#customizing-counters-to-be-collected)」を参照してください。

#### <a name="dotnet-monitor"></a>dotnet-monitor

`dotnet-monitor` ツールは、.NET プロセスでの診断情報へのアクセスを容易にする実験用のツールです。 このツールは、すべての診断ツールのスーパーセットとして機能します。 トレースに加えて、メトリックの監視、メモリ ダンプの収集、および GC ダンプの収集を行うことができます。 CLI ツールと Docker イメージの両方として配布されます。 これによって REST API が公開され、診断アーティファクトの収集は REST 呼び出しを介して行われます。

詳細については、「[実験用のツール、dotnet-monitor の概要](https://devblogs.microsoft.com/dotnet/introducing-dotnet-monitor)」を参照してください。

### <a name="consume-in-proc"></a>インプロセスで使用する

<xref:System.Diagnostics.Tracing.EventListener> API を介して、カウンター値を使用することができます。 <xref:System.Diagnostics.Tracing.EventListener> は、アプリケーション内の <xref:System.Diagnostics.Tracing.EventSource> のすべてのインスタンスによって書き込まれるすべてのイベントを使用するインプロセスの方法です。 `EventListener` API の使用方法の詳細については、<xref:System.Diagnostics.Tracing.EventListener> に関するページを参照してください。

まず、カウンター値を生成する <xref:System.Diagnostics.Tracing.EventSource> を有効にする必要があります。 <xref:System.Diagnostics.Tracing.EventSource> が作成されたときに通知を受け取るように <xref:System.Diagnostics.Tracing.EventListener.OnEventSourceCreated%2A?displayProperty=nameWithType> メソッドをオーバーライドします。これが EventCounters に適切な <xref:System.Diagnostics.Tracing.EventSource> である場合は、それに対して <xref:System.Diagnostics.Tracing.EventListener.EnableEvents%2A?displayProperty=nameWithType> を呼び出すことができます。 オーバーライドの例を以下に示します。

:::code language="csharp" source="snippets/EventCounters/SimpleEventListener.cs" range="16-27":::

#### <a name="sample-code"></a>サンプル コード

以下は、内部カウンター (`System.Runtime`) を一定の間隔で公開するために、.NET ランタイムの <xref:System.Diagnostics.Tracing.EventSource> からすべてのカウンターの名前と値を出力する <xref:System.Diagnostics.Tracing.EventListener> クラスのサンプルです。

:::code language="csharp" source="snippets/EventCounters/SimpleEventListener.cs":::

前述のように、<xref:System.Diagnostics.Tracing.EventListener.EnableEvents%2A> を呼び出す場合は、`filterPayload` 引数に `"EventCounterIntervalSec"` 引数が設定されていることを確認する "_必要があります_"。 そうしないと、カウンターによってフラッシュする必要がある間隔が把握されないため、値をフラッシュできなくなります。

## <a name="see-also"></a>関連項目

- [dotnet-カウンター](dotnet-counters.md)
- [dotnet-トレース](dotnet-trace.md)
- <xref:System.Diagnostics.Tracing.EventCounter>
- <xref:System.Diagnostics.Tracing.EventListener>
- <xref:System.Diagnostics.Tracing.EventSource>
