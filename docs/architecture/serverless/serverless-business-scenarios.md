---
title: サーバーレスアプリのビジネスシナリオとユースケースの例
description: 画像処理からモバイルバックエンドおよび ETL パイプラインまでの範囲のサンプルにアクセスすることにより、サーバーレスで実践的なアプローチを学ぶことができます。
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 7024a33f8a7fccd6afa51c126454afedd87cceee
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834294"
---
# <a name="serverless-business-scenarios-and-use-cases"></a>サーバーレスのビジネス シナリオとユース ケース

サーバーレスアプリケーションには、多くのユースケースとシナリオがあります。 この章には、さまざまなシナリオを示すサンプルが含まれています。 このシナリオには、関連するドキュメントやパブリックソースコードリポジトリへのリンクが含まれています。 この章のサンプルを使用すると、サーバーレスソリューションを独自に構築して実装することができます。

## <a name="analyze-and-archive-images"></a>画像の分析とアーカイブ

このサンプルでは、サーバーレスイベント (Event Grid)、ワークフロー (ロジックアプリ)、およびコード (Azure Functions) を示します。 また、別のリソースと統合する方法についても説明します。この場合 Cognitive Services イメージ分析に使用します。

コンソールアプリケーションを使用すると、web 上の URL へのリンクを渡すことができます。 アプリは、この URL をイベントグリッドメッセージとして公開します。 並列では、サーバーレス関数アプリとロジックアプリがメッセージをサブスクライブします。 サーバーレス関数アプリは、イメージを blob ストレージにシリアル化します。 また、Azure Table Storage に情報を格納します。 メタデータには、元のイメージの URL と blob イメージの名前が格納されます。 ロジックアプリは、Custom Vision API とやり取りしてイメージを分析し、コンピューターによって生成されたキャプションを作成します。 キャプションはメタデータテーブルに格納されます。

![イメージアーキテクチャの分析とアーカイブ](./media/image-processing-example.png)

個別のシングルページアプリケーション (SPA) は、サーバーレス関数を呼び出して、イメージとメタデータの一覧を取得します。 イメージごとに、アーカイブからイメージデータを配信する別の関数を呼び出します。 最終的な結果は、キャプションが自動であるギャラリーです。

![自動イメージギャラリー](./media/automated-image-gallery.png)

