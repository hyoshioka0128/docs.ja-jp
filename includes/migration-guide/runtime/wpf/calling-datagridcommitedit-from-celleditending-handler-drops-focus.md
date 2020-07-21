---
ms.openlocfilehash: c3c3ed44cf53625c246dfe0408bb861750ecf336
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622023"
---
### <a name="calling-datagridcommitedit-from-a-celleditending-handler-drops-focus"></a>CellEditEnding ハンドラーから DataGrid.CommitEdit を呼び出すと、フォーカスが削除される

#### <a name="details"></a>説明

<xref:System.Windows.Controls.DataGrid?displayProperty=fullName> の <xref:System.Windows.Controls.DataGrid.CellEditEnding?displayProperty=fullName> イベント ハンドラーのいずれかから <xref:System.Windows.Controls.DataGrid.CommitEdit> を呼び出すと、<xref:System.Windows.Controls.DataGrid?displayProperty=fullName> からフォーカスが失われます。

#### <a name="suggestion"></a>提案される解決策

このバグは .NET framework 4.5.2 で修正されたため、.NET Framework をアップグレードすることによって回避できます。 または、<xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=fullName> を呼び出した後で <xref:System.Windows.Controls.DataGrid?displayProperty=fullName> を明示的に再選択することによって回避できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.DataGrid.CommitEdit?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.DataGrid.CommitEdit(System.Windows.Controls.DataGridEditingUnit,System.Boolean)?displayProperty=nameWithType></li></ul>|
