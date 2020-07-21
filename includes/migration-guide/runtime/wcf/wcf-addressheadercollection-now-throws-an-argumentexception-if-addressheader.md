---
ms.openlocfilehash: d29be721b50d1c93723b325774a06e86f77dbebf
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621224"
---
### <a name="wcf-addressheadercollection-now-throws-an-argumentexception-if-an-addressheader-element-is-null"></a>addressHeader 要素が null の場合、WCF AddressHeaderCollection で ArgumentException がスローされるようになった

#### <a name="details"></a>説明

.NET Framework 4.7.1 以降では、要素のいずれかが <code>null</code> の場合、<xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> コンストラクターで <xref:System.ArgumentException> がスローされます。 .NET Framework 4.7 以前のバージョンでは、例外はスローされません。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 以降のバージョンでこの変更に関する互換性の問題が発生した場合は、次の行を app.config ファイルの <code>&lt;runtime&gt;</code> セクションに追加することで、無効にできます。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.ServiceModel.DisableAddressHeaderCollectionValidation=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.7.1|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})></li></ul>|
