---
ms.openlocfilehash: 06c699281c8890ac65be1d282b72b54774acc280
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620474"
---
### <a name="wpf-datatemplate-elements-are-now-visible-to-uia"></a>WPF DataTemplate 要素が UIA に表示されるようになった

#### <a name="details"></a>説明

以前は、<xref:System.Windows.DataTemplate?displayProperty=fullName> 要素は UI オートメーションには表示されませんでした。 4\.5 から、UI オートメーションは、これらの要素を検出します。 これは、多くの場合に便利ですが、<xref:System.Windows.DataTemplate?displayProperty=fullName> 要素を含まない UIA ツリーに依存するテストは中断することがあります。

#### <a name="suggestion"></a>提案される解決策

このアプリの UI オートメーション テストを更新して、以前は非表示の <xref:System.Windows.DataTemplate?displayProperty=fullName> 要素を含んでいる UIA ツリーに対応できるようにしなければならないことがあります。 たとえば、いくつかの要素が互いに隣り合っていることを予期しているテストでは、以前は非表示であった UIA 要素が間にあることを予期する必要があります。 または、UIA 要素の特定のカウントまたはインデックスに依存するテストは、新しい値で更新しなければならないことがあります。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Windows.DataTemplate.%23ctor></li><li><xref:System.Windows.DataTemplate.%23ctor(System.Object)></li></ul>|
