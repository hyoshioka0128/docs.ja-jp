---
ms.openlocfilehash: b2fcacdb02c411c4dcb12051bf0c6759faccdea2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620390"
---
### <a name="the-replace-method-in-odata-urls-is-disabled-by-default"></a>OData URL の Replace メソッドが既定で無効になる

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、OData URL の Replace メソッドは既定では無効です。 OData Replace が無効のとき (既定)、replace 関数を含むユーザー要求 (一般的ではない) は失敗します。

#### <a name="suggestion"></a>提案される解決策

Replace メソッドが必要な場合 (一般的ではない)、構成設定 (<xref:System.Data.Services.Configuration.DataServicesFeaturesSection.ReplaceFunction?displayProperty=fullName>) によって再び有効にできます。 ただし、有効になった replace メソッドはセキュリティの脆弱性を開くことがあり、慎重にレビューしてから使用する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Data.Services.DataService%601?displayProperty=nameWithType></li></ul>|
