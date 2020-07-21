---
ms.openlocfilehash: 80e61d4dd5b8d4754a39e95e37475fefff57fcbd
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617172"
---
### <a name="new-ambiguous-dispatcherinvoke-overloads-could-result-in-different-behavior"></a>新しい (あいまいな) Dispatcher.Invoke オーバーロードが、異なる動作になる可能性がある

#### <a name="details"></a>説明

.NET Framework 4.5 では、<xref:System.Action> 型のパラメーターを含む <xref:System.Windows.Threading.Dispatcher.Invoke%2A?displayProperty=nameWithType> に新しいオーバーロードが追加されます。 既存のコードを再コンパイルすると、コンパイラは、<xref:System.Delegate> パラメーターを持つ Dispatcher.Invoke メソッドの呼び出しを、<xref:System.Action> パラメーターを持つ Dispatcher.Invoke メソッドの呼び出しとして解決することができます。 <xref:System.Delegate> パラメーターを持つ Dispatcher.Invoke オーバーロードの呼び出しが <xref:System.Action> パラメーターを持つ Dispatcher.Invoke オーバーロードの呼び出しとして解決された場合、次のような動作の差異が生じることがあります。

- 例外が発生した場合、<xref:System.Windows.Threading.Dispatcher.UnhandledExceptionFilter> イベントと <xref:System.Windows.Threading.Dispatcher.UnhandledException> イベントは発生しません。 代わりに、例外は <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException?displayProperty=fullName> イベントによって処理されます。
- <xref:System.Windows.Threading.DispatcherOperation.Result> などの一部のメンバーの呼び出しは、操作が完了するまでブロックされます。

#### <a name="suggestion"></a>提案される解決策

あいまいさ (および例外処理またはブロック動作における考えられる相違点) を回避するために、呼び出し元の Dispatcher.Invoke は Invoke 呼び出しの 2 番目のパラメーターとして空の object[] を渡すことで、.NET Framework 4.0 メソッドのオーバーロードに解決されるようにできます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Object[])?displayProperty=nameWithType>
- <xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Object[])?displayProperty=nameWithType>
- <xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.TimeSpan,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType>
- <xref:System.Windows.Threading.Dispatcher.Invoke(System.Delegate,System.Windows.Threading.DispatcherPriority,System.Object[])?displayProperty=nameWithType>
