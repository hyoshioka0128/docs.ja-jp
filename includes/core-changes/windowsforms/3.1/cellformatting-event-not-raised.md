---
ms.openlocfilehash: 4a34a64eba72ea24c1d830566565ce4fbee8e5b7
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721454"
---
### <a name="cellformatting-event-not-raised-if-tooltip-is-shown"></a>ヒントが表示されていると CellFormatting が発生しない

マウスでポイントしたときと、キーボードで選択したときに、<xref:System.Windows.Forms.DataGridView> にセルのテキストとエラーのヒントが表示されるようになりました。 ヒントが表示されている場合、<xref:System.Windows.Forms.DataGridView.CellFormatting?displayProperty=nameWithType> イベントは発生しません。

#### <a name="change-description"></a>変更の説明

.NET Core 3.1 より前、<xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A> プロパティが `true` に設定されている <xref:System.Windows.Forms.DataGridView> では、セルにマウスでポイントしたときにセルのテキストとエラーのヒントが表示されていました。 セルをキーボード (たとえば、Tab キー、ショートカット キー、矢印ナビゲーションなどを使用して) から選択したときはヒントが表示されませんでした。 ユーザーがセルを編集したときに <xref:System.Windows.Forms.DataGridView> がまだ編集モードだった場合に <xref:System.Windows.Forms.DataGridViewCell.ToolTipText> プロパティが設定されていないセルをポイントすると、セルのテキストをセルに表示する書式設定をするための <xref:System.Windows.Forms.DataGridView.CellFormatting> イベントが発生しました。

.NET Core 3.1 以降では、アクセシビリティの標準を満たすため、<xref:System.Windows.Forms.DataGridView.ShowCellToolTips%2A> プロパティが `true` に設定されている <xref:System.Windows.Forms.DataGridView> には、セルがポイントされたときだけでなく、キーボードを使用して選択されたときにも、セルのテキストとエラーのヒントが表示されます。 この変更の結果、<xref:System.Windows.Forms.DataGridView> が編集モードの間に <xref:System.Windows.Forms.DataGridViewCell.ToolTipText> プロパティが設定されていないセルをポイントしても、<xref:System.Windows.Forms.DataGridView.CellFormatting> イベントは発生*しません*。 イベントが発生しないのは、ポイントされたセルの内容が、セルに表示される代わりにヒントとして表示されるためです。

#### <a name="version-introduced"></a>導入されたバージョン

3.1

#### <a name="recommended-action"></a>推奨アクション

<xref:System.Windows.Forms.DataGridView> が編集モードのときに、<xref:System.Windows.Forms.DataGridView.CellFormatting> イベントに依存するすべてのコードをリファクターします。

#### <a name="category"></a>カテゴリ

Windows フォーム

#### <a name="affected-apis"></a>影響を受ける API

None

<!-- 

#### Affected APIs

Not detectable via API analysis.

-->
