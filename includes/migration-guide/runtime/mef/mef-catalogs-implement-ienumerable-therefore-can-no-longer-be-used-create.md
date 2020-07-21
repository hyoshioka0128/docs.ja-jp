---
ms.openlocfilehash: 598df2121b480d411dac9c5571772a4a8d22b5ff
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620340"
---
### <a name="mef-catalogs-implement-ienumerable-and-therefore-can-no-longer-be-used-to-create-a-serializer"></a>MEF カタログは IEnumerable を実装するため、シリアライザーの作成には使用できなくなった

#### <a name="details"></a>説明

.NET Framework 4.5 以降では、MEF カタログは IEnumerable を実装するため、シリアライザー (<xref:System.Xml.Serialization.XmlSerializer?displayProperty=fullName> オブジェクト) の作成には使用できなくなりました。 MEF カタログをシリアル化しようとすると、例外がスローされます。

#### <a name="suggestion"></a>提案される解決策

シリアライザーの作成に MEF を使用できなくなりました。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5|
|種類|ランタイム|
