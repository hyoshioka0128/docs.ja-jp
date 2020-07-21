---
title: '方法: 継承された変数を隠す'
ms.date: 07/20/2015
helpviewer_keywords:
- qualification [Visual Basic], of element names
- element names [Visual Basic], qualification
- references [Visual Basic], declared elements
- declaration statements [Visual Basic], declared elements
- referencing declared elements [Visual Basic]
- declared elements [Visual Basic], referencing
- declared elements [Visual Basic], about declared elements
- variables [Visual Basic], hiding inherited
ms.assetid: 765728d9-7351-4a30-999d-b5f34f024412
ms.openlocfilehash: f49bba0497f9f4f2774b01284c815bba9aaed119
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84357271"
---
# <a name="how-to-hide-an-inherited-variable-visual-basic"></a>方法: 継承された変数を非表示にする (Visual Basic)

派生クラスは、その基底クラスのすべての定義を継承します。 基底クラスの要素と同じ名前を使用して変数を定義する場合は、派生クラスで変数を定義するときに、その基底クラスの要素を非表示にする (*シャドウ*する) ことができます。 これを行うと、シャドウのメカニズムを明示的にバイパスしない限り、派生クラスのコードは変数にアクセスします。

継承された変数を非表示にするもう 1 つの理由は、基底クラスの改訂から保護するためです。 基底クラスには、継承している要素を変える変更が加えられる場合があります。 この場合、`Shadows` 修飾子は、派生クラスからの参照が、基底クラス要素ではなく変数に強制的に解決されるようにします。

## <a name="to-hide-an-inherited-variable"></a>継承された変数を非表示にするには

1. 非表示にする変数がクラス レベル (プロシージャの外側) で宣言されていることを確認してください。 そうでない場合、非表示にする必要はありません。
  
2. 派生クラス内に、変数を宣言する [Dim ステートメント](../../../language-reference/statements/dim-statement.md)を記述します。 継承された変数と同じ名前を使用します。

3. 宣言に [Shadows](../../../language-reference/modifiers/shadows.md) キーワードを含めます。

     派生クラスのコードで変数名を参照すると、コンパイラによって、変数への参照が解決されます。

     次の例は、継承された変数のシャドウ処理を示しています。
  
    ```vb  
    Public Class ShadowBaseClass  
        Public shadowString As String = "This is the base class string."  
    End Class  
    Public Class ShadowDerivedClass  
        Inherits ShadowBaseClass  
        Public Shadows shadowString As String = "This is the derived class string."  
        Public Sub ShowStrings()  
            Dim s As String = $"Unqualified shadowString: {shadowString}{vbCrLf}MyBase.shadowString: {MyBase.shadowString}"
            MsgBox(s)  
        End Sub  
    End Class  
    ```  
  
     前の例では、基底クラスで `shadowString` 変数を宣言し、派生クラスでそれをシャドウしています。 派生クラスのプロシージャ `ShowStrings` では、名前 `shadowString` が修飾されていない場合に、文字列のシャドウしているバージョンが表示されます。 さらに、`shadowString` が `MyBase` キーワードで修飾されている場合は、シャドウされたバージョンが表示されます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング

シャドウによって、同じ名前の変数の複数のバージョンが取り込まれます。 コード ステートメントで変数名を参照する場合、コンパイラによる参照の解決先のバージョンは、コード ステートメントの場所や修飾文字列の存在などの要因によって異なります。 これにより、シャドウされた変数の意図しないバージョンを参照するリスクが高まる可能性があります。 シャドウされた変数へのすべての参照を完全に修飾することで、そのリスクを軽減することができます。

## <a name="see-also"></a>関連項目

- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic におけるシャドウ](shadowing.md)
- [シャドウとオーバーライドの違い](differences-between-shadowing-and-overriding.md)
- [方法: 自分で宣言した変数と同じ名前の変数を非表示にする](how-to-hide-a-variable-with-the-same-name-as-your-variable.md)
- [方法: 派生クラスによって非表示になっている変数にアクセスする](how-to-access-a-variable-hidden-by-a-derived-class.md)
- [Overrides](../../../language-reference/modifiers/overrides.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
- [継承の基本](../objects-and-classes/inheritance-basics.md)
