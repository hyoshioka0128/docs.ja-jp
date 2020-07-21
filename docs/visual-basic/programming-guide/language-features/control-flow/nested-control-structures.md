---
title: 入れ子になった制御構造
ms.date: 07/20/2015
helpviewer_keywords:
- Visual Basic code, control flow
- control structures [Visual Basic], nested
- conditional statements [Visual Basic], nested
- statements [Visual Basic], control flow
- control flow [Visual Basic], nested control statements
- structures [Visual Basic], nested control
- nested control statements [Visual Basic]
ms.assetid: cf60b061-65d9-44a8-81f2-b0bdccd23a05
ms.openlocfilehash: 539ad639320615c1e53176fe47e5468864aa21d8
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84414390"
---
# <a name="nested-control-structures-visual-basic"></a>入れ子になった制御構造 (Visual Basic)
`For...Next` ループ内の `If...Then...Else` ブロックなど、制御ステートメントを他の制御ステートメントに配置することができます。 別の制御ステートメントに配置された制御ステートメントは、"*入れ子にされた*" ステートメントと呼ばれます。  
  
## <a name="nesting-levels"></a>入れ子のレベル  
 Visual Basic の制御構造は、必要な数のレベルで入れ子にできます。 一般的には、入れ子構造を読みやすくするには、各本体をインデントします。 統合開発環境 (IDE) エディターでは、これが自動的に行われます。  
  
 次の例では、プロシージャ `sumRows` は、マトリックスの各行の正の要素をすべて加算します。  
  
```vb
Public Sub sumRows(ByVal a(,) As Double, ByRef r() As Double)  
    Dim i, j As Integer  
    For i = 0 To UBound(a, 1)  
        r(i) = 0  
        For j = 0 To UBound(a, 2)  
            If a(i, j) > 0 Then  
                r(i) = r(i) + a(i, j)  
            End If  
        Next j  
    Next i  
End Sub  
```  
  
 前の例では、最初の `Next` ステートメントが内側の `For` ループを閉じ、最後の `Next` ステートメントが外側の `For` ループを閉じます。  
  
 同様に、入れ子にされた `If` ステートメントでは、`End If` ステートメントは、最も近い前の `If` ステートメントに自動的に適用されます。 入れ子にされた `Do` ループも同じように機能し、最も内側の `Loop` ステートメントと最も内側の `Do` ステートメントが一致します。  
  
> [!NOTE]
> 多くの制御構造で、キーワードの 1 つをクリックすると、構造内のすべてのキーワードが強調表示されます。 たとえば、`If...Then...Else` コンストラクションで `If` をクリックすると、コンストラクション内の `If`、`Then`、`ElseIf`、`Else`、および `End If` のすべてのインスタンスが強調表示されます。 次または前の強調表示されたキーワードに移動するには、Ctrl + Shift + ↓キーを押すか、Ctrl + Shift + ↑キーを押します。  
  
## <a name="nesting-different-kinds-of-control-structures"></a>入れ子にされたさまざまな種類の制御構造  
 ある種類の制御構造を、別の種類の制御構造の中で入れ子にできます。 次の例は、`For Each` ループ内の `With` ブロックと、`With` ブロック内の入れ子にされた `If` ブロックを使用しています。  
  
```vb
For Each ctl As System.Windows.Forms.Control In Me.Controls  
    With ctl  
        .BackColor = System.Drawing.Color.Yellow  
        .ForeColor = System.Drawing.Color.Black  
        If .CanFocus Then  
            .Text = "Colors changed"  
            If Not .Focus() Then  
                ' Insert code to process failed focus.  
            End If  
        End If  
    End With  
Next ctl  
```  
  
## <a name="overlapping-control-structures"></a>制御構造のオーバーラップ  
 制御構造をオーバーラップさせることはできません。 つまり、入れ子構造は、次の最も内側にある構造に完全に含まれている必要があります。 たとえば、次の配置は、内側の `With` ブロックが終了する前に `For` ループが終了するため無効です。  
  
 ![無効な入れ子の例を示す図。](./media/nested-control-structures/example-invalid-nesting.gif)
  
 Visual Basic コンパイラは、このような制御構造の重なりを検出し、コンパイル時にエラーが発生したことを通知します。  
  
## <a name="see-also"></a>関連項目

- [制御フロー](index.md)
- [条件判断構造](decision-structures.md)
- [ループ構造](loop-structures.md)
- [その他の制御構造](other-control-structures.md)
