---
title: メニューの概要
ms.date: 03/30/2017
helpviewer_keywords:
- Menu control [WPF]
- controls [WPF], Menu
ms.assetid: 67df6de5-db96-4c71-b752-af90729a6537
ms.openlocfilehash: 53bc8f10e61b6e4e9e1f3b9a484340d9e2ec2a85
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186971"
---
# <a name="menu-overview"></a>メニューの概要
<xref:System.Windows.Controls.Menu> クラスを使うと、コマンドおよびイベント ハンドラーに関連付けられている要素を階層順に整理できます。 各 <xref:System.Windows.Controls.Menu> 要素には、<xref:System.Windows.Controls.MenuItem> 要素のコレクションが含まれます。  

<a name="menu_control"></a>
## <a name="menu-control"></a>メニュー コントロール  
 <xref:System.Windows.Controls.Menu> コントロールには、アプリケーションのコマンドまたはオプションを指定する項目の一覧が表示されます。 通常、<xref:System.Windows.Controls.MenuItem> をクリックすると、サブメニューが開かれるか、またはアプリケーションによってコマンドが実行されます。  
  
<a name="creating_menus"></a>
## <a name="creating-menus"></a>メニューの作成  
 次の例では、<xref:System.Windows.Controls.TextBox> のテキストを操作するための <xref:System.Windows.Controls.Menu> を作成します。 <xref:System.Windows.Controls.Menu> に含まれる <xref:System.Windows.Controls.MenuItem> オブジェクトでは、<xref:System.Windows.Controls.MenuItem.Command%2A>、<xref:System.Windows.Controls.MenuItem.IsCheckable%2A>、<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> の各プロパティと、<xref:System.Windows.Controls.MenuItem.Checked>、<xref:System.Windows.Controls.MenuItem.Unchecked>、<xref:System.Windows.Controls.MenuItem.Click> の各イベントが使用されます。  
  
 [!code-xaml[MenuItemCommandsAndEvents#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml#1)]  
  
 [!code-csharp[MenuItemCommandsAndEvents#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandsAndEvents/CSharp/Window1.xaml.cs#2)]
 [!code-vb[MenuItemCommandsAndEvents#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandsAndEvents/VisualBasic/Window1.xaml.vb#2)]  
  
<a name="menus_with_shortcutkeys"></a>
## <a name="menuitems-with-keyboard-shortcuts"></a>キーボード ショートカット付きのメニュー項目  
 キーボード ショートカットは、<xref:System.Windows.Controls.Menu> コマンドを呼び出すために、キーボードを使用して入力できる文字の組み合わせです。 たとえば、**コピー**のショートカットは CTRL+C です。 キーボード ショートカットとメニュー項目で使用するプロパティは、<xref:System.Windows.Controls.MenuItem.InputGestureText%2A> または <xref:System.Windows.Controls.MenuItem.Command%2A> の 2 つです。  
  
<a name="menus_inputgesturetext"></a>
### <a name="inputgesturetext"></a>InputGestureText  
 次の例では、<xref:System.Windows.Controls.MenuItem.InputGestureText%2A> プロパティを使用し、キーボード ショートカットのテキストを <xref:System.Windows.Controls.MenuItem> コントロールに割り当てる方法を示します。 これは、キーボード ショートカットをメニュー項目に配置するだけです。  コマンドと <xref:System.Windows.Controls.MenuItem> が関連付けられることはありません。 アプリケーションでは、アクションを実行するために、ユーザーの入力を処理する必要があります。  
  
 [!code-xaml[MenuEvent#6](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#6)]  
  
<a name="menus_commands"></a>
### <a name="command"></a>コマンド  
 次の例では、<xref:System.Windows.Controls.MenuItem.Command%2A> プロパティを使用して、**開く**コマンドと**保存**コマンドを <xref:System.Windows.Controls.MenuItem> コントロールに関連付ける方法を示します。 コマンドのプロパティでは、コマンドと <xref:System.Windows.Controls.MenuItem> が関連付けられるだけでなく、ショートカットとして使用する入力ジェスチャのテキストも提供されます。  
  
 [!code-xaml[MenuEvent#8](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuEvent/CSharp/Pane1.xaml#8)]  
  
 <xref:System.Windows.Controls.MenuItem> クラスには <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> プロパティもあり、このプロパティではコマンドが発生する要素を指定します。 <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> が設定されていない場合は、キーボード フォーカスを持つ要素がコマンドを受信します。 コマンドの詳細については、[Commanding Overview](../advanced/commanding-overview.md)を参照してください。  
  
<a name="menu_styling"></a>
## <a name="menu-styling"></a>メニューのスタイル指定  
 コントロールのスタイル設定では、<xref:System.Windows.Controls.Menu> コントロールの動作と外観を大幅に変更できます。カスタム コントロールを作成する必要はありません。 ビジュアル プロパティの設定の他、<xref:System.Windows.Style> をコントロールの各パーツに適用し、プロパティを使用してコントロールのパーツの動作を変更、パーツを追加またはコントロールのレイアウトを変更できます。 次の例では、<xref:System.Windows.Style> を <xref:System.Windows.Controls.Menu> コントロールに追加するいくつかの方法を示します。  
  
 最初のコード例は、スタイルの現在のシステム設定を使用する方法を示す `Simple` という名前の <xref:System.Windows.Style> を定義します。 このコードは、`MenuHighlightBrush`の色をメニューの背景色として、 `MenuTextBrush`の色をメニューの前景色として割り当てます。 ブラシを割り当てるには、リソース キーを使用することに注意してください。  
  
 [!code-xaml[MenuStylesSnippet#1](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#1)]  
  
 次のサンプルでは、<xref:System.Windows.Controls.Menu> で発生したイベントに応じて <xref:System.Windows.Controls.MenuItem> の外観を変更できる <xref:System.Windows.Trigger> 要素が使用されています。 <xref:System.Windows.Controls.Menu> をポイントすると、メニュー項目の前景色およびフォント文字が変更されます。  
  
 [!code-xaml[MenuStylesSnippet#2](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuStylesSnippet/CS/app.xaml#2)]  
  
## <a name="see-also"></a>関連項目

- [WPF Controls Gallery Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Getting%20Started/ControlsAndLayout)
