---
title: モデル ビルダーの概要としくみ
description: ML.NET モデル ビルダーを使用し、機械学習モデルを自動的にトレーニングする方法
author: natke
ms.date: 08/07/2019
ms.custom: overview
ms.openlocfilehash: 77fe56dba3532617ad9fb0c89bfaac7c8e031ce7
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73971522"
---
# <a name="what-is-model-builder-and-how-does-it-work"></a>モデル ビルダーの概要としくみ

ML.NET モデル ビルダーは、直観的なグラフィックスでカスタムの機械学習モデルを構築、トレーニング、展開できる Visual Studio 拡張機能です。

モデル ビルダーでは自動化された機械学習 (AutoML) を利用してさまざまな機械学習のアルゴリズムや設定を見つけます。自分のシナリオに最適なものを見つけるのに役立ちます。

モデル ビルダーは機械学習の専門知識がなくても使用できます。 必要なものはいくつかのデータと解決すべき問題です。 モデル ビルダーでは、.NET アプリケーションにモデルを追加するコードが生成されます。

![モデル ビルダー Visual Studio 拡張機能のユーザー インターフェイスのアニメーション](media/ml-dotnet-model-builder.gif)

> [!NOTE]
> モデル ビルダーは現在のところ、プレビュー段階です。

## <a name="scenarios"></a>シナリオ

さまざまなシナリオをモデル ビルダーに取り込み、自分のアプリケーションのための機械学習モデルを生成できます。

シナリオは、自分のデータを使用して行う予測の種類を説明するものです。 次に例を示します。

- 過去の販売データに基づいて今後の製品売上高を予測する
- 顧客のレビューに基づいてセンチメントを肯定的と否定的に分類する
- 銀行取引が詐欺かどうかを検出する
- 顧客がフィードバックした問題を社内の該当チームに送信する

## <a name="choose-a-model-type"></a>モデルの種類の選択

モデル ビルダーでは、機械学習モデルの種類を選択する必要があります。 モデルの種類は、行おうとしている予測の種類によって異なります。

数値を予測するシナリオの場合、機械学習モデルの種類は `regression` と呼ばれます。

カテゴリを予測するシナリオの場合、モデルの種類は `classification` です。 分類には、次の 2 つがあります。

- カテゴリが 2 つのみの場合は `binary classification`。
- カテゴリが 3 つ以上ある場合は `multiclass classification`。

### <a name="which-model-type-is-right-for-me"></a>適切なモデルの種類はどれですか?

#### <a name="predict-a-category-when-there-are-only-two-categories"></a>カテゴリを予測する (カテゴリが 2 つのみの場合)

二項分類は、データを 2 つのカテゴリ (はい/いいえ、合格/不合格、真/偽、正/負) に分類するために使用されます。

![不正検出、リスク軽減、アプリケーション スクリーニングなど、二項分類の例を示す図](media/binary-classification-examples.png)

センチメント分析は、顧客からのフィードバックの肯定性/否定性を予測する目的で利用できます。 これは二項分類のモデルの種類の一例です。

2 つのカテゴリに分類することが自分のシナリオで求められる場合、独自のデータセットと共にこのテンプレートを使用できます。

#### <a name="predict-a-category-when-there-are-three-or-more-categories"></a>カテゴリを予測する (3 つ以上のカテゴリがある場合)

多クラス分類は、データを 3 つ以上のクラスに分類する目的で利用できます。

![ドキュメントと製品の分類、サポート チケットのルーティング、顧客の問題の優先度設定など、多クラス分類の例](media/multiclass-classification-examples.png)

問題分類は、顧客からのフィードバック (たとえば、GitHub で) に含まれる問題を問題のタイトルや説明で分類する目的で利用できます。 これは多クラス分類のモデルの種類の一例です。

データを 3 つ以上のカテゴリに分類する場合、シナリオに問題分類テンプレートを使用できます。

#### <a name="predict-a-number"></a>数値を予測する

回帰は、数値を予測する目的で利用されます。

![価格予測、売上予測、予測メンテナンスなどの回帰の例を示す図](media/regression-examples.png)

価格予測は、家の場所、規模、その他の特徴を利用し、家の価格を予測する目的で利用できます。 これは回帰のモデルの種類の一例です。

独自のデータセットで数値を予測する場合、自分のシナリオに価格予測テンプレートを使用できます。

#### <a name="custom-scenario-choose-your-model-type"></a>カスタム シナリオ (モデルの種類を選択する)

カスタム シナリオでは、自分のモデルの種類を手動で選択できます。

## <a name="data"></a>データ

モデルの種類を選択すると、モデル ビルダーからデータセットを提供するように求められます。 このデータはモデルをトレーニングし、評価し、シナリオに最適なモデルを選択するために使用されます。

![モデル ビルダーの手順を示す図](media/model-builder-steps.png)

### <a name="choose-the-output-to-predict-label"></a>予測する出力を選択します (ラベル)

データセットは、トレーニング サンプルの行と属性の列からなるテーブルです。 各行の内容:

- **ラベル** (予測する属性)
- **特徴** (ラベルを予測するための入力として使用される属性)。

