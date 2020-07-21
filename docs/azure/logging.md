---
title: Azure SDK for .NET を使用したログ記録
description: Azure SDK for .NET クライアント ライブラリを使用してログ記録を有効にする方法について説明します。
ms.date: 03/20/2020
ms.custom: azure-sdk-dotnet
ms.author: casoper
author: camsoper
ms.openlocfilehash: 0b255713bc9c13e0cbdaeb25a3d0fe46e91e815d
ms.sourcegitcommit: 3492dafceb5d4183b6b0d2f3bdf4a1abc4d5ed8c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2020
ms.locfileid: "86416028"
---
# <a name="logging-with-the-azure-sdk-for-net"></a>Azure SDK for .NET を使用したログ記録

[Azure SDK](https://azure.microsoft.com/downloads/) for .NET クライアント ライブラリには、クライアント ライブラリの操作をログに記録する機能が含まれています。 これにより、クライアント ライブラリが Azure サービスに対して行う I/O 要求と応答を監視できます。 通常、このログは、通信の問題をデバッグまたは診断するために使用されます。 この記事では、Azure SDK for .NET を使用してログ記録を有効にする 3 つの方法について説明します。

- コンソール ウィンドウにログを記録する
- .NET 診断トレースにログを記録する
- カスタム ログ記録を構成する

> [!IMPORTANT]
> この記事は、最新バージョンの Azure SDK for .NET を使用するクライアント ライブラリに適用されます。 ライブラリがサポートされているかどうかを確認するには、「[Azure SDK の最新リリース](https://azure.github.io/azure-sdk/releases/latest/index.html)」の一覧を参照してください。 Azure SDK クライアント ライブラリの古いバージョンをアプリケーションで使用している場合は、該当するサービスのドキュメントで具体的な手順を参照してください。

## <a name="log-information"></a>ログ情報

SDK では、次の情報がログに記録されます。パラメーター クエリとヘッダー値はサニタイズされ、個人データが削除されます。

HTTP 要求ログ エントリ:

- 一意の ID
- HTTP メソッド
- URI
- 送信要求ヘッダー

HTTP 応答ログ エントリ:

- I/O 操作の実行時間 (時間経過)
- 要求 ID
- HTTP 状態コード
- HTTP 理由語句
- 応答ヘッダー
- エラー情報 (該当する場合)

要求と応答のコンテンツの場合:

- Content-type ヘッダーに応じて、コンテンツ ストリームはテキストまたはバイトになります。
     > [!メモ} コンテンツ ログは既定で無効になっています。 有効にするには、`ClientOptions` で `Diagnostics.IsLoggingContentEnabled` を `true` に設定します。

イベント ログは通常、次の 3 つのレベルのいずれかで出力されます。

- 要求と応答イベントの情報
- エラーの警告
- 詳細なメッセージとコンテンツ ログの詳細

## <a name="enable-logging-with-built-in-methods"></a>組み込みメソッドを使用してログ記録を有効にする

Azure SDK for .NET クライアント ライブラリは、[`EventSource` クラス](/dotnet/api/system.diagnostics.tracing.eventsource)を使用して Windows イベント トレーシング (ETW) にイベントを記録します。これは、.NET では一般的です。 イベント ソースを使用すると、パフォーマンスのオーバーヘッドを最小限に抑えながら、アプリケーション コードで構造化されたログを使用できます。 これらのイベン トログにアクセスするには、イベント リスナーを登録する必要があります。

SDK には `Azure.Core.Diagnostics.AzureEventSourceListener` クラス (Azure.Core NuGet パッケージで定義されています) が含まれています。これには、.NET アプリケーションの包括的なログ記録を簡略化する 2 つの静的メソッド (`CreateConsoleLogger` と `CreateTraceLogger`) が含まれています。 これらのメソッドでは、ログ レベルを指定する省略可能なパラメーターを受け取ります。

### <a name="log-to-the-console-window"></a>コンソール ウィンドウにログを記録する

Azure SDK for .NET クライアント ライブラリの主な原則は、包括的なログをリアルタイムで簡単に表示できるようにすることです。 `CreateConsoleLogger` メソッドを使用すると、1 行のコードでログをコンソール ウィンドウに送信できます。

```csharp
using AzureEventSourceListener listener = AzureEventSourceListener.CreateConsoleLogger();
```

### <a name="log-to-diagnostic-traces"></a>診断トレースにログを記録する

トレース リスナーを実装する場合は、`CreateTraceLogger` メソッドを使用して、標準の .NET イベント トレース機構 ([`System.Diagnostics.Tracing`](/dotnet/api/system.diagnostics.tracing)) にログを記録できます。 .NET でのイベント トレースの詳細については、「[トレース リスナー](../framework/debug-trace-profile/trace-listeners.md)」を参照してください。 この例では、詳細レベルのログ記録を指定します。

```csharp
using AzureEventSourceListener listener = AzureEventSourceListener.CreateTraceLogger(EventLevel.Verbose);
```

## <a name="configure-custom-logging"></a>カスタム ログ記録を構成する

前述のように、Azure SDK for .NET からログ メッセージを受信するには、イベント リスナーを登録する必要があります。 包括的なログを実装する際に上記の簡略化されたメソッドを使用しない場合は、`AzureEventSourceListener` クラスのインスタンスを作成して、作成したコールバック関数に渡すことができます。 このメソッドでは、必要に応じて好きに処理できるログ メッセージを受信します。 また、インスタンスを構築するときに、含めるログ レベルを指定することもできます。

次の例では、カスタム メッセージを使用してコンソールにログを記録するイベント リスナーを作成し、それを詳細レベルの Azure コア イベントでフィルター処理します。

```csharp
using AzureEventSourceListener listener = new AzureEventSourceListener((e, message) =>
    {
        // Only log messages from Azure-Core event source
        if (e.EventSource.Name == "Azure-Core")
        {
            Console.WriteLine($"{DateTime.Now} {message}");
        }
    },
    level: EventLevel.Verbose);
```

## <a name="next-steps"></a>次の手順

- [Azure App Service のアプリの診断ログの有効化](/azure/app-service/troubleshoot-diagnostic-logs)
- [Azure のセキュリティ ログと監査のオプション](/azure/security/fundamentals/log-audit)を確認する
- [Azure プラットフォーム ログ](/azure/azure-monitor/platform/platform-logs-overview)を操作する方法を確認する
- [.NET Core のログ記録とトレース](../core/diagnostics/logging-tracing.md)の詳細について読む
