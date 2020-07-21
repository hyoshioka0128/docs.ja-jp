---
ms.openlocfilehash: a8f51dfa1c82e3b166449d2432dfe8a9b96564b9
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620199"
---
### <a name="blockingcollectionlttgttrytakefromany-does-not-throw-anymore"></a>BlockingCollection&lt;T&gt;.TryTakeFromAny がスローしなくなった

#### <a name="details"></a>説明

入力コレクションの 1 つに完了のマークが付けられた場合、<xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)> -1 を返さず、<xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)>例外をスローしなくなりました。 この変更の結果、コレクションの 1 つが空であったり完了していても、他のコレクションに取得できる項目がある場合にコレクションで作業をすることができるようになりました。

#### <a name="suggestion"></a>提案される解決策

-1 を返す TryTakeFromAny またはスローする TakeFromAny が制御フロー目的で使用されていた場合、ブロッキング コレクションが完了する場合、そのようなコードは、その条件を検出するように <code>.Any(b =&gt; b.IsCompleted)</code> を使用するように変更される必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Threading.CancellationToken)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.Int32)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li><li><xref:System.Collections.Concurrent.BlockingCollection%601.TryTakeFromAny(System.Collections.Concurrent.BlockingCollection{%600}[],%600@,System.TimeSpan)?displayProperty=nameWithType></li></ul>|
