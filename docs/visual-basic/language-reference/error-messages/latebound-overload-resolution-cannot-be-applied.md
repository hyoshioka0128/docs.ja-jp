---
title: アクセスするインスタンスがインターフェイス型であるため、遅延バインドされたオーバーロードの解決は '<procedurename>' に適用されません。
ms.date: 07/20/2015
f1_keywords:
- vbc30933
- bc30933
helpviewer_keywords:
- overload resolution [Visual Basic], with late-bound argument
- BC30933
ms.assetid: 8182eea0-dd34-4d6e-9ca0-41d8713e9dc4
ms.openlocfilehash: 4500a177c7a4729fe5131af1b007fd38e77afe07
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397338"
---
# <a name="latebound-overload-resolution-cannot-be-applied-to-procedurename-because-the-accessing-instance-is-an-interface-type"></a>アクセスするインスタンスがインターフェイス型であるため、遅延バインドされたオーバーロードの解決は '\<procedurename>' に適用されません。

コンパイラでは、オーバーロードされたプロパティまたはプロシージャへの参照を解決しようとしますが、引数の型が `Object` であり、参照元のオブジェクトがインターフェイスのデータ型を持つため、参照が失敗します。 `Object` 引数は、コンパイラに参照を遅延バインドとして強制的に解決させます。

このような状況では、コンパイラは、基になるインターフェイスを使用するのではなく、実装するクラスを使用してオーバーロードを解決します。 クラスで、オーバーロードされたいずれかのバージョンの名前が変更された場合、コンパイラは、そのバージョンの名前が異なるため、それをオーバーロードされているものと見なしません。 これにより、名前が変更されたバージョンが参照を解決するための正しい選択である可能性がある場合に、コンパイラがそれを無視します。

**エラー ID:** BC30933

## <a name="to-correct-this-error"></a>このエラーを解決するには

- `CType` を使用して、`Object` からの引数を、呼び出すオーバーロードのシグネチャで指定された型にキャストします。

  参照元のオブジェクトを、基になるインターフェイスにキャストすることは役に立ちません。 このエラーを回避するには、引数をキャストする必要があります。

## <a name="example"></a>例

次の例では、コンパイル時にこのエラーを発生させるオーバーロードされた `Sub` プロシージャの呼び出しを示しています。

```vb
Module m1
    Interface i1
        Sub s1(ByVal p1 As Integer)
        Sub s1(ByVal p1 As Double)
    End Interface
    Class c1
        Implements i1
        Public Overloads Sub s1(ByVal p1 As Integer) Implements i1.s1
        End Sub
        Public Overloads Sub s2(ByVal p1 As Double) Implements i1.s1
        End Sub
    End Class
    Sub Main()
        Dim refer As i1 = New c1
        Dim o1 As Object = 3.1415
        ' The following reference is INVALID and causes a compiler error.
        refer.s1(o1)
    End Sub
End Module
```

前の例で、コンパイラが記述どおりに `s1` の呼び出しを許可した場合、インターフェイス `i1` ではなく `c1` クラスを使用して解決が行われます。 これは、`i1` によって定義されているとおりに、正しい選択であっても、`c1` でその名前が異なるため、コンパイラが `s2` を考慮しないことを意味します。

このエラーを修正するには、呼び出しを次のいずれかのコード行に変更します。

```vb
refer.s1(CType(o1, Integer))
refer.s1(CType(o1, Double))
```

前の各コード行では、`Object` 変数 `o1` をオーバーロードに定義されているいずれかのパラメーター型に明示的にキャストしています。

## <a name="see-also"></a>関連項目

- [プロシージャのオーバーロード](../../programming-guide/language-features/procedures/procedure-overloading.md)
- [オーバーロードの解決](../../programming-guide/language-features/procedures/overload-resolution.md)
- [CType 関数](../functions/ctype-function.md)
