---
title: メインのプロシージャ
ms.date: 07/20/2015
f1_keywords:
- vb.Main
helpviewer_keywords:
- Main procedure
- Main method [Visual Basic]
- main function
ms.assetid: f0db283e-f283-4464-b521-b90858cc1b44
ms.openlocfilehash: cf6003206566dfe8f70a7f75cd4d7ec7565794a5
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84403175"
---
# <a name="main-procedure-in-visual-basic"></a>Visual Basic の Main プロシージャ
すべての Visual Basic アプリケーションには、`Main` と呼ばれるプロシージャが含まれている必要があります。 このプロシージャは、アプリケーションの開始点となり、アプリケーションの全体的な制御を行います。 .NET Framework では、アプリケーションが読み込まれ、制御を渡す準備ができると、`Main` プロシージャを呼び出します。 Windows フォーム アプリケーションを作成する場合を除き、単独で実行されるアプリケーションでは、`Main` プロシージャを記述する必要があります。

 `Main` には、最初に実行されるコードが含まれます。 `Main` では、プログラムの起動時に最初に読み込まれるフォームを決定したり、アプリケーションのコピーがシステムで既に実行されているかどうかを確認したりできます。また、アプリケーションの一連の変数を確立したり、アプリケーションに必要なデータベースを開いたりすることもできます。

## <a name="requirements-for-the-main-procedure"></a>Main プロシージャの要件
 単独で実行されるファイル (通常は拡張子が .exe) には、`Main` プロシージャが含まれている必要があります。 ライブラリ (拡張子.dll など) は単独では実行されないので、`Main` プロシージャは不要です。 作成できるさまざまな種類のプロジェクトの要件は次のとおりです。

- コンソール アプリケーションは単独で実行されるので、少なくとも 1 つの `Main` プロシージャを指定する必要があります。

- Windows フォーム アプリケーションは単独で実行されます。 ただし、このようなアプリケーションの `Main` プロシージャは、Visual Basic コンパイラによって自動的に生成されるので、記述する必要はありません。

- クラス ライブラリには、`Main` プロシージャは不要です。 これには、Windows コントロール ライブラリや Web コントロール ライブラリが含まれます。 Web アプリケーションは、クラス ライブラリとして展開されます。

## <a name="declaring-the-main-procedure"></a>Main プロシージャの宣言
 `Main` プロシージャを宣言するには、4 つの方法があります。 引数を受け取ることも、受け取らないこともできます。また、値を返すことも返さないこともできます。

> [!NOTE]
> `Main` をクラスで宣言する場合は、`Shared` キーワードを使用する必要があります。 モジュールでは、`Main` は `Shared` である必要はありません。

- 最も簡単な方法は、引数を受け取らず、値を返さない `Sub` プロシージャを宣言することです。

    ```vb
    Module mainModule
        Sub Main()
            MsgBox("The Main procedure is starting the application.")
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```

- `Main` では、オペレーティング システムがプログラムの終了コードとして使用する `Integer` 値を返すこともできます。 他のプログラムは Windows の ERRORLEVEL 値を調べることで、このコードをテストできます。 終了コードを返すには、`Sub` プロシージャではなく、`Function` プロシージャとして `Main` を宣言する必要があります。

    ```vb
    Module mainModule
        Function Main() As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- `Main` では、引数として `String` 配列を受け取ることもできます。 配列内の各文字列には、プログラムの呼び出しに使用されるコマンド ライン引数の 1 つが含まれます。 値に応じてさまざまなアクションを実行できます。

    ```vb
    Module mainModule
        Function Main(ByVal cmdArgs() As String) As Integer
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            ' On return, assign appropriate value to returnValue.
            ' 0 usually means successful completion.
            MsgBox("The application is terminating with error level " &
                 CStr(returnValue) & ".")
            Return returnValue
        End Function
    End Module
    ```

- 次のように、コマンド ライン引数を調べ、終了コードは返さないように、`Main` を宣言できます。

    ```vb
    Module mainModule
        Sub Main(ByVal cmdArgs() As String)
            MsgBox("The Main procedure is starting the application.")
            Dim returnValue As Integer = 0
            ' See if there are any arguments.
            If cmdArgs.Length > 0 Then
                For argNum As Integer = 0 To UBound(cmdArgs, 1)
                    ' Insert code to examine cmdArgs(argNum) and take
                    ' appropriate action based on its value.
                Next
            End If
            ' Insert call to appropriate starting place in your code.
            MsgBox("The application is terminating.")
        End Sub
    End Module
    ```
  
## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>
- <xref:System.Array.Length%2A>
- <xref:Microsoft.VisualBasic.Information.UBound%2A>
- [Visual Basic プログラムの構造](structure-of-a-visual-basic-program.md)
- [-main](../../reference/command-line-compiler/main.md)
- [Shared](../../language-reference/modifiers/shared.md)
- [Sub ステートメント](../../language-reference/statements/sub-statement.md)
- [Function ステートメント](../../language-reference/statements/function-statement.md)
- [Integer データ型](../../language-reference/data-types/integer-data-type.md)
- [String データ型](../../language-reference/data-types/string-data-type.md)
