---
ms.openlocfilehash: a3ba42868577ac20ea2e082f90fc4973a1bfe108
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85622368"
---
### <a name="ribbongroup-background-is-set-to-transparent-in-localized-builds"></a>ローカライズされたビルドで RibbonGroup の背景が透明に設定される

#### <a name="details"></a>説明

ローカライズされたビルドの <xref:System.Windows.Controls.Ribbon.RibbonGroup?displayProperty=fullName> の背景が常に透明のブラシで塗りつぶされており、UI の操作性が低下していました。 これは、.NET Framework 4.7 WPF 修正プログラムで修正されます。<xref:System.Windows.Controls.Ribbon.RibbonGroup?displayProperty=fullName> のローカライズされたリソースが更新され、正しいブラシが確実に選択されるようになります。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 にアップグレードします

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6.2|
|種類|ランタイム|
