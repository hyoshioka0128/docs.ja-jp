---
ms.openlocfilehash: 1be68c2968d0eaa9024007bcf37abf9e44c36f1c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622058"
---
### <a name="scrolling-a-wpf-treeview-or-grouped-listbox-in-a-virtualizingstackpanel-can-cause-a-hang"></a>VirtualizingStackPanel 内の WPF TreeView またはグループ化された ListBox をスクロールすると、ハングすることがある

#### <a name="details"></a>説明

.NET Framework v4.5 では、仮想化されたスタック パネル内の WPF <xref:System.Windows.Controls.TreeView?displayProperty=fullName> をスクロールすると、ビューポートに余白があった場合 (たとえば、<xref:System.Windows.Controls.TreeView?displayProperty=fullName> 内の項目間や、ItemsPresenter 要素上)、ハングすることがあります。 さらに、場合によっては、ビュー内にサイズの異なる項目があると、余白がない場合でも、不安定になることがあります。

#### <a name="suggestion"></a>提案される解決策

このバグは、.NET Framework 4.5.1 にアップグレードすることによって回避できます。 または、含まれているすべての項目が同じサイズである場合は、仮想化されたスタック パネル内のビュー コレクション (<xref:System.Windows.Controls.TreeView?displayProperty=fullName> など) から余白を削除できます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |Major|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.VirtualizingStackPanel.SetIsVirtualizing(System.Windows.DependencyObject,System.Boolean)?displayProperty=nameWithType></li></ul>|
