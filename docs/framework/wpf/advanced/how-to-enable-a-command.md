---
title: '方法: コマンドを有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CommandBindings [WPF]
- commanding [WPF]
ms.assetid: d8016266-58d9-48f7-8298-a86b7ed49fbd
ms.openlocfilehash: bf01066a35672e1996f193abc6d76153e5e9dd46
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62031998"
---
# <a name="how-to-enable-a-command"></a>方法: コマンドを有効にする
次の例では、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] でコマンドを使用する方法を示します。  この例では、<xref:System.Windows.Input.RoutedCommand> を <xref:System.Windows.Controls.Button> に関連付け、<xref:System.Windows.Input.CommandBinding> を作成し、<xref:System.Windows.Input.RoutedCommand> を実装するイベント ハンドラーを作成する方法を示します。  コマンド実行の詳細については、「[コマンド実行の概要](commanding-overview.md)」を参照してください。  
  
## <a name="example"></a>例  
 コードの最初のセクションでは <xref:System.Windows.Controls.Button> と <xref:System.Windows.Controls.StackPanel> で構成される [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] が作成され、<xref:System.Windows.Input.RoutedCommand> とコマンド ハンドラーを関連付ける <xref:System.Windows.Input.CommandBinding> が作成されます。  
  
 <xref:System.Windows.Controls.Button> の <xref:System.Windows.Input.ICommandSource.Command%2A> プロパティは <xref:System.Windows.Input.ApplicationCommands.Close%2A> コマンドと関連付けられます。  
  
 <xref:System.Windows.Input.CommandBinding> はルート <xref:System.Windows.Window> の <xref:System.Windows.Input.CommandBindingCollection> に追加されます。 イベント ハンドラーの <xref:System.Windows.Input.CommandBinding.Executed> と <xref:System.Windows.Input.CommandBinding.CanExecute> はこのバインディングに添付され、<xref:System.Windows.Input.ApplicationCommands.Close%2A> コマンドと関連付けられます。  
  
 <xref:System.Windows.Input.CommandBinding> なしではコマンド ロジックはなく、コマンドを呼び出すメカニズムのみが存在します。  <xref:System.Windows.Controls.Button> がクリックされると、コマンド ターゲットで <xref:System.Windows.Input.CommandManager.PreviewExecuted> <xref:System.Windows.RoutedEvent> が発生し、それに <xref:System.Windows.Input.CommandManager.Executed> <xref:System.Windows.RoutedEvent> が続きます。  これらのイベントによって、その特定のコマンドの <xref:System.Windows.Input.CommandBinding> を探すために要素ツリーが走査されます。  <xref:System.Windows.RoutedEvent> のトンネリングおよびバブリングでは要素ツリーを通過するため、<xref:System.Windows.Input.CommandBinding> の配置場所には注意が必要である点にご留意ください。   <xref:System.Windows.Input.CommandBinding> がコマンド ターゲットの兄弟ノード上にあるか、<xref:System.Windows.RoutedEvent> のルート上にはない別のノード上にある場合、<xref:System.Windows.Input.CommandBinding> はアクセスされません。  
  
 [!code-xaml[EnableCloseCommand#CloseCommandBinding](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml#closecommandbinding)]  
  
 [!code-csharp[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandbindingcodebehind)]
 [!code-vb[EnableCloseCommand#CloseCommandBindingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandbindingcodebehind)]  
  
 コードの次のセクションでは、イベント ハンドラーの <xref:System.Windows.Input.CommandManager.Executed> と <xref:System.Windows.Input.CommandBinding.CanExecute> が実装されます。  
  
 <xref:System.Windows.Input.CommandManager.Executed> ハンドラーにより、開いているファイルを閉じるメソッドが呼び出されます。  <xref:System.Windows.Input.CommandBinding.CanExecute> ハンドラーにより、ファイルが開いているかどうかを判断するメソッドが呼び出されます。  ファイルが開いている場合、<xref:System.Windows.Input.CanExecuteRoutedEventArgs.CanExecute%2A> が `true` に設定されます。それ以外の場合、`false` に設定されます。  
  
 [!code-csharp[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/EnableCloseCommand/CSharp/Window1.xaml.cs#closecommandhandler)]
 [!code-vb[EnableCloseCommand#CloseCommandHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/EnableCloseCommand/VisualBasic/Window1.xaml.vb#closecommandhandler)]  
  
## <a name="see-also"></a>関連項目

- [コマンド実行の概要](commanding-overview.md)
