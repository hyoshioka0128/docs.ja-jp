---
title: '方法: 2 つのオブジェクトが関連しているかどうかを決める'
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [Visual Basic], Visual Basic objects
- objects [Visual Basic], inheritance
- object variables [Visual Basic], determining relation
ms.assetid: da002e3f-6616-4bad-a229-f842d06652bb
ms.openlocfilehash: 30e88a21e737aa57513745899577381ed34151a2
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410465"
---
# <a name="how-to-determine-whether-two-objects-are-related-visual-basic"></a>方法: 2 つのオブジェクトが関連しているかどうかを判別する (Visual Basic)

2 つのオブジェクトを比較することで、それらの作成元であるクラス間のリレーションシップ (存在する場合) を特定することができます。 指定したクラスが現在のクラスを継承している場合、または現在の型が、指定したクラスでサポートされているインターフェイスである場合、<xref:System.Type?displayProperty=nameWithType> クラスの <xref:System.Type.IsInstanceOfType%2A> メソッドから `True` が返されます。

### <a name="to-determine-if-one-object-inherits-from-another-objects-class-or-interface"></a>あるオブジェクトが別のオブジェクトのクラスまたはインターフェイスを継承しているかどうかを判別するには

1. 基本データ型と考えられるオブジェクトで、<xref:System.Object.GetType%2A> メソッドを呼び出します。

2. <xref:System.Object.GetType%2A> から返された <xref:System.Type?displayProperty=nameWithType> オブジェクト上で、<xref:System.Type.IsInstanceOfType%2A> メソッドを呼び出します。

3. <xref:System.Type.IsInstanceOfType%2A> の引数リスト内で、派生型であると考えられるオブジェクトを指定します。

    その引数の型がオブジェクトの型 <xref:System.Type?displayProperty=nameWithType> を継承している場合は、<xref:System.Type.IsInstanceOfType%2A> から `True` が返されます。

## <a name="example"></a>例
 次の例では、あるオブジェクトが、別のオブジェクトのクラスから派生したクラスを表しているかどうかを判別します。

```vb
Public Class baseClass
End Class
Public Class derivedClass : Inherits baseClass
End Class
Public Class testTheseClasses
    Public Sub seeIfRelated()
        Dim baseObj As Object = New baseClass()
        Dim derivedObj As Object = New derivedClass()
        Dim related As Boolean
        related = baseObj.GetType().IsInstanceOfType(derivedObj)
        MsgBox(CStr(related))
    End Sub
End Class
```

<xref:System.Type.IsInstanceOfType%2A> への呼び出しで、2 つのオブジェクト変数が予期しない配置である点に注目してください。 想定される基本データ型を使用して <xref:System.Type?displayProperty=nameWithType> クラスを生成し、想定される派生型を引数として <xref:System.Type.IsInstanceOfType%2A> メソッドに渡します。

## <a name="see-also"></a>関連項目

- <xref:System.Object.GetType%2A>
- <xref:System.Type?displayProperty=nameWithType>
- <xref:System.Type.IsInstanceOfType%2A>
- [Object 型](../../../language-reference/data-types/object-data-type.md)
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の値](object-variable-values.md)
- [方法: 2 つのオブジェクトが同一であるかどうかを判別する](how-to-determine-whether-two-objects-are-identical.md)
