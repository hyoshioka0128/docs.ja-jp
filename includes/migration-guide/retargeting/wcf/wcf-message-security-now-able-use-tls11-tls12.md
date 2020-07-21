---
ms.openlocfilehash: c646372104457e8bc5d418744847f3ee771c8d8b
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614807"
---
### <a name="wcf-message-security-now-is-able-to-use-tls11-and-tls12"></a>WCF メッセージ セキュリティで TLS1.1 と TLS1.2 が使用可能に

#### <a name="details"></a>説明

.NET Framework 4.7 以降、顧客はアプリケーション構成設定を介し、SSL3.0 と TLS1.0 に加え、WCF メッセージ セキュリティで TLS1.1 または TLS1.2 を構成できます。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.7 では、WCF メッセージ セキュリティの TLS1.1 と TLS1.2 のサポートは既定で無効になっています。 app.config または web.config ファイルの `<runtime>` セクションに次の行を追加することで有効にできます。

```xml
<runtime>
<AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" />
</runtime>
```

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.7         |
| 種類    | 再ターゲット中 |
