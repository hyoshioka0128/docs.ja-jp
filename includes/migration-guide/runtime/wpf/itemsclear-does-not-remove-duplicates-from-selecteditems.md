---
ms.openlocfilehash: 75f176133697056bab9349ba1d18d7a0e1aa7da2
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620127"
---
### <a name="itemsclear-does-not-remove-duplicates-from-selecteditems"></a>Items.Clear で SelectedItems から重複部分が削除されない

#### <a name="details"></a>説明

セレクター (複数選択が有効になっている) の <xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> コレクションに重複部分があるとします。その場合、同じ項目が複数回表示されます。  データ ソースからこれらの項目を削除すると (たとえば、Items.Clear を呼び出すことにより)、<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> からそれらの項目を削除できなくなります。最初のインスタンスのみが削除されます。 さらに、<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> (SelectedItems.Clear() など) を引き続き使用すると、<xref:System.ArgumentException?displayProperty=fullName> などの問題が発生する可能性があります。これは、<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=fullName> に、データ ソース内にはもう存在しない項目が含まれているためです。

#### <a name="suggestion"></a>提案される解決策

可能であれば、.NET Framework 4.6.2 にアップグレードします。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.Primitives.MultiSelector.SelectedItems?displayProperty=nameWithType></li></ul>|
