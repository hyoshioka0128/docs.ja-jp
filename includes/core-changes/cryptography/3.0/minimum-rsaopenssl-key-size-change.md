---
ms.openlocfilehash: 3d94023fc508a56304587121c6cf1444c87b0d52
ms.sourcegitcommit: 0926684d8d34f4c6b5acce58d2193db093cb9cf2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/20/2020
ms.locfileid: "83720915"
---
### <a name="minimum-size-for-rsaopenssl-key-generation-has-increased"></a>RSAOpenSsl キー生成の最小サイズが増加しました

Linux で新しい RSA キーを生成する場合の最小サイズが、384 ビットから 512 ビットに増加しました。

#### <a name="change-description"></a>変更の説明

.NET Core 3.0 以降では、Linux で <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>、<xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A>、および <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A> から RSA インスタンス上の `LegalKeySizes` プロパティによって報告される最小の有効キー サイズが 384 から 512 に増えました。

その結果、.NET Core 2.2 以前のバージョンでは、`RSA.Create(384)` などのメソッドの呼び出しが成功しています。 .NET Core 3.0 以降のバージョンでは、メソッドの呼び出し `RSA.Create(384)` によって、サイズが小さすぎることを示す例外がスローされます。

この変更は、Linux で暗号化操作を実行する OpenSSL によって、バージョン 1.0.2 と 1.1.0 の間で最小値が増加したためです。 .NET Core 3.0 では、OpenSSL 1.0.x よりも 1.1.x が優先され、報告される最小バージョンが引き上げられ、この新しい依存関係のより高い制限が反映されます。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="recommended-action"></a>推奨アクション

影響を受ける API を呼び出す場合は、生成されるキーのサイズがプロバイダーの最小を下回らないようにしてください。

> [!NOTE]
> 384 ビットの RSA は、既に安全ではないと見なされています (512 ビットの RSA も同様)。 [NIST Special Publication 800-57 Part 1 Revision 4](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf) などの最新の推奨設定では、新しく生成されるキーの最小サイズとして 2,048 ビットが提案されています。

#### <a name="category"></a>カテゴリ

暗号

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RSAOpenSsl.%23ctor%2A>
- <xref:System.Security.Cryptography.RSACryptoServiceProvider.%23ctor%2A>

<!--
#### Affected APIs

- `P:System.Security.Cryptography.AsymmetricAlgorithm.LegalKeySizes`
- `Overload:System.Security.Cryptography.RSA.Create`
- `Overload:System.Security.Cryptography.RSAOpenSsl.#ctor`
- `Overload:System.Security.Cryptography.RSACryptoServiceProvider.#ctor`

-->
