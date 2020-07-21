---
ms.openlocfilehash: 0e25d5d9b545e5cb400cbf701fb13da572fadf10
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614673"
---
### <a name="etw-event-names-cannot-differ-only-by-a-start-or-stop-suffix"></a>サフィックスの "Start" または "Stop" のみで ETW イベント名を使い分けることができない

#### <a name="details"></a>説明

.NET Framework 4.6 と4.6.1 では、2 つの Windows イベント トレーシング (ETW) のイベント名の違いが、"Start" または "Stop" のサフィックスのみである場合 (あるイベントの名前が `LogUser` で、別のイベントの名前が `LogUserStart` の場合など)、ランタイムにより <xref:System.ArgumentException> がスローされます。 この場合、ランタイムはイベント ソースを作成できないため、ログ記録は生成できません。

#### <a name="suggestion"></a>提案される解決策

この例外を回避するには、"Start" または "Stop" のサフィックスだけが異なる 2 つのイベント名が存在しないようにします。この要件は、.NET Framework 4.6.2 以降では削除されています。ランタイムは、"Start" と "Stop" のサフィックスだけが異なるイベント名を明確に区別できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |
