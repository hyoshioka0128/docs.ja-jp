---
ms.openlocfilehash: 5c09bee92f679cd7e7a95cd23d5ce0ca9b57170c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85614744"
---
### <a name="wcf-transport-security-supports-certificates-stored-using-cng"></a>WCF トランスポート セキュリティで CNG を使用して格納される証明書をサポート

#### <a name="details"></a>説明

.NET Framework 4.6.2 を対象とするアプリ以降では、WCF トランスポート セキュリティでは、Windows 暗号化ライブラリ (CNG) を使用して格納される証明書がサポートされます。 このサポートは、指数の長さが 32 ビット以下の公開キーを持つ証明書に限定されます。 アプリケーションが対象 .NET Framework 4.6.2、ときにこの機能は既定でオンです。 .NET Framework の以前のバージョンで X509 を使用しようとすると、証明書を CSG のキー記憶域プロバイダーが例外をスローします。

#### <a name="suggestion"></a>提案される解決策

.NET Framework 4.6.1 以前を対象とするものの、.NET Framework 4.6.2 で実行されているアプリの場合、app.config または web.config ファイルの `<runtime>` セクションに次の行を追加することで、CNG 証明書のサポートを有効にできます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableCngCertificates=false" />
</runtime>
```

次のコードを使用してプログラムで行うこともできます。

```csharp
private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificate";

AppContext.SetSwitch(disableCngCertificates, false);
```

```vb
Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates"
AppContext.SetSwitch(disableCngCertificates, False)
```

この変更のため、CNG 証明書の失敗で、セキュリティで保護された通信を開始する試行に依存する例外処理コードは、実行されなくなることに注意してください。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | マイナー       |
| バージョン | 4.6.2       |
| 種類    | 再ターゲット中 |
