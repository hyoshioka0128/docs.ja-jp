---
ms.openlocfilehash: abef47c64a7cfd99c5b50bf2100401a2d5fcc5c3
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614733"
---
### <a name="x509certificateclaimsetfindclaims-considers-all-claimtypes"></a>X509CertificateClaimSet.FindClaims は、すべての claimTypes を考慮します

#### <a name="details"></a>説明

X509 クレーム セットがその SAN フィールド内の複数の DNS エントリを含む証明書から初期化される場合は、.NET Framework 4.6.1 を対象とするアプリで、<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=fullName>メソッドをすべての DNS エントリの claimType 引数と一致を試みます。 .NET Framework の以前のバージョンを対象とするアプリに対して、<xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=fullName>メソッドは claimType 引数と最後の DNS エントリのみを一致させようとしています。

#### <a name="suggestion"></a>提案される解決策

この変更は、.NET Framework 4.6.1 を対象とするアプリケーションのみに影響します。 この変更は、[DisableMultipleDNSEntries](~/docs/framework/migration-guide/mitigation-x509certificateclaimset-findclaims-method.md#mitigation) 互換性スイッチで無効にできます (または、4.6.1 より前を対象としている場合は、有効にできます)。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.IdentityModel.Claims.X509CertificateClaimSet.FindClaims(System.String,System.String)?displayProperty=nameWithType>
