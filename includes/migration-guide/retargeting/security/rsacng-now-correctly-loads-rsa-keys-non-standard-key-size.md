---
ms.openlocfilehash: c1e85941c8c6c31c7d937d0671ad955fa6490783
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614649"
---
### <a name="rsacng-now-correctly-loads-rsa-keys-of-non-standard-key-size"></a>RSACng でキー サイズが非標準の RSA キーが正しく読み込まれるようになりました

#### <a name="details"></a>説明

4\.6.2 より前の .NET Framework バージョンでは、RSA 証明書のキー サイズが標準ではない顧客は、拡張メソッドの <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=fullName> や <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=fullName> でそのキーにアクセスできません。  &quot;The requested key size is not supported (要求されたサイズのキーには対応していません)&quot; というメッセージと共に <xref:System.Security.Cryptography.CryptographicException?displayProperty=fullName> がスローされます。 .NET Framework 4.6.2 では、この問題が修正されました。 同様に、<xref:System.Security.Cryptography.RSA.ImportParameters(System.Security.Cryptography.RSAParameters)> と <xref:System.Security.Cryptography.RSACng.ImportParameters(System.Security.Cryptography.RSAParameters)> で <xref:System.Security.Cryptography.CryptographicException?displayProperty=fullName> をスローすることなく非標準サイズのキーが処理されるようになりました。

#### <a name="suggestion"></a>提案される解決策

非標準サイズのキーが使用されるときに <xref:System.Security.Cryptography.CryptographicException?displayProperty=fullName> がスローされるという以前の動作に依存する例外処理ロジックがある場合、そのロジックを除くことを検討してください。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.RSA.ImportParameters(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSACng.ImportParameters(System.Security.Cryptography.RSAParameters)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?displayProperty=nameWithType>
