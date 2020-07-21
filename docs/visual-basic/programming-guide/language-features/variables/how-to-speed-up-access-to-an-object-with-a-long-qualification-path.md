---
title: '方法: 長い修飾パスを持つオブジェクトへのアクセス時間を短縮する'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], accessing
- variables [Visual Basic], object
- With statement [Visual Basic]
- With block
- object variables [Visual Basic], accessing
ms.assetid: 3eb7657f-c9fe-4e05-8bc3-4bb14d5ae585
ms.openlocfilehash: fe93e7bac2a21f1060d1f93765eb35e1ad0c7eb0
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410413"
---
# <a name="how-to-speed-up-access-to-an-object-with-a-long-qualification-path-visual-basic"></a>方法: 長い修飾パスを持つオブジェクトに対するアクセス時間を短縮する (Visual Basic)

複数のメソッドおよびプロパティの修飾パスを必要とするオブジェクトに頻繁にアクセスする場合は、修飾パスを繰り返さないことでコードを高速化することができます。

修飾パスの繰り返しを回避するには、2 つの方法があります。 オブジェクトを変数に割り当てることも、`With`...`End With` ブロック内で使用することもできます。

### <a name="to-speed-up-access-to-a-heavily-qualified-object-by-assigning-it-to-a-variable"></a>頻繁に使用する修飾オブジェクトへのアクセスを変数への代入によって高速化するには

1. 頻繁にアクセスするオブジェクトの型の変数を宣言します。 宣言の初期化部分に修飾パスを指定します。

    ```vb
    Dim ctrlActv As Control = someForm.ActiveForm.ActiveControl
    ```

2. オブジェクトのメンバーにアクセスするには、変数を使用します。

    ```vb
    ctrlActv.Text = "Test"
    ctrlActv.Location = New Point(100, 100)
    ctrlActv.Show()
    ```

### <a name="to-speed-up-access-to-a-heavily-qualified-object-by-using-a-withend-with-block"></a>頻繁に使用する修飾オブジェクトへのアクセスを With...End の With ブロックを使用して高速化するには

1. `With` ステートメントに修飾パスを配置します。

    ```vb
    With someForm.ActiveForm.ActiveControl
    ```

2. `End With` ステートメントの前に、`With` ブロック内でオブジェクトのメンバーにアクセスします。

    ```vb
        .Text = "Test"
        .Location = New Point(100, 100)
        .Show()
    End With
    ```

## <a name="see-also"></a>関連項目

- [オブジェクト変数](object-variables.md)
- [With...End With ステートメント](../../../language-reference/statements/with-end-with-statement.md)
