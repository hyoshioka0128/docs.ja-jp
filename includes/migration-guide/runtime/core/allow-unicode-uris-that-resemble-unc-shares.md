---
ms.openlocfilehash: 3e8601ba76dfb05e3d70b3af7440bd7e228768d0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621171"
---
### <a name="allow-unicode-in-uris-that-resemble-unc-shares"></a>UNC 共有に似た URI での Unicode の許可

#### <a name="details"></a>説明

<xref:System.Uri?displayProperty=fullName> では、UNC 共有名と Unicode 文字の両方を含むファイル URI の構築時に、URI が無効な内部状態にならなくなります。 以下のすべてに該当する場合にのみ、動作が変わります。<ul><li>URI にスキーム <code>file:</code> があり、4 つ以上のスラッシュが続く。</li><li>ホスト名がアンダースコアまたはその他の予約されていないシンボルで始まる。</li><li>URI に Unicode 文字が含まれている。</li></ul>

#### <a name="suggestion"></a>提案される解決策

Unicode を含む URI を一貫して操作するアプリケーションでこの動作を使用して、UNC 共有への参照を許可しないようにした可能性があります。 これらのアプリケーションでは代わりに <xref:System.Uri.IsUnc> を使用する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Uri?displayProperty=nameWithType></li></ul>|
