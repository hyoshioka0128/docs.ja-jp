---
ms.openlocfilehash: 00ffc782c9a15c0d88f797f52372b4658706b350
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620426"
---
### <a name="glyphruncomputeinkboundingbox-and-formattedtextextent-return-different-values-beginning-in-net-framework-45"></a>GlyphRun.ComputeInkBoundingBox() と FormattedText.Extent が、.NET Framework 4.5 以降では、異なる値を返す

#### <a name="details"></a>説明

.NET Framework 4.5 では、<xref:System.Windows.Media.GlyphRun.ComputeInkBoundingBox> と <xref:System.Windows.Media.FormattedText.Extent> が改善され、場合によっては含まれるグリフに対してボックスが小さすぎるという .NET Framework 4.0 での問題に対応しました。 この結果、.NET Framework 4.5 以降では、いくつかの境界ボックスが大きくなり、UI のレイアウトにわずかな違いが生じます。

#### <a name="suggestion"></a>提案される解決策

いくつかのグリフの境界ボックスのサイズが大きくなったことに注意してください。 このような変更は、通常、プレゼンテーションおよびヒット ボックス テストを向上させますが、以前の (.NET 4.5 より前の) 動作が望ましい場合は、次のエントリをアプリの構成ファイルに追加することによって実現できます。<pre><code class="lang-xml">&lt;appsettings&gt;&#13;&#10;&lt;add key=&quot;IncludeAllInkInBoundingBox&quot; value=&quot;false&quot;&gt;&#13;&#10;&lt;/appsettings&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Media.GlyphRun.ComputeInkBoundingBox?displayProperty=nameWithType></li><li><xref:System.Windows.Media.FormattedText.Extent?displayProperty=nameWithType></li></ul>|
