---
title: '方法: デリゲート メソッドを呼び出す'
ms.date: 07/20/2015
ms.assetid: b56866ae-abf9-4a5a-a855-486359455e9c
ms.openlocfilehash: f319727c007b93c7b334af0598f1b9f7c034144d
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84410722"
---
# <a name="how-to-invoke-a-delegate-method-visual-basic"></a>方法: デリゲート メソッドを呼び出す (Visual Basic)

この例では、メソッドをデリゲートに関連付け、デリゲートからそのメソッドを呼び出す方法を示します。

### <a name="create-the-delegate-and-matching-procedures"></a>デリゲートおよび一致するプロシージャを作成する

1. `MySubDelegate` という名前のデリゲートを作成します。

    ```vb
    Delegate Sub MySubDelegate(ByVal x As Integer)
    ```

2. デリゲートと同じシグネチャのメソッドを含むクラスを宣言します。

    ```vb
    Class class1
        Sub Sub1(ByVal x As Integer)
            MsgBox("The value of x is: " & CStr(x))
        End Sub
    End Class
    ```

3. デリゲートのインスタンスを作成して、デリゲートに関連付けられているメソッドを、組み込みの `Invoke` メソッドを呼び出すことで起動するメソッドを定義します。

    ```vb
    Protected Sub DelegateTest()
        Dim c1 As New class1
        ' Create an instance of the delegate.
        Dim msd As MySubDelegate = AddressOf c1.Sub1
        ' Call the method.
        msd.Invoke(10)
    End Sub
    ```

## <a name="see-also"></a>関連項目

- [Delegate ステートメント](../../../language-reference/statements/delegate-statement.md)
- [デリゲート](index.md)
- [イベント](../events/index.md)
- [マルチスレッド アプリケーション](../../../../standard/threading/using-threads-and-threading.md)
