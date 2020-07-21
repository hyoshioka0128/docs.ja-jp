---
ms.openlocfilehash: 4cd06fd02fadbaa9f74e40f850e688ee883454ed
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620445"
---
### <a name="winforms-checkforoverflowunderflow-property-is-now-true-for-systemdrawing"></a>WinForm の CheckForOverflowUnderflow プロパティが System.Drawing に対して true に設定されるようになった

#### <a name="details"></a>説明

System.Drawing.dll アセンブリの CheckForOverflowUnderflow プロパティが true に設定されます。

#### <a name="suggestion"></a>提案される解決策

これまではオーバーフローが発生すると、その結果は自動的に切り捨てられました。 現在では、<xref:System.OverflowException?displayProperty=fullName> 例外がスローされます。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
