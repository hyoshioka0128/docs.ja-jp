---
ms.openlocfilehash: 207dba9327cfd6debd15c5573697f8950b6c2c95
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2020
ms.locfileid: "86218066"
---
### <a name="tls-1x-by-default-passes-the-sch_send_aux_record-flag-to-the-underlying-schannel-api"></a>TLS 1.x は既定で SCH_SEND_AUX_RECORD フラグを基になる SCHANNEL API に渡す

#### <a name="details"></a>説明

TLS 1.x を使用するとき、.NET Framework は基になる Windows SCHANNEL API に依存します。 .NET Framework 4.6 以降、[SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/win32/api/schannel/ns-schannel-schannel_cred) フラグは既定で SCHANNEL に渡されます。 SCHANNEL によって、暗号化するデータが 2 つの別個のレコードに分割されます。1 つ目のレコードはシングル バイトで、2 つ目のレコードは <em>n</em>-1 バイトです。その結果、まれに、データがシングル レコードに置かれていると想定する既存サーバーとクライアントの間の通信が途切れることがあります。

#### <a name="suggestion"></a>提案される解決策

この変更によって既存サーバーとの接続が途切れる場合、[SCH_SEND_AUX_RECORD](https://docs.microsoft.com/windows/win32/api/schannel/ns-schannel-schannel_cred) フラグの送信を無効にし、アプリ構成ファイルの [`<runtime>`](~/docs/framework/configure-apps/file-schema/runtime/runtime-element.md) セクションで次のスイッチを [`<AppContextSwitchOverrides>`](~/docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) 要素に追加することで、データを別個のレコードに分割しない、以前の動作に復元できます。

```xml
<runtime>
  <AppContextSwitchOverrides value="Switch.System.Net.DontEnableSchSendAuxRecord=true" />
</runtime>
```

> [!IMPORTANT]
> この設定は下位互換性のためにのみ提供されます。 それ以外の目的での使用はお勧めしません。

| 名前    | 値       |
|:--------|:------------|
| スコープ   | エッジ        |
| バージョン | 4.6         |
| 種類    | 再ターゲット中 |

#### <a name="affected-apis"></a>影響を受ける API

- <xref:System.Net.Security.SslStream?displayProperty=nameWithType>
- <xref:System.Net.ServicePointManager?displayProperty=nameWithType>
- <xref:System.Net.Http.HttpClient?displayProperty=nameWithType>
- <xref:System.Net.Mail.SmtpClient?displayProperty=nameWithType>
- <xref:System.Net.HttpWebRequest?displayProperty=nameWithType>
- <xref:System.Net.FtpWebRequest?displayProperty=nameWithType>
