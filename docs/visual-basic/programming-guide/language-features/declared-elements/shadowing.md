---
title: シャドウ
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [Visual Basic], shadowing
- overriding, and shadowing
- shadowing
- duplicate names [Visual Basic]
- shadowing, by inheritance
- declared elements [Visual Basic], referencing
- shadowing, by scope
- declared elements [Visual Basic], hiding
- naming conflicts, shadowing
- declared elements [Visual Basic], shadowing
- shadowing, and overriding
- scope [Visual Basic], shadowing
- Shadows keyword [Visual Basic], about
- objects [Visual Basic], names
- names [Visual Basic], shadowing
ms.assetid: 54bb4c25-12c4-4181-b4a0-93546053964e
ms.openlocfilehash: 7d76e2e7398c2f954ff4274f77ffa350efbd3617
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410748"
---
# <a name="shadowing-in-visual-basic"></a>Visual Basic におけるシャドウ
2 つのプログラミング要素が同じ名前を共有している場合、それらのうちの 1 つで他方を非表示にしたり、*シャドウ*したりすることができます。 このような状況では、シャドウされた要素を参照することはできません。代わりに、コードで要素名を使用すると、Visual Basic コンパイラによって、それがシャドウする要素に解決されます。  
  
## <a name="purpose"></a>目的  
 シャドウの主な目的は、クラス メンバーの定義を保護することです。 基底クラスには、既に定義されているものと同じ名前の要素を作成する変更が含まれる場合があります。 この場合、`Shadows` 修飾子は、クラスによる参照が、新しい基底クラス要素ではなく定義したメンバーに強制的に解決されるようにします。  
  
## <a name="types-of-shadowing"></a>シャドウの種類  
 要素では、2 つの異なる方法で別の要素をシャドウできます。 シャドウする要素は、シャドウされる要素を含む領域のサブ領域内で宣言できます。この場合、シャドウは*スコープによって*実現されます。 または、派生クラスで、基底クラスのメンバーを再定義できます。この場合、シャドウは*継承によって*行われます。  
  
### <a name="shadowing-through-scope"></a>スコープによるシャドウ  
 同じモジュール、クラス、または構造体内のプログラミング要素で、同じ名前で、異なるスコープを持つことができます。 2 つの要素がこのように宣言されていて、コードでそれらが共有する名前を参照する場合、スコープが狭い方の要素によって、他方の要素がシャドウされます (ブロック スコープが最も狭い)。  
  
 たとえば、モジュールで `temp` という名前の `Public` 変数を定義でき、モジュール内のプロシージャでも、`temp` という名前のローカル変数を宣言できます。 プロシージャ内から `temp` への参照ではローカル変数にアクセスしますが、プロシージャの外部から `temp` への参照では `Public` 変数にアクセスします。 この場合、プロシージャ変数 `temp` によって、モジュール変数 `temp` がシャドウされます。  
  
 次の図は、どちらも `temp` という名前の 2 つの変数を示します。 ローカル変数 `temp` は、それ自身のプロシージャ `p` 内からアクセスされるときに、メンバー変数 `temp` をシャドウします。 ただし、`MyClass` キーワードによって、シャドウをバイパスし、メンバー変数にアクセスできます。  
  
 ![スコープによるシャドウを示すグラフィック。](./media/shadowing/shadow-scope-diagram.gif)
  
 スコープによるシャドウの例については、「[方法:自分で宣言した変数と同じ名前の変数を隠す](how-to-hide-a-variable-with-the-same-name-as-your-variable.md)」を参照してください。  
  
### <a name="shadowing-through-inheritance"></a>継承によるシャドウ  
 派生クラスで、基底クラスから継承されたプログラミング要素を再定義する場合、再定義する要素によって、元の要素がシャドウされます。 任意の型の宣言された要素、またはオーバーロードされた要素のセットを、他の型でシャドウできます。 たとえば、`Integer` 変数によって、`Function` プロシージャをシャドウできます。 別のプロシージャでプロシージャをシャドウする場合、別のパラメーター リストと別の戻り値の型を使用できます。  
  
 次の図は、基底クラス `b` と、`b` から継承する派生クラス `d` を示しています。 基底クラスで `proc` という名前のプロシージャを定義しており、派生クラスでは、同じ名前の別のプロシージャでそれをシャドウします。 最初の `Call` ステートメントで、派生クラスのシャドウする `proc` にアクセスしています。 ただし、`MyBase` キーワードによって、シャドウをバイパスし、基底クラスのシャドウされたプロシージャにアクセスしています。  
  
 ![継承によるシャドウのグラフィック ダイアグラム](./media/shadowing/shadowing-inherit-diagram.gif)  
  
 継承によるシャドウの例については、「[方法:自分で宣言した変数と同じ名前の変数を隠す](how-to-hide-a-variable-with-the-same-name-as-your-variable.md)」と「[方法:継承された変数を隠す](how-to-hide-an-inherited-variable.md)」を参照してください。  
  
#### <a name="shadowing-and-access-level"></a>シャドウとアクセス レベル  
 シャドウする要素には、常に派生クラスを使用して、コードからアクセスできるとは限りません。 たとえば、それが `Private` として宣言されているとします。 そのような場合、シャドウが無効化され、コンパイラによって、同じ要素への参照が、シャドウがなかった場合のように解決されます。 この要素は、シャドウするクラスからさかのぼって最も少ない派生ステップでアクセス可能な要素です。 シャドウされた要素がプロシージャの場合は、同じ名前、パラメーター リスト、および戻り値の型を持つ、最も近いアクセス可能なバージョンに解決されます。  
  
 次の例に、3 つのクラスの継承階層を示します。 各クラスで `Sub` プロシージャ`display` を定義し、各派生クラスで、その基底クラスの `display` プロシージャをシャドウしています。  
  
