---
title: C# における数値 - C# の概要に関するチュートリアル
description: 数値型とその用途、プロパティ、メソッドを詳しく見ていくことで C# について学習します。
ms.date: 10/31/2017
ms.custom: mvc
ms.openlocfilehash: 3dc2a5afc6321da45351525a632f586cb84bf7fe
ms.sourcegitcommit: de7f589de07a9979b6ac28f54c3e534a617d9425
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82794612"
---
# <a name="manipulate-integral-and-floating-point-numbers-in-c"></a>C\# で整数と浮動小数点数を操作する

このチュートリアルでは、対話形式で C# の数値型について説明します。 少量のコードを記述したら、そのコードをコンパイルして実行します。 このチュートリアルには、C# の数値と算術演算に関する一連のレッスンが含まれています。 これらのレッスンでは、C# 言語の基本を説明します。

このチュートリアルでは、開発用に使用できるマシンがあることを想定しています。 Windows、Linux、または macOS 上でローカルの開発環境を設定する手順については、.NET チュートリアル [Hello World in 10 minutes](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro) (10 分で Hello World) に記載されています。 使用するコマンドの概要については、詳細な情報へのリンクが掲載されている、[開発ツールに対する理解を深める](local-environment.md)方法に関するページをご覧ください。

## <a name="explore-integer-math"></a>整数の演算の確認

「*numbers-quickstart*」という名前のディレクトリを作成します。 それを現在のディレクトリにして、次のコマンドを実行します。

```dotnetcli
dotnet new console -n NumbersInCSharp -o .
```

お好みのエディターで *Program.cs* を開き、`Console.WriteLine("Hello World!");` の行を次のコードで置き換えます。

```csharp
int a = 18;
int b = 6;
int c = a + b;
Console.WriteLine(c);
```

コマンド ウィンドウで「`dotnet run`」を入力し、このコードを実行します。

整数を使用した基本的な算術演算の 1 つを確認しました。 `int` 型は、**整数**を表します (ゼロ、正の整数、または負の整数)。 加算には `+` 記号を使用します。 他の一般的な整数の算術演算には次のものがあります。

- `-`: 減算
- `*`: 乗算
- `/`: 除算

まずは、上記の各種演算を実行してみます。 `c` の値を記述した行の後に、次の数行を追加します。

```csharp

// subtraction
c = a - b;
Console.WriteLine(c);

// multiplication
c = a * b;
Console.WriteLine(c);

// division
c = a / b;
Console.WriteLine(c);
```

コマンド ウィンドウで「`dotnet run`」を入力し、このコードを実行します。

必要であれば、同じ行で複数の算術演算を記述することもできます。 例として `c = a + b - 12 * 17;` を試してみてください。 変数と定数を混在させることができます。

> [!TIP]
> C# (または何らかのプログラミング言語) について詳しく学習するに従い、コードを記述する際にミスをすることもあるでしょう。 **コンパイラ**は、そうしたエラーを発見して報告します。 エラー メッセージが出力された場合は、例のコードをよく確認して、ウィンドウで修正すべきコードを見つけます。
> こうした実習が C# コードの構造を理解するのに役立ちます。

最初の手順が完了しました。 次のセクションを開始する前に、現在のコードを別のメソッドに移動してみましょう。 移動しておくと、新しい例で作業を開始するときに楽になります。 `Main` メソッドの名前を `WorkingWithIntegers` に変更し、`WorkingWithIntegers` を呼び出す新しい `Main` メソッドを記述します。 完成したコードは次のようになります。

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();
        }
    }
}
```

## <a name="explore-order-of-operations"></a>演算の順序の確認

`WorkingWithIntegers()` の呼び出しをコメント アウトします。 こうしておくと、このセクションの作業を進めるにあたって出力がすっきりします。

```csharp
//WorkingWithIntegers();
```

C# では、`//` の後ろが**コメント**になります。 コードとしては実行せずにソース コード内に残したい任意のテキストを、コメントにすることができます。 コンパイラは、コメントから実行可能コードを生成しません。

C# 言語は、数学で学んだ規則と同じ規則で各演算の優先順位を定義します。
乗算と除算は、加算と減算よりも優先されます。
`Main` メソッドに次のコードを追加し、`dotnet run` を実行して詳しく見てみます。

