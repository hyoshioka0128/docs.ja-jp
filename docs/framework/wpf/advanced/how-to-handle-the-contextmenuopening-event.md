---
title: '方法: ContextMenuOpening イベントを処理する'
ms.date: 03/30/2017
helpviewer_keywords:
- ContextMenuOpening properties [WPF]
ms.assetid: 789652fb-1951-4217-934a-7843e355adf4
ms.openlocfilehash: b3d0f5c77ebf8527e4854d4edf12d6fa8a4b5f0c
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2019
ms.locfileid: "64614626"
---
# <a name="how-to-handle-the-contextmenuopening-event"></a>方法: ContextMenuOpening イベントを処理する
アプリケーションで <xref:System.Windows.FrameworkElement.ContextMenuOpening> イベントを処理して、既存のコンテキスト メニューを表示する前に調整する、またはイベント データで <xref:System.Windows.RoutedEventArgs.Handled%2A> プロパティを `true` に設定して、表示されるはずのメニューを非表示にすることができます。 イベント データで <xref:System.Windows.RoutedEventArgs.Handled%2A> を `true` に設定する一般的な理由は、メニューを新しい <xref:System.Windows.Controls.ContextMenu> オブジェクトに完全に置き換えるためです。この場合、操作をキャンセルして、新しいオープンの開始が必要になる場合があります。 <xref:System.Windows.FrameworkElement.ContextMenuOpening> イベント用のハンドラーを記述する場合は、<xref:System.Windows.Controls.ContextMenu> コントロールと、コントロール全般のコンテキスト メニューを開いて配置する役割を担うサービスの間のタイミングの問題に注意する必要があります。 このトピックでは、さまざまなコンテキスト メニューを開くシナリオのコード手法をいくつか紹介し、タイミングの問題が発生するケースを示します。  
  
 <xref:System.Windows.FrameworkElement.ContextMenuOpening> イベントの処理には、次のようにいくつかのシナリオがあります。  
  
- 表示する前にメニュー項目を調整する。  
  
- 表示する前にメニュー全体を置換する。  
  
- 既存のコンテキスト メニューを完全に非表示にし、コンテキスト メニューを表示しない。  
  
## <a name="example"></a>例  
  
