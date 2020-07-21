---
title: ダイアログ ボックスの概要
description: 情報を収集して表示するために使用できる、Windows Foundation Presentation (WPF) のさまざまなダイアログ ボックスについて説明します。
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- modeless dialog boxes [WPF]
- dialog boxes [WPF]
- message boxes [WPF]
- modal dialog boxes [WPF]
ms.assetid: 0d23d544-a393-4a02-a3aa-d8cd5d3d6511
ms.openlocfilehash: 822604dd694f2f6260496872fd7a1a8440a62535
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618143"
---
# <a name="dialog-boxes-overview"></a>ダイアログ ボックスの概要
スタンドアロン アプリケーションには、通常、メイン ウィンドウがあり、そこには、アプリケーションが操作する主なデータが表示され、そのデータをメニュー バー、ツール バー、ステータス バーなどの [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] メカニズムを通じて処理する機能が公開されます。 重要なアプリケーションは、次のようなことをするための追加のウィンドウを表示することもあります。  
  
- 固有の情報をユーザーに表示する。  
  
- ユーザーから情報を収集する。  
  
- 情報の表示と収集の両方を行う。  
  
 これらの種類のウィンドウは "*ダイアログ ボックス*" と呼ばれ、モーダルとモードレスの 2 種類があります。  
  
 "*モーダル*" ダイアログ ボックスは、機能が続行するにはユーザーからの追加データが必要なときに、機能によって表示されます。 機能は、モーダル ダイアログ ボックスに依存してデータを収集するため、モーダル ダイアログ ボックスが開いている間、ユーザーはアプリケーション内の他のウィンドウをアクティブ化することはできません。 ほとんどの場合、ユーザーは **[OK]** または **[キャンセル]** ボタンを押すことによって、モーダル ダイアログ ボックスの操作を終了したことをモーダル ダイアログ ボックスに知らせることができます。 **[OK]** ボタンを押すことは、ユーザーがデータを入力し、そのデータの処理を続行することを機能に求めていることを示します。 **[キャンセル]** ボタンを押すことは、ユーザーが機能の実行を停止することを求めていることを示します。 モーダル ダイアログ ボックスの最も一般的な例は、データを開く、保存する、および印刷するために表示されます。  
  
 一方、"*モードレス*" ダイアログ ボックスは、それが開いている間も、ユーザーは他のウィンドウをアクティブ化できます。 たとえば、ユーザーがドキュメント内の特定の単語の出現箇所を検索する場合、メイン ウィンドウは、多くの場合、ダイアログ ボックスを開いて、検索する単語をユーザーに尋ねます。 しかし、単語の検索中もユーザーはドキュメントを編集できるため、ダイアログ ボックスがモーダルである必要はありません。 モードレス ダイアログ ボックスには、少なくとも、ダイアログ ボックスを閉じる **[閉じる]** ボタンがあり、単語検索の検索条件に一致する次の単語を検索するための **[次を検索]** ボタンなど、特定の機能を実行するための追加のボタンが表示されることもあります。  
  
 Windows Presentation Foundation (WPF) では、メッセージ ボックス、コモン ダイアログ ボックス、カスタム ダイアログ ボックスなど、いくつかの種類のダイアログ ボックスを作成できます。 このトピックでは、それぞれについて説明し、該当する例として、[ダイアログ ボックスのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Windows/DialogBox)を示します。  