```csharp
int a = 5;
int b = 4;
int c = 2;
int d = a + b * c;
Console.WriteLine(d);
 ```

出力を見ると、加算の前に乗算が実行されていることがわかります。

最初に実行したい演算を囲むように丸かっこを追加することで、演算の順序を変えることができます。 次の行を追加して、もう一度実行します。

```csharp
d = (a + b) * c;
Console.WriteLine(d);
```

さまざまな演算を多数組み合わせて、他にも試してみましょう。 `Main` メソッドの下部に、次のような行を追加します。 もう一度 `dotnet run` を実行してください。

```csharp
d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
Console.WriteLine(d);
```

整数について面白い動作をしていることに気づいたでしょうか。 結果に小数点や小数部分が含まれると予想される場合でも、整数の除算は常に整数の結果を算出します。

この動作を確認できない場合は、`Main` メソッドの最後で次のコードを試してください。

```csharp
int e = 7;
int f = 4;
int g = 3;
int h = (e + f) / g;
Console.WriteLine(h);
```

もう一度 `dotnet run` を入力して結果を確認します。

続行する前に、このセクションで記述したコードをすべて新しいメソッドに移します。 新しいメソッドを `OrderPrecedence` とします。
次のように記述します。

```csharp
using System;

namespace NumbersInCSharp
{
    class Program
    {
        static void WorkingWithIntegers()
        {
            int a = 18;
            int b = 6;

            // addition
            int c = a + b;
            Console.WriteLine(c);

            // subtraction
            c = a - b;
            Console.WriteLine(c);

            // multiplication
            c = a * b;
            Console.WriteLine(c);

            // division
            c = a / b;
            Console.WriteLine(c);
        }

        static void OrderPrecedence()
        {
            int a = 5;
            int b = 4;
            int c = 2;
            int d = a + b * c;
            Console.WriteLine(d);

            d = (a + b) * c;
            Console.WriteLine(d);

            d = (a + b) - 6 * c + (12 * 4) / 3 + 12;
            Console.WriteLine(d);

            int e = 7;
            int f = 4;
            int g = 3;
            int h = (e  + f) / g;
            Console.WriteLine(h);
        }

        static void Main(string[] args)
        {
            WorkingWithIntegers();

            OrderPrecedence();

        }
    }
}
```

## <a name="explore-integer-precision-and-limits"></a>整数の有効桁数と制限の確認

この最後のサンプルでは、整数の除算における結果の切り捨てについて確認します。
**modulo** 演算子 (`%` 文字) を使用して、**剰余**を得ることができます。 `Main` メソッドで次のコードを試してみてください。

```csharp
int a = 7;
int b = 4;
int c = 3;
int d = (a + b) / c;
int e = (a + b) % c;
Console.WriteLine($"quotient: {d}");
Console.WriteLine($"remainder: {e}");
```

C# の整数型は算術における整数ともう 1 つ異なる点があります。それは `int` 型には最小値と最大値の制限があるということです。 `Main` メソッドに次のコードを追加して、この制限を確認します。

```csharp
int max = int.MaxValue;
int min = int.MinValue;
Console.WriteLine($"The range of integers is {min} to {max}");
```

計算によってこれらの制限を超える値が作られると、**アンダーフロー**または**オーバーフロー**の状態になります。 計算の結果が 1 つの制限からもう 1 つの制限に折り返されているように見えます。 `Main` メソッドに次の 2 行を追加して、例を確認します。

```csharp
int what = max + 3;
Console.WriteLine($"An example of overflow: {what}");
```

計算の結果が最小値の (負の) 整数に極めて近いことに注目してください。 これは `min + 2` と同じです。
加算演算が許容された整数値を**オーバーフロー**しました。
整数がオーバーフローして最大値から最小値に ”折り返され” たため、計算結果が非常に大きな負の値になっています。

他にもさまざまな制限や有効桁数を持つ数値型があり、`int` 型がご自分のニーズと合わない場合は、そちらも使用できます。 次に、その他の型について説明します。

もう一度、このセクションで記述したコードを別のメソッドに移します。 これに `TestLimits` という名前を付けます。

## <a name="work-with-the-double-type"></a>double 型の処理

