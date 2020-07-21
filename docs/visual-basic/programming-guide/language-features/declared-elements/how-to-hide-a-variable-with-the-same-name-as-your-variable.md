---
title: '方法: 自分で宣言した変数と同じ名前の変数を隠す'
ms.date: 07/20/2015
helpviewer_keywords:
- qualification [Visual Basic], of element names
- declarations [Visual Basic], elements
- element names [Visual Basic], qualification
- references [Visual Basic], declared elements
- declaration statements [Visual Basic], declared elements
- declaring elements [Visual Basic]
- referencing declared elements [Visual Basic]
- declared elements [Visual Basic], referencing
- declared elements [Visual Basic], about declared elements
ms.assetid: e39c0752-f19f-4d2e-a453-00df1b5fc7ee
ms.openlocfilehash: c1f4c2fbf339358be77e76468b1db94616bf04a2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357233"
---
# <a name="how-to-hide-a-variable-with-the-same-name-as-your-variable-visual-basic"></a>方法: 自分で宣言した変数と同じ名前の変数を隠す (Visual Basic)

変数を隠すには、それを*シャドウ*します。つまり、同じ名前の変数でそれを再定義します。 隠す変数は、次の 2 つの方法でシャドウできます。

- **スコープによるシャドウ。** スコープによってそれをシャドウするには、隠す変数が含まれている領域のサブ領域内でそれを再宣言します。

- **継承によるシャドウ。** 隠す変数がクラス レベルで定義されている場合は、派生クラスで [Shadows](../../../language-reference/modifiers/shadows.md) キーワードを使用してそれを再宣言することで、継承によってそれをシャドウできます。

## <a name="two-ways-to-hide-a-variable"></a>変数を隠す 2 つの方法

#### <a name="to-hide-a-variable-by-shadowing-it-through-scope"></a>変数をスコープによってシャドウして隠すには

1. 隠す変数を定義している領域を特定し、独自の変数でそれを再定義するサブ領域を決定します。

    |変数の領域|その再定義に使用できるサブ領域|
    |-----------------------|-------------------------------------------|
    |Module|モジュール内のクラス|
    |クラス|クラス内のサブクラス<br /><br /> クラス内のプロシージャ|

    そのプロシージャ内のブロック (`If`...`End If` コンストラクションや `For` ループなど) でプロシージャ変数を再定義することはできません。

2. サブ領域がまだ存在しない場合は作成します。

3. サブ領域内で、シャドウ変数を宣言する [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を記述します。

    サブ領域内のコードで変数名を参照すると、コンパイラによって、シャドウしている変数への参照が解決されます。

    次の例は、スコープによるシャドウに加えて、シャドウをバイパスする参照を示しています。

    ```vb
    Module shadowByScope
        ' The following statement declares num as a module-level variable.
        Public num As Integer
        Sub show()
            ' The following statement declares num as a local variable.
            Dim num As Integer
            ' The following statement sets the value of the local variable.
            num = 2
            ' The following statement displays the module-level variable.
            MsgBox(CStr(shadowByScope.num))
        End Sub
        Sub useModuleLevelNum()
            ' The following statement sets the value of the module-level variable.
            num = 1
            show()
        End Sub
    End Module
    ```

    前の例では、モジュール レベルとプロシージャ レベル (プロシージャ `show` 内) の両方で変数 `num` を宣言しています。 ローカル変数 `num` で、`show` 内のモジュールレベル変数 `num` をシャドウしているため、ローカル変数は 2 に設定されます。 ただし、`useModuleLevelNum` プロシージャの `num` をシャドウするローカル変数はありません。 そのため、`useModuleLevelNum` では、モジュールレベル変数の値が 1 に設定されます。

    `show` 内の `MsgBox` 呼び出しでは、モジュール名で `num` を修飾することによって、シャドウ メカニズムがバイパスされます。 そのため、ローカル変数ではなくモジュールレベルの変数が表示されます。

#### <a name="to-hide-a-variable-by-shadowing-it-through-inheritance"></a>変数を継承によってシャドウして隠すには

1. 隠す変数がクラス内かつクラス レベル (プロシージャの外部) で宣言されていることを確認してください。 それ以外の場合、継承によってそれをシャドウすることはできません。

2. 変数がまだ存在しない場合は、変数のクラスから派生したクラスを定義します。

3. 派生クラス内で、変数を宣言する `Dim` ステートメントを記述します。 宣言に [Shadows](../../../language-reference/modifiers/shadows.md) キーワードを含めます。

    派生クラスのコードで変数名を参照すると、コンパイラによって、変数への参照が解決されます。

    次の例に、継承によるシャドウを示しています。 それによって、2 つの参照が作成されます。シャドウする変数にアクセスするものと、シャドウ処理をバイパスするものです。

    ```vb
    Public Class shadowBaseClass
        Public shadowString As String = "This is the base class string."
    End Class
    Public Class shadowDerivedClass
        Inherits shadowBaseClass
        Public Shadows shadowString As String = "This is the derived class string."
        Public Sub showStrings()
            Dim s As String = "Unqualified shadowString: " & shadowString &
                 vbCrLf & "MyBase.shadowString: " & MyBase.shadowString
            MsgBox(s)
        End Sub
    End Class
    ```

    前の例では、基底クラスで `shadowString` 変数を宣言し、派生クラスでそれをシャドウしています。 派生クラスのプロシージャ `showStrings` では、名前 `shadowString` が修飾されていない場合に、文字列のシャドウしているバージョンが表示されます。 さらに、`shadowString` が `MyBase` キーワードで修飾されている場合は、シャドウされたバージョンが表示されます。

## <a name="robust-programming"></a>信頼性の高いプログラミング

シャドウによって、同じ名前の変数の複数のバージョンが取り込まれます。 コード ステートメントで変数名を参照する場合、コンパイラによる参照の解決先のバージョンは、コード ステートメントの場所や修飾文字列の存在などの要因によって異なります。 これにより、シャドウされた変数の意図しないバージョンを参照するリスクが高まる可能性があります。 シャドウされた変数へのすべての参照を完全に修飾することで、そのリスクを軽減することができます。

## <a name="see-also"></a>関連項目

- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic におけるシャドウ](shadowing.md)
- [シャドウとオーバーライドの違い](differences-between-shadowing-and-overriding.md)
- [方法: 継承された変数を隠す](how-to-hide-an-inherited-variable.md)
- [方法: 派生クラスによって非表示になっている変数にアクセスする](how-to-access-a-variable-hidden-by-a-derived-class.md)
- [Overrides](../../../language-reference/modifiers/overrides.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
- [継承の基本](../objects-and-classes/inheritance-basics.md)