完全なリポジトリとロジックアプリを構築するための手順については、こちらを参照してください。[イベントグリッドの接着](https://github.com/JeremyLikness/Event-Grid-Glue)。

## <a name="cross-platform-mobile-client-using-xamarinforms-and-functions"></a>Xamarin. Forms と functions を使用したクロスプラットフォームモバイルクライアント

Azure Web ポータルまたは Visual Studio で、単純なサーバーレス Azure 関数を実装する方法について説明します。 Android、iOS、Windows で実行される Xamarin. フォームを使用してクライアントを構築します。 次に、サーバーとサーバーレスバックエンドを使用したモバイルクライアントの間の通信メディアとして JavaScript Object Notation (JSON) を使用するようにアプリケーションを調整します。

詳細については、「 [Xamarin. Forms クライアントを使用した単純な Azure 関数の実装](https://azure.microsoft.com/resources/samples/functions-xamarin-getting-started/)」を参照してください。

## <a name="generate-a-photo-mosaic-with-serverless-image-recognition"></a>サーバーレスイメージ認識で photo モザイクを生成します

このサンプルでは、Azure Functions と Microsoft Cognitive Services Custom Vision Service を使用して、入力画像から photo モザイクを生成します。 モデルは画像を認識するようにトレーニングされています。 画像がアップロードされると、画像が認識され、Bing で検索されます。 元のイメージは、検索結果を使用して再構成されます。

![州オーランド目の写真とモザイク](./media/orlando-eye-both.png)

たとえば、州オーランドの目印 (州オーランドアイなど) を使用してモデルをトレーニングできます。 Custom Vision は州オーランド目の画像を認識し、この関数は "州オーランドアイ" の Bing イメージの検索結果で構成される写真のモザイクを作成します。

詳細については、「 [photo モザイクジェネレーターの Azure Functions](https://azure.microsoft.com/resources/samples/functions-dotnet-photo-mosaic/)」を参照してください。

## <a name="migrate-an-existing-application-to-the-cloud"></a>既存のアプリケーションをクラウドに移行する

前の章で説明したように、アプリケーションをオンプレミスでホストするための N 層アーキテクチャを採用するのが一般的です。 「仮想マシンを使用したリソースの移行」はクラウドへの最も危険なパスですが、多くの企業では、アプリケーションをリファクターする機会を使用することを選択しています。 幸い、リファクタリングは、"すべての" 労力である必要はありません。 実際には、アプリケーションを移行してから、コンポーネントをクラウドネイティブに置き換えることができます。

アプリケーションでは、Azure Functions のプロキシ機能を使用して、従来のオンプレミスコードからサーバーレスエンドポイントへのエンドポイントのリファクタリングを有効にします。

![移行のアーキテクチャ](./media/migration-architecture.png)

プロキシは、サーバーレス関数に移動されるたびに個々の要求を再ルーティングするために更新される1つの API エンドポイントを提供します。

移行全体の手順を説明したビデオを見ることができます。[サーバーレスの Azure functions でリフトアンドシフトを行うことが](https://channel9.msdn.com/Events/Connect/2017/E102)できます。 サンプルコードにアクセスします。[独自のアプリを利用](https://github.com/JeremyLikness/bring-own-app-connect-17)できます。

## <a name="parse-a-csv-file-and-insert-into-a-database"></a>CSV ファイルを解析してデータベースに挿入する

抽出、変換、読み込み (ETL) は、さまざまなシステムを統合する共通のビジネス機能です。 従来の方法では、多くの場合、専用の FTP サーバーを設定し、スケジュールされたジョブを展開してファイルを解析し、ビジネスで使用できるように変換します。 サーバーレスアーキテクチャを使用すると、ファイルがアップロードされたときにトリガーが起動するため、ジョブが簡単になります。 どんなのようなタスクは、特定の問題に焦点を当てる小さなコードの理想的な構成によって、ETL などのタスクを実行します。 Azure Functions

![Csv 解析プロセスを示すスクリーンショット。](./media/serverless-business-scenarios/csv-parse-database-import.png)

ソースコードとハンズオンラボについては、「 [CSV インポートラボ](https://github.com/JeremyLikness/azure-fn-file-process-hol)」を参照してください。

## <a name="shorten-links-and-track-metrics"></a>リンクを短くしてメトリックを追跡する

リンクの短縮ツールでは、最初に、短い twitter の投稿での Url のエンコードが140文字の制限に対応しました。 多くの用途が含まれるようになっており、分析のためにクリックスルーを追跡するのが最も一般的です。 リンク短縮のシナリオは、リンクとレポートのメトリックを管理する完全なサーバーレスアプリケーションです。

Azure Functions は、長い URL を貼り付けて短い Url を生成できるシングルページアプリケーション (SPA) を提供するために使用されます。 これらの Url には、キャンペーン (トピック) やメディア (リンクが投稿されているソーシャルネットワークなど) を追跡するタグが付けられます。 短いコードはキーとして Azure Table Storage に格納され、長い URL は値として格納されます。 ショートリンクをクリックすると、別の関数によって長い URL が検索され、リダイレクトが送信され、イベントに関する情報がキューに格納されます。 別の Azure 関数がキューを処理し、情報を Azure Cosmos DB に配置します。

![リンク短縮のアーキテクチャ](./media/link-shortener-architecture.png)

次に、Power BI ダッシュボードを作成して、収集されたデータに関する洞察を収集できます。 バックエンドでは、Application Insights は重要なメトリックを提供します。 テレメトリには、平均的なユーザーのリダイレクトにかかる時間と、Azure Table Storage にアクセスするためにかかる時間が含まれます。

![Power BI の例](./media/power-bi-example.png)

詳細については、「完全なリンク短縮リポジトリ」を参照してください。[サーバーレス URL 短縮](https://github.com/jeremylikness/serverless-url-shortener)。 簡略化されたバージョンについては、こちらを参照してください。[サーバーレスの .net アプリを数分で Azure Storage](https://devblogs.microsoft.com/aspnet/azure-storage-for-serverless-net-apps-in-minutes/)します。

## <a name="verify-device-connectivity-using-a-ping"></a>Ping を使用してデバイスの接続を確認する

このサンプルは、Azure IoT Hub と Azure 関数で構成されています。 IoT Hub に新しいメッセージが表示され、Azure 関数がトリガーされます。 サーバーレスコードは、送信元のデバイスに同じメッセージの内容を送り返します。 このプロジェクトには、ソリューションに必要なすべてのコードと配置の構成が含まれています。

詳細については、「 [ping の Azure IoT Hub](https://azure.microsoft.com/resources/samples/iot-hub-node-ping/)」を参照してください。

## <a name="recommended-resources"></a>推奨されるリソース

* [Photo モザイクジェネレーターの Azure Functions](https://azure.microsoft.com/resources/samples/functions-dotnet-photo-mosaic/)
* [Ping の Azure IoT Hub](https://azure.microsoft.com/resources/samples/iot-hub-node-ping/)
* [サーバーレスの .NET アプリを数分で Azure Storage](https://devblogs.microsoft.com/aspnet/azure-storage-for-serverless-net-apps-in-minutes/)
* [独自のアプリを持ち込む](https://github.com/JeremyLikness/bring-own-app-connect-17)
* [CSV インポートラボ](https://github.com/JeremyLikness/azure-fn-file-process-hol)
* [イベントグリッドの接着](https://github.com/JeremyLikness/Event-Grid-Glue)
* [Xamarin クライアントを使用した単純な Azure 関数の実装](https://azure.microsoft.com/resources/samples/functions-xamarin-getting-started/)
* [サーバーレス Azure functions を使用したリフトアンドシフト](https://channel9.msdn.com/Events/Connect/2017/E102)
* [サーバーレス URL 短縮](https://github.com/jeremylikness/serverless-url-shortener)

>[!div class="step-by-step"]
>[前へ](orchestration-patterns.md)
>[次へ](serverless-conclusion.md)
