---
title: デリゲートとラムダ
description: 特定のメソッド シグネチャを指定する型をデリゲートで定義する方法について説明します。このようなメソッドは、直接呼び出すか、別のメソッドに渡して呼び出すことができます。
author: richlander
ms.author: wiwagn
ms.date: 06/20/2016
ms.technology: dotnet-standard
ms.assetid: fe2e4b4c-6483-4106-a4b4-a33e2e306591
ms.openlocfilehash: 184c9f61fd8456b22e8ecb262c131793160b49b0
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85244011"
---
# <a name="delegates-and-lambdas"></a>デリゲートとラムダ

デリゲートは、特定のメソッド シグネチャを指定する型を定義します。 このシグネチャを満たすメソッド (静的またはインスタンス) は、その型の変数に代入し、(適切な引数を使用して) 直接呼び出したり、別のメソッドに引数そのものとして渡してから呼び出すことができます。 次の例は、デリゲートの使い方を示しています。

```csharp
using System;
using System.Linq;

public class Program
{
    public delegate string Reverse(string s);

    static string ReverseString(string s)
    {
        return new string(s.Reverse().ToArray());
    }

    static void Main(string[] args)
    {
        Reverse rev = ReverseString;

        Console.WriteLine(rev("a string"));
    }
}
```

* `public delegate string Reverse(string s);` の行で特定のシグネチャのデリゲート型が作成されています。この場合、文字列パラメーターを取ってから文字列パラメーターを返すメソッドです。
* `static string ReverseString(string s)` メソッド (定義済みのデリゲート型とまったく同じシグネチャを持つ) では、デリゲートが実装されます。
* `Reverse rev = ReverseString;` 行では、対応するデリゲート型の変数にメソッドを割り当てることができることを示しています。
* `Console.WriteLine(rev("a string"));` 行では、デリゲート型の変数を使用してデリゲートを呼び出す方法を示しています。

開発プロセスを効率化するため、.NET にはプログラマが再利用できるデリゲート型のセットが含まれているため、新しい型を作成する必要はありません。 これらの型は `Func<>`、`Action<>` および `Predicate<>` であり、新しいデリゲート型を定義しなくても使用できます。 使用を意図した方法で実行する必要がある 3 つの型には、いくつかの違いがあります。

* `Action<>` は、デリゲートの引数を使用してアクションを実行する必要がある場合に使用されます。 カプセル化されるメソッドは、値を返しません。
* `Func<>` は、通常、変換が手元にあるときに使用されます。つまり、デリゲートの引数を異なる結果に変換する必要があります。 予測が良い例です。 カプセル化されるメソッドは、指定された値を返します。
* `Predicate<>` は、引数がデリゲートの条件を満たすかどうかを判断する必要がある場合に使用されます。 また、`Func<T, bool>` として書き込むこともできます。これは、メソッドがブール値を返すことを意味します。

ここで、上記の例を使用して、カスタム型の代わりに `Func<>` デリゲートを使用して書き換えることができます。 プログラムは引き続きまったく同じに実行されます。

```csharp
using System;
using System.Linq;

public class Program
{
    static string ReverseString(string s)
    {
        return new string(s.Reverse().ToArray());
    }

    static void Main(string[] args)
    {
        Func<string, string> rev = ReverseString;

        Console.WriteLine(rev("a string"));
    }
}
```

このシンプルな例では、`Main` メソッドの外部にメソッドを定義することは、少し余分なようです。 .NET Framework 2.0 では、*匿名デリゲート*の概念が導入されました。これにより、追加の型やメソッドを指定しなくても "インライン" デリゲートを作成できます。

次の例では、匿名デリゲートによってリストが偶数だけにフィルター処理され、コンソールに出力されます。

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main(string[] args)
    {
        List<int> list = new List<int>();

        for (int i = 1; i <= 100; i++)
        {
            list.Add(i);
        }

        List<int> result = list.FindAll(
          delegate (int no)
          {
              return (no % 2 == 0);
          }
        );

        foreach (var item in result)
        {
            Console.WriteLine(item);
        }
    }
}
```

ご覧のように、デリゲートの本体は、他のデリゲートと同じく、単なる式のセットです。 しかし、それを別の定義にする代わりに、<xref:System.Collections.Generic.List%601.FindAll%2A?displayProperty=nameWithType> メソッドへの呼び出しでそれを_アド ホック_で導入しました。

ただし、この方法でも、破棄できる多くのコードがまだ残ります。 このような場合に*ラムダ式*が機能します。 ラムダ式 (または略して単に "ラムダ") は、C# 3.0 で統合言語クエリ (LINQ) のコア ビルディング ブロックの 1 つとして導入されました。 これらは、デリゲートの使用の利便性を高める構文です。 これらは、シグネチャとメソッド本体を宣言しますが、デリゲートに割り当てられない限り、独自の正式な ID を持ちません。 デリゲートの場合とは異なり、これらをイベント登録の右側として、またはさまざまな LINQ 句およびメソッド内に、直接割り当てることができます。

ラムダ式はデリゲートを指定するもう 1 つの方法であるため、上記のサンプルを匿名デリゲートの代わりにラムダ式を使用するように書き換えることができるようになる必要があります。

```csharp
using System;
using System.Collections.Generic;

public class Program
{
    public static void Main(string[] args)
    {
        List<int> list = new List<int>();

        for (int i = 1; i <= 100; i++)
        {
            list.Add(i);
        }

        List<int> result = list.FindAll(i => i % 2 == 0);

        foreach (var item in result)
        {
            Console.WriteLine(item);
        }
    }
}
```

上の例で、使用されているラムダ式は `i => i % 2 == 0` です。 これも、デリゲートの使用の利便性を高める構文にすぎません。 内部で行われる処理は、匿名デリゲートの場合と似ています。

ここでも、ラムダは単なるデリゲートです。つまり、次のコード スニペットに示すように、ラムダは問題なくイベント ハンドラーとして使用することができます。

```csharp
public MainWindow()
{
    InitializeComponent();

    Loaded += (o, e) =>
    {
        this.Title = "Loaded";
    };
}
```

このコンテキストでの `+=` 演算子は、[イベント](../csharp/language-reference/keywords/event.md)をサブスクライブするために使用されます。 詳細については、「[イベントのサブスクリプションとサブスクリプション解除を行う方法](../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)」を参照してください。

## <a name="further-reading-and-resources"></a>参考資料とリソース

* [デリゲート](../csharp/programming-guide/delegates/index.md)
* [匿名関数](../csharp/programming-guide/statements-expressions-operators/anonymous-functions.md)
* [ラムダ式](../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md)
