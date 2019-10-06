---
title: 型のプロパティは別のプロパティを初期化するために使用されるため、匿名型を式のツリーに変換することはできません。
ms.date: 07/20/2015
f1_keywords:
- bc36548
- vbc36548
helpviewer_keywords:
- BC36548
ms.assetid: 27de068f-080e-4160-86bf-1ec23fd1925a
ms.openlocfilehash: ba14c0cd8781b8771ac8b746e3efec29a457294a
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701188"
---
# <a name="cannot-convert-anonymous-type-to-expression-tree-because-it-contains-a-field-that-is-used-in-the-initialization-of-another-field"></a>型のプロパティは別のプロパティを初期化するために使用されるため、匿名型を式のツリーに変換することはできません。
匿名型の1つのプロパティを使用して匿名型の別のプロパティを初期化する場合、コンパイラは匿名型から式ツリーへの変換を受け入れません。 たとえば、次のコードでは、`Prop1` は初期化リストで宣言され、`Prop2` の初期値として使用されます。  
  
```vb  
Module M2  
  
    Sub ExpressionExample(Of T)(ByVal x As Expressions.Expression(Of Func(Of T)))  
    End Sub  
  
    Sub Main()  
        ' The following line causes the error.  
        ' ExpressionExample(Function() New With {.Prop1 = 2, .Prop2 = .Prop1})  
  
    End Sub  
End Module  
```  
  
 **エラー ID:** BC36548  
  
## <a name="to-correct-this-error"></a>このエラーを解決するには  
  
- @No__t-0 の初期値をローカル変数に代入します。 次のコードに示すように、その変数を `Prop1` と `Prop2` の両方に割り当てます。  
  
    ```vb  
    Sub Main()  
  
        Dim temp = 2  
        ExpressionExample(Function() New With {.Prop1 = temp, .Prop2 = temp})  
  
    End Sub  
    ```  
  
## <a name="see-also"></a>関連項目

- [匿名型 (Visual Basic)](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [式ツリー (Visual Basic)](../../programming-guide/concepts/expression-trees/index.md)
- [2 つのオブジェクトが等しいかどうかをテストする方法式ツリーを使用して動的クエリを作成する (Visual Basic) ](../../programming-guide/concepts/expression-trees/how-to-use-expression-trees-to-build-dynamic-queries.md)
