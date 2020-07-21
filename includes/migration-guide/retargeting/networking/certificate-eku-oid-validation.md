---
ms.openlocfilehash: c996dafcf65b1fd428be908be346de603ead6e0b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85615681"
---
### <a name="certificate-eku-oid-validation"></a>証明書 EKU OID の検証

#### <a name="details"></a>説明

.NET Framework 4.6 以降、<xref:System.Net.Security.SslStream> または <xref:System.Net.ServicePointManager> クラスで EKU (拡張キー使用法) の OID (オブジェクト識別子) が検証されます。 EKU (拡張キー使用法) 拡張は、キーを使用するアプリケーションを示すオブジェクト識別子 (OID) の集まりです。 EKU OID 検証では、リモート証明書に意図している目的にかなった OID が与えられるようにリモート証明書コールバックが使用されます。

#### <a name="suggestion"></a>提案される解決策

この変更が望ましくない場合は、アプリ構成ファイルの [`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) の [\<AppContextSwitchOverrides>](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) に次のスイッチを追加することで、証明書 EKU OID の検証を無効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Net.DontCheckCertificateEKUs=true" />
</runtime>
```

> [!IMPORTANT]
> この設定は下位互換性のためにのみ提供されます。 それ以外の目的での使用はお勧めしません。

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.Security.SslStream?displayProperty=nameWithType>
- <xref:System.Net.ServicePointManager?displayProperty=nameWithType>
- <xref:System.Net.Http.HttpClient?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>
- <xref:System.Net.FtpWebRequest?displayProperty=nameWithType>
