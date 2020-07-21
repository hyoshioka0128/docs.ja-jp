---
ms.openlocfilehash: d78d083b16ac034c6c393dbc0f6094ee4c6c63c0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622370"
---
### <a name="datagridcellspanelbringindexintoview-throws-argumentoutofrangeexception"></a>DataGridCellsPanel.BringIndexIntoView で ArgumentOutOfRangeException がスローされる

#### <a name="details"></a>説明

列の仮想化は有効になっているが、列の幅がまだ決定されていない場合、<xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)> は非同期で動作します。  非同期動作が発生する前に列が削除されると、<xref:System.ArgumentOutOfRangeException?displayProperty=fullName> が発生する場合があります。

#### <a name="suggestion"></a>提案される解決策

以下のいずれかを実行してください。<ol><li>.NET Framework 4.7 にアップグレードします。</li><li>.NET Framework 4.6.2 の最新のサービス パッチをインストールします。</li><li><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)> に対する非同期応答が完了するまでは列を削除しないようにする。</li></ol>

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6.2|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object)?displayProperty=nameWithType></li><li><xref:System.Windows.Controls.DataGrid.ScrollIntoView(System.Object,System.Windows.Controls.DataGridColumn)?displayProperty=nameWithType></li></ul>|
