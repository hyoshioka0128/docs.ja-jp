---
title: WPF で Win32 コントロールをホストする
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Win32 control in WPF [WPF]
- Win32 code [WPF], WPF interoperation
ms.assetid: a676b1eb-fc55-4355-93ab-df840c41cea0
ms.openlocfilehash: 5185e60640c652b79bd105db54830ac3acc57129
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186750"
---
# <a name="walkthrough-host-a-win32-control-in-wpf"></a>チュートリアル: WPF で Win32 コントロールをホストする
Windows Presentation Foundation (WPF) では、アプリケーションを作成するための充実した環境が提供されます。 ただし、Win32 コードにかなりの投資がある場合は、それを完全に書き換えるより、そのコードの一部でも WPF アプリケーションで再利用する方が効率的な場合があります。 WPF には、WPF ページで Win32 ウィンドウをホストするための簡単なメカニズムがあります。  
  
 このトピックでは、Win32 のリスト ボックス コントロールをホストするアプリケーション ([WPF で Win32 の ListBox コントロールをホストするサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control)) について説明します。 この一般的な手順を拡張し、任意の Win32 ウィンドウをホストできます。  

<a name="requirements"></a>
## <a name="requirements"></a>必要条件  
 このトピックは、WPF と Windows API 両方のプログラミングについての基本的な知識があることを前提としています。 WPF のプログラミングの基本的な概要については、[概要](../getting-started/index.md)に関する記事を参照してください。 Windows API のプログラミングの概要については、この主題に関する数多くの書籍 (特に Charles Petzold の『*Programming Windows (プログラミング Windows)* 』) を参照してください。  
  
 このトピックに付属するサンプルは C# で実装されているため、Windows API へのアクセスにはプラットフォーム呼び出しサービス (PInvoke) が使用されています。 PInvoke の知識があると役に立ちますが、必須ではありません。  
  
> [!NOTE]
> このトピックには、関連するサンプルからのコード例が多数含まれています。 しかし、読みやすくするため、完全なサンプル コードは含まれていません。 完全なコードは、[WPF で Win32 の ListBox コントロールをホストするサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control)のページで取得または表示できます。  
  
<a name="basic_procedure"></a>
## <a name="the-basic-procedure"></a>基本手順  
 このセクションでは、WPF ページで Win32 ウィンドウをホストするための基本手順の概要を説明します。 残りのセクションでは、各ステップについて詳細に説明します。  
  
 基本的なホスティング手順は次のとおりです。  
  
1. ウィンドウをホストするための WPF ページを実装します。 たとえば、<xref:System.Windows.Controls.Border> 要素を作成し、ページのセクションをホストされるウィンドウ用に予約します。  
  
2. コントロールをホストするために、<xref:System.Windows.Interop.HwndHost> を継承するクラスを実装します。  
  
3. そのクラスで、<xref:System.Windows.Interop.HwndHost> クラスのメンバー <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> をオーバーライドします。  
  
4. WPF ページを含むウィンドウの子として、ホストされるウィンドウを作成します。 従来の WPF プログラミングでは明示的にそれを使用する必要はありませんが、ホストするページはハンドル (HWND) を持つウィンドウです。 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> メソッドの `hwndParent` パラメーターを使用して、ページの HWND を受け取ります。 ホストされるウィンドウは、この HWND の子として作成する必要があります。  
  
5. ホスト ウィンドウを作成したら、ホストされるウィンドウの HWND を返します。 Win32 コントロールをホストする場合は、通常、HWND の子としてホスト ウィンドウを作成し、コントロールをそのホスト ウィンドウの子にします。 ホスト ウィンドウでコントロールをラップすると、WPF ページでコントロールからの通知を簡単に受け取ることができるようになり、HWND の境界を越える通知に関する特定の Win32 の問題に対処できます。  
  
6. 子コントロールからの通知など、ホスト ウィンドウに送信されるように選択されたメッセージを処理します。 これには、2 つの方法があります。  
  
    - ホスティング クラスでメッセージを処理したい場合は、<xref:System.Windows.Interop.HwndHost> クラスの <xref:System.Windows.Interop.HwndHost.WndProc%2A> メソッドをオーバーライドします。  
  
    - WPF でメッセージを処理したい場合は、コードビハインドで <xref:System.Windows.Interop.HwndHost> クラスの <xref:System.Windows.Interop.HwndHost.MessageHook> イベントを処理します。 このイベントは、ホストされているウィンドウが受信するすべてのメッセージに対して発生します。 このオプションを選択した場合でも、<xref:System.Windows.Interop.HwndHost.WndProc%2A> をオーバーライドする必要がありますが、最低限の実装のみが必要です。  
  
