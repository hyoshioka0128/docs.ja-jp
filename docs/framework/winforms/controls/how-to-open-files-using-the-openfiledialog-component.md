---
title: '方法: OpenFileDialog コンポーネントを使用してファイルを開く'
ms.date: 02/11/2019
description: OpenFileDialog コンポーネントを使用して、ファイルを参照および選択するための [Windows] ダイアログボックスを開く方法について説明します。
dev_langs:
- csharp
- vb
helpviewer_keywords:
- OpenFileDialog component [Windows Forms], opening files
- OpenFile method [Windows Forms], OpenFileDialog component
- files [Windows Forms], opening with OpenFileDialog component
ms.assetid: 9d88367a-cc21-4ffd-be74-89fd63767d35
ms.openlocfilehash: d571885011b0f0c723c73a417f294f30f96952f4
ms.sourcegitcommit: 3824ff187947572b274b9715b60c11269335c181
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2020
ms.locfileid: "84904430"
---
# <a name="how-to-open-files-with-the-openfiledialog"></a>方法: OpenFileDialog を使用してファイルを開く

[ <xref:System.Windows.Forms.OpenFileDialog?displayProperty=nameWithType> Windows] ダイアログボックスが開き、ファイルを参照して選択できます。 選択したファイルを開いて読み取るに <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A?displayProperty=nameWithType> は、メソッドを使用するか、クラスのインスタンスを作成し <xref:System.IO.StreamReader?displayProperty=nameWithType> ます。 次の例では、両方の方法を示します。

.NET Framework では、プロパティを取得または設定するには、 <xref:System.Windows.Forms.FileDialog.FileName%2A> クラスによって権限レベルが付与されている必要があり <xref:System.Security.Permissions.FileIOPermission?displayProperty=nameWithType> ます。 この例では、 <xref:System.Security.Permissions.FileIOPermission> アクセス許可チェックを実行し、部分信頼コンテキストで実行する場合は特権が不足しているため例外をスローできます。 詳細については、「[コードアクセスセキュリティの基礎](../../misc/code-access-security-basics.md)」を参照してください。

これらの例は、C# または Visual Basic のコマンドラインから .NET Framework アプリとしてビルドして実行できます。 詳細については、「 [csc.exeを使用したコマンドライン](../../../csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)からのビルド」または「[コマンドラインからのビルド](../../../visual-basic/reference/command-line-compiler/building-from-the-command-line.md)」を参照してください。

.NET Core 3.0 以降では、.NET Core Windows フォーム* \<folder name> .csproj*プロジェクトファイルを持つフォルダーから、Windows .net core アプリとして例をビルドして実行することもできます。

## <a name="example-read-a-file-as-a-stream-with-streamreader"></a>例: StreamReader を使用してファイルをストリームとして読み取る  
  
次の例では、Windows フォームコントロールのイベントハンドラーを使用して、メソッドを使用してを <xref:System.Windows.Forms.Button> <xref:System.Windows.Forms.Control.Click> 開き <xref:System.Windows.Forms.OpenFileDialog> <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> ます。 ユーザーがファイルを選択して **[OK]** を選択すると、クラスのインスタンスによって <xref:System.IO.StreamReader> ファイルが読み取られ、その内容がフォームのテキストボックスに表示されます。 ファイルストリームからの読み取りの詳細については、「」および「」を参照してください <xref:System.IO.FileStream.BeginRead%2A?displayProperty=nameWithType> <xref:System.IO.FileStream.Read%2A?displayProperty=nameWithType> 。  

 [!code-csharp[OpenFileDialog#1](~/samples/snippets/winforms/open-files/example1/cs/Form1.cs)]
 [!code-vb[OpenFileDialog#1](~/samples/snippets/winforms/open-files/example1/vb/Form1.vb)]  

## <a name="example-open-a-file-from-a-filtered-selection-with-openfile"></a>例: OpenFile を使用してフィルター選択された選択からファイルを開く

次の例では <xref:System.Windows.Forms.Button> 、コントロールのイベントハンドラーを使用して <xref:System.Windows.Forms.Control.Click> 、 <xref:System.Windows.Forms.OpenFileDialog> テキストファイルのみを表示するフィルターを指定してを開きます。 ユーザーがテキストファイルを選択して **[OK]** を選択した後、メソッドを使用して <xref:System.Windows.Forms.OpenFileDialog.OpenFile%2A> メモ帳でファイルを開きます。

 [!code-csharp[OpenFileDialog#2](~/samples/snippets/winforms/open-files/example2/cs/Form1.cs)]
 [!code-vb[OpenFileDialog#2](~/samples/snippets/winforms/open-files/example2/vb/Form1.vb)]  

## <a name="see-also"></a>こちらもご覧ください

- <xref:System.Windows.Forms.OpenFileDialog>
- [OpenFileDialog コンポーネント](openfiledialog-component-windows-forms.md)
