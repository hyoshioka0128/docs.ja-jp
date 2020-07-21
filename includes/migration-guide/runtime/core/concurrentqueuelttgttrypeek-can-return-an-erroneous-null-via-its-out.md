---
ms.openlocfilehash: 02a15f6b9c02002b60c568b9e1d871af49744092
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622047"
---
### <a name="concurrentqueuelttgttrypeek-can-return-an-erroneous-null-via-its-out-parameter"></a>ConcurrentQueue&lt;T&gt;.TryPeek は、出力パラメーターを介して誤った null を返すことがあります

#### <a name="details"></a>説明

一部のマルチ スレッド シナリオでは、<xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=fullName> は true を返すことができますが、出力パラメーターに (正しいピーク値の代わりに) null 値を入れることがあります。

#### <a name="suggestion"></a>提案される解決策

この問題は、.NET Framework 4.5.1 で修正されます。 この Framework にアップグレードすると、問題が解決されます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Collections.Concurrent.ConcurrentQueue%601.TryPeek(%600@)?displayProperty=nameWithType></li></ul>|
