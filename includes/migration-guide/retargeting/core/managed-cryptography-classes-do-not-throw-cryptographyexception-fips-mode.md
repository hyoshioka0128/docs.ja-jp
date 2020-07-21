---
ms.openlocfilehash: 0b62eff8d70873293aafa539f40bf032672df57a
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85616269"
---
### <a name="managed-cryptography-classes-do-not-throw-a-cryptographyexception-in-fips-mode"></a>FIPS モードのマネージド暗号クラスで CryptographyException がスローされない

#### <a name="details"></a>説明

.NET Framework 4.7.2 以前のバージョンでは、システムの暗号化ライブラリが FIPS モードで構成されていると、<xref:System.Security.Cryptography.SHA256Managed> などのマネージド暗号化プロバイダー クラスで <xref:System.Security.Cryptography.CryptographicException> がスローされます。 これらの例外がスローされるのは、マネージド バージョンが FIPS (Federal Information Processing Standards) 140-2 の認定を受けていないためであり、また、FIPS ルールに基づく承認の対象と見なされなかった暗号アルゴリズムをブロックするためです。  少数の開発者は開発用コンピューターを FIPS モードで利用するため、これらの例外は運用システムでのみ頻繁にスローされます。 .NET Framework 4.8 以降のバージョンをターゲットとするアプリケーションでは、より新しい緩いポリシーに自動的に切り替えられるため、そのような場合、<xref:System.Security.Cryptography.CryptographicException> が既定でスローされなくなりました。 代わりに、マネージド暗号化クラスでは、暗号化操作がシステムの暗号化ライブラリにリダイレクトされます。 このポリシー変更により、開発者環境と運用環境での混乱を招く可能性のある違いは実質的になくなり、ネイティブ コンポーネントとマネージド コンポーネントは同じ暗号化ポリシーの下で動作するようになります。

#### <a name="suggestion"></a>提案される解決策

この動作が望ましくない場合は、それを選択せずに、以前の動作を復元し、次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 構成設定を、アプリケーション構成ファイルの [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに追加することで、<xref:System.Security.Cryptography.CryptographicException> が FIPS モードでスローされるようにすることができます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.UseLegacyFipsThrow=true" />
</runtime>
```

アプリケーションのターゲットが .NET Framework 4.7.2 以前である場合は、次の [AppContextSwitchOverrides](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 構成設定を、アプリケーション構成ファイルの [\<runtime>](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに追加することで、この変更を選択することもできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Security.Cryptography.UseLegacyFipsThrow=false" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.8         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.AesManaged?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.MD5Cng?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.MD5CryptoServiceProvider?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RC2CryptoServiceProvider?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RijndaelManaged?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.RIPEMD160Managed?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.SHA1Managed?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.SHA256Managed?displayProperty=nameWithType>
