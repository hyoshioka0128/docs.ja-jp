---
title: '方法: 拡張メソッドを作成する'
ms.date: 07/20/2015
helpviewer_keywords:
- extending data types [Visual Basic]
- writing extension methods [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: fb2739cc-958d-4ef4-a38b-214a74c93413
ms.openlocfilehash: 697508f86ff4ff0a89150b65782121395d0fed12
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74346013"
---
# <a name="how-to-write-an-extension-method-visual-basic"></a>方法: 拡張メソッドを作成する (Visual Basic)

拡張メソッドを使用すると、既存のクラスにメソッドを追加できます。 拡張メソッドは、そのクラスのインスタンスであるかのように呼び出すことができます。

### <a name="to-define-an-extension-method"></a>拡張メソッドを定義するには

1. Visual Studio で、新規または既存の Visual Basic アプリケーションを開きます。

2. 拡張メソッドを定義するファイルの先頭に、次のインポート ステートメントを含めます。

    ```vb
    Imports System.Runtime.CompilerServices
    ```

3. 新規または既存のアプリケーションのモジュール内で、メソッド定義を [`<Extension>`](xref:System.Runtime.CompilerServices.ExtensionAttribute) 属性で開始します。

    ```vb
    <Extension()>
    ```

    `Extension` 属性は、Visual Basic の [Module](../../../language-reference/statements/module-statement.md) 内のメソッド (`Sub` または `Function` プロシージャ) にのみ適用できます。 `Class` または `Structure` 内のメソッドに適用すると、Visual Basic コンパイラは、エラー [BC36551](../../../misc/bc36551.md) "Extension methods can be defined only in modules\(拡張メソッドはモジュール内でのみ定義できます\)" を生成します。

4. 通常の方法でメソッドを宣言します。ただし、最初のパラメーターの型は、拡張するデータ型である必要があります。

    ```vb
    <Extension()>
    Public Sub SubName(para1 As ExtendedType, <other parameters>)
         ' < Body of the method >
    End Sub
    ```

## <a name="example"></a>例

次の例では、モジュール `StringExtensions` で拡張メソッドを宣言しています。 2 番目のモジュール `Module1` は、`StringExtensions` をインポートし、このメソッドを呼び出します。 拡張メソッドは、呼び出されるときのスコープ内にある必要があります。 拡張メソッド `PrintAndPunctuate` は、文字列インスタンスを表示し、その後にパラメーターとして送信された句読記号の文字列を表示するメソッドで <xref:System.String> クラスを拡張します。

```vb
' Declarations will typically be in a separate module.
Imports System.Runtime.CompilerServices

Module StringExtensions
    <Extension()>
    Public Sub PrintAndPunctuate(aString As String, punc As String)
        Console.WriteLine(aString & punc)
    End Sub

End Module
```

```vb
' Import the module that holds the extension method you want to use,
' and call it.

Imports ConsoleApplication2.StringExtensions

Module Module1

    Sub Main()
        Dim example = "Hello"
        example.PrintAndPunctuate("?")
        example.PrintAndPunctuate("!!!!")
    End Sub

End Module
```

このメソッドは 2 つのパラメーターで定義され、その 1 つでのみ呼び出されることに注意してください。 メソッド定義の最初のパラメーターである `aString` は、メソッドを呼び出す `String` のインスタンスである `example` にバインドされています。 この例の出力は次のとおりです。

```console
Hello?
Hello!!!!
```

## <a name="see-also"></a>関連項目

- <xref:System.Runtime.CompilerServices.ExtensionAttribute>
- [拡張メソッド](extension-methods.md)
- [Module ステートメント](../../../language-reference/statements/module-statement.md)
- [プロシージャのパラメーターと引数](procedure-parameters-and-arguments.md)
- [Visual Basic におけるスコープ](../declared-elements/scope.md)
