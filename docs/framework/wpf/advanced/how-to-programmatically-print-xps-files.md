---
title: '方法: XPS ファイルをプログラムにより印刷する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- printing XPS files programmatically [WPF]
- XPS files [WPF], printing programmatically
ms.assetid: 0b1c0a3f-b19e-43d6-bcc9-eb3ec4e555ad
ms.openlocfilehash: cc86a7e7c6a816af37c3d063825ed62583afa78a
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73966996"
---
# <a name="how-to-programmatically-print-xps-files"></a>方法: XPS ファイルをプログラムにより印刷する

<xref:System.Printing.PrintQueue.AddJob%2A> メソッドの 1 つのオーバーロードを使用して、<xref:System.Windows.Controls.PrintDialog>、または原則として一切の [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] を開かずに、XML Paper Specification (XPS) ファイルを印刷することができます。

また、多くの <xref:System.Windows.Xps.XpsDocumentWriter.Write%2A?displayProperty=nameWithType> および <xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A?displayProperty=nameWithType> メソッドを使用して XPS ファイルを印刷することもできます。 詳細については、「[XPS ドキュメントの印刷](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771525(v=vs.90))」を参照してください。

XPS を印刷するもう 1 つの方法は、<xref:System.Windows.Controls.PrintDialog.PrintDocument%2A?displayProperty=nameWithType> または <xref:System.Windows.Controls.PrintDialog.PrintVisual%2A?displayProperty=nameWithType> メソッドを使用することです。 [印刷ダイアログ ボックスの呼び出し](how-to-invoke-a-print-dialog.md)に関するページをご覧ください。

## <a name="example"></a>例

3 つのパラメーターの <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> メソッドを使用する主な手順は次のとおりです。 詳細は、下記の例に示します。

1. プリンターが XPSDrv プリンターかどうかを確認します XPSDrv の詳細については、「[印刷の概要](printing-overview.md)」を参照してください。

2. プリンターが XPSDrv プリンターでない場合は、スレッドのアパートメントをシングル スレッドに設定します。

3. プリント サーバーと印刷キューのオブジェクトをインスタンス化します。

4. ジョブ名、印刷するファイル、プリンターが XPSDrv プリンターであるかどうかを示す <xref:System.Boolean> フラグを指定して、メソッドを呼び出します。

次の例は、ディレクトリ内のすべての XPS ファイルをバッチ印刷する方法を示しています。 アプリケーションはディレクトリを指定するようにユーザーに要求しますが、3 つのパラメーターの <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> メソッドには [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] は必要ありません。 このメソッドは、これに渡すことができる XPS ファイル名とパスが記述された任意のコード パスで使用できます。

<xref:System.Printing.PrintQueue.AddJob%2A> の 3 つのパラメーターの <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> オーバーロードは、<xref:System.Boolean> パラメーターが `false` のとき (XPSDrv 以外のプリンターを使用する場合は必須) は常に 1 つのスレッド アパートメントで実行する必要があります。 ただし、.NET の既定のアパートメント状態は、複数のスレッドです。 この例では XPSDrv 以外のプリンターを前提にしているため、この既定の状態を逆にする必要があります。

既定の状態を変更する方法は 2 つあります。 1 つの方法は、アプリケーションの `Main` メソッドの最初の行 (通常は "`static void Main(string[] args)`") のすぐ上に、<xref:System.STAThreadAttribute> (つまり "`[System.STAThreadAttribute()]`") を追加するだけです。 しかし、多くのアプリケーションでは、`Main` メソッドのアパートメント状態はマルチスレッドである必要があります。2 つ目の方法があるのはこのためです。この方法では、<xref:System.Threading.Thread.SetApartmentState%2A> でアパートメント状態を <xref:System.Threading.ApartmentState.STA> に設定した別のスレッドに、<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> の呼び出しを配置します。 次の例では、この 2 番目の方法を使用します。

