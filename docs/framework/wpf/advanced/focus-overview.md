---
title: フォーカスの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- applications [WPF], focus
- focus in applications [WPF]
ms.assetid: 0230c4eb-0c8a-462b-ac4b-ae3e511659f4
ms.openlocfilehash: de788ec3f0628ff2f7c422c76c73ff7985424113
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186669"
---
# <a name="focus-overview"></a>フォーカスの概要
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、キーボード フォーカスと論理フォーカスという、フォーカスに関する 2 つの主要な概念があります。  キーボード フォーカスはキーボード入力を受け取る要素を指し、論理フォーカスはフォーカスを持つフォーカス範囲内の要素を指します。  これらの概念については、この概要で詳しく説明します。  フォーカスを取得可能な領域を複数持つ複雑なアプリケーションを作成する場合は、これらの概念の違いを理解することが重要です。  
  
 フォーカス管理に関与する主要なクラスには、<xref:System.Windows.Input.Keyboard> クラス、<xref:System.Windows.Input.FocusManager> クラス、および <xref:System.Windows.UIElement> や <xref:System.Windows.ContentElement> などの基本要素クラスがあります。  基本要素の詳細については、「[基本要素の概要](base-elements-overview.md)」を参照してください。  
  
 <xref:System.Windows.Input.Keyboard> クラスは主にキーボード フォーカスに関連し、<xref:System.Windows.Input.FocusManager> は主に論理フォーカスに関連しますが、これは絶対的な区別ではありません。  キーボード フォーカスを持つ要素は論理フォーカスも持ちますが、論理フォーカスを持つ要素は必ずしもキーボード フォーカスを持ちません。  <xref:System.Windows.Input.Keyboard> クラスを使用してキーボード フォーカスを持つ要素を設定したときには、要素に論理フォーカスも設定されるので、この違いがよくわかります。  

