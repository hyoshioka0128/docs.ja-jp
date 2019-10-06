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
ms.openlocfilehash: d44f372fe5ef9633e91d8e46cca9e9a0967b9615
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71834572"
---
# <a name="how-to-programmatically-print-xps-files"></a>方法: XPS ファイルをプログラムにより印刷する

メソッドの1つのオーバーロードを<xref:System.Printing.PrintQueue.AddJob%2A>使用して、 <xref:System.Windows.Controls.PrintDialog> XML Paper Specification (XPS) ファイルを出力することができます。 [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]またはを開く必要はありません。

また、多数<xref:System.Windows.Xps.XpsDocumentWriter.Write%2A?displayProperty=nameWithType>のメソッドと<xref:System.Windows.Xps.XpsDocumentWriter.WriteAsync%2A?displayProperty=nameWithType>メソッドを使用して XPS ファイルを印刷することもできます。 詳細については、「 [XPS ドキュメントの印刷](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771525(v=vs.90))」を参照してください。

XPS を印刷するもう1つの方法<xref:System.Windows.Controls.PrintDialog.PrintDocument%2A?displayProperty=nameWithType>は<xref:System.Windows.Controls.PrintDialog.PrintVisual%2A?displayProperty=nameWithType> 、メソッドまたはメソッドを使用することです。 [印刷ダイアログ ボックスの呼び出し](how-to-invoke-a-print-dialog.md)に関するページをご覧ください。

## <a name="example"></a>例

3つのパラメーター <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>を持つメソッドを使用する主な手順は次のとおりです。 詳細は、下記の例に示します。

1. プリンターが XPSDrv プリンターかどうかを確認します XPSDrv の詳細については、「[印刷の概要](printing-overview.md)」を参照してください。

2. プリンターが XPSDrv プリンターでない場合は、スレッドのアパートメントをシングル スレッドに設定します。

3. プリント サーバーと印刷キューのオブジェクトをインスタンス化します。

4. ジョブ名、印刷するファイル、および<xref:System.Boolean>プリンターが XPSDrv プリンターであるかどうかを示すフラグを指定して、メソッドを呼び出します。

次の例は、ディレクトリ内のすべての XPS ファイルをバッチ印刷する方法を示しています。 アプリケーションはディレクトリを指定するようにユーザーに要求しますが、 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29> 3 つのパラメーターを[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]持つメソッドはを必要としません。 これは、XPS ファイル名とパスが含まれているすべてのコードパスで使用できます。

の3つの<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>パラメーターの<xref:System.Printing.PrintQueue.AddJob%2A>オーバーロードは、 <xref:System.Boolean>パラメーターがの場合は`false`常に1つのスレッドアパートメントで実行する必要があります。これは、XPSDrv 以外のプリンターが使用されているときに行う必要があります。 ただし、.NET の既定のアパートメント状態は、複数のスレッドになります。 この例では XPSDrv 以外のプリンターを前提にしているため、この既定の状態を逆にする必要があります。

既定の状態を変更する方法は 2 つあります。 1つの方法として<xref:System.STAThreadAttribute> 、アプリケーション`static void Main(string[] args)`の`Main`メソッドの`[System.STAThreadAttribute()]`最初の行 (通常は "") のすぐ上に (つまり、"") を追加するだけです。 ただし、多くのアプリケーションでは`Main` 、メソッドにマルチスレッドアパートメント状態がある必要があるため、2番目のメソッドが<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>あります。の呼び出しを、 <xref:System.Threading.ApartmentState.STA>アパートメント状態がに<xref:System.Threading.Thread.SetApartmentState%2A>設定された別のスレッドに配置します。 次の例では、この 2 番目の方法を使用します。

したがって、この例では、 <xref:System.Threading.Thread>まずオブジェクトをインスタンス化し、 <xref:System.Threading.ThreadStart>パラメーターとして**printxps**メソッドを渡します。 (**PrintXPS** メソッドは、例の後半で定義されます)。次に、そのスレッドをシングル スレッド アパートメントに設定します。 それ以降の `Main` メソッドのコードは、この新しいスレッドを開始します。

