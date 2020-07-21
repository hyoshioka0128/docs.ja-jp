---
ms.openlocfilehash: 36a9db601f7637185bf48dfcbe2233b4489fcdcf
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614660"
---
### <a name="aescryptoserviceprovider-decryptor-provides-a-reusable-transform"></a>AesCryptoServiceProvider の復号で変換が再利用可能に

#### <a name="details"></a>説明

.NET Framework 4.6.2 以降を対象とするアプリでは、<xref:System.Security.Cryptography.AesCryptoServiceProvider> の復号で変換を再利用できます。 <xref:System.Security.Cryptography.CryptoAPITransform.TransformFinalBlock(System.Byte[],System.Int32,System.Int32)?displayProperty=fullName> の呼び出しの後、変換は初期化し直され、再利用することができます。 以前のバージョンの .NET Framework を対象とするアプリでは、<xref:System.Security.Cryptography.CryptoAPITransform.TransformFinalBlock(System.Byte[],System.Int32,System.Int32)?displayProperty=fullName> の呼び出しの後に、<xref:System.Security.Cryptography.CryptoAPITransform.TransformBlock(System.Byte[],System.Int32,System.Int32,System.Byte[],System.Int32)?displayProperty=fullName> を呼び出して、復号を再利用しようとすると、<xref:System.Security.Cryptography.CryptographicException> をスローするか、破損しているデータが生成されます。

#### <a name="suggestion"></a>提案される解決策

この動作は想定済みであり、この変更の影響は最小限に抑えられているはずです。この変更の影響は前の動作に依存するアプリケーションは、そのアプリケーションの構成ファイルの `<runtime>` セクションに次の構成設定を追加して、この動作の使用を無効にすることができます。

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=true"/>
</runtime>
```

また、以前のバージョンの .NET Framework を対象とするものの、.NET Framework 4.6.2 以降のバージョンの .NET Framework で実行されているアプリでは、そのアプリケーションの構成ファイルの `<runtime>` セクションに次の構成設定を追加して、この動作を有効にできます。

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.Security.Cryptography.AesCryptoServiceProvider.DontCorrectlyResetDecryptor=false"/>
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.AesCryptoServiceProvider.CreateDecryptor?displayProperty=nameWithType>
