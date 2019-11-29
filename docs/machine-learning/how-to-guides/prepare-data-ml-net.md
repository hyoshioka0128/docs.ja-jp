---
title: モデル構築用のデータを準備する
description: ML.NET での変換を利用して、追加処理やモデルのビルドのためにデータを操作して準備する方法について説明します。
author: luisquintanilla
ms.author: luquinta
ms.date: 09/11/2019
ms.custom: mvc, how-to, title-hack-0625
ms.openlocfilehash: e9bfad4724b353b0f3bfc615a40f1d72b80a2cd4
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73976980"
---
# <a name="prepare-data-for-building-a-model"></a>モデル構築用のデータを準備する

ML.NET を利用して、追加処理やモデルのビルドのためのデータを準備する方法について説明します。

多くの場合、データは未整理であり、分散しています。 ML.NET 機械学習アルゴリズムでは、入力値などの特性が単一の数値ベクターになっていることを想定しています。 同様に、予測する値 (ラベル) は、カテゴリ データの場合は特に、エンコードする必要があります。 したがって、データ準備の目標の 1 つは、データを ML.NET アルゴリズムから期待されている形式にすることです。

## <a name="filter-data"></a>データのフィルター処理

データセット内の全データが、分析に関係するわけではない場合もあります。 関係のないデータを除去する方法が、フィルター処理です。 [`DataOperationsCatalog`](xref:Microsoft.ML.DataOperationsCatalog) には、全データを含む [`IDataView`](xref:Microsoft.ML.IDataView) を取得して目的のデータだけを含む [IDataView](xref:Microsoft.ML.IDataView) を返す一連のフィルター操作が用意されています。 フィルター操作は、[`TransformsCatalog`](xref:Microsoft.ML.TransformsCatalog) にあるような [`IEstimator`](xref:Microsoft.ML.IEstimator%601) または [`ITransformer`](xref:Microsoft.ML.ITransformer) ではないため、[`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) または [`TransformerChain`](xref:Microsoft.ML.Data.TransformerChain%601) データ準備パイプラインの一部に含めることはできません。

次の入力データを使用して、[`IDataView`](xref:Microsoft.ML.IDataView) に読み込ませます。

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

列の値に基づいてデータをフィルター処理するには、[`FilterRowsByColumn`](xref:Microsoft.ML.DataOperationsCatalog.FilterRowsByColumn*) メソッドを使用します。

```csharp
// Apply filter
IDataView filteredData = mlContext.Data.FilterRowsByColumn(data, "Price", lowerBound: 200000, upperBound: 1000000);
```

上記のサンプルでは、データセット内の価格が 200000 から 1000000 までの行を取得します。 このフィルターを適用した結果として、データ内の最後の 2 行だけが返されます。最初の行は価格が 100000 になっており、指定された範囲外にあるために除外されます。

## <a name="replace-missing-values"></a>欠損値を置き換える

欠損値は、データセット内でよく発生します。 欠損値を処理する 1 つの方法は、指定された型の既定値があればその値に、またはそのデータの平均値などの意味のある別の値に置き換えることです。

次の入力データを使用して、[`IDataView`](xref:Microsoft.ML.IDataView) に読み込ませます。

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=float.NaN
    }
};
```

リスト内の最後の要素では、`Price` が欠損値になっていることに注意してください。 `Price` 列内の欠損値を置き換えるには、[`ReplaceMissingValues`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) メソッドを使用して該当の欠損値を入力します。

> [!IMPORTANT]
> [`ReplaceMissingValue`](xref:Microsoft.ML.ExtensionsCatalog.ReplaceMissingValues*) は、数値データのみで機能します。

```csharp
// Define replacement estimator
var replacementEstimator = mlContext.Transforms.ReplaceMissingValues("Price", replacementMode: MissingValueReplacingEstimator.ReplacementMode.Mean);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer replacementTransformer = replacementEstimator.Fit(data);

// Transform data
IDataView transformedData = replacementTransformer.Transform(data);
```

ML.NET では、さまざまな[置換モード](xref:Microsoft.ML.Transforms.MissingValueReplacingEstimator.ReplacementMode)をサポートしています。 上記のサンプルでは、該当の列の平均値を使って欠損値を入力する、`Mean` 置換モードを使用しています。 置換の結果、データ内の最後の要素である `Price` プロパティには、100,000 と 300,000 の平均として 200,000 が入力されます。

## <a name="use-normalizers"></a>ノーマライザーを使用する

[正規化](https://en.wikipedia.org/wiki/Feature_scaling)は、アルゴリズムの適用を迅速に行えるように、同じスケール上にない特性を標準化する目的で使用されるデータの事前処理手法です。 たとえば、年齢と収入のような値の範囲は、年齢は一般的に 0 から 100 の範囲で、また、収入は一般的に 0 から 1000 単位の範囲で、大きく変わります。 正規化変換のより詳細な一覧と説明については、[変換に関するページ](../resources/transforms.md)を確認してください。

### <a name="min-max-normalization"></a>最小 - 最大の正規化

次の入力データを使用して、[`IDataView`](xref:Microsoft.ML.IDataView) に読み込ませます。

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms = 2f,
        Price = 200000f
    },
    new HomeData
    {
        NumberOfBedrooms = 1f,
        Price = 100000f
    }
};
```

正規化は、1 つの数値およびベクターを含む列に適用できます。 [`NormalizeMinMax`](xref:Microsoft.ML.NormalizationCatalog.NormalizeMinMax*) メソッドによる最小 - 最大の正規化を使って、`Price` 列のデータを正規化します。

```csharp
// Define min-max estimator
var minMaxEstimator = mlContext.Transforms.NormalizeMinMax("Price");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer minMaxTransformer = minMaxEstimator.Fit(data);

