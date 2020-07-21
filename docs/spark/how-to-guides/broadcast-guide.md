---
title: .NET for Apache Spark でブロードキャスト変数を使用する
description: .NET for Apache Spark アプリケーションでブロードキャスト変数を使用する方法について説明します。
ms.date: 06/25/2020
ms.topic: conceptual
ms.custom: mvc,how-to
ms.openlocfilehash: d86b160855cc4d3f3a6502f5606d4766b7c06aa0
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85617857"
---
# <a name="use-broadcast-variables-in-net-for-apache-spark"></a>.NET for Apache Spark でブロードキャスト変数を使用する

この記事では、.NET for Apache Spark でブロードキャスト変数を使用する方法を学習します。 [Apache Spark のブロードキャスト変数](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables)は、読み取り専用であることを意図した、Executor で変数を共有するためのメカニズムです。 ブロードキャスト変数を使用すると、読み取り専用の変数をコピーしたものをタスクと共に送るのではなく、各マシンにキャッシュしたままにすることができます。 ブロードキャスト変数を使用すると、すべてのノードに大きな入力データセットのコピーを効率的な方法で渡すことができます。

データは 1 回しか送信されないため、タスクごとに Executor に送られるローカル変数と比較した場合、ブロードキャスト変数の方がパフォーマンスが優れています。 ブロードキャスト変数とそれらが使用される理由について理解を深めるには、[ブロードキャスト変数の公式ドキュメント](https://spark.apache.org/docs/2.2.0/rdd-programming-guide.html#broadcast-variables)を参照してください。

[!INCLUDE [spark-preview-note](../../../includes/spark-preview-note.md)]

## <a name="create-broadcast-variables"></a>ブロードキャスト変数を作成する

ブロードキャスト変数を作成するには、任意の変数 `v` に対して `SparkContext.Broadcast(v)` を呼び出します。 ブロードキャスト変数は、変数 `v` のラッパーであり、`Value()` メソッドを呼び出すとその値にアクセスできます。

次のコード スニペットでは文字列変数 `v` が作成され、`SparkContext.Broadcast(v)` が呼び出されたときに、ブロードキャスト変数 `bv` が作成されます。 `Broadcast` の型パラメーター string が、ブロードキャストされている変数の型と一致していることがわかります。 ユーザー定義関数 (UDF) により、`bv` の値が返されます。

```csharp
string v = "Variable to be broadcasted";
Broadcast<string> bv = SparkContext.Broadcast(v);

Func<Column, Column> udf = Udf<string, string>(
    str => $"{str}: {bv.Value()}");
```

## <a name="delete-broadcast-variables"></a>ブロードキャスト変数を削除する

ブロードキャスト変数は、`Destroy()` メソッドを呼び出すと、すべての Executor から削除することができます。

```csharp
bv.Destroy();
```

`Destroy()` によって、ブロードキャスト変数に関連するすべてのデータとメタデータが削除されるため、注意して使用する必要があります。 ブロードキャスト変数が一度破棄されると、再度使用することはできません。

## <a name="limit-broadcast-variable-scope-in-udfs"></a>UDF のブロードキャスト変数のスコープを制限する

UDF でブロードキャスト変数を使用する場合は、変数を参照している UDF のみに変数のスコープを制限する必要があります。 この事象については、[UDF の使用に関するガイド](udf-guide.md)で詳しく説明しています。 スコープは、ブロードキャスト変数に対して `Destroy()` を呼び出すときに特に重要です。

破棄されたブロードキャスト変数が他の UDF から参照できる場合、またはアクセスできる場合は、それが参照されていない場合でも、そのすべての UDF がシリアル化の対象として選択されます。 .NET for Apache Spark では、破棄されたブロードキャスト変数をシリアル化できないため、エラーが発生します。 次のコード スニペットは、このエラーを示しています。

```csharp
string v = "Variable to be broadcasted";
Broadcast<string> bv = SparkContext.Broadcast(v);

// Using the broadcast variable in a UDF:
Func<Column, Column> udf1 = Udf<string, string>(
    str => $"{str}: {bv.Value()}");

// Destroying bv
bv.Destroy();

// Calling udf1 after destroying bv throws the following expected exception:
// org.apache.spark.SparkException: Attempted to use Broadcast(0) after it was destroyed
df.Select(udf1(df["_1"])).Show();

// Different UDF udf2 that is not referencing bv
Func<Column, Column> udf2 = Udf<string, string>(
    str => $"{str}: not referencing broadcast variable");

// Calling udf2 throws the following (unexpected) exception:
// [Error] [JvmBridge] org.apache.spark.SparkException: Task not serializable
df.Select(udf2(df["_1"])).Show();
```

次のコード スニペットは、予期しないシリアル化の動作により、`bv` の破棄が確実に `udf2` に影響しないようにする方法を示しています。

```csharp
string v = "Variable to be broadcasted";
// Restricting the visibility of bv to only the UDF referencing it
{
    Broadcast<string> bv = SparkContext.Broadcast(v);

    // Using the broadcast variable in a UDF:
    Func<Column, Column> udf1 = Udf<string, string>(
        str => $"{str}: {bv.Value()}");

    // Destroying bv
    bv.Destroy();
}

// Different UDF udf2 that is not referencing bv
Func<Column, Column> udf2 = Udf<string, string>(
    str => $"{str}: not referencing broadcast variable");

// Calling udf2 works fine as expected
df.Select(udf2(df["_1"])).Show();
```

## <a name="next-steps"></a>次の手順

* [.NET for Apache Spark の概要](../tutorials/get-started.md)
* [Windows で .NET for Apache Spark アプリケーションをデバッグする](debug.md)
* [.NET for Apache Spark ワーカーとユーザー定義関数のバイナリを展開する](deploy-worker-udf-binaries.md)