この例の要点は、`static`**staticBatchXPSPrinter.PrintXPS** メソッド内にあります。 プリントサーバーとキューを作成した後、メソッドは XPS ファイルを含むディレクトリの入力をユーザーに求めます。 ディレクトリが存在することと\*、そのディレクトリに .xps ファイルが存在することを検証した後、メソッドは、このようなファイルを印刷キューに追加します。 この例では、プリンターが非 XPSDrv であることを前提と`false`しています。 <xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>そのため、メソッドの最後のパラメーターに渡します。 このため、メソッドは、ファイル内の XPS マークアップを、プリンターのページ記述言語への変換を試みる前に検証します。 検証に失敗すると、例外がスローされます。 このコード例では、例外をキャッチし、そのことをユーザーに通知した後、次の XPS ファイルの処理に移ります。

[!code-csharp[BatchPrintXPSFiles#BatchPrintXPSFiles](~/samples/snippets/csharp/VS_Snippets_Wpf/BatchPrintXPSFiles/CSharp/Program.cs#batchprintxpsfiles)]
[!code-vb[BatchPrintXPSFiles#BatchPrintXPSFiles](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BatchPrintXPSFiles/visualbasic/program.vb#batchprintxpsfiles)]

XPSDrv プリンターを使用している場合は、最後のパラメーターを `true` に設定できます。 この場合、XPS はプリンターのページ記述言語であるため、このメソッドは、ファイルを検証したり、別のページ記述言語に変換したりせずに、そのファイルをプリンターに送信します。 アプリケーションが XPSDrv プリンターを使用するかどうかがデザイン時にわからない場合は、アプリケーションを変更して、 <xref:System.Printing.PrintQueue.IsXpsDevice%2A>プロパティを読み取って、内容に従って分岐するようにすることができます。

と Microsoft .NET Framework の[!INCLUDE[TLA#tla_winvista](../../../../includes/tlasharptla-winvista-md.md)]リリース後すぐに使用できる XPSDrv プリンターがほとんどないため、XPSDrv 以外のプリンターを XPSDrv プリンターとして偽装することが必要になる場合があります。 そのためには、アプリケーションを実行しているコンピューターで、以下のレジストリ キーのファイルの一覧に Pipelineconfig.xml を追加します。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Print\Environments\Windows NT x86\Drivers\Version-3\\ *\<PseudoXPSPrinter>* \DependentFiles

ここで、 *\<PseudoXPSPrinter* は任意の印刷キューです。 その後、コンピューターを再起動する必要があります。

このような偽装により、 `true`例外を発生させ<xref:System.Printing.PrintQueue.AddJob%28System.String%2CSystem.String%2CSystem.Boolean%29>ずにの最後のパラメーターとして渡すことができますが、  *\<PseudoXPSPrinter >* は実際には XPSDrv プリンターではないため、出力されるのはガベージのみです。

> [!NOTE]
> わかりやすくするために、上記の例では\*、ファイルが xps であることをテストするために、.xps 拡張子の存在を使用します。 ただし、XPS ファイルにはこの拡張機能は必要ありません。 [Isxps (Isxps 適合性ツール)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa348104(v=vs.100))は、XPS の有効性をテストするための1つの方法です。

## <a name="see-also"></a>関連項目

- <xref:System.Printing.PrintQueue>
- <xref:System.Printing.PrintQueue.AddJob%2A>
- <xref:System.Threading.ApartmentState>
- <xref:System.STAThreadAttribute>
- [XPS ドキュメント](/windows/desktop/printdocs/documents)
- [XPS ドキュメントの印刷](https://docs.microsoft.com/previous-versions/dotnet/netframework-3.5/ms771525(v=vs.90))
- [マネージスレッド処理とアンマネージスレッド処理](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/5s8ee185(v=vs.100))
- [isXPS.exe (isXPS 適合性ツール)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/aa348104(v=vs.100))
- [WPF のドキュメント](documents-in-wpf.md)
- [印刷の概要](printing-overview.md)
