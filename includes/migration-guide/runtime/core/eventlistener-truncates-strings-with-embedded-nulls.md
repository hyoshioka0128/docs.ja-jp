---
ms.openlocfilehash: 6f5c1ecead4e2f74e621354058aab70bfa1cccb6
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620225"
---
### <a name="eventlistener-truncates-strings-with-embedded-nulls"></a>EventListener は、null が埋め込まれた文字列を切り捨てる

#### <a name="details"></a>説明

<xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> は、埋め込まれた null のある文字列を切り捨てます。 null 文字は <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> クラスでサポートされません。 変更は、プロセスの <xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> データを読み取るために <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> を使用し、区切り記号として null 文字を使用するアプリにのみ影響します。

#### <a name="suggestion"></a>提案される解決策

可能な場合は、埋め込まれた null 文字を使用しないように <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> データを更新する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5.1|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Diagnostics.Tracing.EventListener.%23ctor></li><li><xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords)?displayProperty=nameWithType></li><li><xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords,System.Collections.Generic.IDictionary{System.String,System.String})?displayProperty=nameWithType></li></ul>|
