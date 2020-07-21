---
title: ラムダ式はこのイベント ハンドラーから削除されません
ms.date: 07/20/2015
f1_keywords:
- bc42326
- vbc42326
helpviewer_keywords:
- BC42326
ms.assetid: 63214dc6-0112-4245-8ebf-7c9e8f5a5782
ms.openlocfilehash: 07ace3f1b9c5e512227dc1f718ef768b631c8303
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397377"
---
# <a name="lambda-expression-will-not-be-removed-from-this-event-handler"></a>ラムダ式はこのイベント ハンドラーから削除されません

ラムダ式はこのイベント ハンドラーから削除されません。 ラムダ式に変数を割り当て、その変数を使用してイベントを追加または削除します。

ラムダ式をイベント ハンドラーと共に使用すると、期待どおりの動作が見られない場合があります。 コンパイラは、定義が同一であっても、ラムダ式ごとに新しいメソッドを生成します。 そのため、次のコードは `False` を表示します。

```vb
Module Module1

    Sub Main()
        Dim fun1 As ChangeInteger = Function(p As Integer) p + 1
        Dim fun2 As ChangeInteger = Function(p As Integer) p + 1
        Console.WriteLine(fun1 = fun2)
    End Sub

    Delegate Function ChangeInteger(ByVal x As Integer) As Integer

End Module
```

ラムダ式をイベント ハンドラーと共に使用すると、予期しない結果が発生する可能性があります。 次の例では、`AddHandler` によって追加されたラムダ式は、`RemoveHandler` ステートメントによって削除されません。

```vb
Module Module1

    Event ProcessInteger(ByVal x As Integer)

    Sub Main()

        ' The following line adds one listener to the event.
        AddHandler ProcessInteger, Function(m As Integer) m

        ' The following statement searches the current listeners
        ' for a match to remove. However, this lambda is not the same
        ' as the previous one, so nothing is removed.
        RemoveHandler ProcessInteger, Function(m As Integer) m

    End Sub
End Module
```

既定では、このメッセージは警告です。 警告を表示しない方法や、警告をエラーとして扱う方法の詳細については、「 [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic)」を参照してください。

**エラー ID:** BC42326

## <a name="to-correct-this-error"></a>このエラーを解決するには

この警告を回避し、ラムダ式を削除するには、次の例に示すように、ラムダ式を変数に割り当て、`AddHandler` と `RemoveHandler` の両方のステートメントで変数を使用します。

```vb
Module Module1

    Event ProcessInteger(ByVal x As Integer)

    Dim PrintHandler As ProcessIntegerEventHandler

    Sub Main()

        ' Assign the lambda expression to a variable.
        PrintHandler = Function(m As Integer) m

        ' Use the variable to add the listener.
        AddHandler ProcessInteger, PrintHandler

        ' Use the variable again when you want to remove the listener.
        RemoveHandler ProcessInteger, PrintHandler

    End Sub
End Module
```

## <a name="see-also"></a>関連項目

- [ラムダ式](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [厳密でないデリゲート変換](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
- [イベント](../../programming-guide/language-features/events/index.md)
