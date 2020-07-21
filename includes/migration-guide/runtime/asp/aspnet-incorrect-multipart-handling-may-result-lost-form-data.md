---
ms.openlocfilehash: 135d59de135c8416d384b221379f912c8a9172ad
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621972"
---
### <a name="aspnet-incorrect-multipart-handling-may-result-in-lost-form-data"></a>ASP.NET 正しくないマルチパート処理により、フォーム データが失われる場合がある。

#### <a name="details"></a>説明

.NET Framework 4.7.2 以前のバージョンをターゲットとするアプリケーションでは、ASP.Net でマルチパート境界の値が正しく解析されないために、要求の実行中にフォーム データが使用できなくなる場合があります。 .NET Framework 4.8 以降のバージョンをターゲットとするアプリケーションではマルチパート データが正しく解析されるため、要求の実行中にフォーム値を使用することができます。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.8 以降で実行されているアプリケーションで、Framework 4.8 以降をターゲットとする場合は、<code>targetFrameworkVersion</code> 要素を使用して、区切り記号を削除するように既定の動作を変更します。 以前のフレームワークのバージョンをターゲットとするか、<code>targetFrameworkVersion</code> を使用しない場合、一部の値の末尾の区切り記号が引き続き返されます。この動作は、<code>appSetting</code> で明示的に制御することもできます。<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;aspnet:UseLegacyMultiValueHeaderHandling&quot;  value=&quot;true&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |不明|
|バージョン|4.8|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Web.HttpRequest.Form?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.Files?displayProperty=nameWithType></li><li><xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType></li></ul>|
