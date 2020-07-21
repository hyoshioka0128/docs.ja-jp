---
title: コントロールに対してスレッドセーフな呼び出しを行う
ms.date: 02/19/2019
description: スレッドセーフな方法でスレッド間の制御を呼び出すことによって、アプリにマルチスレッドを実装する方法について説明します。
dev_langs:
- csharp
- vb
f1_keywords:
- EHInvalidOperation.WinForms.IllegalCrossThreadCall
helpviewer_keywords:
- thread safety [Windows Forms], calling controls [Windows Forms]
- calling controls [Windows Forms], thread safety [Windows Forms]
- CheckForIllegalCrossThreadCalls property [Windows Forms]
- Windows Forms controls [Windows Forms], multithreading
- BackgroundWorker class [Windows Forms], examples
- threading [Windows Forms], cross-thread calls
- controls [Windows Forms], multithreading
ms.assetid: 138f38b6-1099-4fd5-910c-390b41cbad35
ms.openlocfilehash: b5f4de7bd3d8d89de98dbe27e2dbf360763670d0
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904183"
---
# <a name="how-to-make-thread-safe-calls-to-windows-forms-controls"></a>方法: Windows フォームコントロールに対してスレッドセーフな呼び出しを行う

マルチスレッドは Windows フォームアプリのパフォーマンスを向上させることができますが、Windows フォームコントロールへのアクセスは本質的にスレッドセーフではありません。 マルチスレッドでは、非常に深刻で複雑なバグにコードを公開できます。 コントロールを操作する2つ以上のスレッドによって、コントロールが一貫性のない状態になり、競合状態、デッドロック、フリーズまたはハングが発生する可能性があります。 アプリにマルチスレッドを実装する場合は、スレッドセーフな方法でスレッド間コントロールを呼び出すようにしてください。 詳細については、「[マネージスレッド処理のベストプラクティス](../../../standard/threading/managed-threading-best-practices.md)」を参照してください。

コントロールを作成していないスレッドから Windows フォームコントロールを安全に呼び出すには、2つの方法があります。 メソッドを使用して、 <xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=fullName> メインスレッドで作成されたデリゲートを呼び出すことができます。このデリゲートは、コントロールを呼び出します。 または、を実装できます <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType> 。これは、イベントドリブンモデルを使用して、バックグラウンドスレッドで実行された作業を結果のレポートから分離します。

## <a name="unsafe-cross-thread-calls"></a>安全でないクロススレッド呼び出し

コントロールを作成していないスレッドから直接呼び出すことは安全ではありません。 次のコードスニペットは、コントロールへの安全でない呼び出しを示してい <xref:System.Windows.Forms.TextBox?displayProperty=nameWithType> ます。 `Button1_Click`イベントハンドラーは、 `WriteTextUnsafe` メインスレッドのプロパティを直接設定する新しいスレッドを作成し <xref:System.Windows.Forms.TextBox.Text%2A?displayProperty=nameWithType> ます。

```csharp
private void Button1_Click(object sender, EventArgs e)
{
    thread2 = new Thread(new ThreadStart(WriteTextUnsafe));
    thread2.Start();
}
private void WriteTextUnsafe()
{
    textBox1.Text = "This text was set unsafely.";
}
```

```vb
Private Sub Button1_Click(ByVal sender As Object, e As EventArgs) Handles Button1.Click
    Thread2 = New Thread(New ThreadStart(AddressOf WriteTextUnsafe))
    Thread2.Start()
End Sub

Private Sub WriteTextUnsafe()
    TextBox1.Text = "This text was set unsafely."
End Sub
```

Visual Studio デバッガーは、メッセージを使用してを発生 <xref:System.InvalidOperationException> させ、スレッド間の操作が無効であることによって、これらのアンセーフスレッド呼び出しを検出し**ます。コントロール "" が作成されたスレッド以外のスレッドからアクセスされました。** は、 <xref:System.InvalidOperationException> Visual Studio のデバッグ中に安全でないクロススレッド呼び出しに対して常に発生し、アプリの実行時に発生する可能性があります。 この問題は解決する必要がありますが、プロパティをに設定することによって例外を無効にすることができ <xref:System.Windows.Forms.Control.CheckForIllegalCrossThreadCalls%2A?displayProperty=nameWithType> `false` ます。

## <a name="safe-cross-thread-calls"></a>安全なクロススレッド呼び出し

次のコード例は、作成されていないスレッドから Windows フォームコントロールを安全に呼び出す2つの方法を示しています。

1. <xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=fullName>メソッド。このメソッドは、コントロールを呼び出すメインスレッドからデリゲートを呼び出します。
2. <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType>イベントドリブンモデルを提供するコンポーネント。

どちらの例でも、バックグラウンドスレッドは1秒間スリープして、そのスレッドで実行されている作業をシミュレートします。

