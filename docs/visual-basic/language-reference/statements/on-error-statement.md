---
title: On Error ステートメント
ms.date: 07/20/2015
f1_keywords:
- vb.OnError
helpviewer_keywords:
- Visual Basic code, control flow
- Resume Next statement [Visual Basic]
- errors [Visual Basic], trapping
- error handling, On Error statement
- Next statement [Visual Basic], On Error
- control flow [Visual Basic], branching
- Error keyword [Visual Basic]
- execution [Visual Basic], conditional
- Resume statement [Visual Basic], and On Error statement
- Error statement [Visual Basic], and On Error statement
- GoTo statement [Visual Basic], and On Error statement
- branching [Visual Basic], on error
- conditional statements [Visual Basic], On Error
- On Error statement [Visual Basic], syntax
- On keyword [Visual Basic]
- run-time errors [Visual Basic], handling
- On Error statement [Visual Basic]
ms.assetid: ff947930-fb84-40cf-bd66-1ea219561d5c
ms.openlocfilehash: 0297f7af29faf5a08472fd1d18ca52e9b2fda1af
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84404409"
---
# <a name="on-error-statement-visual-basic"></a>On Error ステートメント (Visual Basic)
エラー処理ルーチンを有効にし、プロシージャ内のルーチンの場所を指定します。エラー処理ルーチンを無効にするためにも使用できます。 `On Error` ステートメントは、非構造化エラー処理で使用し、構造化例外処理の代わりに使用できます。 [構造化例外処理](../../../standard/exceptions/index.md)は .NET に組み込まれており、一般に効率的であるため、アプリケーションで実行時エラーを処理する場合に推奨されます。

 エラー処理または例外処理を使用しない場合、発生したすべての実行時エラーが致命的になります。エラーメッセージが表示され、実行が停止します。

> [!NOTE]
> `Error` キーワードは、下位互換性のためにサポートされている [Error ステートメント](error-statement.md)でも使用します。

## <a name="syntax"></a>構文

```vb
On Error { GoTo [ line | 0 | -1 ] | Resume Next }
```

## <a name="parts"></a>指定項目

|用語|定義|
|---|---|
|`GoTo` *line*|必須の *line* 引数に指定された行から始まるエラー処理ルーチンを有効にします。 *line* 引数は、任意の行ラベルまたは行番号です。 実行時エラーが発生した場合、制御が指定された行に分岐し、エラー ハンドラーがアクティブになります。 指定した行は、`On Error` ステートメントと同じプロシージャ内に存在する必要があります。さもないと、コンパイル時エラーが発生します。|
|`GoTo 0`|現在のプロシージャで有効になっているエラー ハンドラーを無効にし、`Nothing` にリセットします。|
|`GoTo -1`|現在のプロシージャで有効になっている例外を無効にし、`Nothing` にリセットします。|
|`Resume Next`|実行時エラーが発生したときに、エラーが発生したステートメントの直後のステートメントに制御を移動し、そのポイントから実行を続行することを指定します。 オブジェクトにアクセスする場合は、`On Error GoTo` ではなく、この形式を使用します。|

## <a name="remarks"></a>Remarks

> [!NOTE]
> コードでは、非構造化例外処理と `On Error` ステートメントを使用するのではなく、可能な限り、構造化例外処理を使用することをお勧めします。 詳しくは、「[Try...Catch...Finally ステートメント](try-catch-finally-statement.md)」をご覧ください。

 "有効な" エラー ハンドラーは、`On Error` ステートメントによって有効にされるものです。 "アクティブな" エラー ハンドラーは、エラーの処理中に有効にされているハンドラーです。

 エラー ハンドラーがアクティブになっている間 (エラーの発生と、`Resume`、`Exit Sub`、`Exit Function`、または `Exit Property` ステートメントの間) にエラーが発生した場合、現在のプロシージャのエラー ハンドラーではエラーを処理できません。 呼び出し元のプロシージャに制御が戻ります。
  
 呼び出し元のプロシージャに有効なエラー ハンドラーがある場合、エラーを処理するために、それがアクティブ化されます。 呼び出し元のプロシージャのエラー ハンドラーもアクティブな場合は、有効だが非アクティブなエラー ハンドラーが見つかるまで、前の呼び出し元プロシージャをさかのぼって、制御が戻されます。 そのようなエラー ハンドラーが見つからない場合、エラーは実際に発生した時点で致命的になります。
  
 エラー ハンドラーによって呼び出し元のプロシージャに制御が戻されるたびに、そのプロシージャが現在のプロシージャになります。 いずれかのプロシージャのエラーハンドラーによってエラーが処理されると、`Resume` ステートメントで指定されたポイントにある現在のプロシージャで、実行が再開されます。
  
