---
ms.openlocfilehash: cd59818fe674e10a206725bea8a74c4aceed99b1
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620469"
---
### <a name="wpf-textbox-selected-text-appears-a-different-color-when-the-text-box-is-inactive"></a>WPF TextBox で選択されているテキストが、テキスト ボックスがアクティブでないときに異なる色で表示される

#### <a name="details"></a>説明

.NET Framework 4.5 では、WPF テキスト ボックス コントロールがアクティブでないとき (フォーカスがないとき)、ボックス内で選択されているテキストは、コントロールがアクティブなときとは別の色で表示されます。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Windows.FrameworkCompatibilityPreferences.AreInactiveSelectionHighlightBrushKeysSupported> プロパティを <code>false</code> に設定することで、以前 (.NET Framework 4.0) の動作が復元される可能性があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.TextBox?displayProperty=nameWithType></li></ul>|
