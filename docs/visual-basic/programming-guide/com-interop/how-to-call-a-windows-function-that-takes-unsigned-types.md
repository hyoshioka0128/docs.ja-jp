---
title: '方法: 符号なしの型を使用する Windows の機能を呼び出す'
ms.date: 07/20/2015
helpviewer_keywords:
- Windows functions [Visual Basic], calling
- unsigned data types [Visual Basic]
- UShort data type [Visual Basic], using
- functions [Visual Basic], calling Windows functions
- ULong data type [Visual Basic], using
- UInteger data type [Visual Basic], using
- data types [Visual Basic], using
- unsigned types [Visual Basic]
- data types [Visual Basic], unsigned
- data types [Visual Basic], numeric
- unsigned types [Visual Basic], using
ms.assetid: c2c0e712-8dc2-43b9-b4c6-345fbb02e7ce
ms.openlocfilehash: f30b78a2f0c38f233796e18006c889438dce4c58
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396831"
---
# <a name="how-to-call-a-windows-function-that-takes-unsigned-types-visual-basic"></a>方法: 符号なしの型を使用する Windows の機能を呼び出す (Visual Basic)

符号なし整数型のメンバーを含むクラス、モジュール、または構造体を使用している場合、これらのメンバーに Visual Basic を使用してアクセスできます。

## <a name="to-call-a-windows-function-that-takes-an-unsigned-type"></a>符号なしの型を使用する Windows の関数を呼び出すには

1. [Declare ステートメント](../../language-reference/statements/declare-statement.md)を使用して、どのライブラリに関数が含まれるか、そのライブラリ内での名前、呼び出し元シーケンス、および呼び出す際の文字列の変換方法を Visual Basic に指定します。

2. `Declare` ステートメントでは、符号なしの型の各パラメーターで必要に応じて、`UInteger`、`ULong`、`UShort`、または `Byte` を使用します。

3. 呼び出す Windows 関数のドキュメントを参照して、使用される定数の名前と値を確認します。 これらの多くは、WinUser.h ファイルで定義されています。

4. 必要な定数をコードで宣言します。 多くの Windows 定数は、32 ビットの符号なしの値であるため、これらを `As UInteger` で宣言する必要があります。

5. 通常の方法で関数を呼び出します。 次の例では、符号なし整数引数を受け取る Windows 関数 `MessageBox` を呼び出します。

    ```vb
    Public Class windowsMessage
        Private Declare Auto Function mb Lib "user32.dll" Alias "MessageBox" (
            ByVal hWnd As Integer,
            ByVal lpText As String,
            ByVal lpCaption As String,
            ByVal uType As UInteger) As Integer
        Private Const MB_OK As UInteger = 0
        Private Const MB_ICONEXCLAMATION As UInteger = &H30
        Private Const IDOK As UInteger = 1
        Private Const IDCLOSE As UInteger = 8
        Private Const c As UInteger = MB_OK Or MB_ICONEXCLAMATION
        Public Function messageThroughWindows() As String
            Dim r As Integer = mb(0, "Click OK if you see this!",
                "Windows API call", c)
            Dim s As String = "Windows API MessageBox returned " &
                 CStr(r)& vbCrLf & "(IDOK = " & CStr(IDOK) &
                 ", IDCLOSE = " & CStr(IDCLOSE) & ")"
            Return s
        End Function
    End Class
    ```

     次のコードを使用して、関数 `messageThroughWindows` をテストできます。

    ```vb
    Public Sub consumeWindowsMessage()
        Dim w As New windowsMessage
        w.messageThroughWindows()
    End Sub
    ```

    > [!CAUTION]
    > `UInteger`、`ULong`、`UShort`、および `SByte` データ型は、[言語への非依存性、および言語非依存コンポーネント](../../../standard/language-independence-and-language-independent-components.md) (CLS) の一部ではないため、CLS 準拠のコードではこれらを使用するコンポーネントを使用できません。

    > [!IMPORTANT]
    > Windows アプリケーション プログラミング インターフェイス (API) などのアンマネージド コードを呼び出すと、コードが潜在的なセキュリティ リスクにさらされます。

    > [!IMPORTANT]
    > Windows API を呼び出すには、アンマネージド コードのアクセス許可が必要です。これは、部分信頼状況での実行に影響を与える可能性があります。 詳細については、「<xref:System.Security.Permissions.SecurityPermission>」および「[コード アクセス許可](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/h846e9b3(v=vs.100))」を参照してください。

## <a name="see-also"></a>関連項目

- [データの種類](../../language-reference/data-types/index.md)
- [Integer データ型](../../language-reference/data-types/integer-data-type.md)
- [UInteger データ型](../../language-reference/data-types/uinteger-data-type.md)
- [Declare ステートメント](../../language-reference/statements/declare-statement.md)
- [チュートリアル: Windows API の呼び出し](walkthrough-calling-windows-apis.md)