<a name="Keyboard_Focus"></a>
## <a name="keyboard-focus"></a>キーボード フォーカス  
 キーボード フォーカスは、現在キーボード入力を受け取っている要素を指します。  キーボード フォーカスを持つ要素は、デスクトップ全体で 1 つしかありません。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、キーボード フォーカスを持つ要素は <xref:System.Windows.IInputElement.IsKeyboardFocused%2A> が `true` に設定されます。  <xref:System.Windows.Input.Keyboard> クラスの静的プロパティ <xref:System.Windows.Input.Keyboard.FocusedElement%2A> では、現在キーボード フォーカスを持っている要素が取得されます。  
  
 要素でキーボード フォーカスを取得するには、基本要素で <xref:System.Windows.UIElement.Focusable%2A> プロパティと <xref:System.Windows.UIElement.IsVisible%2A> プロパティを `true` に設定する必要があります。  <xref:System.Windows.Controls.Panel> 基底クラスなどの一部のクラスでは、<xref:System.Windows.UIElement.Focusable%2A> が既定で `false` に設定されます。したがって、そのような要素でキーボード フォーカスを取得できるようにする場合は、<xref:System.Windows.UIElement.Focusable%2A> を `true` に設定する必要があります。  
  
 キーボード フォーカスは、要素への Tab キーでの移動や特定の要素でのマウスのクリックなど、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] でのユーザー操作を通じて取得できます。  キーボード フォーカスは、プログラムで <xref:System.Windows.Input.Keyboard> クラスの <xref:System.Windows.Input.Keyboard.Focus%2A> メソッドを使用して取得することもできます。  <xref:System.Windows.Input.Keyboard.Focus%2A> メソッドでは、指定した要素へのキーボード フォーカスの設定が試みられます。  返される要素はキーボード フォーカスが設定された要素ですが、古いフォーカス オブジェクトまたは新しいフォーカス オブジェクトが要求をブロックする場合は、要求された要素とは異なる可能性があります。  
  
 <xref:System.Windows.Input.Keyboard.Focus%2A> メソッドを使用して、キーボード フォーカスを <xref:System.Windows.Controls.Button> に設定する例を次に示します。  
  
 [!code-csharp[focussample#FocusSampleSetFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplesetfocus)]
 [!code-vb[focussample#FocusSampleSetFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplesetfocus)]  
  
 基底要素クラスの <xref:System.Windows.UIElement.IsKeyboardFocused%2A> プロパティでは、要素にキーボード フォーカスがあるかどうかを示す値が取得されます。  基底要素クラスの <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> プロパティでは、要素またはいずれかの子ビジュアル要素にキーボード フォーカスがあるかどうかを示す値が取得されます。  
  
 アプリケーションの起動時に初期フォーカスを設定する場合は、フォーカスを受け取る要素が、アプリケーションによって読み込まれる初期ウィンドウのビジュアル ツリーに含まれていて、<xref:System.Windows.UIElement.Focusable%2A> と <xref:System.Windows.UIElement.IsVisible%2A> が `true` に設定されている必要があります。  初期フォーカスは <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーで設定することをお勧めします。  <xref:System.Windows.Threading.Dispatcher> コールバックは、<xref:System.Windows.Threading.Dispatcher.Invoke%2A> または <xref:System.Windows.Threading.Dispatcher.BeginInvoke%2A> を呼び出して使用することもできます。  
  
<a name="Logical_Focus"></a>
## <a name="logical-focus"></a>論理フォーカス  
 論理フォーカスでは、フォーカス範囲内の <xref:System.Windows.Input.FocusManager.FocusedElement%2A?displayProperty=nameWithType> が参照されます。  フォーカス範囲は、その範囲内の <xref:System.Windows.Input.FocusManager.FocusedElement%2A> を追跡する要素です。  キーボード フォーカスがフォーカス範囲を離れると、フォーカスがある要素はキーボード フォーカスを失いますが、論理フォーカスは引き続き保持します。  キーボード フォーカスがフォーカス範囲に戻ると、フォーカスがある要素はキーボード フォーカスを取得します。  これにより、キーボード フォーカスが複数のフォーカス範囲間で変更されても、フォーカスがフォーカス範囲に戻ると、そのフォーカス範囲内のフォーカスがある要素はキーボード フォーカスを取り戻すことができます。  
  
 アプリケーションでは、複数の要素が論理フォーカスを持つことがありますが、特定のフォーカス範囲で論理フォーカスを持つ要素は 1 つだけに限られます。  
  
 キーボード フォーカスを持つ要素は、その要素が属するフォーカス範囲の論理フォーカスを持ちます。  
  
 <xref:System.Windows.Input.FocusManager> の添付プロパティ <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> を `true` に設定することにより、要素を [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] のフォーカス範囲内にすることができます。  コードでは、<xref:System.Windows.Input.FocusManager.SetIsFocusScope%2A> を呼び出すことにより、要素をフォーカス範囲内にすることができます。  
  
 <xref:System.Windows.Input.FocusManager.IsFocusScope%2A> 添付プロパティを設定して、<xref:System.Windows.Controls.StackPanel> をフォーカス範囲内にする例を次に示します。  
  
 [!code-xaml[MarkupSnippets#MarkupIsFocusScopeXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupisfocusscopexaml)]  
  
 [!code-csharp[FocusSnippets#FocusSetIsFocusScope](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focussetisfocusscope)]
 [!code-vb[FocusSnippets#FocusSetIsFocusScope](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focussetisfocusscope)]  
  
 <xref:System.Windows.Input.FocusManager.GetFocusScope%2A> では、指定した要素のフォーカス範囲が返されます。  
  
 既定でフォーカス範囲になる、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のクラスは、<xref:System.Windows.Window>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Controls.ToolBar>、および <xref:System.Windows.Controls.ContextMenu> です。  
  
 <xref:System.Windows.Input.FocusManager.GetFocusedElement%2A> を使うと、指定したフォーカス範囲のフォーカスを持つ要素を取得できます。  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> を使うと、指定したフォーカス範囲でフォーカスを持つ要素を設定できます。  <xref:System.Windows.Input.FocusManager.SetFocusedElement%2A> は、通常、最初にフォーカスを得る要素を設定するために使用します。  
  
 フォーカス範囲にフォーカスを持つ要素を設定し、フォーカス範囲のフォーカスを持つ要素を取得する例を次に示します。  
  
 [!code-csharp[FocusSnippets#FocusGetSetFocusedElement](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSnippets/CSharp/Window1.xaml.cs#focusgetsetfocusedelement)]
 [!code-vb[FocusSnippets#FocusGetSetFocusedElement](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSnippets/visualbasic/window1.xaml.vb#focusgetsetfocusedelement)]  
  
<a name="Keyboard_Navigation"></a>
## <a name="keyboard-navigation"></a>キーボード ナビゲーション  
 <xref:System.Windows.Input.KeyboardNavigation> クラスにより、ナビゲーション キーのいずれかが押されたときに、既定のキーボード フォーカスのナビゲーションが実装されます。  ナビゲーション キーは次のとおりです: Tab、Shift + Tab、Ctrl + Tab、Ctrl + Shift + Tab、上方向、下方向、左方向、右方向の各キー。  
  
 ナビゲーション コンテナーのナビゲーション動作は、<xref:System.Windows.Input.KeyboardNavigation> の添付プロパティ <xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A>、<xref:System.Windows.Input.KeyboardNavigation.ControlTabNavigation%2A>、<xref:System.Windows.Input.KeyboardNavigation.DirectionalNavigation%2A> を設定することにより変更できます。  これらのプロパティは <xref:System.Windows.Input.KeyboardNavigationMode> 型であり、指定可能な値は <xref:System.Windows.Input.KeyboardNavigationMode.Continue>、<xref:System.Windows.Input.KeyboardNavigationMode.Local>、<xref:System.Windows.Input.KeyboardNavigationMode.Contained>、<xref:System.Windows.Input.KeyboardNavigationMode.Cycle>、<xref:System.Windows.Input.KeyboardNavigationMode.Once>、および <xref:System.Windows.Input.KeyboardNavigationMode.None> です。  既定値は <xref:System.Windows.Input.KeyboardNavigationMode.Continue> であり、これは要素がナビゲーション コンテナーではないことを意味します。  
  
 複数の <xref:System.Windows.Controls.MenuItem> オブジェクトを使用して <xref:System.Windows.Controls.Menu> を作成する例を次に示します。  <xref:System.Windows.Controls.Menu> では、<xref:System.Windows.Input.KeyboardNavigation.TabNavigation%2A> 添付プロパティが <xref:System.Windows.Input.KeyboardNavigationMode.Cycle> に設定されます。  <xref:System.Windows.Controls.Menu> 内で Tab キーを使用してフォーカスを変更すると、各要素間をフォーカスが移動し、最後の要素に達すると最初の要素にフォーカスが戻ります。  
  
 [!code-xaml[MarkupSnippets#MarkupKeyboardNavigationTabNavigationXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml#markupkeyboardnavigationtabnavigationxaml)]  
  
 [!code-csharp[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](~/samples/snippets/csharp/VS_Snippets_Wpf/MarkupSnippets/CSharp/Window1.xaml.cs#markupkeyboardnavigationtabnavigationcode)]
 [!code-vb[MarkupSnippets#MarkupKeyboardNavigationTabNavigationCODE](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MarkupSnippets/visualbasic/window1.xaml.vb#markupkeyboardnavigationtabnavigationcode)]  
  
<a name="Manipulating_Focus_Programmatically"></a>
## <a name="navigating-focus-programmatically"></a>プログラムによるフォーカスのナビゲーション  
 フォーカスを操作するための追加の API は、<xref:System.Windows.UIElement.MoveFocus%2A> と <xref:System.Windows.UIElement.PredictFocus%2A> です。  
  
 <xref:System.Windows.FrameworkElement.MoveFocus%2A> では、アプリケーション内の次の要素にフォーカスが変更されます。  <xref:System.Windows.Input.TraversalRequest> は、方向を指定するために使用されます。   <xref:System.Windows.UIElement.MoveFocus%2A> に渡す <xref:System.Windows.Input.FocusNavigationDirection> では、<xref:System.Windows.Input.FocusNavigationDirection.First>、<xref:System.Windows.Input.FocusNavigationDirection.Last>、<xref:System.Windows.Input.FocusNavigationDirection.Up>、<xref:System.Windows.Input.FocusNavigationDirection.Down> など、フォーカスを移動できるさまざまな方向を指定します。  
  
 <xref:System.Windows.FrameworkElement.MoveFocus%2A> を使用してフォーカスがある要素を変更する例を次に示します。  
  
 [!code-csharp[focussample#FocusSampleMoveFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/FocusSample/CSharp/Window1.xaml.cs#focussamplemovefocus)]
 [!code-vb[focussample#FocusSampleMoveFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/FocusSample/visualbasic/window1.xaml.vb#focussamplemovefocus)]  
  
 <xref:System.Windows.FrameworkElement.PredictFocus%2A> では、フォーカスが変更された場合にフォーカスを受け取るオブジェクトが返されます。  現時点で <xref:System.Windows.FrameworkElement.PredictFocus%2A> によってサポートされているのは、<xref:System.Windows.Input.FocusNavigationDirection.Up>、<xref:System.Windows.Input.FocusNavigationDirection.Down>、<xref:System.Windows.Input.FocusNavigationDirection.Left>、<xref:System.Windows.Input.FocusNavigationDirection.Right> だけです。  
  
<a name="Focus_Events"></a>
## <a name="focus-events"></a>フォーカス イベント  
 キーボード フォーカスに関連するイベントには、<xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus>、<xref:System.Windows.Input.Keyboard.GotKeyboardFocus>、<xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocus>、<xref:System.Windows.Input.Keyboard.LostKeyboardFocus> があります。  イベントは、<xref:System.Windows.Input.Keyboard> クラスで添付イベントとして定義されていますが、基底要素クラスで同等のルーティング イベントとしてより簡単にアクセスできます。  イベントの詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
 <xref:System.Windows.Input.Keyboard.GotKeyboardFocus> は、要素がキーボード フォーカスを取得したときに発生します。  <xref:System.Windows.Input.Keyboard.LostKeyboardFocus> は、要素がキーボード フォーカスを失ったときに発生します。  <xref:System.Windows.Input.Keyboard.PreviewGotKeyboardFocus> イベントまたは <xref:System.Windows.Input.Keyboard.PreviewLostKeyboardFocusEvent> イベントが処理され、<xref:System.Windows.RoutedEventArgs.Handled%2A> が `true` に設定されると、フォーカスは変更されなくなります。  
  
 <xref:System.Windows.UIElement.GotKeyboardFocus> イベント ハンドラーと <xref:System.Windows.UIElement.LostKeyboardFocus> イベント ハンドラーを <xref:System.Windows.Controls.TextBox> に添付する例を次に示します。  
  
 [!code-xaml[keyboardsample#KeyboardSampleXAMLHandlerHookup](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml#keyboardsamplexamlhandlerhookup)]  
  
 <xref:System.Windows.Controls.TextBox> がキーボード フォーカスを取得すると、<xref:System.Windows.Controls.TextBox> の <xref:System.Windows.Controls.Control.Background%2A> プロパティが <xref:System.Windows.Media.Brushes.LightBlue%2A> に変更されます。  
  
 [!code-csharp[keyboardsample#KeyboardSampleGotFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplegotfocus)]
 [!code-vb[keyboardsample#KeyboardSampleGotFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplegotfocus)]  
  
 <xref:System.Windows.Controls.TextBox> がキーボード フォーカスを失うと、<xref:System.Windows.Controls.TextBox> の <xref:System.Windows.Controls.Control.Background%2A> プロパティが白に戻ります。  
  
 [!code-csharp[keyboardsample#KeyboardSampleLostFocus](~/samples/snippets/csharp/VS_Snippets_Wpf/KeyboardSample/CSharp/Window1.xaml.cs#keyboardsamplelostfocus)]
 [!code-vb[keyboardsample#KeyboardSampleLostFocus](~/samples/snippets/visualbasic/VS_Snippets_Wpf/KeyboardSample/visualbasic/window1.xaml.vb#keyboardsamplelostfocus)]  
  
 論理フォーカスに関連するイベントは、<xref:System.Windows.UIElement.GotFocus> および <xref:System.Windows.UIElement.LostFocus> です。  これらのイベントは、<xref:System.Windows.Input.FocusManager> で添付イベントとして定義されていますが、<xref:System.Windows.Input.FocusManager> はで CLR イベント ラッパーは公開されません。  <xref:System.Windows.UIElement> および <xref:System.Windows.ContentElement> では、これらのイベントがより使いやすい形で公開されています。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Input.FocusManager>
- <xref:System.Windows.UIElement>
- <xref:System.Windows.ContentElement>
- [入力の概要](input-overview.md)
- [基本要素の概要](base-elements-overview.md)
