---
title: Visual Basic の NameOf 演算子
description: Visual Basic での参照演算子の使用方法について説明します。
ms.date: 10/27/2019
helpviewer_keywords:
- NameOf operator [Visual Basic]
ms.openlocfilehash: 8416bb1a1715c1c37b62cac6a9e0b427a9c72547
ms.sourcegitcommit: ad800f019ac976cb669e635fb0ea49db740e6890
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73041353"
---
# <a name="nameof-operator---visual-basic"></a>Visual Basic の NameOf 演算子

`NameOf` 演算子を使うと、変数、型、またはメンバーの名前を文字列定数として取得できます。

```vb
Console.WriteLine(NameOf(System.Collections.Generic))  ' output: Generic
Console.WriteLine(NameOf(List(Of Integer)))  ' output: List
Console.WriteLine(NameOf(List(Of Integer).Count))  ' output: Count
Console.WriteLine(NameOf(List(Of Integer).Add))  ' output: Add

Dim numbers As New List(Of Integer) From { 1, 2, 3 }
Console.WriteLine(NameOf(numbers))  ' output: numbers
Console.WriteLine(NameOf(numbers.Count))  ' output: Count
Console.WriteLine(NameOf(numbers.Add))  ' output: Add
```

前の例で示されているように、型と名前空間の場合、生成される名前は通常[完全修飾](~/_csharplang/spec/basic-concepts.md#fully-qualified-names)ではありません。

`NameOf` 演算子はコンパイル時に評価され、実行時には影響を与えません。

`NameOf` 演算子を使って、引数をチェックするコードを保守しやすくすることができます。

```vb
Private _name As String

Public Property Name As String
    Get
        Return _name
    End Get
    Set
        If value Is Nothing Then
            Throw New ArgumentNullException(NameOf(value), $"{NameOf(name)} cannot be null.")
        End If
    End Set
End Property
```

`NameOf` 演算子は Visual Basic 14 以降で使用できます。

## <a name="see-also"></a>関連項目

- [Visual Basic の言語リファレンス](../index.md)
- [演算子 (Visual Basic)](index.md)
