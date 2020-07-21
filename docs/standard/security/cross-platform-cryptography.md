---
title: .NET Core と .NET 5 でのクロスプラットフォーム暗号化
description: .NET でサポートされているプラットフォームの暗号化機能について説明します。
ms.date: 06/19/2020
ms.technology: dotnet-standard
helpviewer_keywords:
- cryptography, cross-platform
- encryption, cross-platform
ms.openlocfilehash: 793a9bc55e5bd660374abd2ae81899e63ce3f36a
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85854025"
---
# <a name="cross-platform-cryptography-in-net-core-and-net-5"></a>.NET Core と .NET 5 でのクロスプラットフォーム暗号化

.NET Core と .NET 5 での暗号化操作は、オペレーティングシステム (OS) ライブラリによって行われます。 この依存関係には、次のような利点があります。

* .NET アプリは OS の信頼性を向上します。 暗号化ライブラリを脆弱性から保護することは、OS ベンダーにとって高い優先順位です。 これを行うには、システム管理者が適用する必要がある更新プログラムを提供します。
* OS ライブラリが FIPS 検証されている場合、.NET アプリは FIPS 検証アルゴリズムにアクセスできます。

OS ライブラリに対する依存関係は、OS がサポートする暗号化機能のみを .NET アプリで使用できることも意味します。 すべてのプラットフォームで特定のコア機能がサポートされますが、.NET でサポートされている一部のプラットフォームでは、一部の機能を使用できません。 この記事では、各プラットフォームでサポートされている機能について説明します。

この記事では、.NET での暗号化に関する実用的な知識があることを前提としています。 詳細については、「 [.Net 暗号化モデル](cryptography-model.md)と[.net 暗号化サービス](cryptographic-services.md)」を参照してください。

## <a name="hash-algorithms"></a>ハッシュ アルゴリズム

クラスを含むすべてのハッシュアルゴリズムとハッシュベースメッセージ認証 (HMAC) クラスは、 `*Managed` OS ライブラリに従います。 さまざまな OS ライブラリはパフォーマンスが異なりますが、互換性がある必要があります。

## <a name="symmetric-encryption"></a>対称暗号化

基になる暗号とチェーンはシステムライブラリによって行われ、すべてのプラットフォームでサポートされています。

| 暗号 + モード | Windows | Linux | macOS |
|---------------|---------|-------|-------|
| AES-CBC       | ✔️     | ✔️    | ✔️   |
| AES-ECB       | ✔️     | ✔️    | ✔️   |
| 3DES-CBC      | ✔️     | ✔️    | ✔️   |
| 3DES-ECB      | ✔️     | ✔️    | ✔️   |
| DES-CBC       | ✔️     | ✔️    | ✔️   |
| DES-ECB       | ✔️     | ✔️    | ✔️   |

## <a name="authenticated-encryption"></a>認証された暗号化

認証済み暗号化 (AE) のサポートは、およびクラスを使用して、AES CCM と AES GCM に対して提供され <xref:System.Security.Cryptography.AesCcm?displayProperty=fullName> <xref:System.Security.Cryptography.AesGcm?displayProperty=fullName> ます。

Windows および Linux では、AES-CCM と AES-GCM の実装は OS ライブラリによって提供されます。

### <a name="aes-ccm-and-aes-gcm-on-macos"></a>AES-CCM と AES-macOS での GCM

MacOS では、システムライブラリはサードパーティコード用の AES-CCM または AES GCM をサポートしていないため、 <xref:System.Security.Cryptography.AesCcm> クラスとクラスは、 <xref:System.Security.Cryptography.AesGcm> サポートのために OpenSSL を使用します。 MacOS のユーザーは、これらの型を機能させるために OpenSSL (libcrypto) の適切なコピーを取得する必要があります。また、既定では、システムがライブラリを読み込むパスにする必要があります。 Homebrew などのパッケージマネージャーから OpenSSL をインストールすることをお勧めします。

`libcrypto.0.9.7.dylib` `libcrypto.0.9.8.dylib` MacOS に含まれるおよびライブラリは、以前のバージョンの OpenSSL からのものであり、使用されません。 `libcrypto.35.dylib`、 `libcrypto.41.dylib` 、およびの各 `libcrypto.42.dylib` ライブラリは、libressl からのものであり、使用されません。

### <a name="aes-ccm-keys-nonces-and-tags"></a>AES-CCM キー、nonce、タグ

