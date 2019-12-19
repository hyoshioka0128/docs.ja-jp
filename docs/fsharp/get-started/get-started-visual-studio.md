---
title: Visual Studio でF#の作業の開始
description: Visual Studio でをF#使用する方法について説明します。
ms.date: 07/03/2018
ms.openlocfilehash: 80b4fc5b7631eace719832fe32003cad578ead27
ms.sourcegitcommit: 93762e1a0dae1b5f64d82eebb7b705a6d566d839
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2019
ms.locfileid: "74552828"
---
# <a name="get-started-with-f-in-visual-studio"></a>Visual Studio でF#の作業の開始

F#また、visual F# Studio IDE ではビジュアルツールがサポートされています。

まず、 [Visual Studio がと共F#にインストールされ](install-fsharp.md#install-f-with-visual-studio)ていることを確認します。

## <a name="creating-a-console-application"></a>コンソールアプリケーションの作成

Visual Studio の最も基本的なプロジェクトの1つは、コンソールアプリケーションです。  これを行う方法を次に示します。  Visual Studio が開いたら、次のようにします。

1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

2. 新しいプロジェクト ダイアログの **テンプレート** の下に **、 F#ビジュアル**が表示されます。  テンプレートを表示するにF#は、これを選択します。

3. **.Net Core コンソールアプリ**または**コンソールアプリ**のいずれかを選択します。

4. プロジェクトを作成するには、[Ok] をクリックします。 F#  ソリューションエクスプローラーにF#プロジェクトが表示されます。

## <a name="writing-your-code"></a>コードの記述

まず、コードをいくつか記述してみましょう。  `Program.fs` ファイルが開いていることを確認し、その内容を次の内容に置き換えます。

[!code-fsharp[HelloSquare](~/samples/snippets/fsharp/getting-started/hello-square.fs)]

前のコードサンプルでは、`x` という名前の入力を受け取り、それを単独で乗算する関数 `square` が定義されています。  でF#は[型の推定](../language-reference/type-inference.md)が使用されるため、`x` の型を指定する必要はありません。  コンパイラF#は、乗算が有効な型を認識し、`square` の呼び出し方法に基づいて `x` に型を割り当てます。  `square`にマウスポインターを合わせると、次のように表示されます。

```fsharp
val square: x:int -> int
```

これは、関数の型シグネチャとして知られています。  これは、次のように読み取ることができます。 "Square は、x という整数を受け取り、整数を生成する関数です。"  コンパイラによって現在の `int` 型が `square` されていることに注意してください。これは、乗算が*すべて*の型のジェネリックではなく、閉じられた型のセット全体でジェネリックであるためです。  コンパイラF#はこの時点で `int` を選択しましたが、`float`などの別の入力型を使用して `square` を呼び出すと、型シグネチャが調整されます。

別の関数 `main`が定義されています。これは、プログラムの実行F#を開始する必要があることをコンパイラに通知するために、`EntryPoint` 属性で修飾されています。  これは、コマンドライン引数をこの関数に渡すことができる他の[C スタイルのプログラミング言語](https://en.wikipedia.org/wiki/Entry_point#C_and_C.2B.2B)と同じ規則に従い、整数のコードが返されます (通常は `0`)。

この関数は、`12`の引数を使用して `square` 関数を呼び出します。  次F#に、コンパイラは `square` の型を `int -> int` に割り当てます。これは、`int` を受け取り、`int`を生成する関数です。  `printfn` の呼び出しは、C スタイルのプログラミング言語に似た書式指定文字列を使用する書式設定された印刷関数で、書式指定文字列で指定されたパラメーターに対応するパラメーターで、結果と改行を出力します。

## <a name="running-your-code"></a>コードの実行

**Ctrl**+**F5**キーを押してコードを実行し、結果を確認できます。  これにより、デバッグなしでプログラムが実行され、結果を確認できるようになります。  または、Visual Studio で **[デバッグ]** トップレベルメニュー項目を選択し、 **[デバッグなしで開始]** をクリックします。

次のように、Visual Studio がポップアップ表示されたコンソールウィンドウに出力されます。

```console
12 squared is 144!
```

おめでとうございます!  Visual Studio で最初F#のプロジェクトを作成し、関数をF#呼び出した結果を出力する関数を記述し、プロジェクトを実行して結果を確認しました。

## <a name="next-steps"></a>次のステップ:

このF#言語の主要機能の一部については、「」 [ F#のツアー](../tour.md)をご覧ください。  ここでは、のF#一部の機能の概要を説明し、Visual Studio にコピーして実行できるコードサンプルをいくつか紹介します。  ドキュメントのF#詳細については、 [ F# docs ホームページ](../index.yml)を参照してください。

## <a name="see-also"></a>参照

- [F# のツアー](../tour.md)
- [F#言語リファレンス](../language-reference/index.md)
- [型の推論](../language-reference/type-inference.md)
- [シンボルと演算子のリファレンス](../language-reference/symbol-and-operator-reference/index.md)
