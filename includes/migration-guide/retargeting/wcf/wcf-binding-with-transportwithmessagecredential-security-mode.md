---
ms.openlocfilehash: 0e949cbdeda99dd7b94e919b903a21171a57f527
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614732"
---
### <a name="wcf-binding-with-the-transportwithmessagecredential-security-mode"></a>TransportWithMessageCredential セキュリティ モードを使用する WCF バインド

#### <a name="details"></a>説明

.NET Framework 4.6.1 より、TransportWithMessageCredential セキュリティ モードを使用する WCF バインドで署名のない非対称セキュリティ キーの &quot;to&quot; ヘッダーを含むメッセージを取得するように設定できるようになりました。既定では、署名のない &quot;to&quot; ヘッダーは .NET Framework 4.6.1 でも引き続き拒否されます。 これは、アプリケーションが Switch.System.ServiceModel.AllowUnsignedToHeader 構成スイッチを使用するこの新しい動作モードをオプトインした場合にのみ許可されます。

#### <a name="suggestion"></a>提案される解決策

これはオプトイン機能であるため、既存のアプリの動作に影響はないはずです。<br/>新しい動作を使用するかどうかを制御するには、次の構成設定を使用します。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.ServiceModel.AllowUnsignedToHeader=true" />
</runtime>
```

| 名前    | [値]       |
|:--------|:------------|
| スコープ   | 透明 |
| バージョン | 4.6.1       |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.ServiceModel.BasicHttpSecurityMode.TransportWithMessageCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.BasicHttpsSecurityMode.TransportWithMessageCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.SecurityMode.TransportWithMessageCredential?displayProperty=nameWithType>
- <xref:System.ServiceModel.WSFederationHttpSecurityMode.TransportWithMessageCredential?displayProperty=nameWithType>
