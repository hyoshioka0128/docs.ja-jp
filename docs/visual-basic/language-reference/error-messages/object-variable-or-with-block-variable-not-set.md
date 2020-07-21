---
title: オブジェクト変数または With ブロック変数が設定されていません。
ms.date: 07/20/2015
f1_keywords:
- vbrID91
ms.assetid: 2f03e611-f0ed-465c-99a2-a816e034faa3
ms.openlocfilehash: d1778e2bb58d32e976f10b3fba1637918278d36e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409284"
---
# <a name="object-variable-or-with-block-variable-not-set"></a>オブジェクト変数または With ブロック変数が設定されていません。
無効なオブジェクト変数が参照されています。   このエラーが発生する原因は複数あります。

- 型を指定せずに変数が宣言されました。 型を指定せずに変数が宣言されている場合、既定で `Object` 型になります。

    たとえば、`Dim x` で宣言された変数は、`Object;` 型になり、`Dim x As String` で宣言された変数は、`String` 型になります。

    > [!TIP]
    > `Option Strict` ステートメントでは、結果が `Object` 型となる暗黙の型指定が許可されません。 型を省略すると、コンパイル時エラーが発生します。 「[Option Strict ステートメント](../statements/option-strict-statement.md)」を参照してください。

- `Nothing` に設定されているオブジェクトを参照しようとしています。

- 正しく宣言されていない配列変数の要素にアクセスしようとしています。

    たとえば、`products() As String` として宣言された配列では、配列 `products(3) = "Widget"` の要素を参照しようとした場合に、エラーがトリガーされます。 配列には要素がなく、オブジェクトとして扱われます。

- ブロックが初期化される前に、`With...End With` ブロック内のコードにアクセスしようとしています。   `With` ステートメントのエントリ ポイントを実行して、`With...End With` ブロックを初期化する必要があります。

> [!NOTE]
> Visual Basic または VBA の以前のバージョンでは、このエラーは、`Set` キーワードを使用せずに変数に値を代入する (`Set x = "name"` ではなく `x = "name"`) ことによってもトリガーされていました。 `Set` キーワードは、Visual Basic .Net では無効になりました。

## <a name="to-correct-this-error"></a>このエラーを解決するには

1. ファイルの先頭に次のコードを追加して、`Option Strict` を `On` に設定します。

    ```vb
    Option Strict On
    ```

    プロジェクトを実行すると、**エラー一覧**に、型を使用せずに指定された任意の変数についてのコンパイラ エラーが表示されます。

2. `Option Strict` を有効にしない場合、コードで、型を使用せずに指定されたすべての変数 (`Dim x As String` ではなく `Dim x`) を検索し、目的の型を宣言に追加します。

3. `Nothing` に設定されているオブジェクト変数を参照していないことを確認してください。  コードでキーワード `Nothing` を検索し、オブジェクトを参照した後までオブジェクトが `Nothing` に設定されないように、コードを修正します。

4. 配列変数にアクセスする前に、それらの次元が設定されていることを確認してください。 最初に配列を作成するときに次元を割り当てる (`Dim x() As String` ではなく `Dim x(5) As String`) か、または配列に最初にアクセスする前に、`ReDim` キーワードを使用して、その次元を設定できます。

5. `With` ステートメントのエントリ ポイントを実行して、`With` ブロックが初期化されていることを確認します。

## <a name="see-also"></a>関連項目

- [オブジェクト変数の宣言](../../programming-guide/language-features/variables/object-variable-declaration.md)
- [ReDim ステートメント](../statements/redim-statement.md)
- [With...End With ステートメント](../statements/with-end-with-statement.md)