そのため、この例では、まず、<xref:System.Threading.Thread> オブジェクトをインスタンス化し、それを <xref:System.Threading.ThreadStart> パラメーターとして **PrintXPS** メソッドに渡します (**PrintXPS** メソッドは、例の後半で定義されます)。次に、そのスレッドをシングル スレッド アパートメントに設定します。 それ以降の `Main` メソッドのコードは、この新しいスレッドを開始します。

この例の要点は、`static`**staticBatchXPSPrinter.PrintXPS** メソッド内にあります。 このメソッドは、プリント サーバーとキューを作成した後、XPS ファイルを含むディレクトリを指定するようにユーザーに要求します。 さらに、ディレクトリの有無と、その中に \*.xps ファイルがあるかどうかを確認した後、このような各ファイルを印刷キューに追加します。 この例では、プリンターが XPSDrv 以外であることを前提としているため、<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> メソッドの最後のパラメーターに `false`を渡しています。 このため、このメソッドはファイル内の XPS マークアップを検証してから、それをプリンターのページ記述言語に変換することを試みます。 検証に失敗すると、例外がスローされます。 このコード例では、その例外をキャッチし、ユーザーに例外の発生を通知した後、次の XPS ファイルの処理に進みます。

[!code-csharp[BatchPrintXPSFiles#BatchPrintXPSFiles](~/samples/snippets/csharp/VS_Snippets_Wpf/BatchPrintXPSFiles/CSharp/Program.cs#batchprintxpsfiles)]
[!code-vb[BatchPrintXPSFiles#BatchPrintXPSFiles](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BatchPrintXPSFiles/visualbasic/program.vb#batchprintxpsfiles)]

XPSDrv プリンターを使用している場合は、最後のパラメーターを `true` に設定できます。 その場合、XPS はプリンターのページ記述言語であるため、メソッドはファイルの検証や別のページ記述言語への変換を行わずにファイルをプリンターに送信します。 設計時に、アプリケーションが XPSDrv プリンターを使用するかどうかがわからない場合は、<xref:System.Printing.PrintQueue.IsXpsDevice%2A> プロパティを読み込んで、その検出内容に従って分岐するようにアプリケーションを変更できます。

Windows Vista および Microsoft .NET Framework のリリースの直後は、利用できる XPSDrv プリンターが少ないため、XPSDrv プリンター以外のプリンターを XPSDrv プリンターとして偽装することが必要な場合があります。 そのためには、アプリケーションを実行しているコンピューターで、以下のレジストリ キーのファイルの一覧に Pipelineconfig.xml を追加します。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Environments\Windows NT x86\Drivers\Version-3\\ *\<PseudoXPSPrinter>* \DependentFiles

ここで、 *\<PseudoXPSPrinter* は任意の印刷キューです。 その後、コンピューターを再起動する必要があります。

このような偽装により、例外を発生させることなく、<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> の最後のパラメーターとして `true` を渡すことができます。ただし、 *\<PseudoXPSPrinter>* は実際には XPSDrv プリンターではないため、ガベージのみが印刷されます。

> [!NOTE]
> 上記の例では、わかりやすくするために、\*.xps 拡張子の有無で、ファイルが XPS であるかどうかをテストしていますが、 XPS ファイルに、この拡張子を付ける必要はありません。 [isXPS.exe (isXPS 適合性ツール)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa348104(v=vs.100)) は、ファイルが XPS に適合しているかどうかをテストする 1 つの方法です。

## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.AddJob%2A>
- <xref:System.Threading.ApartmentState>
- <xref:System.STAThreadAttribute>
- [XPS ドキュメント](/windows/desktop/printdocs/documents)
- [XPS ドキュメントの印刷](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771525(v=vs.90))
- [マネージド スレッドとアンマネージド スレッド](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5s8ee185(v=vs.100))
- [isXPS.exe (isXPS 適合性ツール)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa348104(v=vs.100))
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
