---
ms.openlocfilehash: 13d3799aeede86b01aa81ce1cd69b3c4c22311ca
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620481"
---
### <a name="wpf-textbox-defaults-to-undo-limit-of-100"></a>WPF TextBox は既定で元に戻す上限が 100 に設定される

#### <a name="details"></a>説明

.NET Framework 4.5 では、WPF テキスト ボックスの既定の元に戻す上限は 100 です (.NET Framework 4.0 では無制限でした)。

#### <a name="suggestion"></a>提案される解決策

元に戻す上限が 100 では低すぎる場合、<xref:System.Windows.Controls.Primitives.TextBoxBase.UndoLimit> を使用して上限を明示的に設定できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType></li></ul>|
