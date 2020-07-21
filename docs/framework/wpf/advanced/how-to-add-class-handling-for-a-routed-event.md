---
title: '方法: ルーティング イベントのクラス処理を追加する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], class handlers
- task_core_add_class_handling_routed_properties [WPF]
- class handlers [WPF], routed events
ms.assetid: 15b7b06c-9112-4ee5-b30a-65d10c5c5df6
ms.openlocfilehash: 7b897954cbdab461dc0305c6290e67c1af5282c3
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61777040"
---
# <a name="how-to-add-class-handling-for-a-routed-event"></a>方法: ルーティング イベントのクラス処理を追加する
ルーティング イベントは、ルート内の特定のノードのクラス ハンドラーまたはインスタンス ハンドラーのいずれかによって処理されます。 クラス ハンドラーを最初に呼び出し、クラス実装で使用して、インスタンス処理からのイベントを抑制したり、基底クラスによって所有されるイベントに他のイベント固有の動作を導入したりすることができます。 この例は、クラス ハンドラーを実装するための密接に関連する 2 つの手法を示しています。  
  
## <a name="example"></a>例  
 この例では、<xref:System.Windows.Controls.Canvas> パネルに基づくカスタム クラスを使用しています。 アプリケーションの基本的な前提は、カスタム クラスによって、その子要素に動作が導入されるということです。たとえば、子要素クラスまたはそれに対するインスタンス ハンドラーが呼び出される前に、左マウス ボタンのクリックがインターセプトされ処理済みとしてマークされることなどです。  
  
 <xref:System.Windows.UIElement> クラスによって仮想メソッドが公開され、イベントをオーバーライドするだけで、<xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> イベントに対するクラス処理が可能になります。 クラスの階層のどこかでこのような仮想メソッドを使用できる場合、これがクラス処理を実装する最もシンプルな方法です。 次のコードは、<xref:System.Windows.Controls.Canvas> から派生した "MyEditContainer" での <xref:System.Windows.UIElement.OnPreviewMouseLeftButtonDown%2A> の実装を示しています。 この実装では、引数でイベントを処理済みとマークし、ソース要素に基本的な目に見える変更を加えるコードを追加します。  
  
 [!code-csharp[ClassHandling#OnStarClassHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#onstarclasshandler)]
 [!code-vb[ClassHandling#OnStarClassHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#onstarclasshandler)]  
  
 基底クラスまたはその特定のメソッドで使用できる仮想がない場合は、<xref:System.Windows.EventManager> クラスのユーティリティ メソッド <xref:System.Windows.EventManager.RegisterClassHandler%2A> を使用して、クラス処理を直接追加できます。 このメソッドは、クラス処理を追加しているクラスの静的初期化内でのみ呼び出す必要があります。 この例では、<xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> のハンドラーをもう 1 つ追加します。この場合、登録されるクラスはカスタム クラスです。 これに対し、仮想を使用する場合、登録されるクラスは実際には <xref:System.Windows.UIElement> 基底クラスです。 基底クラスとサブクラスのそれぞれにクラス処理が登録される場合、サブクラス ハンドラーが最初に呼び出されます。 アプリケーションの動作では、最初にこのハンドラーでメッセージ ボックスが表示され、次に仮想メソッドのハンドラーのビジュアルの変更が表示されます。  
  
 [!code-csharp[ClassHandling#StaticAndRegisterClassHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/ClassHandling/CSharp/SDKSampleLibrary/class1.cs#staticandregisterclasshandler)]
 [!code-vb[ClassHandling#StaticAndRegisterClassHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ClassHandling/visualbasic/sdksamplelibrary/class1.vb#staticandregisterclasshandler)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.EventManager>
- [ルーティング イベントの処理済みとしてのマーキング、およびクラス処理](marking-routed-events-as-handled-and-class-handling.md)
- [ルーティング イベントを処理する](how-to-handle-a-routed-event.md)
- [ルーティング イベントの概要](routed-events-overview.md)