家の価格予測シナリオの場合、特徴は次のようになります。

- 家の面積
- 寝室と浴室の数
- 郵便番号

ラベルは、面積、寝室数、浴室数、郵便番号からなるその行の過去の住宅価格です。

![サイズ、部屋数、郵便番号、価格ラベルから構成される特徴を持つ住宅価格データからなる行と列を示す表](media/model-builder-data.png)

### <a name="example-datasets"></a>データセットの例

独自のデータをまだ用意していない場合、次のいずれかのデータセットをお試しください。

|シナリオ|モデルの種類|データ|group1|フィーチャー|
|-|-|-|-|-|
|価格の予測|回帰|[タクシーの料金データ](https://github.com/dotnet/machinelearning-samples/blob/master/datasets/taxi-fare-train.csv)|料金|乗車時間、距離|
|異常検出|二項分類|[製品の売上データ](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/AnomalyDetection_Sales/SpikeDetection/Data/product-sales.csv)|製品の売上|月|
|センチメント分析|二項分類|[Web サイトのコメント データ](https://raw.githubusercontent.com/dotnet/machinelearning/master/test/data/wikipedia-detox-250-line-data.tsv)|ラベル (否定的なセンチメントのときは 0、肯定的なセンチメントのときは 1)|コメント、年度|
|不正行為の検出|二項分類|[クレジット カードのデータ](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/getting-started/BinaryClassification_CreditCardFraudDetection/CreditCardFraudDetection.Trainer/assets/input/creditcardfraud-dataset.zip)|クラス (詐欺の場合は 1、それ以外の場合 0)|金額、V1-V28 (匿名化された特徴)|
|テキスト分類|多クラス分類|[GitHub 問題のデータ](https://github.com/dotnet/machinelearning-samples/blob/master/samples/csharp/end-to-end-apps/MulticlassClassification-GitHubLabeler/GitHubLabeler/Data/corefx-issues-train.tsv)|区分|タイトル、説明|

## <a name="train"></a>トレーニング

シナリオ、データ、ラベルを選択すると、モデル ビルダーによってモデルがトレーニングされます。

### <a name="what-is-training"></a>トレーニングとは何か?

トレーニングとは、モデル ビルダーがシナリオの質問に対する回答方法をモデルに教える自動プロセスです。 トレーニングが終わると、モデルは以前に見たことがない入力データで予測できます。 たとえば、住宅価格を予測しているなら、新しい住宅が市場に出たとき、その販売価格を予測できます。

モデル ビルダーで使用される機械学習は自動化されているため (AutoML)、トレーニング中に、ユーザーが入力したり、調整したりする必要がありません。

## <a name="evaluate"></a>評価

評価は、トレーニングしたモデルを使用し、新しいテスト データで予測し、予測の精度を測定するプロセスです。

モデル ビルダーでは、トレーニング セットとテスト セットにトレーニング データが分割されます。 トレーニング データ (80%) はモデルのトレーニングに使用されます。テスト データ (20%) はモデルの評価のための控えとなります。 モデル ビルダーでは、メトリックを使用して、モデルがどの程度適切かを測定します。 使用される特定のメトリックは、モデルの種類によって異なります。 詳しくは、[モデルの評価メトリック](resources/metrics.md)に関する記事をご覧ください。

## <a name="improve"></a>改善

モデルのパフォーマンス スコアが予想ほど良くない場合、次のことができます。

- トレーニングの時間を長くします。 時間を増やせば、自動化された機械学習エンジンは試行するアルゴリズムや設定をそれだけ増やします。

- データを追加します。 高品質の機械学習モデルをトレーニングするにはデータ量が十分ではないことがあります。

- データのバランスを調整します。 分類タスクの場合、カテゴリ全体でトレーニング セットのバランスが取れていることを確認します。 たとえば、100 のトレーニング例に対してクラスが 4 つあるとき、90 個のレコードに最初の 2 つのクラス (tag1 と tag2) を使用するが、残りの 2 つ (tag3 と tag4) は残りの 10 個のレコードでのみ使用する場合、データにバランスが欠け、tag3 か tag4 を正しく予測することがモデルにとって難しくなります。

## <a name="code"></a>コード

評価フェーズ後、モデル ビルダーからモデル ファイルとコードが出力されます。このコードを使用し、モデルをアプリケーションに追加できます。 ML.NET モデルは zip ファイルで保存されます。 モデルを読み込み、使用するためのコードがソリューションに新しいプロジェクトとして追加されます。 モデル ビルダーからはサンプル コンソール アプリも追加されます。これを実行すると、実際に動作するモデルを確認できます。

さらに、モデル ビルダーからはモデルを生成したコードが出力されます。モデルの生成に使用された手順を理解できます。 モデル トレーニング コードを使用し、モデルを新しいデータで再トレーニングすることもできます。

## <a name="whats-next"></a>次の内容

モデル ビルダーの Visual Studio 拡張機能の[インストール](how-to-guides/install-model-builder.md)

[価格予測または回帰のシナリオ](tutorials/predict-prices-with-model-builder.md)をお試しください。
