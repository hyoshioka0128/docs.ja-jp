---
title: .NET for Apache Spark と ML.NET での感情分析のチュートリアル
description: このチュートリアルでは、感情分析に ML.NET と .NET for Apache Spark を使用する方法について説明します。
author: mamccrea
ms.author: mamccrea
ms.date: 06/25/2020
ms.topic: tutorial
ms.openlocfilehash: 69deb30419b98536fa309547d94f59bb266e413c
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617582"
---
# <a name="tutorial-sentiment-analysis-with-net-for-apache-spark-and-mlnet"></a>チュートリアル: .NET for Apache Spark と ML.NET での感情分析

このチュートリアルでは、ML.NET と .NET for Apache Spark を使用してオンライン レビューの感情分析を行う方法について説明します。 [ML.NET](http://dot.net/ml) は、クロスプラットフォームでオープンソースの機械学習フレームワークであり無料です。 ML.NET と .NET for Apache Spark を使用して、機械学習アルゴリズムのトレーニングと予測をスケーリングできます。

このチュートリアルでは、次の作業を行う方法について説明します。

> [!div class="checklist"]
>
> * Visual Studio で ML.NET モデル ビルダー を使用して感情分析モデルを作成します。
> * .NET for Apache Spark コンソール アプリを作成します。
> * ユーザー定義関数を記述して実装します。
> * .NET for Apache Spark コンソール アプリを実行します。

[!INCLUDE [spark-preview-note](../../../includes/spark-preview-note.md)]

## <a name="prerequisites"></a>必須コンポーネント

* これまでに .NET for Apache Spark アプリケーションを開発したことがない場合は、最初に[概要のチュートリアル](get-started.md)に関する記事を読んで、基本についての理解を深めてください。 このチュートリアルを続ける前に、概要チュートリアルのすべての前提条件を満たしてください。

* このチュートリアルでは、Visual Studio で使用できるビジュアル インターフェイスである ML.NET モデル ビルダー (プレビュー) を使用します。 Visual Studio がない場合は、無料で [Visual Studio の Community バージョンをダウンロードする](https://visualstudio.microsoft.com/downloads/)ことができます。

* ML.NET モデル ビルダー (プレビュー) を[ダウンロードしてインストール](https://marketplace.visualstudio.com/items?itemName=MLNET.07)します。

* Yelp レビュー データセットの [yelptest.csv](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/MachineLearning/Sentiment/Resources/yelptest.csv) と [yelptrain.csv](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/MachineLearning/Sentiment/Resources/yelptrain.csv) をダウンロードします。

## <a name="review-the-data"></a>データを確認する

Yelp レビュー データセットには、さまざまなサービスに関するオンライン Yelp レビューが含まれています。 [yelptrain.csv](https://github.com/dotnet/spark/blob/master/examples/Microsoft.Spark.CSharp.Examples/MachineLearning/Sentiment/Resources/yelptrain.csv) を開き、データの構造を確認します。 1 番目の列にはレビュー テキストが含まれ、2 番目の列にはセンチメントのスコアが含まれます。 センチメント スコアが 1 の場合、レビューは肯定的になり、センチメント スコアが 0 の場合、レビューは否定的になります。

サンプル データを次の表に示します。

|ReviewText|Sentiment|
|-|-|
|Wow...Loved this place.|    1|
|Crust is not good.|    0|

## <a name="build-your-machine-learning-model"></a>機械学習モデルを構築する

1. Visual Studio を開き、新しい C# コンソール アプリ (.NET Core) を作成します。 プロジェクトには「*MLSparkModel*」という名前を付けます。

1. **ソリューション エクスプローラー**で、*MLSparkModel* プロジェクトを右クリックします。 次に、 **[追加] > [機械学習]** を選択します。

1. ML.NET モデル ビルダーで、 **[Sentiment Analysis]\(感情分析\)** シナリオ タイルを選択します。

1. **[Add data]\(データの追加\)** ページで、*yelptrain.csv* データセットをアップロードします。

1. **[Columns to Predict]\(予測する列\)** ドロップダウンから *[Sentiment]\(感情\)* を選択します。

1. **[Train]\(トレーニング\)** ページで、トレーニング時間を "*60 秒*" に設定し、 **[Start training]\(トレーニングの開始\)** を選択します。 **[Progress]\(進行状況\)** の下にトレーニングの状態が表示されます。

1. モデル ビルダーのトレーニングが完了したら、トレーニングの結果を **[Evaluate]\(評価\)** します。 **[Try your model]\(モデルを試す\)** の下のテキスト ボックスに語句を入力して **[Predict]\(予測\)** を選択し、出力を確認することができます。

1. **[Code]\(コード\)** を選択してから **[Projects]\(プロジェクトの追加\)** を選択して、ML モデルをソリューションに追加します。

1. ソリューションに次の 2 つのプロジェクトが追加されることに注意してください: **MLSparkModelML.ConsoleApp** と **MLSparkModelML.Model**。

1. *MLSpark* C# プロジェクトをダブルクリックして、次のプロジェクト参照が追加されていることを確認します。

   ```xml
   <ItemGroup>
       <ProjectReference Include="..\MLSparkModelML.Model\MLSparkModelML.Model.csproj" />
   </ItemGroup>
   ```

## <a name="create-a-console-app"></a>コンソール アプリを作成する

モデル ビルダーによってコンソール アプリが自動的に作成されます。

1. ソリューション エクスプローラーで **MLSparkModelML.Console** を右クリックし、 **[NuGet パッケージの管理]** を選択します。

1. **Microsoft.Spark** を検索し、パッケージをインストールします。 **Microsoft.ML** は、モデル ビルダーによって自動的にインストールされます。

### <a name="create-a-sparksession"></a>SparkSession を作成する

1. **MLSparkModelML.ConsoleApp** の *Program.cs* ファイルを開きます。 このファイルは、モデル ビルダーによって自動生成されたものです。 `using` ステートメント、Main() メソッドの内容、および `CreateSingleDataSample` 領域を削除します。

1. 次に示す別の `using` ステートメントを *Program.cs* ファイルの先頭に追加します。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.ML;
   using Microsoft.ML.Data;
   using Microsoft.Spark.Sql;
   using MLSparkModelML.Model;
   ```

1. `DATA_FILEPATH` を実際の *yelptest.csv* のパスに変更します。

1. 新しい `SparkSession` を作成するために、次のコードを `Main` メソッドに追加します。 Spark セッションは、Dataset API と DataFrame API を使用して Spark をプログラミングするためのエントリ ポイントです。

   ```csharp
   SparkSession spark = SparkSession
        .Builder()
        .AppName(".NET for Apache Spark Sentiment Analysis")
        .GetOrCreate();
   ```

   上で作成した *spark* オブジェクトを呼び出すことで、プログラムの至るところで Spark と DataFrame の機能にアクセスできます。

### <a name="create-a-dataframe-and-print-to-console"></a>DataFrame を作成してコンソールに出力する

`DataFrame` として、*yelptest.csv* ファイルから Yelp レビュー データを読み取ります。 `header` オプションと `inferSchema` オプションを指定します。 `header` オプションを指定すると、*yelptest.csv* の最初の行が、データではなく列名として読み取られます。 `inferSchema` オプションを指定すると、データに基づいて列の型が推測されます。

```csharp
DataFrame df = spark
    .ReadStream()
    .Option("header", true)
    .Option("inferSchema", true)
    .Csv(DATA_FILEPATH);

df.Show();
```

### <a name="register-a-user-defined-function"></a>ユーザー定義関数を登録する

Spark アプリケーションで UDF ("*ユーザー定義関数*") を使用して、データの計算と分析を行うことができます。 このチュートリアルでは、ML.NET と UDF を使用して、各 Yelp レビューを評価します。

`MLudf` という名前の UDF を登録するために、次のコードを `Main` メソッドに追加します。

```csharp
spark.Udf()
    .Register<string, bool>("MLudf", predict);
```

この UDF は、入力として Yelp レビュー文字列を受け取り、肯定的または否定的な感情に対して、それぞれ true または false を出力します。 後のステップで定義する *predict()* メソッドが使用されます。

### <a name="use-spark-sql-to-call-the-udf"></a>Spark SQL を使用して UDF を呼び出す

データを読み取り、ML を組み込んだので、Spark SQL を使用して、DataFrame の各行に対して感情分析を実行する UDF を呼び出します。 次のコードを `Main` メソッドに追加します。

```csharp
// Use Spark SQL to call ML.NET UDF
// Display results of sentiment analysis on reviews
df.CreateOrReplaceTempView("Reviews");
DataFrame sqlDf = spark.Sql("SELECT ReviewText, MLudf(ReviewText) FROM Reviews");
sqlDf.Show();

// Print out first 20 rows of data
// Prevent data getting cut off by setting truncate = 0
sqlDf.Show(20, 0, false);

spark.Stop();
```

### <a name="create-predict-method"></a>predict() メソッドを作成する

`Main()` メソッドの前に、次のコードを追加します。 このコードは、モデル ビルダーによって *ConsumeModel.cs* に生成されるものと似ています。 このメソッドをコンソールに移動すると、アプリを実行するたびにモデルが読み込まれます。

```csharp
private static readonly PredictionEngine<ModelInput, ModelOutput> _predictionEngine;

static Program()
{
    MLContext mlContext = new MLContext();
    ITransformer model = mlContext.Model.Load("MLModel.zip", out DataViewSchema schema);
    _predictionEngine = mlContext.Model.CreatePredictionEngine<ModelInput, ModelOutput>(model);
}

static bool predict(string text)
{
    ModelInput input = new ModelInput
    {
        ReviewText = text
    };

    return _predictionEngine.Predict(input).Prediction;
}
```

## <a name="add-the-model-to-your-console-app"></a>コンソール アプリにモデルを追加する

ソリューション エクスプローラーで、**MLSparkModelML.Model** プロジェクトから *MLModel.zip* ファイルをコピーし、**MLSparkModelML.ConsoleApp** プロジェクトにそれを貼り付けます。 *MLSparkModelML.ConsoleApp.csproj* に参照が自動的に追加されます。

## <a name="run-your-code"></a>コードを実行する

`spark-submit` を使用してコードを実行します。 コマンド プロンプトを使用してコンソール アプリのルート フォルダーに移動し、次のコマンドを実行します。

最初に、アプリをクリーンにして発行します。

```dotnetcli
dotnet clean
dotnet publish
```

次に、コンソール アプリの発行フォルダーに移動して、次の `spark-submit` コマンドを実行します。 忘れずに、実際の Microsoft Spark jar ファイルのパスで、コマンドを更新してください。

```dotnetcli
%SPARK_HOME%\bin\spark-submit --class org.apache.spark.deploy.dotnet.DotnetRunner --master local microsoft-spark-2.4.x-0.10.0.jar dotnet MLSparkModelML.ConsoleApp.dll
```

## <a name="get-the-code"></a>コードを取得する

このチュートリアルは、「[ビッグ データでの感情分析](https://github.com/dotnet/spark/tree/master/examples/Microsoft.Spark.CSharp.Examples/MachineLearning/Sentiment)」の例のコードに似ています。

## <a name="next-steps"></a>次の手順

次の記事に進み、.NET for Apache Spark で構造化ストリーミングを行う方法を学習してください。
> [!div class="nextstepaction"]
> [チュートリアル: .NET for Apache Spark を使用した構造化ストリーミング](streaming.md)
