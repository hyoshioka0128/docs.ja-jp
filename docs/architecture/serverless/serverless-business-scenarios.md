---
title: サーバーレス アプリのサンプルのビジネス シナリオとユースケース
description: 画像処理からモバイル サポートや ETL パイプラインまで、サンプルへのアクセスによるハンズオン アプローチを使用してサーバーレスについて学習します。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/17/2020
ms.openlocfilehash: 3cb3b73325fccc327ccf17f7298048f2eeb3577a
ms.sourcegitcommit: c2c1269a81ffdcfc8675bcd9a8505b1a11ffb271
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/25/2020
ms.locfileid: "82158451"
---
# <a name="serverless-business-scenarios-and-use-cases"></a>サーバーレスのビジネス シナリオとユース ケース

サーバーレス アプリケーションには、多くのユースケースとシナリオがあります。 この章には、さまざまなシナリオを示すサンプルが含まれています。 シナリオには、関連するドキュメントおよびパブリック ソース コード リポジトリへのリンクが含まれています。 この章のサンプルを使用して、サーバーレス ソリューションの独自の構築および実装を開始することができます。

## <a name="big-data-processing"></a>ビッグ データの処理

![map/reduce の図](https://docs.microsoft.com/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/media/mapreducearchitecture.png)

この例では、サーバーレスを使用して、ビッグ データ セットに対して map/reduce 操作を実行します。 ニューヨークのタクシーの 2017 年における 1 日の平均速度を決定します。

[ビッグ データ処理: Azure でのサーバーレス MapReduce](https://docs.microsoft.com/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/)

## <a name="create-serverless-applications-hands-on-lab"></a>サーバーレス アプリケーションを作成する: ハンズオン ラボ

関数を使用してサーバー側のロジックを実行し、サーバーレス アーキテクチャを構築する方法について説明します。

- ビジネスに最適な Azure サービスの選択
- Azure 関数の作成
- トリガーの使用
- 関数のチェーン
- 実行時間の長いワークフロー
- 監視
- 開発、テスト、展開

[サーバーレス アプリケーションの作成](https://docs.microsoft.com/learn/paths/create-serverless-applications/)

## <a name="customer-reviews"></a>顧客レビュー

このサンプルでは、Visual Studio の C# クラス ライブラリ用の新しい Azure Functions ツールを紹介します。 Azure Storage Blob および CosmosDB に格納される製品レビューを顧客が送信する Web サイトを作成します。 Azure Cognitive Services を使用して顧客レビューの自動モデレーションを実行する Azure 関数を追加します。 Azure ストレージ キューを使用して、Web サイトを関数から分離します。

[Cognitive Services による顧客レビュー アプリ](https://docs.microsoft.com/samples/azure-samples/functions-customer-reviews/customer-reviews-cognitive-services/)

## <a name="docker-linux-image-support"></a>Docker Linux イメージのサポート

このサンプルでは、Linux Docker コンテナーで Azure 関数をビルドして実行するための `Dockerfile` を作成する方法を示します。

[Linux 上の Azure 関数](https://docs.microsoft.com/samples/azure-samples/functions-linux-custom-image/azure-functions-on-linux-custom-image-tutorial-sample-project/)

## <a name="file-processing-and-validation"></a>ファイルの処理と検証

この例では、架空の顧客からの一連の CSV ファイルを解析します。 顧客の "バッチ" に必要なすべてのファイルの準備ができていることを確認した後、各ファイルの構造を検証します。 Azure Functions、Logic Apps、Durable Functions を使用して、異なるソリューションを示します。

[Azure Functions、Logic Apps、Durable Functions を使用した、ファイルの処理と検証](https://docs.microsoft.com/samples/azure-samples/serverless-file-validation/file-processing-and-validation-using-azure-functions-logic-apps-and-durable-functions/)

## <a name="game-data-visualization"></a>ゲーム データの視覚化

![ゲーム テレメトリ](https://docs.microsoft.com/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/media/points.png)

開発者がゲーム用にエディター内データ視覚化ソリューションを実装する方法の例です。 実際、Unreal Engine 4 プラグインと Unity プラグインは、このサンプルをバックエンドとして使用して開発されました。 サービス コンポーネントは、ゲーム エンジンに依存しません。

[エディター内でのゲーム テレメトリの視覚化](https://docs.microsoft.com/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/)

## <a name="graphql"></a>GraphQL

GraphQL API を公開するサーバーレス関数を作成します。

[GraphQL 用のサーバーレス関数](https://github.com/softchris/graphql-workshop-dotnet/blob/master/docs/workshop/4.md)

## <a name="internet-of-things-iot-reliable-edge-relay"></a>モノのインターネット (IoT) の高信頼性エッジ リレー

![IoT アーキテクチャ](https://docs.microsoft.com/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/media/architecture.png)

このサンプルでは、IoT デバイスからの高信頼性のアップストリーム通信を可能にする新しい通信プロトコルを実装します。 データ ギャップの検出とバックフィルを自動化します。

[IoT 高信頼性エッジ リレー](https://docs.microsoft.com/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/)

## <a name="microservices-reference-architecture"></a>マイクロサービス参照アーキテクチャ

![参照アーキテクチャ](https://docs.microsoft.com/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/media/macro-architecture.png)

Relecloud (架空の会社) による Rideshare アプリケーションの設計、開発、配布に関連する意思決定プロセスの手順を示す参照アーキテクチャです。 アーキテクチャのすべてのコンポーネントを構成して展開するための実践的な手順が含まれています。

[サーバーレス マイクロサービス参照アーキテクチャ](https://docs.microsoft.com/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/)

## <a name="migrate-console-apps-to-serverless"></a>コンソール アプリをサーバーレスに移行する

このサンプルは、任意のコンソール アプリケーションを Azure Functions の HTTP Web サービスに変換するために使用できる汎用関数 (`.csx` ファイル) です。 必要な作業は、構成ファイルを編集し、`.exe` に引数として渡す入力パラメーターを指定することだけです。

[Azure Functions でコンソール アプリを実行する](https://docs.microsoft.com/samples/azure-samples/functions-dotnet-migrating-console-apps/run-console-apps-on-azure-functions/)

## <a name="serverless-for-mobile"></a>モバイル用のサーバーレス

Azure Functions は実装と保守が簡単で、HTTP を介してアクセスできます。 モバイル アプリケーション用の API を実装する優れた方法です。 Microsoft では、iOS、Android、Windows 向けの優れたクロスプラットフォーム ツールが Xamarin で提供されています。 そのため、Xamarin と Azure Functions は連携して機能します。 この記事では、最初に Azure portal または Visual Studio で Azure 関数を実装してから、Android、iOS、Windows で実行される Xamarin.Forms を使用してクロスプラットフォーム クライアントを構築する方法について説明します。

[Xamarin.Forms クライアントを使用するシンプルな Azure 関数の実装](https://docs.microsoft.com/samples/azure-samples/functions-xamarin-getting-started/implementing-a-simple-azure-function-with-a-xamarinforms-client/)

## <a name="serverless-messaging"></a>サーバーレス メッセージング

このサンプルでは、Durable Functions のファンアウト パターンを使用して、任意の数のセッションまたはパーティションから任意の数のメッセージを読み込む方法を示します。 Service Bus、Event Hubs、またはストレージ キューを対象としています。 また、このサンプルでは、それらのメッセージを別の Azure 関数で使用し、結果のタイミング データを別のイベント ハブに読み込む機能を追加します。 その後、データは、Azure Data Explorer などの分析サービスに取り込まれます。

[Service Bus、Event Hubs、ストレージ キューと Azure Functions によりメッセージを生成して使用する](https://docs.microsoft.com/samples/azure-samples/durable-functions-producer-consumer/product-consume-messages-az-functions/)

## <a name="recommended-resources"></a>推奨リソース

- [Linux 上の Azure 関数](https://docs.microsoft.com/samples/azure-samples/functions-linux-custom-image/azure-functions-on-linux-custom-image-tutorial-sample-project/)
- [ビッグ データ処理: Azure でのサーバーレス MapReduce](https://docs.microsoft.com/samples/azure-samples/durablefunctions-mapreduce-dotnet/big-data-processing-serverless-mapreduce-on-azure/)
- [サーバーレス アプリケーションの作成](https://docs.microsoft.com/learn/paths/create-serverless-applications/)
- [Cognitive Services による顧客レビュー アプリ](https://docs.microsoft.com/samples/azure-samples/functions-customer-reviews/customer-reviews-cognitive-services/)
- [Azure Functions、Logic Apps、Durable Functions を使用した、ファイルの処理と検証](https://docs.microsoft.com/samples/azure-samples/serverless-file-validation/file-processing-and-validation-using-azure-functions-logic-apps-and-durable-functions/)
- [Xamarin.Forms クライアントを使用するシンプルな Azure 関数の実装](https://docs.microsoft.com/samples/azure-samples/functions-xamarin-getting-started/implementing-a-simple-azure-function-with-a-xamarinforms-client/)
- [エディター内でのゲーム テレメトリの視覚化](https://docs.microsoft.com/samples/azure-samples/gaming-in-editor-telemetry/in-editor-telemetry-visualization/)
- [IoT 高信頼性エッジ リレー](https://docs.microsoft.com/samples/azure-samples/iot-reliable-edge-relay/iot-reliable-edge-relay/)
- [Service Bus、Event Hubs、ストレージ キューと Azure Functions によりメッセージを生成して使用する](https://docs.microsoft.com/samples/azure-samples/durable-functions-producer-consumer/product-consume-messages-az-functions/)
- [Azure Functions でコンソール アプリを実行する](https://docs.microsoft.com/samples/azure-samples/functions-dotnet-migrating-console-apps/run-console-apps-on-azure-functions/)
- [GraphQL 用のサーバーレス関数](https://github.com/softchris/graphql-workshop-dotnet/blob/master/docs/workshop/4.md)
- [サーバーレス マイクロサービス参照アーキテクチャ](https://docs.microsoft.com/samples/azure-samples/serverless-microservices-reference-architecture/serverless-microservices-reference-architecture/)

>[!div class="step-by-step"]
>[前へ](orchestration-patterns.md)
>[次へ](serverless-conclusion.md)