<a name="Message_Boxes"></a>
## <a name="message-boxes"></a>メッセージ ボックス  
 "*メッセージ ボックス*" は、テキスト情報を表示するために使用され、ユーザーがボタンで意思決定を行うことができるダイアログ ボックスです。 次の図は、テキスト情報と質問を表示して、ユーザーが質問に回答するための 3 つのボタンを表示するメッセージ ボックスを示しています。  
  
 ![アプリケーションを終了する前にドキュメントへの変更を保存するかどうかを確認する [ワード プロセッサ] ダイアログ ボックス。](./media/dialog-boxes-overview/word-processor-dialog.png)  
  
 メッセージ ボックスを作成するには、<xref:System.Windows.MessageBox> クラスを使用します。 <xref:System.Windows.MessageBox> では、次のようなコードを使用して、メッセージ ボックスのテキスト、タイトル、アイコン、およびボタンを構成できます。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxconfigurecodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxConfigureCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxconfigurecodebehind)]  
  
 メッセージ ボックスを表示するには、次のコードに示されているように、`static`<xref:System.Windows.MessageBox.Show%2A> メソッドを呼び出します。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowcodebehind)]  
  
 メッセージ ボックスを表示するコードで、ユーザーの決定 (どのボタンが押されたか) を検出して処理する必要があるときには、コードは、次のコードに示されているように、メッセージ ボックスの結果を検査できます。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#msgboxshowandresultcodebehind1)]
 [!code-vb[DialogBoxesOverviewSnippets#MsgBoxShowAndResultCODEBEHIND1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#msgboxshowandresultcodebehind1)]  
  
 メッセージ ボックスの使用の詳細については、<xref:System.Windows.MessageBox>、「[メッセージ ボックスのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Windows/MessageBox)」、および「[ダイアログ ボックスのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Windows/DialogBox)」を参照してください。  
  
 <xref:System.Windows.MessageBox> では単純なダイアログ ボックス ユーザー エクスペリエンスを提供できますが、<xref:System.Windows.MessageBox> を使用する利点は XAML ブラウザー アプリケーション (XBAP) など、部分信頼セキュリティ サンドボックス (「[セキュリティ](../security-wpf.md)」を参照) 内で実行するアプリケーションによって表示できる唯一の種類のウィンドウであることです。  
  
 ほとんどのダイアログ ボックスは、テキスト、選択 (チェック ボックス)、相互に排他的な選択 (オプション ボタン)、リスト選択 (リスト ボックス、コンボ ボックス、ドロップダウン リスト ボックス) など、メッセージ ボックスの結果よりも複雑なデータを表示し、収集します。 これらのために、Windows Presentation Foundation (WPF) には、いくつかのコモン ダイアログ ボックスが用意されていて、ユーザー独自のダイアログ ボックスを作成することもできますが、どちらの使用も、完全な信頼で実行しているアプリケーションに限られます。  
  
<a name="Common_Dialogs"></a>
## <a name="common-dialog-boxes"></a>コモン ダイアログ ボックス  
 Windows では、ファイルを開く、ファイルを保存する、印刷するためのダイアログ ボックスなど、すべてのアプリケーションに共通の、さまざまな再利用可能なダイアログ ボックスが実装されます。 これらのダイアログ ボックスはオペレーティング システムによって実装されるため、そのオペレーティング システム上で実行するすべてのアプリケーション間で共有でき、ユーザー エクスペリエンスの一貫性を保つことができます。ユーザーが 1 つのアプリケーションで、オペレーティング システムによって提供されるダイアログ ボックスの使用に慣れると、他のアプリケーションでも、そのダイアログ ボックスの使用法を学ぶ必要はありません。 これらのダイアログ ボックスはすべてのアプリケーションで使用でき、一貫したユーザー エクスペリエンスの提供に役立つため、"*コモン ダイアログ ボックス*" と呼ばれます。  
  
 Windows Presentation Foundation (WPF) では、ファイルを開く、ファイルを保存する、および印刷コモン ダイアログ ボックスがカプセル化され、スタンドアロン アプリケーション内で使用できるマネージド クラスとして公開されます。 このトピックでは、それぞれの概要を簡単に説明します。  
  
<a name="Open_File_Dialog"></a>
### <a name="open-file-dialog"></a>[ファイルを開く] ダイアログ  
 [ファイルを開く] ダイアログ ボックスは、次の図に示されているように、開くファイルの名前を取得するために、ファイルを開く機能によって使用されます。  
  
 ![ファイルを取得する場所を示す、開いているダイアログ ボックス。](./media/dialog-boxes-overview/open-file-dialog-box.png)  
  
 [ファイルを開く] コモン ダイアログ ボックスは、<xref:Microsoft.Win32.OpenFileDialog> クラスとして実装され、<xref:Microsoft.Win32> 名前空間にあります。 次のコードは、[ファイルを開く] ダイアログ ボックスの作成、構成、および表示の方法と、結果を処理する方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#openfiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#OpenFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#openfiledialogboxcodebehind)]  
  
 ファイルを開くダイアログ ボックスの詳細については、「<xref:Microsoft.Win32.OpenFileDialog?displayProperty=nameWithType>」を参照してください。  
  
> [!NOTE]
> <xref:Microsoft.Win32.OpenFileDialog> を使用すると、部分信頼で実行しているアプリケーションがファイル名を安全に取得できます (「[セキュリティ](../security-wpf.md)」を参照)。  
  
<a name="Save_File_Dialog"></a>
### <a name="save-file-dialog-box"></a>[ファイルの保存] ダイアログ ボックス  
 [ファイルの保存] ダイアログ ボックスは、次の図に示されているように、保存するファイルの名前を取得するために、ファイルを保存する機能によって使用されます。  
  
 ![ファイルを取得する場所を示す、[名前を付けて保存] ダイアログ ボックス。](./media/dialog-boxes-overview/save-file-dialog-box.png)  
  
 [ファイルの保存] コモン ダイアログ ボックスは、<xref:Microsoft.Win32.SaveFileDialog> クラスとして実装され、<xref:Microsoft.Win32> 名前空間にあります。 次のコードは、[ファイルを開く] ダイアログ ボックスの作成、構成、および表示の方法と、結果を処理する方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#savefiledialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#SaveFileDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#savefiledialogboxcodebehind)]  
  
 [ファイルの保存] ダイアログ ボックスの詳細については、「<xref:Microsoft.Win32.SaveFileDialog?displayProperty=nameWithType>」を参照してください。  
  
<a name="Print_Dialog"></a>
### <a name="print-dialog-box"></a>[印刷] ダイアログ ボックス

次の図に示されているように、[印刷] ダイアログ ボックスは、ユーザーがデータを印刷するプリンターを選択し、構成するために、印刷機能によって使用されます。  
  
![[印刷] ダイアログ ボックスを表示するスクリーンショット。](./media/dialog-boxes-overview/print-data-dialog-box.png)  
  
[印刷] コモン ダイアログ ボックスは、<xref:System.Windows.Controls.PrintDialog> クラスとして実装され、<xref:System.Windows.Controls> 名前空間にあります。 次のコードは、[印刷] ダイアログ ボックスの作成、構成、および表示の方法を示しています。  
  
 [!code-csharp[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/CSharp/Window1.xaml.cs#printdialogboxcodebehind)]
 [!code-vb[DialogBoxesOverviewSnippets#PrintDialogBoxCODEBEHIND](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxesOverviewSnippets/VisualBasic/window1.xaml.vb#printdialogboxcodebehind)]  
  
 [印刷] ダイアログ ボックスの詳細については、「<xref:System.Windows.Controls.PrintDialog?displayProperty=nameWithType>」を参照してください。 WPF での印刷の詳細については、「[印刷の概要](../advanced/printing-overview.md)」を参照してください。  
  
<a name="Custom_Dialog_Boxes"></a>
## <a name="custom-dialog-boxes"></a>カスタム ダイアログ ボックス

コモン ダイアログ ボックスは便利であり、可能なときにはコモン ダイアログ ボックスを使用する必要がありますが、ドメイン固有のダイアログ ボックスの要件はサポートしていません。 このような場合は、独自のダイアログ ボックスを作成する必要があります。 これから説明するように、ダイアログ ボックスは、特殊な動作を持つウィンドウです。 <xref:System.Windows.Window> は、これらの動作を実装するため、カスタムのモーダルおよびモードレス ダイアログ ボックスを作成するには、<xref:System.Windows.Window> を使用します。  
  
<a name="Creating_a_Modal_Custom_Dialog_Box"></a>
### <a name="creating-a-modal-custom-dialog-box"></a>モーダルのカスタム ダイアログ ボックスの作成

このトピックでは、<xref:System.Windows.Window> を使用して一般的なモーダル ダイアログ ボックス実装を作成する方法を示し、`Margins` ダイアログ ボックスを例として使用します (「[ダイアログ ボックスのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Windows/DialogBox)」を参照)。 `Margins` ダイアログ ボックスを次の図に示します。  
  
 ![左余白、上余白、右余白、および下余白を定義するフィールドを含む [余白] ダイアログ ボックス。](./media/dialog-boxes-overview/margin-size-dialog-box.png)  
  
#### <a name="configuring-a-modal-dialog-box"></a>モーダル ダイアログ ボックスの構成

一般的なダイアログ ボックスのユーザー インターフェイスには、次の項目が含まれます。  
  
- 必要なデータを収集するために必要なさまざまなコントロール。  
  
- ユーザーがクリックすると、ダイアログ ボックスを閉じ、機能に戻り、処理を続行する **[OK]** ボタン。  
  
- ユーザーがクリックすると、ダイアログ ボックスを閉じ、機能が処理を続行するのを停止する **[キャンセル]** ボタン。  
  
- タイトル バーの **[閉じる]** ボタン。  
  
- アイコン。  
  
- **最小化**ボタン、**最大化**ボタン、および**元に戻す**ボタン。  
  
- ダイアログ ボックスを最小化、最大化、元に戻す、および閉じるための **[システム]** メニュー。  
  
- ダイアログ ボックスを開いたウィンドウの中央上の位置。  
  
- 可能な場合は、ダイアログ ボックスが小さすぎないようにサイズを変更し、ユーザーに便利な既定サイズを提供する機能。 これには、既定のディメンションと最小ディメンションの両方を設定する必要があります。  
  
- **[キャンセル]** ボタンを押すことと同じ効果を持つキーボード ショートカットとしての ESC キー。 これを行うには、 **[キャンセル]** ボタンの <xref:System.Windows.Controls.Button.IsCancel%2A> プロパティを `true` に設定します。  
  
- **[OK]** ボタンを押すことと同じ効果を持つキーボード ショートカットとしての ENTER (または RETURN) キー。 これを行うには、 **[OK]** ボタンの <xref:System.Windows.Controls.Button.IsDefault%2A> プロパティを `true` に設定します。  
  
次のコードは、この構成の例を示しています。  
  
[!code-xaml[MarginsDialogBox XAML file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,106-112)]  

[!code-csharp[MarginsDialogBox C# code-behind](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-12,67-68)]
[!code-vb[MarginsDialogBox VB code-behind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-11,61-62)]  
  
ダイアログ ボックスのユーザー エクスペリエンスは、ダイアログ ボックスを開くウィンドウのメニュー バーにも及びます。 メニュー項目が、機能の続行には、ダイアログ ボックスでのユーザーの操作を必要とする機能を実行するときには、次に示されているように、その機能のメニュー項目の見出しに省略記号を付けます。  
  
[!code-xaml[Menu bar of MainWindow.Xaml file](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L26-L27)]  
  
メニュー項目が、[バージョン情報] ダイアログ ボックスなど、ユーザーの操作を必要としないダイアログ ボックスを表示する機能を実行するときには、省略記号は必要ありません。  
  
#### <a name="opening-a-modal-dialog-box"></a>モーダル ダイアログ ボックスを開く

ダイアログ ボックスは、通常、ワード プロセッサでドキュメントの余白を設定するなど、ドメイン固有の機能を実行するためにユーザーがメニュー項目を選択した結果として表示されます。 ウィンドウをダイアログ ボックスとして表示するのは、通常のウィンドウを表示するのと同様ですが、ダイアログ ボックス固有の追加の構成が必要です。 ダイアログ ボックスのインスタンス化、構成、および開くプロセスの全体を、次のコードに示します。  
  
[!code-csharp[Opening a modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-11,78-88,193-195)]
[!code-vb[Opening a modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58-67,130-132)]  

ここでは、コードは、既定の情報 (現在の余白) をダイアログ ボックスに渡しています。 また、<xref:System.Windows.Window.Owner%2A?displayProperty=nameWithType> プロパティに、ダイアログ ボックスを表示しているウィンドウへの参照を設定します。 一般には、常にダイアログ ボックスの所有者を設定して、すべてのダイアログ ボックスに共通のウィンドウ状態に関連する動作を提供する必要があります (詳細については、「[WPF ウィンドウの概要](wpf-windows-overview.md)」を参照してください)。

> [!NOTE]
> ダイアログ ボックスのユーザー インターフェイス (UI) オートメーションを所有者に提供する必要があります (「[UI オートメーションの概要](../../ui-automation/ui-automation-overview.md)」を参照)。

構成されたダイアログ ボックスは、<xref:System.Windows.Window.ShowDialog%2A> メソッドを呼び出すことによって、モーダルとして表示されます。  
  
#### <a name="validating-user-provided-data"></a>ユーザー指定データの検証

ダイアログ ボックスが開かれ、ユーザーが必要なデータを指定すると、ダイアログ ボックスは、指定されたデータが有効であることを確認する必要があります。これは、次のような理由からです。  
  
- セキュリティの観点から、すべての入力を検証する必要があります。  
  
- ドメイン固有の観点から、データの検証は、誤ったデータがコードによって処理されて、例外がスローされるのを防ぎます。  
  
- ユーザー エクスペリエンスの観点から、ダイアログ ボックスは、入力したデータが無効であることを示すことによって、ユーザーを支援できます。  
  
- パフォーマンスの観点から、多層アプリケーションでのデータの検証は、特に、アプリケーションが Web サービスまたはサーバーベースのデータベースで構成される場合、クライアント層とアプリケーション層の間のラウンド トリップの回数を減らすことができます。  

WPF 内でバインド コントロールを検証するには、検証規則を定義して、バインドに関連付ける必要があります。 検証規則は、<xref:System.Windows.Controls.ValidationRule> から派生するカスタム クラスです。 次の例は、バインドされた値が <xref:System.Double> であり、指定された範囲内にあることを確認する検証規則 `MarginValidationRule` を示しています。  

[!code-csharp[Margin validation rules](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginValidationRule.cs)]
[!code-vb[Margin validation rules](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginValidationRule.vb)]  

このコードでは、データを検証して適切な <xref:System.Windows.Controls.ValidationResult> を返す <xref:System.Windows.Controls.ValidationRule.Validate%2A> メソッドをオーバーライドすることによって、検証規則の検証ロジックを実装しています。  

検証規則をバインド コントロールに関連付けるには、次のマークアップを使用します。  
  
[!code-xaml[Associating a validation rule with a control](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml?range=1-16,57-68,111-112)]

検証規則が関連付けられた後、データがバインド コントロールに入力されると、WPF によって検証規則が自動的に適用されます。 コントロールに無効なデータが含まれているときには、次の図に示されているように、無効なコントロールの周囲に赤い境界線が WPF によって表示されます。  
  
![無効な左余白の値の周囲に赤い枠線が付いた[余白] ダイアログ ボックス。](./media/dialog-boxes-overview/invalid-left-margin-dialog.png)  

WPF では、ユーザーが有効なデータを入力するまで、ユーザーが無効なコントロールに制限されるわけではありません。 これは、ダイアログ ボックスとして適切な動作です。データが有効かどうかにかかわらず、ユーザーはダイアログ ボックス内のコントロールを自由に移動できる必要があります。 ただしこれは、ユーザーが無効なデータを入力して、 **[OK]** ボタンをクリックできることを意味します。 このため、 **[OK]** ボタンが押されたときには、コードも <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理することによって、ダイアログ ボックス内のすべてのコントロールを検証する必要はあります。  
  
[!code-csharp[Validating all controls in a dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,26-29,33-68)]
[!code-vb[Validating all controls in a dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27-29,33-62)]  

このコードでは、ウィンドウ上のすべての依存関係オブジェクトが列挙されます。いずれかが無効な場合 (<xref:System.Windows.Controls.Validation.GetHasError%2A> によって返される) は、無効なコントロールがフォーカスを取得し、`IsValid` メソッドでは `false` が返され、ウィンドウは無効とみなされます。  
  
ダイアログ ボックスが有効な場合は、安全に閉じて、戻ることができます。 復帰プロセスの一環として、呼び出し元の機能に結果を返す必要があります。  
  
#### <a name="setting-the-modal-dialog-result"></a>モーダル ダイアログの結果を設定する

<xref:System.Windows.Window.ShowDialog%2A> を使用してダイアログ ボックスを開くことは、基本的にメソッドの呼び出しと似ています。<xref:System.Windows.Window.ShowDialog%2A> を使用してダイアログ ボックスを開いたコードは、<xref:System.Windows.Window.ShowDialog%2A> が戻るまで待機します。 <xref:System.Windows.Window.ShowDialog%2A> が戻ると、それを呼び出したコードは、ユーザーが **[OK]** ボタンを押したか、それとも **[キャンセル]** ボタンを押したかに基づいて、処理を続行するか、それとも処理を停止するかを決定する必要があります。 この決定を容易にするために、ダイアログ ボックスは、ユーザーの選択を <xref:System.Windows.Window.ShowDialog%2A> メソッドから返された <xref:System.Boolean> 値として返す必要があります。  

**[OK]** ボタンがクリックされたときに、<xref:System.Windows.Window.ShowDialog%2A> では `true` を返す必要があります。 このためには、 **[OK]** ボタンがクリックされたときに、ダイアログ ボックスの <xref:System.Windows.Window.DialogResult%2A> プロパティを設定します。  

[!code-csharp[Responding to the OK button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,25-27,32-33,67-68)]
[!code-vb[Responding to the OK button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,27,31-33,61-62)]  

<xref:System.Windows.Window.DialogResult%2A> プロパティを設定すると、ウィンドウも自動的に閉じられるため、<xref:System.Windows.Window.Close%2A> を明示的に呼び出す必要がなくなることに注意してください。  
  
**[キャンセル]** ボタンがクリックされたときには、<xref:System.Windows.Window.ShowDialog%2A> は `false` を返す必要があり、<xref:System.Windows.Window.DialogResult%2A> プロパティを設定する必要もあります。  
  
[!code-csharp[Responding to the Cancel button](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml.cs?range=1-8,19-24,67-68)]
[!code-vb[Responding to the Cancel button](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MarginsDialogBox.xaml.vb?range=1-8,22-25,61-62)]  

ボタンの <xref:System.Windows.Controls.Button.IsCancel%2A> プロパティが `true` に設定され、ユーザーが **[キャンセル]** ボタンか Esc キーを押すと、<xref:System.Windows.Window.DialogResult%2A> は自動的に `false` に設定されます。 次のマークアップは、前のコードと同じ効果を持ち、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理する必要はありません。  
  
[!code-xaml[Markup instead of handling the Click event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MarginsDialogBox.xaml#L109-L109)]  

ユーザーがタイトル バーの **[閉じる]** ボタンを押すか、 **[システム]** メニューの **[閉じる]** メニュー項目を選ぶと、ダイアログ ボックスによって自動的に `false` が返されます。  

#### <a name="processing-data-returned-from-a-modal-dialog-box"></a>モーダル ダイアログ ボックスから返されたデータの処理  

<xref:System.Windows.Window.DialogResult%2A> がダイアログ ボックスによって設定されると、ダイアログ ボックスを開いた機能は、<xref:System.Windows.Window.ShowDialog%2A> が戻ったときに、<xref:System.Windows.Window.DialogResult%2A> プロパティを検査することによって、ダイアログ ボックスの結果を取得することができます。  
  
[!code-csharp[Processing data returned from the modal dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,77-79,89-96,194-195)]
[!code-vb[Processing data returned from the modal dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,58,69-73,131-132)]

ダイアログの結果が `true` の場合、機能ではそれをキューとして使用して、ユーザーによって指定されたデータを取得し、処理します。  
  
> [!NOTE]
> <xref:System.Windows.Window.ShowDialog%2A> が戻った後、ダイアログ ボックスを再び開くことはできません。 代わりに、新しいインスタンスを作成する必要があります。

ダイアログの結果が `false` の場合、機能では処理を適切に終了する必要があります。  
  
<a name="Creating_a_Modeless_Custom_Dialog_Box"></a>
### <a name="creating-a-modeless-custom-dialog-box"></a>モードレス カスタム ダイアログ ボックスの作成

次の図に示されている [検索] ダイアログ ボックスなどのモードレス ダイアログ ボックスは、基本的な外観はモーダル ダイアログ ボックスと同じです。  

![[検索] ダイアログ ボックスを表示するスクリーンショット。](./media/dialog-boxes-overview/find-modeless-dialog-box.png)  

しかし、次のセクションで説明するように、動作は少し異なります。  
  
#### <a name="opening-a-modeless-dialog-box"></a>モードレス ダイアログ ボックスを開く

モードレス ダイアログ ボックスは、<xref:System.Windows.Window.Show%2A> メソッドを呼び出すことによって開かれます。  

[!code-xaml[XAML to define a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml#L21-L22)]  

[!code-csharp[Opening a modeless dialog box](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,65-76,194-195)]
[!code-vb[Openng a modeless dialog box](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,18-23,131,132)]  

<xref:System.Windows.Window.ShowDialog%2A> とは異なり、<xref:System.Windows.Window.Show%2A> は直ちに戻ります。 その結果、呼び出し元のウィンドウは、モードレス ダイアログ ボックスが閉じられたことを知ることができず、したがって、ダイアログ ボックスの結果を確認するタイミングを判断したり、ダイアログ ボックスからデータを取得して、さらに処理したりすることができません。 代わりに、ダイアログ ボックスは、別の方法を作成して、呼び出し元のウィンドウに処理用のデータを返す必要があります。  
  
#### <a name="processing-data-returned-from-a-modeless-dialog-box"></a>モードレス ダイアログ ボックスから返されたデータの処理  

この例では、`FindDialogBox` によって、検索対象のテキストに応じて、特定の頻度ではなく、1 つ以上の検索結果がメイン ウィンドウに返されます。 モーダル ダイアログ ボックスと同様、モードレス ダイアログ ボックスは、プロパティを使用して結果を返すことができます。 ただし、ダイアログ ボックスを所有しているウィンドウは、それらのプロパティを確認するタイミングを知る必要があります。 これを可能にする方法の 1 つは、ダイアログ ボックスで、テキストが見つかったときに発生するイベントを実装することです。 `FindDialogBox` は、この目的で `TextFoundEvent` を実装し、最初にデリゲートを必要とします。  

[!code-csharp[The TextFoundEventHandler delegate](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/TextFoundEventHandler.cs)]
[!code-vb[The TextFoundEventHandler delegate](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/TextFoundEventHandler.vb)]  

`TextFoundEventHandler` デリゲートを使用して、`FindDialogBox` では `TextFoundEvent` が実装されます。
  
[!code-csharp[The TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-17,125-126)]
[!code-vb[The TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-15,102-103)]

その結果、`Find` では、検索結果が見つかった場合にイベントを発生させることができます。  
  
[!code-csharp[Raising the TextFound event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,50-52,91-94,124-127)]
[!code-vb[Raising the TextFound event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,15,60-64,102-103)]  

そのとき、所有者ウィンドウは、このイベントを登録し、処理する必要があります。

[!code-csharp[Registering and handling the event](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/MainWindow.xaml.cs?range=1-10,184-195)]
[!code-vb[Registering and handling the event](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/MainWindow.xaml.vb?range=1-9,126-132)]  

#### <a name="closing-a-modeless-dialog-box"></a>モードレス ダイアログ ボックスを閉じる

<xref:System.Windows.Window.DialogResult%2A> は設定する必要がないため、モードレス ダイアログ ボックスは、次のような、システムによって提供されるメカニズムを使用して閉じることができます。  
  
- タイトル バーの **[閉じる]** ボタンをクリックする。  
  
- Alt キーを押しながら F4 キーを押す。  
  
- **[システム]** メニューの **[閉じる]** を選択する。  
  
または、 **[閉じる]** ボタンがクリックされたときに、コードから <xref:System.Windows.Window.Close%2A> を呼び出すことができます。  

[!code-csharp[Calling the Close method](~/samples/snippets/csharp/VS_Snippets_Wpf/DialogBoxSample/CSharp/FindDialogBox.xaml.cs?range=1-9,119-126)]
[!code-vb[Calling the Close method](~/samples/snippets/visualbasic/VS_Snippets_Wpf/DialogBoxSample/VisualBasic/FindDialogBox.xaml.vb?range=1-9,99-103)]  

## <a name="see-also"></a>関連項目

- [ポップアップの概要](../controls/popup-overview.md)
- [ダイアログ ボックスのサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Windows/DialogBox)
