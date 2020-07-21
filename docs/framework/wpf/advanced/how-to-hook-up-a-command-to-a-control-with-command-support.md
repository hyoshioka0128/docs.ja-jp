---
title: '方法: コマンドをサポートするコントロールにコマンドをフックする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Control class [WPF], attaching a RoutedCommand
- classes [WPF], Control [WPF], attaching a RoutedCommand
- RoutedCommand class [WPF], attaching to a Control
- classes [WPF], RoutedCommand [WPF], attaching to a Control
ms.assetid: 8d8592ae-0c91-469e-a1cd-d179c4544548
ms.openlocfilehash: 981fecf33b60c76ecab760185db7dab4bbb254d7
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61757249"
---
# <a name="how-to-hook-up-a-command-to-a-control-with-command-support"></a>方法: コマンドをサポートするコントロールにコマンドをフックする
次の例では、コマンドのサポートが組み込まれている <xref:System.Windows.Controls.Control> に <xref:System.Windows.Input.RoutedCommand> をフックする方法を示します。  コマンドを複数のソースに関連付けるサンプル全体については、「[カスタム RoutedCommand の作成のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)」を参照してください。  
  
## <a name="example"></a>例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、アプリケーション プログラマがよく使用する一般的なコマンドのライブラリが用意されています。  コマンド ライブラリを構成するクラスは、<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.ComponentCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.MediaCommands>、<xref:System.Windows.Documents.EditingCommands> です。  
  
 これらのクラスを構成する静的な <xref:System.Windows.Input.RoutedCommand> オブジェクトには、コマンド ロジックが用意されていません。  コマンドのロジックは、<xref:System.Windows.Input.CommandBinding> でコマンドに関連付けられます。  一部のコントロールには、コマンドの CommandBindings が組み込まれています。  これにより、コマンドの意味は変わりませんが、実際の実装は変わる場合があります。  たとえば、<xref:System.Windows.Controls.TextBox> は、<xref:System.Windows.Input.ApplicationCommands.Paste%2A> コマンドの処理方法が、イメージをサポートするよう設計されたコントロールとは異なります。ただし、何かを貼り付けるという基本的な概念は変わりません。  コマンド ロジックはコマンドでは提供できませんが、コントロールまたはアプリケーションで提供する必要があります。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の多くのコントロールには、コマンド ライブラリにある一部のコマンドのサポートが組み込まれています。  たとえば、<xref:System.Windows.Controls.TextBox> では、<xref:System.Windows.Input.ApplicationCommands.Paste%2A>、<xref:System.Windows.Input.ApplicationCommands.Copy%2A>、<xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.ApplicationCommands.Redo%2A>、<xref:System.Windows.Input.ApplicationCommands.Undo%2A> などの多くのアプリケーション編集コマンドがサポートされます。  アプリケーション開発者は、コントロールで使用するこれらのコマンドを取得するのに特別な作業を行う必要はありません。  <xref:System.Windows.Controls.TextBox> がコマンド ターゲットである場合は、コマンドを実行すると、コントロールに組み込まれている <xref:System.Windows.Input.CommandBinding> を使用してコマンドが処理されます。  
  
 <xref:System.Windows.Input.ApplicationCommands.Paste%2A> コマンドのコマンド ソースとして <xref:System.Windows.Controls.MenuItem> を使用する方法を以下に示します。この場合、<xref:System.Windows.Controls.TextBox> がコマンドのターゲットとなります。  <xref:System.Windows.Controls.TextBox> での貼り付け方法を定義するすべてのロジックは、<xref:System.Windows.Controls.TextBox> コントロールに組み込まれています。  
  
 <xref:System.Windows.Controls.MenuItem> が作成され、その <xref:System.Windows.Controls.MenuItem.Command%2A> プロパティは <xref:System.Windows.Input.ApplicationCommands.Paste%2A> コマンドに設定されています。  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> は、<xref:System.Windows.Controls.TextBox> オブジェクトに明示的に設定されていません。  <xref:System.Windows.Controls.MenuItem.CommandTarget%2A> が設定されていない場合、コマンドのターゲットは、キーボード フォーカスを持つ要素となります。  キーボード フォーカスを持つ要素が <xref:System.Windows.Input.ApplicationCommands.Paste%2A> コマンドをサポートしていないか、貼り付けコマンドを現在実行できない場合 (クリップボードが空の場合など)、<xref:System.Windows.Controls.MenuItem> は灰色で表示されます。  
  
 [!code-xaml[MenuItemCommandTask_XAML#MenuItemCommanding](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask_XAML/CS/Window1.xaml#menuitemcommanding)]  
  
 [!code-csharp[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/MenuItemCommandTask/CSharp/Window1.xaml.cs#menuitemcommandingcodebehind)]
 [!code-vb[MenuItemCommandTask#MenuItemCommandingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/MenuItemCommandTask/VisualBasic/Window1.xaml.vb#menuitemcommandingcodebehind)]  
  
## <a name="see-also"></a>関連項目

- [コマンド実行の概要](commanding-overview.md)
- [コマンドをサポートしないコントロールにコマンドをフックする](how-to-hook-up-a-command-to-a-control-with-no-command-support.md)
