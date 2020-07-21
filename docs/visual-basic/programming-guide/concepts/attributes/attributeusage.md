---
title: AttributeUsage
ms.date: 07/20/2015
ms.assetid: 48757216-c21d-4051-86d5-8a3e03c39d2c
ms.openlocfilehash: 677d49aba38801f2adf42cc745983af30b3eddc5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84400733"
---
# <a name="attributeusage-visual-basic"></a>AttributeUsage (Visual Basic)

カスタム属性クラスの使用方法を決定します。 `AttributeUsage` は、カスタム属性の定義に適用して新しい属性の適用方法を制御できる属性です。 明示的に適用するときの既定の設定は次のようになります。

```vb
<System.AttributeUsage(System.AttributeTargets.All,
                   AllowMultiple:=False,
                   Inherited:=True)>
Class NewAttribute
    Inherits System.Attribute
End Class
```

この例では、属性にできる任意のコード エンティティに `NewAttribute` クラスを適用できますが、各エンティティに適用できるのは 1 回だけです。 基底クラスに適用すると、派生クラスによって継承されます。

`AllowMultiple` 引数と `Inherited` 引数は省略できるので、次のコードは同じ効果を持ちます。

```vb
<System.AttributeUsage(System.AttributeTargets.All)>
Class NewAttribute
    Inherits System.Attribute
End Class
```

最初の `AttributeUsage` 引数は、<xref:System.AttributeTargets> 列挙型の 1 つまたは複数の要素でなければなりません。 次のように、複数のターゲット型を OR 演算子で 1 つにまとめることができます。

```vb
<AttributeUsage(AttributeTargets.Property Or AttributeTargets.Field)>
Class NewPropertyOrFieldAttribute
    Inherits Attribute
End Class
```

`AllowMultiple` 引数を `true` に設定すると、次のように、結果の属性を 1 つのエンティティに複数回適用できます。

```vb
<AttributeUsage(AttributeTargets.Class, AllowMultiple:=True)>
Class MultiUseAttr
    Inherits Attribute
End Class

<MultiUseAttr(), MultiUseAttr()>
Class Class1
End Class
```

この例では、`AllowMultiple` が `true` に設定されているので、`MultiUseAttr` を繰り返し適用できます。 示されているどちらの形式でも、複数の属性を適用できます。

`Inherited` を `false` に設定すると、属性化されたクラスから派生するクラスは属性を継承しません。 次に例を示します。

```vb
<AttributeUsage(AttributeTargets.Class, Inherited:=False)>
Class Attr1
    Inherits Attribute
End Class

<Attr1()>
Class BClass

End Class

Class DClass
    Inherits BClass
End Class
```

この例では、`Attr1` は継承によって `DClass` に適用されません。

## <a name="remarks"></a>Remarks

`AttributeUsage` 属性は、1 回だけ使用できる属性です。同じクラスに複数回適用することはできません。 `AttributeUsage` は <xref:System.AttributeUsageAttribute> の別名です。

詳細については、「[リフレクションを使用した属性へのアクセス (Visual Basic)](accessing-attributes-by-using-reflection.md)」を参照してください。

## <a name="example"></a>例

次の例を見ると、`AttributeUsage` 属性に対する `Inherited` 引数と `AllowMultiple` 引数の効果、およびクラスに適用されているカスタム属性の列挙方法がわかります。

```vb
' Create some custom attributes:
<AttributeUsage(System.AttributeTargets.Class, Inherited:=False)>
Class A1
    Inherits System.Attribute
End Class

<AttributeUsage(System.AttributeTargets.Class)>
Class A2
    Inherits System.Attribute
End Class

<AttributeUsage(System.AttributeTargets.Class, AllowMultiple:=True)>
Class A3
    Inherits System.Attribute
End Class

' Apply custom attributes to classes:
<A1(), A2()>
Class BaseClass

End Class

<A3(), A3()>
Class DerivedClass
    Inherits BaseClass
End Class

Public Class TestAttributeUsage
    Sub Main()
        Dim b As New BaseClass
        Dim d As New DerivedClass
        ' Display custom attributes for each class.
        Console.WriteLine("Attributes on Base Class:")
        Dim attrs() As Object = b.GetType().GetCustomAttributes(True)

        For Each attr In attrs
            Console.WriteLine(attr)
        Next

        Console.WriteLine("Attributes on Derived Class:")
        attrs = d.GetType().GetCustomAttributes(True)
        For Each attr In attrs
            Console.WriteLine(attr)
        Next
    End Sub
End Class
```

## <a name="sample-output"></a>出力例

```console
Attributes on Base Class:
A1
A2
Attributes on Derived Class:
A3
A3
A2
```

## <a name="see-also"></a>関連項目

- <xref:System.Attribute>
- <xref:System.Reflection>
- [Visual Basic プログラミング ガイド](../../index.md)
- [属性](../../../../standard/attributes/index.md)
- [リフレクション (Visual Basic)](../reflection.md)
- [属性 (Visual Basic)](../../../language-reference/attributes.md)
- [カスタム属性の作成 (Visual Basic)](creating-custom-attributes.md)
- [リフレクションを使用した属性へのアクセス (Visual Basic)](accessing-attributes-by-using-reflection.md)
