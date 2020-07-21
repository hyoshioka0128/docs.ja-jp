---
title: '方法: 拡張メソッドを呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- calling extension methods [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: df07750f-40f4-4c07-a79e-1113a27cfbea
ms.openlocfilehash: 54419c99ae08c9ca2e3cfa86993dc99bc02bbb64
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84388661"
---
# <a name="how-to-call-an-extension-method-visual-basic"></a>方法: 拡張メソッドを呼び出す (Visual Basic)

拡張メソッドを使用すると、既存のクラスにメソッドを追加できます。 拡張メソッドが宣言され、スコープ内に入ると、拡張される型のインスタンス メソッドと同様に呼び出すことができるようになります。 拡張メソッドを記述する方法の詳細については、「[方法: 拡張メソッドを作成する](./how-to-write-an-extension-method.md)」を参照してください。

 次の手順では、拡張メソッド `PrintAndPunctuate` を参照しています。これにより、それを呼び出す文字列インスタンスが表示されてから、2 番目のパラメーター `punc` に送信される値が表示されます。

```vb
Imports System.Runtime.CompilerServices

Module StringExtensions
    <Extension()>
    Public Sub PrintAndPunctuate(ByVal aString As String,
                                 ByVal punc As String)
        Console.WriteLine(aString & punc)
    End Sub

End Module
```

メソッドは、呼び出されるときにスコープ内にある必要があります。

### <a name="to-call-an-extension-method"></a>拡張メソッドを呼び出すには

1. 拡張メソッドの最初のパラメーターのデータ型を持つ変数を宣言します。 `PrintAndPunctuate` の場合、<xref:System.String> 変数が必要です。

    ```vb
    Dim example = "Ready"
    ```

2. この変数によって拡張メソッドが呼び出され、その値は 1 つ目のパラメーター `aString` にバインドされます。 次の呼び出し元ステートメントによって `Ready?` が表示されます。

    ```vb
    example.PrintAndPunctuate("?")
    ```

     この拡張メソッドに対する呼び出しは、1 つのパラメーターを必要とする <xref:System.String> インスタンス メソッドのいずれかに対する呼び出しと同じように見えることに注意してください。

    ```vb
    example.EndsWith("dy")
    example.IndexOf("R")
    ```

3. 別の文字列変数を宣言し、メソッドを再度呼び出して、任意の文字列で機能することを確認します。

    ```vb
    Dim example2 = " or not"
    example2.PrintAndPunctuate("!!!")
    ```

     今回の結果は `or not!!!` になります。

## <a name="example"></a>例
 次のコードは、単純な拡張メソッドの作成と使用の完全な例です。

```vb
Imports System.Runtime.CompilerServices
Imports ConsoleApplication1.StringExtensions

Module Module1

    Sub Main()

        Dim example = "Hello"
        example.PrintAndPunctuate(".")
        example.PrintAndPunctuate("!!!!")

        Dim example2 = "Goodbye"
        example2.PrintAndPunctuate("?")
    End Sub

    <Extension()>
    Public Sub PrintAndPunctuate(ByVal aString As String,
                                 ByVal punc As String)
        Console.WriteLine(aString & punc)
    End Sub
End Module

' Output:
' Hello.
' Hello!!!!
' Goodbye?
```

## <a name="see-also"></a>関連項目

- [方法: 拡張メソッドを作成する](./how-to-write-an-extension-method.md)
- [拡張メソッド](./extension-methods.md)
- [Visual Basic におけるスコープ](../declared-elements/scope.md)
