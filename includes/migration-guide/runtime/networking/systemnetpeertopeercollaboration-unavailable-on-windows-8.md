---
ms.openlocfilehash: 311adfdc98c766adf1e88ee9bc7e601d2cd13ba5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620350"
---
### <a name="systemnetpeertopeercollaboration-unavailable-on-windows-8"></a>Windows 8 で System.Net.PeerToPeer.Collaboration が使用できない

#### <a name="details"></a>説明

System.Net.PeerToPeer.Collaboration 名前空間は、Windows 8 以上では使用できません。

#### <a name="suggestion"></a>提案される解決策

Windows 8 以上をサポートするアプリは、この名前空間またはそのメンバーに依存しないように更新する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Net.PeerToPeer.Collaboration?displayProperty=nameWithType></li></ul>|