// Transform data
IDataView transformedData = minMaxTransformer.Transform(data);
```

0 から 1 の範囲で出力値を生成する `MinMax` 正規化の数式を使用して、元の価格値 `[200000,100000]` が `[ 1, 0.5 ]` に変換されます。

### <a name="binning"></a>ビン分割

[ビン分割](https://en.wikipedia.org/wiki/Data_binning)では、連続する値を不連続な入力値表現に変換します。 たとえば、特性の 1 つが年齢だとします。 実際の年齢値を使用する代わりに、ビン分割によってその値の範囲を作成します。 0 から 18 を 1 つのビン、19 から 35 をもう 1 つのビン、のように指定できます。

次の入力データを使用して、[`IDataView`](xref:Microsoft.ML.IDataView) に読み込ませます。

```csharp
HomeData[] homeDataList = new HomeData[]
{
    new HomeData
    {
        NumberOfBedrooms=1f,
        Price=100000f
    },
    new HomeData
    {
        NumberOfBedrooms=2f,
        Price=300000f
    },
    new HomeData
    {
        NumberOfBedrooms=6f,
        Price=600000f
    }
};
```

[`NormalizeBinning`](xref:Microsoft.ML.NormalizationCatalog.NormalizeBinning*) メソッドを使用して、データをビンに正規化します。 `maximumBinCount` パラメータ―を使用すると、データを分類するために必要なビン数を指定できます。 この例では、データは 2 つのビンに配置されます。

```csharp
// Define binning estimator
var binningEstimator = mlContext.Transforms.NormalizeBinning("Price", maximumBinCount: 2);

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
var binningTransformer = binningEstimator.Fit(data);

// Transform Data
IDataView transformedData = binningTransformer.Transform(data);
```

ビン分割の結果、`[0,200000,Infinity]` のビン境界が作成されます。 したがって、最初の測定範囲を 0 から 200000 まで、それ以外を 200000 より大きいが無限大より小さいとするため、結果として得られるビンは `[0,1,1]` となります。

## <a name="work-with-categorical-data"></a>カテゴリ別データを扱う

非数値のカテゴリ別データは、機械学習モデルのビルドに使用する前に、数値に変換する必要があります。

次の入力データを使用して、[`IDataView`](xref:Microsoft.ML.IDataView) に読み込ませます。

```csharp
CarData[] cars = new CarData[]
{
    new CarData
    {
        Color="Red",
        VehicleType="SUV"
    },
    new CarData
    {
        Color="Blue",
        VehicleType="Sedan"
    },
    new CarData
    {
        Color="Black",
        VehicleType="SUV"
    }
};
```

カテゴリ別の `VehicleType` プロパティは、[`OneHotEncoding`](xref:Microsoft.ML.CategoricalCatalog.OneHotEncoding*) メソッドを使用して数値に変換できます。

```csharp
// Define categorical transform estimator
var categoricalEstimator = mlContext.Transforms.Categorical.OneHotEncoding("VehicleType");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer categoricalTransformer = categoricalEstimator.Fit(data);