7. <xref:System.Windows.Interop.HwndHost> の <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> メソッドと <xref:System.Windows.Interop.HwndHost.WndProc%2A> メソッドをオーバーライドします。 <xref:System.Windows.Interop.HwndHost> のコントラクトを満たすようにこれらのメソッドをオーバーライドする必要がありますが、必要なのは最小限の実装だけです。  
  
8. 分離コード ファイルで、コントロール ホスティング クラスのインスタンスを作成し、ウィンドウをホストするための <xref:System.Windows.Controls.Border> 要素の子にします。  
  
9. Microsoft Windows メッセージを送信し、子ウィンドウからのメッセージ (コントロールによって送信された通知など) を処理することによって、ホストされたウィンドウと通信します。  
  
<a name="page_layout"></a>
## <a name="implement-the-page-layout"></a>ページ レイアウトを実装する  
 ListBox コントロールをホストする WPF ページのレイアウトは、2 つの領域で構成されます。 ページの左側では、Win32 コントロールを操作するための[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] を提供するいくつかの WPF コントロールがホストされています。 ページの右上隅には、ホストされた ListBox コントロールのための四角形の領域があります。  
  
 このレイアウトを実装するコードは非常に単純です。 ルート要素は、2 つの子要素を持つ <xref:System.Windows.Controls.DockPanel> です。 1 つ目は、ListBox コントロールをホストする <xref:System.Windows.Controls.Border> 要素です。 ページの右上隅の 200 x 200 の正方形を占めます。 2 つ目は <xref:System.Windows.Controls.StackPanel> 要素で、情報を表示し、公開される相互運用プロパティを設定することによって ListBox コントロールを操作できる、一連の WPF コントロールが含まれます。 <xref:System.Windows.Controls.StackPanel> の子である各要素の説明や機能について詳しくは、使用されているさまざまな要素のリファレンス資料を参照してください。これらは以下のコード例に記載されていますが、ここでは説明しません (基本的な相互運用モデルにはそれらは必要なく、サンプルに対話機能を追加するために提供されてます)。  
  
 [!code-xaml[WPFHostingWin32Control#WPFUI](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml#wpfui)]  
  
<a name="host_class"></a>
## <a name="implement-a-class-to-host-the-microsoft-win32-control"></a>Microsoft Win32 コントロールをホストするクラスを実装する  
 このサンプルの中核となるのは、コントロールを実際にホストするクラスである ControlHost.cs です。 <xref:System.Windows.Interop.HwndHost> から継承します。 コンストラクターが受け取る 2 つのパラメーター height と width は、ListBox コントロールをホストする <xref:System.Windows.Controls.Border> 要素の高さと幅に対応しています。 後でこれらの値を使用して、コントロールのサイズが <xref:System.Windows.Controls.Border> 要素と一致するようにします。  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostClass](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostclass)]
 [!code-vb[WPFHostingWin32Control#ControlHostClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostclass)]  
  
 定数のセットもあります。 これらの定数のほとんどは Winuser.h から取得され、Win32 関数を呼び出すときは従来の名前を使用できます。  
  
 [!code-csharp[WPFHostingWin32Control#ControlHostConstants](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#controlhostconstants)]
 [!code-vb[WPFHostingWin32Control#ControlHostConstants](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#controlhostconstants)]  
  
<a name="buildwindowcore"></a>
### <a name="override-buildwindowcore-to-create-the-microsoft-win32-window"></a>BuildWindowCore をオーバーライドして Microsoft Win32 ウィンドウを作成する  
 このメソッドをオーバーライドして、ページによってホストされる Win32 ウィンドウを作成し、ウィンドウとページの間の接続を確立します。 このサンプルには ListBox コントロールのホスティングが含まれているため、2 つのウィンドウを作成します。 1 つ目は、WPF ページによって実際にホストされるウィンドウです。 ListBox コントロールは、そのウィンドウの子として作成されます。  
  
 このような方法を使用するのは、コントロールからの通知を受け取るプロセスを簡略化するためです。 <xref:System.Windows.Interop.HwndHost> クラスを使用すると、ホストされているウィンドウに送信されたメッセージを処理できます。 Win32 コントロールを直接ホストする場合は、コントロールの内部メッセージ ループに送信されたメッセージを受け取ります。 コントロールを表示してメッセージを送ることはできますが、コントロールから親ウィンドウに送られた通知を受け取ることはありません。 これは特に、ユーザーがコントロールを操作したことを検出する手段がないことを意味します。 代わりに、ホスト ウィンドウを作成し、コントロールをそのウィンドウの子にします。 これにより、コントロールによって送られる通知も含めて、ホスト ウィンドウに対するメッセージを処理できます。 便宜上、ホスト ウィンドウはコントロールに対する単なるラッパーと大差ないので、パッケージを ListBox コントロールと呼びます。  
  
<a name="create_the_window_and_listbox"></a>
#### <a name="create-the-host-window-and-listbox-control"></a>ホスト ウィンドウと ListBox コントロールを作成する  
 PInvoke を使用して、ウィンドウ クラスなどを作成して登録することにより、コントロールのホスト ウィンドウを作成できます。 ただし、定義済みの "静的" ウィンドウ クラスを使用してウィンドウを作成する方が、はるかに簡単です。 これにより、コントロールからの通知を受け取るために必要なウィンドウ プロシージャが提供され、必要なコーディングが最小限になります。  
  
 コントロールの HWND は読み取り専用のプロパティで公開されるため、ホスト ページでは、このプロパティを使用して、コントロールにメッセージを送信できます。  
  
 [!code-csharp[WPFHostingWin32Control#IntPtrProperty](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#intptrproperty)]
 [!code-vb[WPFHostingWin32Control#IntPtrProperty](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#intptrproperty)]  
  
 ListBox コントロールは、ホスト ウィンドウの子として作成されます。 両方のウィンドウの高さと幅は、前に説明したように、コンストラクターに渡される値に設定されます。 これにより、ホスト ウィンドウとコントロールのサイズは、ページ上の予約領域と同じになります。  ウィンドウが作成された後、サンプルではホスト ウィンドウの HWND が含まれる <xref:System.Runtime.InteropServices.HandleRef> オブジェクトが返されます。  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCore](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcore)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCore](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcore)]  
  
 [!code-csharp[WPFHostingWin32Control#BuildWindowCoreHelper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#buildwindowcorehelper)]
 [!code-vb[WPFHostingWin32Control#BuildWindowCoreHelper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#buildwindowcorehelper)]  
  
<a name="destroywindow_wndproc"></a>
### <a name="implement-destroywindow-and-wndproc"></a>DestroyWindow と WndProc を実装する  
 <xref:System.Windows.Interop.HwndHost.BuildWindowCore%2A> に加えて、<xref:System.Windows.Interop.HwndHost> の <xref:System.Windows.Interop.HwndHost.WndProc%2A> メソッドと <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> メソッドもオーバーライドする必要があります。 この例では、コントロールへのメッセージは <xref:System.Windows.Interop.HwndHost.MessageHook> ハンドラーによって処理されるため、<xref:System.Windows.Interop.HwndHost.WndProc%2A> と <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> の実装は最小限に抑えられます。 <xref:System.Windows.Interop.HwndHost.WndProc%2A> の場合は、`handled` を `false` に設定して、メッセージが処理されなかったことを示し、0 を返します。 <xref:System.Windows.Interop.HwndHost.DestroyWindowCore%2A> の場合は、単にウィンドウを破棄します。  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroy](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroy)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroy](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroy)]  
  
 [!code-csharp[WPFHostingWin32Control#WndProcDestroyHelper](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/ControlHost.cs#wndprocdestroyhelper)]
 [!code-vb[WPFHostingWin32Control#WndProcDestroyHelper](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/ControlHost.vb#wndprocdestroyhelper)]  
  
<a name="host_the_control"></a>
## <a name="host-the-control-on-the-page"></a>ページでコントロールをホストする  
 ページでコントロールをホストするには、最初に `ControlHost` クラスの新しいインスタンスを作成します。 コントロールを含む境界要素の高さと幅 (`ControlHostElement`) を、`ControlHost` コンストラクターに渡します。 これにより、ListBox のサイズが正しく設定されます。 次に、ホスト <xref:System.Windows.Controls.Border> の <xref:System.Windows.Controls.Decorator.Child%2A> プロパティに `ControlHost` オブジェクトを割り当てることによって、ページでコントロールをホストします。  
  
 このサンプルでは、コントロールからメッセージを受け取るため、`ControlHost` の <xref:System.Windows.Interop.HwndHost.MessageHook> イベントにハンドラーをアタッチします。 このイベントは、ホストされているウィンドウに送られるすべてのメッセージで発生します。 この場合は、コントロールからの通知など、実際の ListBox コントロールをラップするウィンドウに送られるメッセージです。 サンプルでは、SendMessage を呼び出して、コントロールから情報を取得し、その内容を変更します。 ページがコントロールと通信する方法の詳細については、次のセクションで説明します。  
  
> [!NOTE]
> SendMessage に対して PInvoke の宣言が 2 つあることに注意してください。 1 つでは `wParam` パラメーターを使用して文字列を渡し、もう 1 つではそれを使用して整数を渡すため、このようにする必要があります。 データが正しくマーシャリングされるようにするには、シグネチャごとに個別の宣言が必要です。  
  
 [!code-csharp[WPFHostingWin32Control#HostWindowClass](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#hostwindowclass)]
 [!code-vb[WPFHostingWin32Control#HostWindowClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#hostwindowclass)]  
  
 [!code-csharp[WPFHostingWin32Control#ControlMsgFilterSendMessage](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#controlmsgfiltersendmessage)]
 [!code-vb[WPFHostingWin32Control#ControlMsgFilterSendMessage](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#controlmsgfiltersendmessage)]  
  
<a name="communication"></a>
## <a name="implement-communication-between-the-control-and-the-page"></a>コントロールとページの間の通信を実装する  
 Windows メッセージをコントロールに送信して、コントロールを操作します。 ユーザーがコントロールを操作すると、コントロールからホスト ウィンドウに通知が送られます。 [WPF で Win32 の ListBox コントロールをホストする](https://github.com/Microsoft/WPF-Samples/tree/master/Migration%20and%20Interoperability/WPFHostingWin32Control)サンプルには、このしくみのいくつかの例を示す UI が含まれています。  
  
- リストに項目を追加します。  
  
- 選択した項目をリストから削除します  
  
- 現在選択されている項目のテキストを表示します。  
  
- リスト内の項目の数を表示します。  
  
 ユーザーは、従来の Win32 アプリケーションの場合と同様に、リスト ボックス内の項目をクリックして選択することもできます。 表示されるデータは、ユーザーが項目を選択したり追加したりすることによってリスト ボックスの状態を変更するたびに、更新されます。  
  
 項目を追加するには、リスト ボックスに [`LB_ADDSTRING` メッセージ](/windows/desktop/Controls/lb-addstring)を送信します。 項目を削除するには、[`LB_GETCURSEL`](/windows/desktop/Controls/lb-getcursel) を送信して現在選択されている項目のインデックスを取得した後、[`LB_DELETESTRING`](/windows/desktop/Controls/lb-deletestring) を送信して項目を削除します。 サンプルでは、[`LB_GETCOUNT`](/windows/desktop/Controls/lb-getcount) も送信され、返された値を使用して項目数を示す表示が更新されます。 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) のどちらのインスタンスでも、前のセクションで説明した PInvoke の宣言のいずれかが使用されます。  
  
 [!code-csharp[WPFHostingWin32Control#AppendDeleteText](~/samples/snippets/csharp/VS_Snippets_Wpf/WPFHostingWin32Control/CSharp/Page1.xaml.cs#appenddeletetext)]
 [!code-vb[WPFHostingWin32Control#AppendDeleteText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/WPFHostingWin32Control/VisualBasic/Page1.xaml.vb#appenddeletetext)]  
  
 ユーザーが項目を選択するか、選択を変更すると、コントロールによって [`WM_COMMAND` メッセージ](/windows/desktop/menurc/wm-command)が送信されてホスト ウィンドウに通知され、これによりページに対する <xref:System.Windows.Interop.HwndHost.MessageHook> イベントが発生します。 ハンドラーは、ホスト ウィンドウのメイン ウィンドウ プロシージャと同じ情報を受け取ります。 また、ブール値 `handled` への参照も渡されます。 メッセージの処理が済み、それ以上の処理は必要ないことを示すには、`handled` を `true` に設定します。  
  
 [`WM_COMMAND`](/windows/desktop/menurc/wm-command) はさまざまな理由で送信されるため、通知 ID を調べて、処理する必要のあるイベントかどうかを確認する必要があります。 ID は、`wParam` パラメーターの上位ワードに格納されています。 サンプルでは、ビットごとの演算子を使用して ID が抽出されます。 ユーザーが選択を行うか変更した場合、ID は [`LBN_SELCHANGE`](/windows/desktop/Controls/lbn-selchange) になります。  
  
 [`LBN_SELCHANGE`](/windows/desktop/Controls/lbn-selchange) を受け取ると、サンプルでは、コントロールに [`LB_GETCURSEL` メッセージ](/windows/desktop/Controls/lb-getcursel)を送信することによって、選択された項目のインデックスが取得されます。 テキストを取得するには、最初に <xref:System.Text.StringBuilder> を作成します。 その後、コントロールに [`LB_GETTEXT` メッセージ](/windows/desktop/Controls/lb-gettext)を送信します。 `wParam` パラメーターとして空の <xref:System.Text.StringBuilder> オブジェクトを渡します。 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) から戻った時点で、<xref:System.Text.StringBuilder> には選択された項目のテキストが格納されています。 [`SendMessage`](/windows/desktop/api/winuser/nf-winuser-sendmessage) をこのように使用するには、PInvoke の宣言がもう 1 つ必要です。  
  
 最後に、`handled` を `true` に設定して、メッセージが処理されたことを示します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.HwndHost>
- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
- [チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)