> [!NOTE]
> エラー処理ルーチンは、`Sub` プロシージャや `Function` プロシージャではありません。 それは、行ラベルまたは行番号でマークされたコードのセクションです。
  
## <a name="number-property"></a>Number プロパティ
 エラー処理ルーチンでは、エラーの原因を特定するために、`Err` オブジェクトの `Number` プロパティの値に依存しています。 ルーチンでは、他のエラーが発生する可能性がある前、またはエラーが発生する可能性のあるプロシージャが呼び出される前に、`Err` オブジェクトの関連するプロパティ値をテストまたは保存する必要があります。 `Err` オブジェクトのプロパティ値は、最新のエラーだけを反映しています。 `Err.Number` に関連付けられたエラー メッセージは `Err.Description` に含まれています。  
  
## <a name="throw-statement"></a>Throw ステートメント  
 `Err.Raise` メソッドで発生したエラーによって、`Exception` プロパティが <xref:System.Exception> クラスの新しく作成されたインスタンスに設定されます。 派生した例外の種類の例外の発生をサポートするために、その言語で `Throw` ステートメントがサポートされています。 これは、スローされる例外インスタンスである 1 つのパラメーターを受け取ります。 次の例に、これらの機能を既存の例外処理サポートと共に使用する方法を示しています。

 [!code-vb[VbVbalrErrorHandling#17](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#17)]  
  
 `On Error GoTo` ステートメントでは、例外クラスに関係なく、すべてのエラーがトラップされることに注意してください。
  
## <a name="on-error-resume-next"></a>On Error Resume Next
 `On Error Resume Next` によって、実行時エラーが発生したステートメントの直後のステートメント、または `On Error Resume Next` ステートメントを含むプロシージャからの最新の呼び出しの直後のステートメントから、実行が続行されます。 このステートメントを使用すると、実行時エラーが発生しても実行を続行できます。 プロシージャ内の別の場所に制御を移すのではなく、エラーが発生しそうな場所に、エラー処理ルーチンを配置できます。 別のプロシージャが呼び出されると、`On Error Resume Next` ステートメントは非アクティブになります。そのため、ルーチン内にエラー処理を埋め込む場合に、呼び出される各ルーチンで `On Error Resume Next` ステートメントを実行する必要があります。
  
> [!NOTE]
> 他のオブジェクトへのアクセス中に生成されたエラーを処理する場合は、`On Error Resume Next` コンストラクトの方が、`On Error GoTo` より推奨されます。 オブジェクトの操作のたびに `Err` をチェックすることで、コードによってアクセスされたオブジェクトについてのあいまいさがなくなります。 `Err.Number` にエラーコードを配置したオブジェクトのほか、最初にエラーを生成したオブジェクト (`Err.Source` に指定されたオブジェクト) を確認できます。

## <a name="on-error-goto-0"></a>On Error GoTo 0
 `On Error GoTo 0` によって、現在のプロシージャのエラー処理が無効になります。 プロシージャに 0 番の行が含まれている場合でも、エラー処理コードの開始として行 0 は指定されません。 `On Error GoTo 0` ステートメントを使用しない場合、プロシージャが終了すると、エラー ハンドラーが自動的に無効になります。

## <a name="on-error-goto--1"></a>On Error GoTo -1
 `On Error GoTo -1` によって、現在のプロシージャの例外が無効になります。 プロシージャに -1 番の行が含まれている場合でも、エラー処理コードの開始として行 -1 は指定されません。 `On Error GoTo -1` ステートメントを使用しない場合、プロシージャが終了すると、例外が自動的に無効になります。

 エラーが発生しなかったときに、エラー処理コードが実行されないようにするには、次のフラグメントのように、エラー処理ルーチンの直前に、`Exit Sub`、`Exit Function`、または `Exit Property` ステートメントを配置します。

 [!code-vb[VbVbalrErrorHandling#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#18)]

 ここで、エラー処理コードは、`Exit Sub` ステートメントの後、`End Sub` ステートメントの前に置いて、プロシージャ フローから分離します。 エラー処理コードは、プロシージャ内の任意の場所に配置できます。

## <a name="untrapped-errors"></a>トラップされないエラー
 オブジェクトが実行可能ファイルとして実行されている場合に、オブジェクトのトラップされないエラーが制御元のアプリケーションに返されます。 開発環境では、適切なオプションが設定されている場合にのみ、トラップされないエラーが制御元のアプリケーションに返されます。 デバッグ時に設定すべきオプション、それらの設定方法、およびホストでクラスを作成できるかどうかの説明については、ホスト アプリケーションのドキュメントを参照してください。

 他のオブジェクトにアクセスするオブジェクトを作成する場合は、返されたハンドルされないエラーの処理を試みる必要があります。 できない場合、`Err.Number` のエラー コードを独自のエラーのいずれかにマップし、次にそれらをオブジェクトの呼び出し元に渡します。 独自のエラーを指定するには、エラー コードを `VbObjectError` 定数に追加します。 たとえば、エラー コードが 1052 の場合は、それを次のように割り当てます。

 [!code-vb[VbVbalrErrorHandling#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#19)]

> [!CAUTION]
> Windows ダイナミックリンク ライブラリ (DLL) の呼び出し時のシステム エラーでは、例外が発生せず、Visual Basic エラー トラップでトラップできません。 DLL 関数を呼び出すときは、API 仕様に従って、各戻り値の成功または失敗を確認し、失敗の場合は `Err` オブジェクトの `LastDLLError` プロパティの値を確認する必要があります。

## <a name="example"></a>例
 この例では、最初に `On Error GoTo` ステートメントを使用して、プロシージャ内のエラー処理ルーチンの場所を指定しています。 例では、0 で除算しようとしてエラー番号 6 が生成されます。 エラー処理ルーチンでエラーが処理され、エラーが発生したステートメントに制御が返されます。 `On Error GoTo 0` ステートメントによって、エラー トラップがオフになります。 さらに、次のステートメントによって生成されるエラーのコンテキストを確実に認識できるように、`On Error Resume Next` ステートメントを使用して、エラー トラップを遅延します。 `Err.Clear` を使用して、エラーが処理された後に `Err` オブジェクトのプロパティがクリアされていることに注目してください。

 [!code-vb[VbVbalrErrorHandling#20](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrErrorHandling/VB/Class1.vb#20)]

## <a name="requirements"></a>必要条件
 **名前空間:** [Microsoft.VisualBasic](../runtime-library-members.md)

 **アセンブリ:** Visual Basic ランタイム ライブラリ (Microsoft.VisualBasic.dll)

## <a name="see-also"></a>関連項目

- <xref:Microsoft.VisualBasic.Information.Err%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Number%2A>
- <xref:Microsoft.VisualBasic.ErrObject.Description%2A>
- <xref:Microsoft.VisualBasic.ErrObject.LastDllError%2A>
- [End ステートメント](end-statement.md)
- [Exit ステートメント](exit-statement.md)
- [Resume ステートメント](resume-statement.md)
- [エラー メッセージ](../error-messages/index.md)
- [Try...Catch...Finally ステートメント](try-catch-finally-statement.md)
