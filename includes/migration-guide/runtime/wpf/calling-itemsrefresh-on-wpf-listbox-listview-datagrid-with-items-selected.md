---
ms.openlocfilehash: 710d1517397f423fa40cc0c4a26c3499aac6179e
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620421"
---
### <a name="calling-itemsrefresh-on-a-wpf-listbox-listview-or-datagrid-with-items-selected-can-cause-duplicate-items-to-appear-in-the-element"></a>項目が選択されている WPF ListBox、ListView、または DataGrid に対して Items.Refresh を呼び出すと、重複した項目が要素に表示されることがある

#### <a name="details"></a>説明

.NET Framework 4.5 では、<xref:System.Windows.Controls.ListBox?displayProperty=fullName> で項目が選択されているときにコードから ListBox.Items.Refresh を呼び出すと、選択された項目がリストに複製されることがあります。 同様の問題が <xref:System.Windows.Controls.ListView?displayProperty=fullName> と <xref:System.Windows.Controls.DataGrid?displayProperty=fullName> で発生します。 これは、.NET Framework 4.6 で修正されます。

#### <a name="suggestion"></a>提案される解決策

この問題は、<xref:System.Windows.Data.CollectionView.Refresh?displayProperty=fullName> が呼び出される前に、プログラムで項目を選択解除して、呼び出しの完了後に再び選択することによって回避できます。 または、この問題は .NET Framework 4.6 で修正されたため、このバージョンの .NET Framework にアップグレードすることによって対処できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Data.CollectionView.Refresh?displayProperty=nameWithType></li></ul>|