これらの例は、C# または Visual Basic のコマンドラインから .NET Framework アプリとしてビルドして実行できます。 詳細については、「 [csc.exeを使用したコマンドライン](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)からのビルド」または「[コマンドラインからのビルド (Visual Basic)](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)」を参照してください。

.NET Core 3.0 以降では、.NET Core Windows フォーム* \<folder name> .csproj*プロジェクトファイルを持つフォルダーから、Windows .net core アプリとして例をビルドして実行することもできます。

## <a name="example-use-the-invoke-method-with-a-delegate"></a>例: デリゲートで Invoke メソッドを使用する

次の例は、Windows フォームコントロールへのスレッドセーフな呼び出しを保証するパターンを示しています。 このメソッドは、プロパティに対してクエリを行います。これにより、 <xref:System.Windows.Forms.Control.InvokeRequired%2A?displayProperty=fullName> コントロールの作成スレッド id が呼び出し元のスレッド id と比較されます。 スレッド Id が同じである場合は、コントロールを直接呼び出します。 スレッド Id が異なる場合は、 <xref:System.Windows.Forms.Control.Invoke%2A?displayProperty=nameWithType> メインスレッドからのデリゲートを使用してメソッドを呼び出します。これにより、コントロールへの実際の呼び出しが行われます。

を使用すると、 `SafeCallDelegate` <xref:System.Windows.Forms.TextBox> コントロールのプロパティを設定でき <xref:System.Windows.Forms.TextBox.Text%2A> ます。 `WriteTextSafe`メソッドがクエリを <xref:System.Windows.Forms.Control.InvokeRequired%2A> 行います。 がを返す場合は、を <xref:System.Windows.Forms.Control.InvokeRequired%2A> `true` `WriteTextSafe` メソッドに渡して、 `SafeCallDelegate` <xref:System.Windows.Forms.Control.Invoke%2A> コントロールへの実際の呼び出しを行います。 が <xref:System.Windows.Forms.Control.InvokeRequired%2A> を返す場合は、 `false` を `WriteTextSafe` 直接設定し <xref:System.Windows.Forms.TextBox.Text%2A?displayProperty=nameWithType> ます。 `Button1_Click`イベントハンドラーは、新しいスレッドを作成し、メソッドを実行し `WriteTextSafe` ます。

 [!code-csharp[ThreadSafeCalls#1](~/samples/snippets/winforms/thread-safe/example1/cs/Form1.cs)]
 [!code-vb[ThreadSafeCalls#1](~/samples/snippets/winforms/thread-safe/example1/vb/Form1.vb)]  

## <a name="example-use-a-backgroundworker-event-handler"></a>例: BackgroundWorker イベントハンドラーを使用する

マルチスレッドを実装する簡単な方法は、 <xref:System.ComponentModel.BackgroundWorker?displayProperty=nameWithType> イベントドリブンモデルを使用するコンポーネントです。 バックグラウンドスレッドは、 <xref:System.ComponentModel.BackgroundWorker.DoWork?displayProperty=nameWithType> メインスレッドと対話しないイベントを実行します。 メインスレッドは、 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged?displayProperty=nameWithType> <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted?displayProperty=nameWithType> メインスレッドのコントロールを呼び出すことができるイベントハンドラーとイベントハンドラーを実行します。

を使用してスレッドセーフな呼び出しを行うには <xref:System.ComponentModel.BackgroundWorker> 、バックグラウンドスレッドでメソッドを作成して作業を実行し、イベントにバインドし <xref:System.ComponentModel.BackgroundWorker.DoWork> ます。 メインスレッドで別のメソッドを作成して、バックグラウンド作業の結果を報告し、 <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> イベントまたはイベントにバインドし <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> ます。 バックグラウンドスレッドを開始するには、を呼び出し <xref:System.ComponentModel.BackgroundWorker.RunWorkerAsync%2A?displayProperty=nameWithType> ます。

この例では、イベントハンドラーを使用して、 <xref:System.ComponentModel.BackgroundWorker.RunWorkerCompleted> <xref:System.Windows.Forms.TextBox> コントロールのプロパティを設定し <xref:System.Windows.Forms.TextBox.Text%2A> ます。 イベントの使用例については <xref:System.ComponentModel.BackgroundWorker.ProgressChanged> 、「」を参照してください <xref:System.ComponentModel.BackgroundWorker> 。

 [!code-csharp[ThreadSafeCalls#2](~/samples/snippets/winforms/thread-safe/example2/cs/Form1.cs)]
 [!code-vb[ThreadSafeCalls#2](~/samples/snippets/winforms/thread-safe/example2/vb/Form1.vb)]  

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.ComponentModel.BackgroundWorker>
- [方法: バックグラウンドで操作を実行する](how-to-run-an-operation-in-the-background.md)
- [方法: バックグラウンド操作を使用するフォームを実装する](how-to-implement-a-form-that-uses-a-background-operation.md)
- [.NET Framework を使用したカスタム Windows フォームコントロールの開発](developing-custom-windows-forms-controls.md)
