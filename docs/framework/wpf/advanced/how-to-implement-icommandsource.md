---
title: '方法: ICommandSource を実装する'
ms.date: 12/05/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ICommandSource interfaces [WPF], implementing
ms.assetid: 7452dd39-6e11-44bf-806a-31d87f3772ac
ms.openlocfilehash: 6c18e0b77ec53d9bd3e7ce610f2940effe603c88
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174694"
---
# <a name="how-to-implement-icommandsource"></a>方法: ICommandSource を実装する

この例では、<xref:System.Windows.Input.ICommandSource> を実装してコマンド ソースを作成する方法について説明します。 コマンド ソースとは、コマンドの呼び出し方法を認識しているオブジェクトのことです。 <xref:System.Windows.Input.ICommandSource> インターフェイスでは、次の 3 つのメンバーが公開されます。

- <xref:System.Windows.Input.ICommandSource.Command%2A>: 呼び出されるコマンド。
- <xref:System.Windows.Input.ICommandSource.CommandParameter%2A>: コマンド ソースからコマンドを処理するメソッドに渡されるユーザー定義のデータ型。
- <xref:System.Windows.Input.ICommandSource.CommandTarget%2A>: コマンド実行の対象となるオブジェクト。

この例では、<xref:System.Windows.Controls.Slider> コントロールを継承し、<xref:System.Windows.Input.ICommandSource> インターフェイスを実装するクラスが作成されます。
  
## <a name="example"></a>例

WPF では、<xref:System.Windows.Input.ICommandSource> を実装するクラスが多数提供されています (<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.MenuItem>、<xref:System.Windows.Documents.Hyperlink> など)。 コマンド ソースでは、コマンドの呼び出し方法が定義されます。 これらのクラスは、自身がクリックされたときにコマンドを呼び出し、<xref:System.Windows.Input.ICommandSource.Command%2A> プロパティが設定されている場合にのみコマンド ソースになります。

この例では、スライダーが動かされたとき (より正確に言うと、<xref:System.Windows.Controls.Primitives.RangeBase.Value%2A> プロパティが変更されたとき) にコマンドを呼び出します。

クラス定義を次に示します。

[!code-csharp[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourceclassdefinition)]
[!code-vb[ImplementICommandSource#ImplementICommandSourceClassDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourceclassdefinition)]

次の手順は、<xref:System.Windows.Input.ICommandSource> メンバーを実装することです。 この例では、プロパティが <xref:System.Windows.DependencyProperty> オブジェクトとして実装されています。 これにより、プロパティでデータ バインディングを使用できるようになります。 <xref:System.Windows.DependencyProperty> クラスの詳細については、「[依存関係プロパティの概要](dependency-properties-overview.md)」を参照してください。 データ バインディングの詳細については、「[データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」を参照してください。

ここでは、<xref:System.Windows.Input.ICommandSource.Command%2A> プロパティのみを示します。

[!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandpropertydefinition)]
[!code-vb[ImplementICommandSource#ImplementICommandSourceCommandPropertyDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandpropertydefinition)]  
  
次に示すのは、<xref:System.Windows.DependencyProperty> の変更コールバックです。

[!code-csharp[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcecommandchanged)]
[!code-vb[ImplementICommandSource#ImplementICommandSourceCommandChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcecommandchanged)]

次の手順は、コマンド ソースに関連付けられているコマンドを追加および削除することです。 新しいコマンドが追加されたときには、<xref:System.Windows.Input.ICommandSource.Command%2A> プロパティを単純に上書きすることはできません。なぜなら、前のコマンドに関連付けられているイベント ハンドラー (存在する場合) を最初に削除する必要があるからです。

[!code-csharp[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandsourcehookunhookcommands)]
[!code-vb[ImplementICommandSource#ImplementICommandSourceHookUnHookCommands](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandsourcehookunhookcommands)]

次の手順は、<xref:System.Windows.Input.ICommand.CanExecuteChanged> ハンドラーのロジックを作成することです。

<xref:System.Windows.Input.ICommand.CanExecuteChanged> イベントは、現在のコマンド ターゲットに対するコマンドの実行可能性が変化した可能性があることを、コマンド ソースに通知します。 コマンド ソースは通常、このイベントを受け取ると、コマンドに対する <xref:System.Windows.Input.ICommand.CanExecute%2A> メソッドを呼び出します。 コマンドを現在のコマンド ターゲットに対して実行できない場合、コマンド ソースは通常、自身を無効化します。 コマンドを現在のコマンド ターゲットに対して実行できる場合、コマンド ソースは通常、自身を有効化します。

[!code-csharp[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandcanexecutechanged)]
[!code-vb[ImplementICommandSource#ImplementICommandCanExecuteChanged](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandcanexecutechanged)]

最後の手順は、<xref:System.Windows.Input.ICommand.Execute%2A> メソッドです。 コマンドが <xref:System.Windows.Input.RoutedCommand>の場合、<xref:System.Windows.Input.RoutedCommand> <xref:System.Windows.Input.RoutedCommand.Execute%2A> メソッドが呼び出されます。それ以外の場合は、<xref:System.Windows.Input.ICommand> <xref:System.Windows.Input.ICommand.Execute%2A> メソッドが呼び出されます。

[!code-csharp[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/csharp/VS_Snippets_Wpf/ImplementICommandSource/CSharp/CommandSlider.cs#implementicommandexecute)]
[!code-vb[ImplementICommandSource#ImplementICommandExecute](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImplementICommandSource/visualbasic/commandslider.vb#implementicommandexecute)]

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Input.ICommandSource>
- <xref:System.Windows.Input.ICommand>
- <xref:System.Windows.Input.RoutedCommand>
- [コマンド実行の概要](commanding-overview.md)
