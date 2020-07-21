---
title: '方法: コマンドをサポートしないコントロールにコマンドをフックする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Control class [WPF], attaching a RoutedCommand
- classes [WPF], Control [WPF], attaching a RoutedCommand
- RoutedCommand class [WPF], attaching to a Control
- classes [WPF], RoutedCommand [WPF], attaching to a Control
ms.assetid: dad08f64-700b-46fb-ad3f-fbfee95f0dfe
ms.openlocfilehash: 3ae45c9a9e33a3cb53ada6e1e5430ae0f9e6c198
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "71263304"
---
# <a name="how-to-hook-up-a-command-to-a-control-with-no-command-support"></a>方法: コマンドをサポートしないコントロールにコマンドをフックする
次の例では、コマンドのサポートが組み込まれていない <xref:System.Windows.Controls.Control> に <xref:System.Windows.Input.RoutedCommand> をフックする方法を示します。  コマンドを複数のソースに関連付けるサンプル全体については、「[カスタム RoutedCommand の作成のサンプル](https://github.com/Microsoft/WPF-Samples/tree/master/Input%20and%20Commands/CustomRoutedCommand)」を参照してください。  
  
## <a name="example"></a>例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、アプリケーション プログラマがよく使用する一般的なコマンドのライブラリが用意されています。  コマンド ライブラリを構成するクラスは、<xref:System.Windows.Input.ApplicationCommands>、<xref:System.Windows.Input.ComponentCommands>、<xref:System.Windows.Input.NavigationCommands>、<xref:System.Windows.Input.MediaCommands>、<xref:System.Windows.Documents.EditingCommands> です。  
  
 これらのクラスを構成する静的な <xref:System.Windows.Input.RoutedCommand> オブジェクトには、コマンド ロジックが用意されていません。  コマンドのロジックは、<xref:System.Windows.Input.CommandBinding> でコマンドに関連付けられます。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の多くのコントロールには、コマンド ライブラリにある一部のコマンドのサポートが組み込まれています。  たとえば、<xref:System.Windows.Controls.TextBox> では、<xref:System.Windows.Input.ApplicationCommands.Paste%2A>、<xref:System.Windows.Input.ApplicationCommands.Copy%2A>、<xref:System.Windows.Input.ApplicationCommands.Cut%2A>、<xref:System.Windows.Input.ApplicationCommands.Redo%2A>、<xref:System.Windows.Input.ApplicationCommands.Undo%2A> などの多くのアプリケーション編集コマンドがサポートされます。  アプリケーション開発者は、コントロールで使用するこれらのコマンドを取得するのに特別な作業を行う必要はありません。  <xref:System.Windows.Controls.TextBox> がコマンド ターゲットである場合は、コマンドを実行すると、コントロールに組み込まれている <xref:System.Windows.Input.CommandBinding> を使用してコマンドが処理されます。  
  
 <xref:System.Windows.Input.ApplicationCommands.Open%2A> コマンドのコマンド ソースとして <xref:System.Windows.Controls.Button> を使用する方法を以下に示します。  <xref:System.Windows.Input.CommandBinding> が作成され、指定された <xref:System.Windows.Input.CanExecuteRoutedEventHandler> と <xref:System.Windows.Input.CanExecuteRoutedEventHandler> が <xref:System.Windows.Input.RoutedCommand> に関連付けられます。  
  
 まず、コマンド ソースが作成されます。  <xref:System.Windows.Controls.Button> はコマンド ソースとして使用されます。  
  
 [!code-xaml[commandWithHandler#CommandHandlerCommandSource](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandsource)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerButtonCommandSource](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbuttoncommandsource)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerButtonCommandSource](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbuttoncommandsource)]  
  
 次に、<xref:System.Windows.Input.ExecutedRoutedEventHandler> と <xref:System.Windows.Input.CanExecuteRoutedEventHandler> が作成されます。  <xref:System.Windows.Input.ExecutedRoutedEventHandler> では単に <xref:System.Windows.MessageBox> が開かれ、コマンドが実行されたことが示されます。  <xref:System.Windows.Input.CanExecuteRoutedEventHandler> は <xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> プロパティを `true` に設定します。  通常、実行可能ハンドラーではより堅牢なチェックが行われ、現在のコマンド ターゲットでコマンドを実行できるかどうかが確認されます。  
  
 [!code-csharp[commandWithHandler#CommandHandlerBothHandlers](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml.cs#commandhandlerbothhandlers)]
 [!code-vb[commandWithHandler#CommandHandlerBothHandlers](~/samples/snippets/visualbasic/VS_Snippets_Wpf/commandWithHandler/VisualBasic/Window1.xaml.vb#commandhandlerbothhandlers)]  
  
 最後に、<xref:System.Windows.Input.CommandBinding> がアプリケーションのルート <xref:System.Windows.Window> に作成され、<xref:System.Windows.Input.ApplicationCommands.Open%2A> コマンドにルーティング イベント ハンドラーが関連付けられます。  
  
 [!code-xaml[commandWithHandler#CommandHandlerCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/commandWithHandler/CSharp/Window1.xaml#commandhandlercommandbinding)]  
  
 [!code-csharp[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandHandlerProcedural/CSharp/Window1.xaml.cs#commandhandlerbindinginit)]
 [!code-vb[CommandHandlerProcedural#CommandHandlerBindingInit](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandHandlerProcedural/visualbasic/window1.xaml.vb#commandhandlerbindinginit)]  
  
## <a name="see-also"></a>関連項目

- [コマンド実行の概要](commanding-overview.md)
- [コマンドをサポートするコントロールにコマンドをフックする](how-to-hook-up-a-command-to-a-control-with-command-support.md)
