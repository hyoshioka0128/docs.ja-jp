---
ms.openlocfilehash: 7d3568fef933758c40e47cefa86c24d31d4119fc
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620132"
---
### <a name="httprequestcontentencoding-property-prohibits-utf7"></a>HttpRequest.ContentEncoding プロパティで UTF7 が禁止される

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、<xref:System.Web.HttpRequest?displayProperty=fullName> の本文では UTF-7 エンコードが禁止されます。 UTF-7 データの受信を必要とするアプリケーションのデータが、正しくデコードされない場合があります。

#### <a name="suggestion"></a>提案される解決策

理想的には、<xref:System.Web.HttpRequest?displayProperty=fullName> で UTF-7 エンコードを使用しないようにアプリケーションを更新する必要があります。 または、 [appSettings](~/docs/framework/configure-apps/file-schema/appsettings/appsettings-element-for-configuration.md) 要素の <code>aspnet:AllowUtf7RequestContentEncoding</code> 属性を使用して、レガシ動作に戻すことができます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType></li></ul>|
