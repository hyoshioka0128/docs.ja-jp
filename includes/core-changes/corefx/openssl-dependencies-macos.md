---
ms.openlocfilehash: a4476fbff572c004632153e5a98812c241efca57
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83721311"
---
### <a name="openssl-versions-on-macos"></a>macOS 上の OpenSSL バージョン

macOS 上の .NET Core 3.0 以降のランタイムでは <xref:System.Security.Cryptography.AesCcm>、<xref:System.Security.Cryptography.AesGcm>、<xref:System.Security.Cryptography.DSAOpenSsl>、<xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl>、<xref:System.Security.Cryptography.ECDsaOpenSsl>、<xref:System.Security.Cryptography.RSAOpenSsl>、<xref:System.Security.Cryptography.SafeEvpPKeyHandle> の各型に対して OpenSSL 1.0.x バージョンよりも OpenSSL 1.1.x バージョンが優先されるようになりました。

.NET Core 2.1 ランタイムでは、OpenSSL 1.1.x バージョンがサポートされるようになりましたが、OpenSSL 1.0.x バージョンが引き続き優先されます。

#### <a name="change-description"></a>変更の説明

以前、.NET Core ランタイムでは、macOS 上の OpenSSL 1.0.x バージョンは OpenSSL とやりとりする型に対して使用されていました。 最新の OpenSSL 1.0.x バージョンである OpenSSL 1.0.2 は現在サポートされていません。 サポートされているバージョンの OpenSSL 上で OpenSSL を使用する型を維持するために、.NET Core 3.0 以降のランタイムでは macOS 上でより新しいバージョンの OpenSSL が使用されるようになりました。

この変更により、macOS 上での .NET Core ランタイムの動作は次のようになります。

- .NET Core 3.0 以降のバージョンのランタイムでは、使用可能な場合は OpenSSL 1.1.x が使用され、使用可能な 1.1.x バージョンがない場合にのみ OpenSSL 1.0.x にフォールバックします。

  カスタムの P/Invoke で OpenSSL 相互運用機能型を使用する呼び出し元については、<xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> の注釈にあるガイダンスに従ってください。 <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion> 値を確認しないと、ご利用のアプリがクラッシュする場合があります。

- .NET Core 2.1 以降のバージョンのランタイムでは、使用可能な場合は OpenSSL 1.0.x が使用され、使用可能な 1.0.x バージョンがない場合にのみ OpenSSL 1.1.x にフォールバックします。

  .NET Core 2.1 には <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> プロパティが存在しないため 2.1 ランタイムでは、以前のバージョンの OpenSSL が優先されます。結果として、実行時に OpenSSL のバージョンを確実に判断することができません。

#### <a name="version-introduced"></a>導入されたバージョン

- .NET Core 2.1.16
- .NET Core 3.0.3
- .NET Core 3.1.2

#### <a name="recommended-action"></a>推奨アクション

- OpenSSL バージョン 1.0.2 が不要になった場合はアンインストールします。

- <xref:System.Security.Cryptography.AesCcm>、<xref:System.Security.Cryptography.AesGcm>、<xref:System.Security.Cryptography.DSAOpenSsl>、<xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl>、<xref:System.Security.Cryptography.ECDsaOpenSsl>、<xref:System.Security.Cryptography.RSAOpenSsl>、または <xref:System.Security.Cryptography.SafeEvpPKeyHandle> の型を使用する場合は、OpenSSL 1.1.x をインストールします。

- カスタムの P/Invoke で OpenSSL 相互運用機能型を使用する場合は、<xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> の注釈にあるガイダンスに従ってください。

#### <a name="category"></a>カテゴリ

Core .NET ライブラリ

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.AesCcm?displayProperty=fullName>
- <xref:System.Security.Cryptography.AesGcm?displayProperty=fullName>
- <xref:System.Security.Cryptography.DSAOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDsaOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.RSAOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.SafeEvpPKeyHandle?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Security.Cryptography.AesCcm``
- `T:System.Security.Cryptography.AesGcm`
- `T:System.Security.Cryptography.DSAOpenSsl`
- `T:System.Security.Cryptography.ECDiffieHellmanOpenSsl`
- `T:System.Security.Cryptography.ECDsaOpenSsl`
- `T:System.Security.Cryptography.RSAOpenSsl`
- `T:System.Security.Cryptography.SafeEvpPKeyHandle`

-->
