---
ms.openlocfilehash: beaac7b14535335a665add4fa056a60793879753
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85620405"
---
### <a name="systemactivities-is-now-aptca"></a>System.Activities が APTCA に

#### <a name="details"></a>説明

アセンブリは <xref:System.Security.AllowPartiallyTrustedCallersAttribute?displayProperty=fullName> 属性でマークされています。

#### <a name="suggestion"></a>提案される解決策

派生クラスに <xref:System.Security.SecurityCriticalAttribute?displayProperty=fullName>のマークを付けることはできません。 以前は、派生型に <xref:System.Security.SecurityCriticalAttribute?displayProperty=fullName>マークを付ける必要がありました。 ただし、この変更によって生じる実質的な影響はないはずです。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.5|
|種類|ランタイム|