// Transform Data
IDataView transformedData = categoricalTransformer.Transform(data);
```

変換の結果、`VehicleType` のテキスト値が数値に変わります。 変換が適用されると、`VehicleType` 列内の項目は次のようになります。

```text
[
    1, // SUV
    2, // Sedan
    1 // SUV
]
```

## <a name="work-with-text-data"></a>テキスト データを操作する

テキスト データは、機械学習モデルのビルドに使用する前に、数値に変換される必要があります。 テキスト変換のより詳細な一覧と説明については、[変換に関するページ](../resources/transforms.md)を確認してください。

以下のようなデータを使用します。データは [`IDataView`](xref:Microsoft.ML.IDataView) に読み込まれています。

```csharp
ReviewData[] reviews = new ReviewData[]
{
    new ReviewData
    {
        Description="This is a good product",
        Rating=4.7f
    },
    new ReviewData
    {
        Description="This is a bad product",
        Rating=2.3f
    }
};
```

テキストを数値ベクター表現に変換する最も簡単な手順は、[`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) メソッドを使用することです。 [`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) 変換を使用することで、一連の変換が入力テキストの列に適用されて、Ip 正則化による単語と文字の N グラムを表した数値ベクターになります。

```csharp
// Define text transform estimator
var textEstimator  = mlContext.Transforms.Text.FeaturizeText("Description");

// Fit data to estimator
// Fitting generates a transformer that applies the operations of defined by estimator
ITransformer textTransformer = textEstimator.Fit(data);

// Transform data
IDataView transformedData = textTransformer.Transform(data);
```

変換の結果、`Description` 列内のテキスト値が、以下の出力のような数値ベクターに変換されます。

```text
[ 0.2041241, 0.2041241, 0.2041241, 0.4082483, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0.2041241, 0, 0, 0, 0, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0.4472136, 0 ]
```

複数のテキスト処理の手順を [`EstimatorChain`](xref:Microsoft.ML.Data.EstimatorChain%601) に結合してノイズを除去し、必要な処理リソース量をニーズに応じて潜在的に低減させます。

```csharp
// Define text transform estimator
var textEstimator = mlContext.Transforms.Text.NormalizeText("Description")
    .Append(mlContext.Transforms.Text.TokenizeIntoWords("Description"))
    .Append(mlContext.Transforms.Text.RemoveDefaultStopWords("Description"))
    .Append(mlContext.Transforms.Conversion.MapValueToKey("Description"))
    .Append(mlContext.Transforms.Text.ProduceNgrams("Description"))
    .Append(mlContext.Transforms.NormalizeLpNorm("Description"));
```

`textEstimator` には、[`FeaturizeText`](xref:Microsoft.ML.TextCatalog.FeaturizeText*) メソッドによって実行される操作のサブセットが含まれています。 より複雑なパイプラインの利点は、データに適用される変換に対する制御と可視性です。

最初の項目を例として使用した場合、`textEstimator` によって定義された変換手順で生成した結果を詳細に説明すると、次のようになります。

**元のテキスト:This is a good product**

|変換 | 説明 | 結果
|--|--|--|
|1.NormalizeText | 既定ですべての文字を小文字に変換します | this is a good product
|2.TokenizeWords | 文字列を個々の単語に分割します | ["this","is","a","good","product"]
|3.RemoveDefaultStopWords | *is* や *a* のようなストップワードを削除します。 | ["good","product"]
|4.MapValueToKey | 入力データに基づくキー (カテゴリ) に値をマップします |  [1,2]
|5.ProduceNGrams | テキストを連続する単語のシーケンスに変換します | [1,1,1,0,0]
|6.NormalizeLpNorm | lp 正則化によって入力値をスケーリングします | [ 0.577350529, 0.577350529, 0.577350529, 0, 0 ]
