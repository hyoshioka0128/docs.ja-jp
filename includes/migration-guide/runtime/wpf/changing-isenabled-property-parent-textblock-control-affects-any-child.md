---
ms.openlocfilehash: 395463225e3c1f1d168dd019ea75966ad54e5a8a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621260"
---
### <a name="changing-the-isenabled-property-of-the-parent-of-a-textblock-control-affects-any-child-controls"></a>TextBlock コントロールの親の IsEnabled プロパティの変更がすべての子コントロールに影響する

#### <a name="details"></a>説明

.NET Framework 4.6.2、変更以降の<xref:System.Windows.UIElement.IsEnabled?displayProperty=fullName>の親のプロパティ、<xref:System.Windows.Controls.TextBlock?displayProperty=fullName>コントロール (ハイパーリンクやボタンなど) などの子コントロールに影響を与える、<xref:System.Windows.Controls.TextBlock?displayProperty=fullName>コントロール。 .NET Framework 4.6.1 以前のバージョンで、内部コントロール、<xref:System.Windows.Controls.TextBlock?displayProperty=fullName>の状態を常に反映されませんでした、<xref:System.Windows.UIElement.IsEnabled?displayProperty=fullName>のプロパティ、<xref:System.Windows.Controls.TextBlock?displayProperty=fullName>親。

#### <a name="suggestion"></a>提案される解決策

[なし] : この変更は、<xref:System.Windows.Controls.TextBlock?displayProperty=fullName> コントロール内部のコントロールに期待される動作に準拠しています。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.UIElement.IsEnabled?displayProperty=nameWithType></li></ul>|
