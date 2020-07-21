---
ms.openlocfilehash: 958dede03e1c15f69f4ee676f13713ff43c29e96
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2020
ms.locfileid: "72393984"
---
### <a name="logging-debuglogger-class-made-internal"></a>ログ:internal になった DebugLogger クラス

`DebugLogger` のアクセス修飾子は、ASP.NET Core 3.0 より前では `public` でした。 このアクセス修飾子は、ASP.NET Core 3.0 では、`internal` に変わっています。

#### <a name="version-introduced"></a>導入されたバージョン

3.0

#### <a name="reason-for-change"></a>変更理由

次の理由により変更されています。

* `ConsoleLogger` などの、その他のロガーの実装との整合性を確保します。
* API サーフェイスを減らします。

#### <a name="recommended-action"></a>推奨アクション

<xref:Microsoft.Extensions.Logging.DebugLoggerFactoryExtensions.AddDebug%2A> `ILoggingBuilder` 拡張メソッドを使用して、デバッグ ログを有効にします。 サービスを手動で登録する必要がある場合、<xref:Microsoft.Extensions.Logging.Debug.DebugLoggerProvider> もまだ `public` です。

#### <a name="category"></a>カテゴリ

ASP.NET Core

#### <a name="affected-apis"></a>影響を受ける API

<xref:Microsoft.Extensions.Logging.Debug.DebugLogger?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.Extensions.Logging.Debug.DebugLogger`

-->
