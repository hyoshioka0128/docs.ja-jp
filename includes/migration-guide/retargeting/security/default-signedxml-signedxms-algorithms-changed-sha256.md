---
ms.openlocfilehash: e2ae329d027d605e6331afe422e550990fab1042
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614808"
---
### <a name="default-signedxml-and-signedxms-algorithms-changed-to-sha256"></a>既定の SignedXML アルゴリズムと SignedXMS アルゴリズムが SHA256 に変更

#### <a name="details"></a>説明

.NET Framework 4.7 以前では、一部の操作において SignedXML と SignedCMS の初期設定が SHA1 でした。 .NET Framework 4.7.1 より、同じ操作で SHA256 が既定で有効になります。 この変更が必要になったのは、SHA1 は安全であると見なされなくなったためです。

#### <a name="suggestion"></a>提案される解決策

SHA1 (安全でない) または SHA256 を既定で使用するかどうかを制御する新しいコンテキスト スイッチ値が 2 つあります。

- Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms
- Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms。.NET Framework 4.7.1 以降のバージョンを対象とするアプリケーションで SHA256 の使用が望ましくない場合は、アプリ構成ファイルの [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに次の構成スイッチを追加することで既定を SHA1 に戻すことができます。

```xml
<AppContextSwitchOverrides value="Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=true;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=true" />
```

.NET Framework 4.7 以前のバージョンを対象とするアプリケーションの場合、アプリの構成ファイルの [runtime](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションに次の構成スイッチを追加することでこの変更を選択できます。

```xml
<AppContextSwitchOverrides value="Switch.System.Security.Cryptography.Xml.UseInsecureHashAlgorithms=false;Switch.System.Security.Cryptography.Pkcs.UseInsecureHashAlgorithms=false" />
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.7.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Security.Cryptography.Pkcs.CmsSigner?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Xml.SignedXml?displayProperty=nameWithType>
- <xref:System.Security.Cryptography.Xml.Reference?displayProperty=nameWithType>
