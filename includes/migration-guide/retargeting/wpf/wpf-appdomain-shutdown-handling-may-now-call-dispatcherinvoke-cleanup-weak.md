---
ms.openlocfilehash: 8b804d23247b95381f3ff83bc12c32215a420fb6
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614961"
---
### <a name="wpf-appdomain-shutdown-handling-may-now-call-dispatcherinvoke-in-cleanup-of-weak-events"></a>WPF での AppDomain のシャットダウン処理により、弱いイベントのクリーンアップで Dispatcher.Invoke が呼び出される可能性がある

#### <a name="details"></a>説明

.NET Framework 4.7.1 以前のバージョンでは、WPF は AppDomain のシャットダウン中に .NET ファイナライザー スレッドで <xref:System.Windows.Threading.Dispatcher?displayProperty=nameWithType> を作成する可能性があります。  これは、.NET Framework 4.7.2 以降のバージョンでは、弱いイベントのクリーンアップをスレッド対応にすることによって修正されました。  このため、WPF は <xref:System.Windows.Threading.Dispatcher.Invoke%2A?displayProperty=nameWithType> を呼び出してクリーンアップ プロセスを完了することがあります。特定のアプリケーションでは、このファイナライザーのタイミングの変更により、AppDomain またはプロセスのシャットダウン中に例外が発生する可能性があります。  これは、プロセスまたは AppDomain のシャットダウン前にワーカー スレッドで実行されているディスパッチャーを正しくシャットダウンしないアプリケーションで一般的に見られます。  そのようなアプリケーションは、ディスパッチャーの有効期間を適切に管理するように注意する必要があります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.2 以降のバージョンでは、開発者は、クリーンアップの変更によって発生する可能性のあるタイミングの問題を軽減する (ただし、排除ではない) ために、この修正を無効にすることができます。クリーンアップの変更を無効にするには、次の AppContext フラグを使用します。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.MS.Internal.DoNotInvokeInWeakEventTableShutdownListener=true&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7.2       |
| 種類    | 再ターゲット中 |