## <a name="adjusting-the-menu-items-before-display"></a>表示する前にメニュー項目を調整する  
 既存のメニュー項目の調整は非常にシンプルであり、おそらく最も一般的なシナリオです。 これは、アプリケーションの現在の状態情報、またはコンテキスト メニューが要求されているオブジェクトのプロパティとして使用できる特定の状態情報に応じて、コンテキスト メニュー オプションを追加または削除するために行う場合があります。  
  
 一般的な手法は、ある特定のコントロールが右クリックされたとき、そのイベントのソースを取得し、そこから <xref:System.Windows.FrameworkElement.ContextMenu%2A> プロパティを取得することです。 通常は、<xref:System.Windows.Controls.ItemsControl.Items%2A> コレクションをチェックして、メニューに既に存在するコンテキスト メニュー項目を確認し、コレクションに対して適切な新しい <xref:System.Windows.Controls.MenuItem> 項目を追加または削除します。  
  
 [!code-csharp[ContextMenuOpeningHandlers#AddItemNoHandle](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#additemnohandle)]  
  
## <a name="replacing-the-entire-menu-before-display"></a>表示する前にメニュー全体を置換する  
 別のシナリオは、コンテキスト メニュー全体を置き換えることです。 もちろん、前述のコードのバリエーションを使用して、既存のコンテキスト メニューのすべての項目を削除し、項目なしの状態から新しい項目を追加することもできます。 しかし、コンテキスト メニューのすべての項目をより直感的に置き換える方法は、新しい <xref:System.Windows.Controls.ContextMenu> を作成し、それに項目を設定して、コントロールの <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType> プロパティを新しい <xref:System.Windows.Controls.ContextMenu> に設定することです。  
  
 <xref:System.Windows.Controls.ContextMenu> を置き換える単純なハンドラー コードを次に示します。 このコードは、カスタム `BuildMenu` メソッドを参照しています。この例では複数のハンドラーから呼び出されるため、このメソッドは分離されています。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceNoReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacenoreopen)]  
  
 [!code-csharp[ContextMenuOpeningHandlers#BuildMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#buildmenu)]  
  
 しかしながら、このスタイルのハンドラーを <xref:System.Windows.FrameworkElement.ContextMenuOpening> に使用すると、<xref:System.Windows.Controls.ContextMenu> を設定しようとしているオブジェクトに既存のコンテキスト メニューがない場合にタイミングの問題が発生する可能性があります。 ユーザーがコントロールを右クリックしたとき、既存の <xref:System.Windows.Controls.ContextMenu> が空または null であっても <xref:System.Windows.FrameworkElement.ContextMenuOpening> が発生します。 しかしこの場合は、ソース要素に設定する新しい <xref:System.Windows.Controls.ContextMenu> が何であれ、表示するには遅すぎます。 また、ユーザーが 2 回目に右クリックすると、今度は新しい <xref:System.Windows.Controls.ContextMenu> が表示され、値が null でないため、ハンドラーが 2 回目に実行されるときに、ハンドラーにより、メニューが適切に置換され、表示されます。 このことは、次の 2 つの可能な回避策を示唆しています。  
  
1. <xref:System.Windows.FrameworkElement.ContextMenuOpening> ハンドラーが、少なくともハンドラー コードで置き換える予定のプレース ホルダー <xref:System.Windows.Controls.ContextMenu> がある使用可能なコントロールに対して、常に実行されることを確実にします。 この場合にも、前述の例で示したハンドラーを使用することはできますが、通常は最初のマークアップ内に <xref:System.Windows.Controls.ContextMenu> プレースホルダーを指定することができます。  
  
     [!code-xaml[ContextMenuOpeningHandlers#XAMLWithInitCM](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml#xamlwithinitcm)]  
  
2. <xref:System.Windows.Controls.ContextMenu> の初期値が、何らかの予備ロジックに基づいて、null の可能性があると仮定します。 <xref:System.Windows.Controls.ContextMenu> が null であるかチェックすることも、またはコードでフラグを使用して、ハンドラーが少なくとも 1 回実行されているかどうかをチェックすることもできます。 <xref:System.Windows.Controls.ContextMenu> が表示されることを仮定しているため、ハンドラーで、イベント データの <xref:System.Windows.RoutedEventArgs.Handled%2A> を `true` に設定します。 コンテキスト メニューの表示を担う <xref:System.Windows.Controls.ContextMenuService> にとって、イベント データ内の <xref:System.Windows.RoutedEventArgs.Handled%2A> の値が `true` であることは、イベントが発生したコンテキスト メニューとコントロールの組み合わせの表示をキャンセルする要求を表します。  
  
 これで問題がある可能性のあるコンテキスト メニューを非表示にしました。次の手順では、新しいものを指定して表示します。 新しいものの設定は、基本的には前のハンドラーと同じです。新しい <xref:System.Windows.Controls.ContextMenu> を作成し、それを使用してコントロール ソースの <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType> プロパティを設定します。 最初の試行を非表示にしたため、ここでは追加の手順として、コンテキスト メニューを強制的に表示する必要があります。 強制的に表示するには、ハンドラー内で <xref:System.Windows.Controls.Primitives.Popup.IsOpen%2A?displayProperty=nameWithType> プロパティを `true` に設定します。 これを行うときは、ハンドラー内でコンテキスト メニューを開くと、<xref:System.Windows.FrameworkElement.ContextMenuOpening> イベントが再度発生すことにご注意ください。 再度ハンドラーに入ると、無限再帰になります。 このため、<xref:System.Windows.FrameworkElement.ContextMenuOpening> イベント ハンドラー内からコンテキスト メニューを開く場合は常に、`null` であるかチェックするか、フラグを使用する必要があります。  
  
## <a name="suppressing-any-existing-context-menu-and-displaying-no-context-menu"></a>既存のコンテキスト メニューを非表示にし、コンテキスト メニューを表示しない  
 最後のシナリオでは、メニューを完全に非表示にするハンドラーを記述しますが、これは一般的ではありません。 特定のコントロールでコンテキスト メニューが表示されないことになっている場合はおそらく、ユーザーが要求したときにのみメニューを非表示にするよりもこれを確実にする適切な方法があるでしょう。 しかし、ハンドラーを使用してコンテキスト メニューを非表示にし、何も表示しないようにしたいのであれば、ハンドラーで、イベント データの <xref:System.Windows.RoutedEventArgs.Handled%2A> を `true` に設定する必要があるだけです。 コンテキスト メニューの表示を担う <xref:System.Windows.Controls.ContextMenuService> で、コントロールで発生したイベントのイベント データがチェックされます。 イベントがルート上のどこかで <xref:System.Windows.RoutedEventArgs.Handled%2A> とマークされた場合、イベントを開始したコンテキスト メニューのアクションが抑制されます。  
  
 [!code-csharp[ContextMenuOpeningHandlers#ReplaceReopen](~/samples/snippets/csharp/VS_Snippets_Wpf/ContextMenuOpeningHandlers/CSharp/Pane1.xaml.cs#replacereopen)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ContextMenu>
- <xref:System.Windows.FrameworkElement.ContextMenu%2A?displayProperty=nameWithType>
- [基本要素の概要](base-elements-overview.md)
- [ContextMenu の概要](../controls/contextmenu-overview.md)