`double` 数値型は、倍精度浮動小数点数を表します。 こうした用語を初めて見た人もいるかもしれません。 **浮動小数点**数は、非常に大きな、または非常に小さな、整数ではない数値を表すのに役立ちます。 **倍精度**は、値の保管に使用される二進数の数値を表す相対語です。 **倍精度**数値は、**単精度**に比べ、二進数の数値が 2 倍になります。 最近のコンピューターでは、単精度よりも倍精度の数値を使用する方が一般的です。 **単精度**数値は、`float` キーワードを使用して宣言されます。
確認してみましょう。 次のコードを追加して結果を確認します。

```csharp
double a = 5;
double b = 4;
double c = 2;
double d = (a + b) / c;
Console.WriteLine(d);
```

計算結果に商の小数部分が含まれていることに注目してください。 double 型を使用して、もう少し複雑な式を試します。

```csharp
double e = 19;
double f = 23;
double g = 8;
double h = (e + f) / g;
Console.WriteLine(h);
```

double 値は整数値よりも範囲が大きくなります。 これまでに記述したコードの下で、次のコードを試します。

```csharp
double max = double.MaxValue;
double min = double.MinValue;
Console.WriteLine($"The range of double is {min} to {max}");
```

これらの値は指数表記で出力されます。 `E` の左側は有効数字です。 右側の数値は指数であり、10 の累乗です。

算術における 10 進数と同じように、C# における double には丸め誤差が発生することがあります。 次のコードを試してみましょう。

```csharp
double third = 1.0 / 3.0;
Console.WriteLine(third);
```

`0.3` の循環小数は `1/3` と完全に同じではありません。

***課題***

`double` 型を使用して、大きい値や小さい値、乗算、除算などの計算してみましょう。 もっと複雑な計算を試してみてください。

しばらく試してみたあとは、これまでに記述したコードを新しいメソッドに移します。 新しいメソッドに `WorkWithDoubles` という名前を付けます。

## <a name="work-with-decimal-types"></a>10 進型を扱う

C# の基本的な数値型である整数と double について見てきました。  もう 1 つ知っておくべき型として、`decimal` 型があります。 `decimal` 型は、`double` 型よりも範囲は小さいですが、有効桁数が大きい型です。 では、始めましょう。

```csharp
decimal min = decimal.MinValue;
decimal max = decimal.MaxValue;
Console.WriteLine($"The range of the decimal type is {min} to {max}");
```

`double` 型よりも範囲が小さいことに注目してください。 次のコードを実行すると、decimal 型では有効桁数がより大きいことを確認できます。

```csharp
double a = 1.0;
double b = 3.0;
Console.WriteLine(a / b);

decimal c = 1.0M;
decimal d = 3.0M;
Console.WriteLine(c / d);
```

数値の末尾の `M` は、定数では `decimal` 型を使用する必要があることを示しています。 それ以外の場合、コンパイラは `double` 型を想定します。

> [!NOTE]
> 文字 `M` は、`double` キーワードと `decimal` キーワードの間で最も視覚的に区別される文字として選択されています。

decimal 型を使用した演算では、小数点の右側の桁数がより多いことに注目してください。

***課題***

さまざまな数値型を確認したので、次は半径が 2.50 センチメートルの円の面積を計算するコードを記述してみます。 円の面積は、半径の 2 乗 x 円周率です。 ヒント: .NET には <xref:System.Math.PI?displayProperty=nameWithType> という円周率の定数があり、その値を使用できます。 <xref:System.Math.PI?displayProperty=nameWithType> は、`System.Math` 名前空間で宣言されているすべての定数と同様に、`double` 値です。 そのため、この課題では `decimal` 値の代わりに `double` を使用してください。

答えは 19 と 20 の間になるはずです。
[GitHub にある完成版のサンプル コード](https://github.com/dotnet/samples/tree/master/csharp/numbers-quickstart/Program.cs#L104-L106)で答えを確認できます。

お好みで他の数式を試してみてください。

これで "C# の数値" に関するクイックスタートは終了です。 続けて独自の開発環境で[分岐とループ](branches-and-loops-local.md)のクイックスタートに進むことができます。

C# の数値の詳細については、次の記事で学習できます。

- [整数数値型](../../language-reference/builtin-types/integral-numeric-types.md)
- [浮動小数点数値型](../../language-reference/builtin-types/floating-point-numeric-types.md)
- [組み込みの数値変換](../../language-reference/builtin-types/numeric-conversions.md)
