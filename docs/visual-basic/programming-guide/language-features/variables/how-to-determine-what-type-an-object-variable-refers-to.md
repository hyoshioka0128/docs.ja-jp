---
title: '方法: オブジェクト変数で参照している型を確認する'
ms.date: 07/20/2015
helpviewer_keywords:
- TypeOf operator [Visual Basic], determining object variable type
- variables [Visual Basic], object
- object variables [Visual Basic], determining type
ms.assetid: 6f6a138d-58a4-40d1-9f4e-0a3c598eaf81
ms.openlocfilehash: d3224000f5958a8619e38c4d2f6dc5dbb275ad45
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410491"
---
# <a name="how-to-determine-what-type-an-object-variable-refers-to-visual-basic"></a>方法: オブジェクト変数で参照している型を確認する (Visual Basic)

オブジェクト変数には、他の場所に格納されているデータへのポインターが含まれています。 データの種類は、実行時に変更可能です。 いつでも、<xref:System.Type.GetTypeCode%2A> メソッドを使用して現在の実行時型を確認できます。[TypeOf 演算子](../../../language-reference/operators/typeof-operator.md) を使用して、現在の実行時型が、指定した型と互換性があるかどうかを調べることもできます。

### <a name="to-determine-the-exact-type-an-object-variable-currently-refers-to"></a>オブジェクト変数で現在参照している正確な型を確認するには

1. オブジェクト変数で、<xref:System.Object.GetType%2A> メソッドを呼び出して、<xref:System.Type?displayProperty=nameWithType> オブジェクトを取得します。

    ```vb
    Dim myObject As Object
    myObject.GetType()
    ```

2. <xref:System.Type?displayProperty=nameWithType> クラスで、共有メソッド <xref:System.Type.GetTypeCode%2A> を呼び出して、オブジェクトの型の <xref:System.TypeCode> 列挙値を取得します。

    ```vb
    Dim myObject As Object
    Dim datTyp As Integer = Type.GetTypeCode(myObject.GetType())
    MsgBox("myObject currently has type code " & CStr(datTyp))
    ```

    <xref:System.TypeCode> 列挙値は、`Double` など、目的の列挙メンバーに対してテストできます。

### <a name="to-determine-whether-an-object-variables-type-is-compatible-with-a-specified-type"></a>オブジェクト変数の型が、指定した型と互換性があるかどうかを判断するには

- `TypeOf` 演算子を [Is 演算子](../../../language-reference/operators/is-operator.md)と組み合わせて使用して、`TypeOf`...`Is` 式でオブジェクトをテストします。

    ```vb
    If TypeOf objA Is System.Windows.Forms.Control Then
        MsgBox("objA is compatible with the Control class")
    End If
    ```

    `TypeOf`...`Is` 式では、オブジェクトの実行時型が、指定した型と互換性がある場合に `True` が返されます。

    互換性の基準は、指定した型がクラス、構造体、またはインターフェイスのいずれであるかによって異なります。 一般に、オブジェクトが、指定した型と同じ型である、指定した型を継承する、または実装する場合、その型は互換性があります。 詳細については、「[TypeOf 演算子](../../../language-reference/operators/typeof-operator.md)」を参照してください。

## <a name="compile-the-code"></a>コードのコンパイル

指定する型を変数または式にすることはできません。 クラス、構造体、インターフェイスなど、定義済みの型の名前である必要があります。 これには、`Integer` や `String` などの組み込み型が含まれます。

## <a name="see-also"></a>関連項目

- <xref:System.Object.GetType%2A>
- <xref:System.Type?displayProperty=nameWithType>
- <xref:System.Type.GetTypeCode%2A>
- <xref:System.TypeCode>
- [オブジェクト変数](object-variables.md)
- [オブジェクト変数の値](object-variable-values.md)
- [Object 型](../../../language-reference/data-types/object-data-type.md)
