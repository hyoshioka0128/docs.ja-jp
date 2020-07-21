---
ms.openlocfilehash: 51208762cea2a5688c5d43e5d444d4e014e5f0b4
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621320"
---
### <a name="x509certificate2tostringboolean-does-not-throw-now-when-net-cannot-handle-the-certificate"></a>.NET で証明書を処理できないときに、X509Certificate2.ToString(Boolean) がスローしなくなった

#### <a name="details"></a>説明

.NET Framework 4.5.2 およびそれより前のバージョンでは、このメソッドは、verbose パラメーターとして <code>true</code> が渡され、.NET Framework ではサポートされない証明書がインストールされていた場合、スローしました。 現在は、メソッドは成功し、証明書のアクセス不能部分を省いた有効な文字列を返します。

#### <a name="suggestion"></a>提案される解決策

<xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString(System.Boolean)?displayProperty=nameWithType> に依存しているコードは、以前は API がスローしていたような場合には、返される文字列から一部の証明書データ (公開鍵、秘密鍵、拡張子など) が除外されることを予期するように更新する必要があります。

| 名前    | 値       |
|:--------|:------------|
| スコープ   |エッジ|
|バージョン|4.6|
|種類|ランタイム

#### <a name="affected-apis"></a>影響を受ける API

-<xref:System.Security.Cryptography.X509Certificates.X509Certificate2.ToString(System.Boolean)?displayProperty=nameWithType></li></ul>|
