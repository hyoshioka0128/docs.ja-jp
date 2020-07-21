---
ms.openlocfilehash: 4a22d78f2308aab544d7a7d2e4d05ddc1ad5457d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617237"
---
### <a name="xml-schema-validation-is-stricter"></a>XML スキーマ検証がより厳格になりました

#### <a name="details"></a>説明

.NET Framework 4.5 では、XML スキーマ検証が厳格化されました。 xsd:anyURI を使用して mailto プロトコルなどの URI を検証したときに、URI にスペースが入っていると検証は失敗します。 .NET Framework の以前のバージョンでは、検証は成功していました。 この変更は、.NET Framework 4.5 を対象とするアプリケーションにのみ影響します。

#### <a name="suggestion"></a>提案される解決策

より緩やかな .NET Framework 4.0 の検証が必要な場合、検証アプリケーションはバージョン 4.0 の .NET Framework をターゲットにできます。 もう一度 .NET Framework 4.5 をターゲットにする場合は、無効な URI (およびスペース) が anyURI データ型の属性値として予期されないように、コード レビューを行う必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.5         |
| 種類    | 再ターゲット中 |
