---
ms.openlocfilehash: f955e270f709ddf6eea2e44bbcf386e372b9f6e3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621315"
---
### <a name="targetframeworkname-for-default-app-domain-no-longer-defaults-to-null-if-not-set"></a>既定のアプリケーション ドメインの TargetFrameworkName は、設定されなかった場合、既定で null に設定されなくなった

#### <a name="details"></a>説明

<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> は、以前は、明示的に設定されない限り、既定のアプリケーション ドメインでは null でした。 4\.6 以降では、既定のアプリケーション ドメインの <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> プロパティは、TargetFrameworkAttribute (ある場合) から派生された既定値を持ちます。 既定以外のアプリケーション ドメインは、明示的にオーバーライドされない限り、既定のアプリケーション ドメイン (4.6 では既定で null に設定されない) から <xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=fullName> を継承し続けます。

#### <a name="suggestion"></a>提案される解決策

<xref:System.AppDomainSetup.TargetFrameworkName> が既定で null に設定されることに依然しないように、コードを更新する必要があります。 このプロパティが引き続き null として評価される必要がある場合、明示的にその値に設定できます。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.AppDomainSetup.TargetFrameworkName?displayProperty=nameWithType></li></ul>|
