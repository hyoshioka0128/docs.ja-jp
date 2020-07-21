---
title: '方法: RoutedCommand を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- RoutedCommand class [WPF], creating
ms.assetid: aaf6979f-69ab-406f-979f-5766daa85fa0
ms.openlocfilehash: d433658a3039c262d2f682eff09df646d978018c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776481"
---
# <a name="how-to-create-a-routedcommand"></a>方法: RoutedCommand を作成する
この例では、カスタムの <xref:System.Windows.Input.RoutedCommand> を作成する方法と、<xref:System.Windows.Input.ExecutedRoutedEventHandler> と <xref:System.Windows.Input.CanExecuteRoutedEventHandler> を作成して <xref:System.Windows.Input.CommandBinding> に添付することによって、カスタム コマンドを実装する方法を示します。  コマンド実行の詳細については、「[コマンド実行の概要](commanding-overview.md)」を参照してください。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Input.RoutedCommand> を作成する最初の手順では、コマンドを定義してインスタンス化します。  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcommanddefinition)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCommandDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcommanddefinition)]  
  
 アプリケーションでコマンドを使用するためには、コマンドの内容を定義するイベント ハンドラーを作成する必要があります。  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewExecuted](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewexecuted)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewExecuted](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewexecuted)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCanExecute](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcanexecute)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCanExecute](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcanexecute)]  
  
 次に、イベント ハンドラーにコマンドを関連付けて、<xref:System.Windows.Input.CommandBinding> が作成されます。 <xref:System.Windows.Input.CommandBinding> は、特定のオブジェクトに作成されます。  このオブジェクトによって、要素ツリーの <xref:System.Windows.Input.CommandBinding> のスコープが定義されます。  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewWindowCommandBindingXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewwindowcommandbindingxaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandbindingcodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandBindingCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandbindingcodebehind)]  
  
 最後の手順では、コマンドを呼び出します。  コマンドを呼び出す方法の 1 つは、<xref:System.Windows.Controls.Button> などの <xref:System.Windows.Input.ICommandSource> に関連付けることです。  
  
 [!code-xaml[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml#commandingoverviewcustomcommandsourcexaml)]  
  
 [!code-csharp[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/CommandingOverviewSnippets/CSharp/Window1.xaml.cs#commandingoverviewcustomcommandsourcecodebehind)]
 [!code-vb[CommandingOverviewSnippets#CommandingOverviewCustomCommandSourceCodeBehind](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CommandingOverviewSnippets/visualbasic/window1.xaml.vb#commandingoverviewcustomcommandsourcecodebehind)]  
  
 この Button がクリックされると、カスタム <xref:System.Windows.Input.RoutedCommand> の <xref:System.Windows.Input.RoutedCommand.Execute%2A> メソッドが呼び出されます。  <xref:System.Windows.Input.RoutedCommand> によって、<xref:System.Windows.Input.CommandManager.PreviewExecuted> と <xref:System.Windows.Input.CommandManager.Executed> ルーティング イベントが発生します。  これらのイベントによって、この特定のコマンドの <xref:System.Windows.Input.CommandBinding> を探すために、要素ツリーが走査されます。  <xref:System.Windows.Input.CommandBinding> が見つかった場合、<xref:System.Windows.Input.CommandBinding> に関連付けられた <xref:System.Windows.Input.ExecutedRoutedEventHandler> が呼び出されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Input.RoutedCommand>
- [コマンド実行の概要](commanding-overview.md)