```vb  
Public Class firstClass  
    Public Sub display()  
        MsgBox("This is firstClass")  
    End Sub  
End Class  
Public Class secondClass  
    Inherits firstClass  
    Private Shadows Sub display()  
        MsgBox("This is secondClass")  
    End Sub  
End Class  
Public Class thirdClass  
    Inherits secondClass  
    Public Shadows Sub display()  
        MsgBox("This is thirdClass")  
    End Sub  
End Class  
Module callDisplay  
    Dim first As New firstClass  
    Dim second As New secondClass  
    Dim third As New thirdClass  
    Public Sub callDisplayProcedures()  
        ' The following statement displays "This is firstClass".  
        first.display()  
        ' The following statement displays "This is firstClass".  
        second.display()  
        ' The following statement displays "This is thirdClass".  
        third.display()  
    End Sub  
End Module  
```  
  
 前の例では、派生クラス `secondClass` で、`Private` プロシージャによって `display` をシャドウしています。 モジュール `callDisplay` で `secondClass` の `display` が呼び出されたときに、呼び出し元のコードは `secondClass` の外部にあるため、プライベートの `display` プロシージャにアクセスできません。 シャドウが無効化され、コンパイラによって、参照が基底クラスの `display` プロシージャに解決されます。  
  
 ただし、さらに派生したクラス `thirdClass` では `display` を `Public` として宣言しているため、`callDisplay` のコードからアクセスできます。  
  
## <a name="shadowing-and-overriding"></a>シャドウとオーバーライド  
 シャドウとオーバーライドを混同しないでください。 どちらも派生クラスが基底クラスから継承されるときに使用し、どちらも一方の宣言された要素を他方の要素で再定義します。 しかし、この 2 つには、大きな違いがあります。 比較については、「[シャドウとオーバーライドの違い](differences-between-shadowing-and-overriding.md)」を参照してください。  
  
## <a name="shadowing-and-overloading"></a>シャドウとオーバーロード  
 派生クラス内で、複数の要素で同じ基底クラス要素をシャドウする場合、シャドウする要素は、その要素のオーバーロードされたバージョンになります。 詳細については、「 [Procedure Overloading](../procedures/procedure-overloading.md)」を参照してください。  
  
## <a name="accessing-a-shadowed-element"></a>シャドウされた要素へのアクセス  
 派生クラスから要素にアクセスする場合、通常、その派生クラスの現在のインスタンスから行いますが、要素名を `Me` キーワードで修飾します。 派生クラスで基底クラスの要素をシャドウする場合は、`MyBase` キーワードで修飾することで、基底クラスの要素にアクセスできます。  
  
 シャドウされた要素にアクセスする例については、「[方法:派生クラスによって非表示になっている変数にアクセスする](how-to-access-a-variable-hidden-by-a-derived-class.md)」を参照してください。  
  
### <a name="declaration-of-the-object-variable"></a>オブジェクト変数の宣言  
 オブジェクト変数を作成する方法は、派生クラスがシャドウする要素またはシャドウされた要素にアクセスするかどうかにも影響する場合があります。 次の例では、派生クラスから 2 つのオブジェクトを作成していますが、一方のオブジェクトは基底クラスとして、他方を派生クラスとして宣言しています。  
  
```vb  
Public Class baseCls  
    ' The following statement declares the element that is to be shadowed.  
    Public z As Integer = 100  
End Class  
Public Class dervCls  
    Inherits baseCls  
    ' The following statement declares the shadowing element.  
    Public Shadows z As String = "*"  
End Class  
Public Class useClasses  
    ' The following statement creates the object declared as the base class.  
    Dim basObj As baseCls = New dervCls()  
    ' Note that dervCls widens to its base class baseCls.  
    ' The following statement creates the object declared as the derived class.  
    Dim derObj As dervCls = New dervCls()  
    Public Sub showZ()
    ' The following statement outputs 100 (the shadowed element).  
        MsgBox("Accessed through base class: " & basObj.z)  
    ' The following statement outputs "*" (the shadowing element).  
        MsgBox("Accessed through derived class: " & derObj.z)  
    End Sub  
End Class  
```  
  
 前の例では、変数 `basObj` が基底クラスとして宣言されています。 `dervCls` オブジェクトをそれに割り当てることは、拡大変換になるため、有効です。 ただし、基底クラスでは派生クラス内の変数 `z` のシャドウするバージョンにアクセスできないため、コンパイラによって `basObj.z` が元の基底クラスの値に解決されます。  
  
## <a name="see-also"></a>関連項目

- [宣言された要素の参照](references-to-declared-elements.md)
- [Visual Basic におけるスコープ](scope.md)
- [拡大変換と縮小変換](../data-types/widening-and-narrowing-conversions.md)
- [Shadows](../../../language-reference/modifiers/shadows.md)
- [Overrides](../../../language-reference/modifiers/overrides.md)
- [Me、My、MyBase、および MyClass](../../program-structure/me-my-mybase-and-myclass.md)
- [継承の基本](../objects-and-classes/inheritance-basics.md)
