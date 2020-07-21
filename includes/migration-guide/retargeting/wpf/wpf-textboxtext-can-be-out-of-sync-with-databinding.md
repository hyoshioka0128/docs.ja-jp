---
ms.openlocfilehash: d0de1a262d57c67dd4dfb258d5ac013af5d8783d
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617232"
---
### <a name="wpf-textboxtext-can-be-out-of-sync-with-databinding"></a>WPF TextBox.Text とデータ バインドを非同期にできる

#### <a name="details"></a>説明

場合によっては、データ バインディングの書き込み操作中にプロパティが変更された場合、<xref:System.Windows.Controls.TextBox.Text> プロパティにデータ バインディング プロパティ値の以前の値が反映されることがあります。

#### <a name="suggestion"></a>提案される解決策

これによって生じる悪影響はないはずです。 ただし、<xref:System.Windows.FrameworkCompatibilityPreferences.KeepTextBoxDisplaySynchronizedWithTextProperty> プロパティを `false` に設定して、以前の動作を復元することは可能です。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.5         |
|種類|再ターゲット中

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Windows.Controls.TextBox.Text?displayProperty=nameWithType>
