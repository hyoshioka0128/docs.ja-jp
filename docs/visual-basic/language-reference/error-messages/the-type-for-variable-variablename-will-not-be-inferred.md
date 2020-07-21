---
title: 変数 '<variablename>' の型は、外側のスコープ内のフィールドにバインドされているため、推論できません。
ms.date: 07/20/2015
f1_keywords:
- vbc42110
- bc42110
helpviewer_keywords:
- BC42110
ms.assetid: ef4442eb-08d1-434f-a03b-4aa2ed4e4414
ms.openlocfilehash: 98aeb5699fdd5e5e538a205acd37436019c3fc03
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84363047"
---
# <a name="the-type-for-variable-variablename-will-not-be-inferred-because-it-is-bound-to-a-field-in-an-enclosing-scope"></a>変数 '\<variablename>' の型は、外側のスコープ内のフィールドにバインドされているため、推論できません。

変数 '\<variablename>' の型は、外側のスコープ内のフィールドにバインドされているため、推論できません。 '\<variablename>' の名前を変更するか、完全修飾名 (例: 'Me.variablename' や 'MyBase.variablename') を使用してください。

コードのループ制御変数は、クラスまたは他の外側のスコープ内のフィールドと同じ名前を持っています。 制御変数は、`As` 句なしで使用されるため、外側のスコープ内のフィールドにバインドされ、コンパイラがこれに対して新しい変数を作成したり、その型を推論したりすることはありません。

次の例では、`Index` (`For` ステートメントの制御変数) が、`Index` クラスの `Customer` フィールドにバインドされています。 コンパイラが制御変数 `Index` に対して新しい変数を作成したり、その型を推論したりすることはありません。

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

    ' The following line will raise this warning.
        For Index = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

既定では、このメッセージは警告です。 警告を表示しない方法や、警告をエラーとして扱う方法については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」を参照してください。

**エラー ID:** BC42110

### <a name="to-address-this-warning"></a>この警告に対処するには

- ループ制御変数の名前を、クラスのフィールドの名前とは異なる識別子に変更して、この変数をローカルにします。

  ```vb
  For I = 1 To 10
  ```

- 変数名の前に `Me.` を付けることにより、クラス フィールドにループ制御変数がバインドされていることを明確にします。

  ```vb
  For Me.Index = 1 To 10
  ```

- ローカル型の推定ではなく `As` 句を使用して、ループ制御変数に型を指定します。

  ```vb
  For Index As Integer = 1 To 10
  ```

## <a name="example"></a>例
 次のコードは、上の例に最初の修正を行ったものです。

```vb
Class Customer

    ' The class has a field named Index.
    Private Index As Integer

    Sub Main()

        For I = 1 To 10
            ' ...
        Next

    End Sub
End Class
```

## <a name="see-also"></a>関連項目

- [Option Infer ステートメント](../statements/option-infer-statement.md)
- [For Each...Next ステートメント](../statements/for-each-next-statement.md)
- [For...Next ステートメント](../statements/for-next-statement.md)
- [方法: オブジェクトの現在のインスタンスを参照する](../../programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)
- [ローカル型の推論](../../programming-guide/language-features/variables/local-type-inference.md)
- [Me、My、MyBase、および MyClass](../../programming-guide/program-structure/me-my-mybase-and-myclass.md)
