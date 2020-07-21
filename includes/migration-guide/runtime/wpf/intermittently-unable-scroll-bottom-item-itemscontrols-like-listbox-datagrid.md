---
ms.openlocfilehash: b92dc8a1c48e83846c3d9a1d86e66629f31b7722
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622022"
---
### <a name="intermittently-unable-to-scroll-to-bottom-item-in-itemscontrols-like-listbox-and-datagrid-when-using-custom-datatemplates"></a>カスタム DataTemplate を使用しているとき、断続的に、ItemsControl (ListBox や DataGrid など) 内の最後の項目までスクロールできない

#### <a name="details"></a>説明

場合によっては、.NET Framework 4.5 のバグにより、カスタム DataTemplate を使用していると、ItemsControl (<xref:System.Windows.Controls.ListBox?displayProperty=fullName>、<xref:System.Windows.Controls.ComboBox?displayProperty=fullName>、<xref:System.Windows.Controls.DataGrid?displayProperty=fullName> など) の最後の項目までスクロールできません。 (上へスクロールした後で) もう一度スクロールを試みると、今度はスクロールできます。

#### <a name="suggestion"></a>提案される解決策

この問題は .NET Framework 4.5.2 で修正されたため、このバージョン (またはそれ以降のバージョン) の .NET Framework にアップグレードすることによって対処できます。 または、ユーザーは、スクロール バーをこれらのコレクションの最後の項目までドラッグできますが、2 回試みなければならないことがあります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |マイナー|
|バージョン|4.5|
|種類|ランタイム|