* キーサイズ

  AES は128、192、および256ビットのキーで動作します。

* Nonce のサイズ

  クラスは、 <xref:System.Security.Cryptography.AesCcm> 56、64、72、80、88、96、および104ビット (7、8、9、10、11、12、13バイト) nonce をサポートしています。

* タグサイズ

  クラスは、 <xref:System.Security.Cryptography.AesCcm> 32、48、64、80、96、112、および128ビット (4、8、10、12、14、16バイト) のタグの作成または処理をサポートしています。

### <a name="aes-gcm-keys-nonces-and-tags"></a>AES-GCM キー、nonce、タグ

* キーサイズ

  AES-GCM は128、192、および256ビットのキーで動作します。

* Nonce のサイズ

  クラスは、 <xref:System.Security.Cryptography.AesGcm> 96 ビット (12 バイト) の nonce のみをサポートしています。

* タグサイズ

  クラスは、 <xref:System.Security.Cryptography.AesGcm> 96、104、112、120、および128ビット (12、13、14、15、16バイト) のタグの作成または処理をサポートしています。

## <a name="asymmetric-cryptography"></a>非対称暗号化

ここでは、次のサブセクションについて説明します。

* [RSA](#rsa)
* [ECDSA](#ecdsa)
* [ECDH](#ecdh)
* [DSA](#dsa)

### <a name="rsa"></a>RSA

RSA (Rivest – Rivest-shamir-adleman – Rivest-shamir-adleman) キーの生成は OS ライブラリによって実行され、サイズの制限とパフォーマンス特性が適用されます。

RSA キー操作は OS ライブラリによって実行され、読み込むことができるキーの種類は OS の要件に従います。

.NET は、"未加工の" (埋め込まれていない) RSA 操作を公開しません。

OS ライブラリは、暗号化と復号化の埋め込みに使用されます。 すべてのプラットフォームで同じパディングオプションがサポートされているわけではありません。

| パディングモード                          | Windows (CNG) | Linux (OpenSSL) | macOS | Windows (CAPI) |
|---------------------------------------|---------------|-----------------|-------|----------------|
| PKCS1 暗号化                      | ✔️           | ✔️              | ✔️   | ✔️             |
| OAEP-1                          | ✔️           | ✔️              | ✔️   | ✔️             |
| OAEP (SHA256、SHA384、SHA512) | ✔️           | ✔️              | ✔️   | ❌             |
| PKCS1 署名 (MD5、SHA-1)          | ✔️           | ✔️              | ✔️   | ✔️             |
| PKCS1 Signature (SHA-1)               | ✔️           | ✔️              | ✔️   | ⚠️\*           |
| PSS                                   | ✔️           | ✔️              | ✔️   | ❌             |

\*Windows CryptoAPI (CAPI) は、SHA-1 アルゴリズムを使用して署名を PKCS1 ことができます。 ただし、個々の RSA オブジェクトは、それをサポートしていない暗号化サービスプロバイダー (CSP) に読み込むことができます。

#### <a name="rsa-on-windows"></a>Windows での RSA

* Windows CryptoAPI (CAPI) は、が使用されるたびに使用され [`new RSACryptoServiceProvider()`](xref:System.Security.Cryptography.RSACryptoServiceProvider) ます。
* Windows Cryptography API Next Generation (CNG) は、が使用されるたびに使用され [`new RSACng()`](xref:System.Security.Cryptography.RSACng) ます。
* によって返されるオブジェクト <xref:System.Security.Cryptography.RSA.Create%2A?displayProperty=nameWithType> は、内部的に WINDOWS CNG を利用しています。 この Windows CNG の使用は実装の詳細であり、変更される可能性があります。
* <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey%2A>の拡張メソッドは、 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> インスタンスを返し <xref:System.Security.Cryptography.RSACng> ます。 このの使用 <xref:System.Security.Cryptography.RSACng> は実装の詳細であり、変更される可能性があります。
* <xref:System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey%2A>現在、の拡張メソッドは <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> インスタンスを推奨して <xref:System.Security.Cryptography.RSACng> いますが、が <xref:System.Security.Cryptography.RSACng> キーを開けない場合は、 <xref:System.Security.Cryptography.RSACryptoServiceProvider> が試行されます。 優先プロバイダーは実装の詳細であり、変更される可能性があります。

#### <a name="rsa-native-interop"></a>RSA ネイティブ相互運用

.NET は、.NET 暗号化コードが使用する OS ライブラリとプログラムが相互運用できるようにする型を公開します。 関連する型はプラットフォーム間で変換されないため、必要な場合にのみ直接使用する必要があります。

| Type                                                         | Windows | Linux         | macOS         |
|--------------------------------------------------------------|---------|---------------|---------------|
| <xref:System.Security.Cryptography.RSACryptoServiceProvider> | ✔️     | ⚠️<sup>1</sup>| ⚠️<sup>1</sup> |
| <xref:System.Security.Cryptography.RSACng>                   | ✔️     | ❌            | ❌            |
| <xref:System.Security.Cryptography.RSAOpenSsl>               | ❌     | ✔️            | ⚠️<sup>3</sup> |

<sup>1</sup> MacOS と Linux では、 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 既存のプログラムとの互換性のために使用できます。 この場合、名前付きキーを開くなど、OS の相互運用を必要とするメソッドは、をスロー <xref:System.PlatformNotSupportedException> します。

<sup>2</sup> macOS では 2 <xref:System.Security.Cryptography.RSAOpenSsl> 。 OpenSSL がインストールされていて、ダイナミックライブラリの読み込みによって適切な libcrypto .dylib が検出された場合に機能します。 適切なライブラリが見つからない場合は、例外がスローされます。

### <a name="ecdsa"></a>ECDSA

ECDSA (楕円曲線デジタル署名アルゴリズム) キーの生成は OS ライブラリによって行われ、サイズの制限とパフォーマンス特性が適用されます。

ECDSA のキー曲線は OS ライブラリによって定義され、制限が適用されます。

| 楕円曲線                     | Windows 10    | Windows 7-8.1 | Linux         | macOS         |
|------------------------------------|---------------|-----------------|---------------|---------------|
| NIST P-256 (secp256r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| NIST P-384 (secp384r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| NIST P-521 (secp521r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| Brainpool 曲線 (名前付き曲線として) | ✔️           | ❌              | ⚠️<sup>1</sup>| ❌           |
| その他の名前付き曲線                 | ⚠️<sup>3</sup>| ❌             | ⚠️<sup>1</sup>| ❌           |
| 明示的な曲線                    | ✔️           | ❌              | ✔️           | ❌            |
| 明示的にエクスポートまたはインポート       | ✔️           | ❌<sup>番</sup>  | ✔️           | ❌<sup>番</sup>|

<sup>1</sup> Linux ディストリビューションでは、同じ名前付き曲線がサポートされていません。

<sup>2</sup>名前付き曲線のサポートは、windows 10 の windows CNG に追加されました。 詳細については、「 [CNG 名前付き楕円曲線](https://msdn.microsoft.com/library/windows/desktop/mt632245(v=vs.85).aspx)」を参照してください。 名前付き曲線は、Windows 7 の3つの曲線を除き、以前のバージョンの Windows では使用できません。

<sup>3</sup>明示的な曲線パラメーターを使用してエクスポートするには、os ライブラリのサポートが必要です。これは、macOS または以前のバージョンの Windows では使用できません。

#### <a name="ecdsa-native-interop"></a>ECDSA ネイティブ相互運用

.NET は、.NET 暗号化コードが使用する OS ライブラリとプログラムが相互運用できるようにする型を公開します。 関連する型はプラットフォーム間で変換されないため、必要な場合にのみ直接使用する必要があります。

| Type                                             | Windows | Linux | macOS |
|--------------------------------------------------|---------|-------|-------|
| <xref:System.Security.Cryptography.ECDsaCng>     | ✔️     | ❌    | ❌    |
| <xref:System.Security.Cryptography.ECDsaOpenSsl> | ❌     | ✔️    | ⚠️\*  |

\*MacOS では、 <xref:System.Security.Cryptography.ECDsaOpenSsl> OpenSSL がシステムにインストールされ、適切な libcrypto .dylib がダイナミックライブラリの読み込みによって検出された場合に機能します。 適切なライブラリが見つからない場合は、例外がスローされます。

### <a name="ecdh"></a>ECDH

ECDH (楕円曲線 Diffie-hellman) キーの生成は OS ライブラリによって行われ、サイズの制限とパフォーマンス特性が適用されます。

クラスは、 <xref:System.Security.Cryptography.ECDiffieHellman> ECDH 計算の "生" の値を返しません。 返されるすべてのデータは、キー派生関数に関して次のようになります。

* ハッシュ (Z)
* HASH (先頭の | |Z | |追記
* HMAC (キー, Z)
* HMAC (キー、先頭に | |Z | |追記
* HMAC (Z, Z)
* HMAC (Z、先頭に | |Z | |追記
* Tls11Prf (ラベル、シード)

ECDH キー曲線は OS ライブラリによって定義され、制限が適用されます。

| 楕円曲線                     | Windows 10    | Windows 7-8.1 | Linux         | macOS         |
|------------------------------------|---------------|-----------------|---------------|---------------|
| NIST P-256 (secp256r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| NIST P-384 (secp384r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| NIST P-521 (secp521r1)             | ✔️           | ✔️              | ✔️           | ✔️            |
| brainpool 曲線 (名前付き曲線として) | ✔️           | ❌              | ⚠️<sup>1</sup>| ❌           |
| その他の名前付き曲線                 | ⚠️<sup>3</sup>| ❌             | ⚠️<sup>1</sup>| ❌           |
| 明示的な曲線                    | ✔️           | ❌              | ✔️           | ❌            |
| 明示的にエクスポートまたはインポート       | ✔️           | ❌<sup>番</sup>  | ✔️           | ❌<sup>番</sup>|

<sup>1</sup> Linux ディストリビューションでは、同じ名前付き曲線がサポートされていません。

<sup>2</sup>名前付き曲線のサポートは、windows 10 の windows CNG に追加されました。 詳細については、「 [CNG 名前付き楕円曲線](https://msdn.microsoft.com/library/windows/desktop/mt632245(v=vs.85).aspx)」を参照してください。 名前付き曲線は、Windows 7 の3つの曲線を除き、以前のバージョンの Windows では使用できません。

<sup>3</sup>明示的な曲線パラメーターを使用してエクスポートするには、os ライブラリのサポートが必要です。これは、macOS または以前のバージョンの Windows では使用できません。

#### <a name="ecdh-native-interop"></a>ECDH ネイティブ相互運用

.NET では、.NET が使用する OS ライブラリとプログラムが相互運用できるように型を公開しています。 関連する型はプラットフォーム間で変換されないため、必要な場合にのみ直接使用する必要があります。

| Type                                                       | Windows | Linux | macOS |
|------------------------------------------------------------|---------|-------|-------|
| <xref:System.Security.Cryptography.ECDiffieHellmanCng>     | ✔️     | ❌    | ❌   |
| <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl> | ❌     | ✔️    | ⚠️\* |

\*MacOS では、 <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl> OpenSSL がインストールされていて、適切な libcrypto .dylib がダイナミックライブラリの読み込みによって検出された場合に機能します。 適切なライブラリが見つからない場合は、例外がスローされます。

### <a name="dsa"></a>DSA

DSA (デジタル署名アルゴリズム) キーの生成はシステムライブラリによって実行されるため、サイズの制限やパフォーマンス特性が適用されます。

| 関数                      | Windows CNG | Linux | macOS         | Windows CAPI |
|-------------------------------|-------------|-------|---------------|--------------|
| キーの作成 (<= 1024 ビット)   | ✔️         | ✔️    | ❌            | ✔️           |
| キーの作成 (> 1024 ビット)    | ✔️         | ✔️    | ❌            | ❌            |
| キーを読み込んでいます (<= 1024 ビット)   | ✔️         | ✔️    | ✔️            | ✔️           |
| キーを読み込んでいます (> 1024 ビット)    | ✔️         | ✔️    | ⚠️\*          | ❌            |
| FIPS 186-2                    | ✔️         | ✔️    | ✔️            | ✔️           |
| FIPS 186-3 (SHA-1 署名) | ✔️         | ✔️    | ❌            | ❌            |

\*macOS は1024ビットを超える DSA キーを読み込みますが、これらのキーの動作は定義されていません。 FIPS 186-3 に従って動作しません。

#### <a name="dsa-on-windows"></a>Windows 上の DSA

* Windows CryptoAPI (CAPI) は、が使用されるたびに使用され [`new DSACryptoServiceProvider()`](xref:System.Security.Cryptography.DSACryptoServiceProvider) ます。
* Windows Cryptography API Next Generation (CNG) は、が使用されるたびに使用され [`new DSACng()`](xref:System.Security.Cryptography.DSACng) ます。
* によって返されるオブジェクト <xref:System.Security.Cryptography.DSA.Create%2A?displayProperty=nameWithType> は、内部的に WINDOWS CNG を利用しています。 この Windows CNG の使用は実装の詳細であり、変更される可能性があります。
* <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A>の拡張メソッドは、 <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> インスタンスを返し <xref:System.Security.Cryptography.DSACng> ます。 このの使用 <xref:System.Security.Cryptography.DSACng> は実装の詳細であり、変更される可能性があります。
* <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A>の拡張メソッドは <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> <xref:System.Security.Cryptography.DSACng> インスタンスを優先しますが、キーを開くことができない場合は <xref:System.Security.Cryptography.DSACng> <xref:System.Security.Cryptography.DSACryptoServiceProvider> 試行されます。  優先プロバイダーは実装の詳細であり、変更される可能性があります。

#### <a name="dsa-native-interop"></a>DSA ネイティブ相互運用

.NET は、.NET 暗号化コードが使用する OS ライブラリとプログラムが相互運用できるようにする型を公開します。 関連する型はプラットフォーム間で変換されないため、必要な場合にのみ直接使用する必要があります。

| Type                                                         | Windows | Linux         | macOS         |
|--------------------------------------------------------------|---------|---------------|---------------|
| <xref:System.Security.Cryptography.DSACryptoServiceProvider> | ✔️     | ⚠️<sup>1</sup> | ⚠️<sup>1</sup> |
| <xref:System.Security.Cryptography.DSACng>                   | ✔️     | ❌             | ❌            |
| <xref:System.Security.Cryptography.DSAOpenSsl>               | ❌      | ✔️            | ⚠️<sup>3</sup> |

<sup>1</sup> MacOS と Linux では、 <xref:System.Security.Cryptography.DSACryptoServiceProvider> 既存のプログラムとの互換性のために使用できます。 この場合、名前付きキーを開くなど、システムの相互運用を必要とするメソッドは、をスロー <xref:System.PlatformNotSupportedException> します。

<sup>2</sup> macOS では 2 <xref:System.Security.Cryptography.DSAOpenSsl> 。 OpenSSL がインストールされていて、ダイナミックライブラリの読み込みによって適切な libcrypto .dylib が検出された場合に機能します。 適切なライブラリが見つからない場合は、例外がスローされます。

## <a name="x509-certificates"></a>X.509 証明書

.NET での x.509 証明書のサポートの大部分は、OS ライブラリから取得されます。 .NET のまたはインスタンスに証明書を読み込むに <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> は、 <xref:System.Security.Cryptography.X509Certificates.X509Certificate> 基になる OS ライブラリから証明書を読み込む必要があります。

### <a name="read-a-pkcs12pfx"></a>PKCS12/PFX の読み取り

| シナリオ                                     | Windows | Linux | macOS |
|----------------------------------------------|---------|-------|-------|
| 空                                        | ✔️     | ✔️    | ✔️   |
| 1つの証明書、秘密キーなし              | ✔️     | ✔️    | ✔️   |
| 1つの証明書 (秘密キーを含む)            | ✔️     | ✔️    | ✔️   |
| 複数の証明書、秘密キーなし       | ✔️     | ✔️    | ✔️   |
| 複数の証明書、1つの秘密キー       | ✔️     | ✔️    | ✔️   |
| 複数の証明書、複数の秘密キー | ✔️     | ⚠️\*  | ✔️   |

\*.NET 5 preview リリースで使用できます。

### <a name="write-a-pkcs12pfx"></a>PKCS12/PFX の作成

| シナリオ                                     | Windows | Linux | macOS |
|----------------------------------------------|---------|-------|-------|
| 空                                        | ✔️     | ✔️    | ⚠️\* |
| 1つの証明書、秘密キーなし              | ✔️     | ✔️    | ⚠️\* |
| 1つの証明書 (秘密キーを含む)            | ✔️     | ✔️    | ✔️   |
| 複数の証明書、秘密キーなし       | ✔️     | ✔️    | ⚠️\* |
| 複数の証明書、1つの秘密キー       | ✔️     | ✔️    | ✔️   |
| 複数の証明書、複数の秘密キー | ✔️     | ⚠️\*  | ✔️   |
| 短期読み込み                            | ✔️     | ✔️    | ⚠️\* |

\*.NET 5 preview リリースで使用できます。

macOS は、キーチェーンオブジェクトを使用せずに証明書の秘密キーを読み込むことができません。この場合、ディスクへの書き込みが必要です。 キーチェーンは PFX 読み込み用に自動的に作成され、使用されなくなったときに削除されます。 この <xref:System.Security.Cryptography.X509Certificates.X509KeyStorageFlags.EphemeralKeySet?displayProperty=nameWithType> オプションは秘密キーがディスクに書き込まれないことを意味するため、macOS でそのフラグをアサートすると、が発生 <xref:System.PlatformNotSupportedException> します。

### <a name="write-a-pkcs7-certificate-collection"></a>PKCS7 証明書コレクションを作成する

Windows と Linux は両方とも DER エンコードされた PKCS7 blob を生成します。 macOS は、長さが CER でエンコードされた PKCS7 blob を出力します。

### <a name="x509store"></a>X509Store

Windows では、 <xref:System.Security.Cryptography.X509Certificates.X509Store> クラスは Windows 証明書ストア api を表現したものです。 これらの Api は、.NET Framework の場合と同様に、.NET Core および .NET 5 でも動作します。

Linux では、 <xref:System.Security.Cryptography.X509Certificates.X509Store> クラスは、システムの信頼の決定 (読み取り専用)、ユーザー信頼の決定 (読み取り/書き込み)、およびユーザーキーストレージ (読み取り/書き込み) の射影です。

MacOS では、 <xref:System.Security.Cryptography.X509Certificates.X509Store> クラスは、システムの信頼の決定 (読み取り専用)、ユーザー信頼の決定 (読み取り専用)、およびユーザーキーの格納 (読み取り/書き込み) の射影です。

次の表は、各プラットフォームでサポートされているシナリオを示しています。 サポートされていないシナリオ ( ❌ テーブル内) の場合は、 <xref:System.Security.Cryptography.CryptographicException> がスローされます。

#### <a name="the-my-store"></a>マイストア

| シナリオ                                         | Windows | Linux | macOS |
|--------------------------------------------------|---------|-------|-------|
| Open CurrentUser\My (ReadOnly)                   | ✔️     | ✔️    | ✔️   |
| Open CurrentUser\My (ReadWrite)                  | ✔️     | ✔️    | ✔️   |
| CurrentUser\My を開く (ExistingOnly)               | ✔️     | ⚠️    | ✔️   |
| LocalMachine\My を開く                             | ✔️     | ❌    | ✔️   |

Linux では、最初の書き込み時にストアが作成され、既定ではユーザーストアは存在しないため、 `CurrentUser\My` を使用して開くことはできません `ExistingOnly` 。

MacOS では、 `CurrentUser\My` ストアはユーザーの既定のキーチェーン (既定では) です `login.keychain` 。 `LocalMachine\My`ストアが `System.keychain` です。

#### <a name="the-root-store"></a>ルートストア

| シナリオ                              | Windows | Linux | macOS           |
|---------------------------------------|---------|-------|-----------------|
| Open CurrentUser\Root (ReadOnly)      | ✔️     | ✔️    | ✔️             |
| Open CurrentUser\Root (ReadWrite)     | ✔️     | ✔️    | ❌              |
| CurrentUser\Root を開く (ExistingOnly)  | ✔️     | ⚠️    | ✔️ (読み取り専用の場合) |
| Open LocalMachine\Root (ReadOnly)     | ✔️     | ✔️    | ✔️             |
| Open LocalMachine\Root (ReadWrite)    | ✔️     | ❌    | ❌              |
| LocalMachine\Root を開く (ExistingOnly) | ✔️     | ⚠️    | ✔️ (読み取り専用の場合) |

Linux では、 `LocalMachine\Root` ストアは、OpenSSL の既定のパスにおける CA バンドルの解釈です。

MacOS では、 `CurrentUser\Root` ストアは `SecTrustSettings` ユーザー信頼ドメインの結果を解釈します。 `LocalMachine\Root`ストアは、 `SecTrustSettings` 管理者ドメインとシステム信頼ドメインの結果を解釈します。

#### <a name="the-intermediate-store"></a>中間ストア

| シナリオ                                      | Windows | Linux | macOS           |
|-----------------------------------------------|---------|-------|-----------------|
| Open CurrentUser\Intermediate (ReadOnly)      | ✔️     | ✔️    | ✔️             |
| Open CurrentUser\Intermediate (ReadWrite)     | ✔️     | ✔️    | ❌              |
| CurrentUser\Intermediate を開く (ExistingOnly)  | ✔️     | ⚠️    | ✔️ (読み取り専用の場合) |
| Open LocalMachine\Intermediate (ReadOnly)     | ✔️     | ✔️    | ✔️             |
| Open LocalMachine\Intermediate (ReadWrite)    | ✔️     | ❌    | ❌              |
| LocalMachine\Intermediate を開く (ExistingOnly) | ✔️     | ⚠️    | ✔️ (読み取り専用の場合) |

Linux では、 `CurrentUser\Intermediate` X509Chain ビルドが成功したときに、機関情報アクセスレコードによって中間 ca をダウンロードするときに、ストアがキャッシュとして使用されます。 `LocalMachine\Intermediate`ストアは、OpenSSL の既定のパスにおける CA バンドルの解釈です。

#### <a name="the-disallowed-store"></a>禁止されているストア

| シナリオ                                    | Windows | Linux | macOS           |
|---------------------------------------------|---------|-------|-----------------|
| Open CurrentUser\Disallowed (ReadOnly)      | ✔️     | ⚠️    | ✔️             |
| Open CurrentUser\Disallowed (ReadWrite)     | ✔️     | ⚠️    | ❌              |
| CurrentUser\Disallowed を開く (ExistingOnly)  | ✔️     | ⚠️    | ✔️ (読み取り専用の場合) |
| Open LocalMachine\Disallowed (ReadOnly)     | ✔️     | ❌    | ✔️             |
| Open LocalMachine\Disallowed (ReadWrite)    | ✔️     | ❌    | ❌              |
| LocalMachine\Disallowed を開く (ExistingOnly) | ✔️     | ❌    | ✔️ (読み取り専用の場合) |

Linux では、 `Disallowed` ストアはチェーン構築では使用されず、そのストアにコンテンツを追加しようとすると、が発生し <xref:System.Security.Cryptography.CryptographicException> ます。 <xref:System.Security.Cryptography.CryptographicException> `Disallowed` コンテンツが既に取得されている場合、ストアを開くと、がスローされます。

MacOS では、CurrentUser\Disallowed ストアと LocalMachine\Disallowed ストアは、信頼がに設定されている証明書の適切な SecTrustSettings 結果を解釈し `Always Deny` ます。

#### <a name="nonexistent-store"></a>存在しないストア

| シナリオ                                         | Windows | Linux | macOS |
|--------------------------------------------------|---------|-------|-------|
| 存在しないストアを開く (ExistingOnly)           | ❌     | ❌     | ❌    |
| CurrentUser が存在しないストア (ReadWrite) を開く  | ✔️     | ✔️     | ⚠️   |
| LocalMachine の存在しないストア (ReadWrite) を開く | ✔️     | ❌     | ❌    |

MacOS では、X509Store API を使用したカスタムストアの作成は、場所でのみサポートされてい `CurrentUser` ます。 これにより、ユーザーのキーチェーンディレクトリにパスワードなしの新しいキーチェーンが作成されます (*~//キーチェーン*)。 パスワードを使用してキーチェーンを作成するには、P/Invoke to を `SecKeychainCreate` 使用できます。 同様に、を使用して、 `SecKeychainOpen` 異なる場所で keychains] を開くこともできます。 結果として得られるを `IntPtr` に渡して、 [`new X509Store(IntPtr)`](xref:System.Security.Cryptography.X509Certificates.X509Store.%23ctor(System.IntPtr)) 現在のユーザーのアクセス許可に従って、読み取り/書き込み可能なストアを取得できます。

### <a name="x509chain"></a>X509Chain

macOS はオフライン CRL の使用をサポートしていないため、 `X509RevocationMode.Offline` はとして扱われ `X509RevocationMode.Online` ます。

macOS では、CRL (証明書失効リスト)/OCSP (オンライン証明書の状態プロトコル)/AIA (機関情報アクセス) のダウンロードでユーザーが開始したタイムアウトをサポートしていないため、 `X509ChainPolicy.UrlRetrievalTimeout` は無視されます。

## <a name="additional-resources"></a>その他の技術情報

* [.NET 暗号化モデル](cryptography-model.md)
* [.NET 暗号化サービス](cryptographic-services.md)
