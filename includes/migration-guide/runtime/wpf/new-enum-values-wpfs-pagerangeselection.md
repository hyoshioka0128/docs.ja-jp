---
ms.openlocfilehash: bae6d7c0f8843211c721c68ce6f16000b35b4401
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620457"
---
### <a name="new-enum-values-in-wpfs-pagerangeselection"></a>WPF の PageRangeSelection の新しい列挙値

#### <a name="details"></a>説明

新しい 2 つのメンバー (<xref:System.Windows.Controls.PageRangeSelection.CurrentPage?displayProperty=fullName> および <xref:System.Windows.Controls.PageRangeSelection.SelectedPages?displayProperty=fullName>) が <xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName> 列挙型に追加されました。

#### <a name="suggestion"></a>提案される解決策

ほとんどの場合、これらの変更はユーザー コードに影響しません。 ただし、<xref:System.Windows.Controls.PageRangeSelection?displayProperty=fullName> 型に対する <xref:System.Enum.GetNames(System.Type)> または <xref:System.Enum.GetValues(System.Type)> 呼び出しに特定の数の要素が存在することに依存するコードは、修正する必要があります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.Controls.PageRangeSelection?displayProperty=nameWithType></li></ul>|
