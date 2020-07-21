---
ms.openlocfilehash: 171b7a3a962f8259e64b88f1ae893e649b5f24bb
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621255"
---
### <a name="chained-popups-with-staysopenfalse"></a>StaysOpen=False でポップアップがチェーンされる

#### <a name="details"></a>説明

ポップアップの外側をクリックすると、StaysOpen=False のポップアップが閉じられることが想定されます。 このような 2 つ以上のポップアップがチェーンされている (つまり、1 つに別のものが含まれている) 場合、次のような、多くの問題が発生します。<ul><li>2 つのレベルを開き、P2 の外側と、P1 の内側をクリックします。  何も起こりません。</li><li>2 つのレベルを開き、P1 の外側をクリックします。  両方のポップアップが閉じます。</li><li>2 つのレベルを開いて閉じます。  次に、P2 をもう一度開いてみます。  何も起こりません。</li><li>3 つのレベルを開いてみます。  この操作を行うことはできません  (クリックする場所に応じて、何も起こらないか、最初の 2 つのレベルが閉じます)。このような場合 (および他のバリアント) は、予期したとおり動作します。</li></ul>

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.7.1|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.Primitives.Popup.StaysOpen?displayProperty=nameWithType></li></ul>|
