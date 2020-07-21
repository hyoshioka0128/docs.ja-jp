---
ms.openlocfilehash: 23e278d38d6904d8afe927e6b54c388d443e41f5
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616093"
---
### <a name="signedxmlgetpublickey-returns-rsacng-on-net462-or-lightup-without-retargeting-change"></a>変更の対象を変更せず、SignedXml.GetPublicKey が net462 (または Light-Up) で RSACng を返す

#### <a name="details"></a>説明

.NET Framework 4.6.2 より、<xref:System.Security.Cryptography.Xml.SignedXml.GetPublicKey%2A?displayProperty=nameWithType> メソッドによって返されるオブジェクトの具象型が CryptoServiceProvider 実装から Cng 実装に変わりました。これは突然の変更ではなく、 `certificate.PublicKey.Key` の使用から、`certificate.GetAnyPublicKey` に転送する内部 <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey%2A?displayProperty=nameWithType> の使用に実装が変わったためです。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7.1 で実行されるアプリから、アプリの構成ファイルの [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに次の構成スイッチを追加することで、.NET Framework 4.6.1 以前のバージョンで既定で使用されていた CryptoServiceProvider 実装を使用できます。

```xml
<AppContextSwitchOverrides value="Switch.System.Security.Cryptography.Xml.SignedXmlUseLegacyCertificatePrivateKey=true" />
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignatureReturningKey(System.Security.Cryptography.AsymmetricAlgorithm@)?displayProperty=nameWithType>
