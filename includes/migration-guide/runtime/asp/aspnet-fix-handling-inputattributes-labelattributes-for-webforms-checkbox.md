---
ms.openlocfilehash: ae557ce57557d027dba35b7da213c08aee85f2c7
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621973"
---
### <a name="aspnet-fix-handling-of-inputattributes-and-labelattributes-for-webforms-checkbox-control"></a>ASP.NET WebForms CheckBox コントロールの InputAttributes および LabelAttributes の処理の修正

#### <a name="details"></a>説明

.NET Framework 4.7.2 以前のバージョンをターゲットとするアプリケーションでは、WebForms <xref:System.Web.UI.WebControls.CheckBox> コントロールにプログラムで追加された <xref:System.Web.UI.WebControls.CheckBox.InputAttributes?displayProperty=nameWithType> および <xref:System.Web.UI.WebControls.CheckBox.LabelAttributes?displayProperty=nameWithType> がポストバック後に失われます。 .NET Framework 4.8 以降のバージョンをターゲットとするアプリケーションでは、これらはポストバック後に保持されます。

#### <a name="suggestion"></a>提案される解決策

ポストバック時に属性を復元する動作を正しいものにするには、<code>targetFrameworkVersion</code> を 4.8 以降に設定します。 次に例を示します。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;system.web&gt;&#13;&#10;&lt;httpRuntime targetFramework=&quot;4.8&quot;/&gt;&#13;&#10;&lt;/system.web&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>これより小さい値に設定した場合、または、まったく設定しない場合、適切でない古い動作が維持されます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |不明|
|バージョン|4.8|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Web.UI.WebControls.CheckBox?displayProperty=nameWithType></li></ul>|
