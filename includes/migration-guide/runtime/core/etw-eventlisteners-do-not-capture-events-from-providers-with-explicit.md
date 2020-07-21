---
ms.openlocfilehash: 7d50962b518c15875a5f1a82f5b89ab87a1db02e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620235"
---
### <a name="etw-eventlisteners-do-not-capture-events-from-providers-with-explicit-keywords-like-the-tpl-provider"></a>ETW EventListeners は、明示的なキーワードを持つプロバイダーからのイベント (TPL プロバイダーなど) をキャプチャしません

#### <a name="details"></a>説明

空白のキーワード マスクを持つ ETW EventListeners は、明示的なキーワードを持つプロバイダーからのイベントを正しくキャプチャしません。 .NET Framework 4.5 では、TPL プロバイダーは、明示的なキーワードを提供するようになり、この問題が発生しました。 .NET Framework 4.6 では、EventListeners が更新され、この問題は修正されました。

#### <a name="suggestion"></a>提案される解決策

この問題を回避するには、<xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel)> の呼び出しを、使用する &quot;任意のキーワード&quot; マスクを明示的に指定する EnableEvents オーバーロード (<code>EnableEvents(eventSource, level, unchecked((EventKeywords)0xFFFFffffFFFFffff))</code>) の呼び出しに置換します。または、この問題は .NET Framework 4.6 で修正されたため、このバージョンの .NET Framework にアップグレードすることによって対処できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel)?displayProperty=nameWithType></li></ul>|
