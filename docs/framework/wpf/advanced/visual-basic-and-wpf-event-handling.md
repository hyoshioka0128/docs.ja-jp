---
title: Visual Basic でイベントを処理する
ms.date: 03/30/2017
helpviewer_keywords:
- Visual Basic [WPF], event handlers
- event handlers [WPF], Visual Basic
ms.assetid: ad4eb9aa-3afc-4a71-8cf6-add3fbea54a1
ms.openlocfilehash: 959ef66f41f6c5f06e18a202109fba058c522d1d
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76735409"
---
# <a name="visual-basic-and-wpf-event-handling"></a>Visual Basic と WPF のイベント処理
特に Microsoft Visual Basic .NET 言語の場合、イベント ハンドラーを属性に添付したり、<xref:System.Windows.UIElement.AddHandler%2A> メソッドを使用したりする代わりに、言語固有の `Handles` キーワードを使用して、イベント ハンドラーをインスタンスに関連付けることができます。 ただし、`Handles` 構文では [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] イベント システムの特定のルーティング イベント機能の一部をサポートできないため、ハンドラーをインスタンスに添付する `Handles` 手法にはいくつかの制限があります。  
  
## <a name="using-handles-in-a-wpf-application"></a>WPF アプリケーションでの "ハンドル" の使用  
 `Handles` を使用するインスタンスとイベントに接続されているイベント ハンドラーは、すべてインスタンスの部分クラス宣言内で定義する必要があります。これは、要素の属性値を介して割り当てられるイベント ハンドラーの要件でもあります。 <xref:System.Windows.FrameworkContentElement.Name%2A> プロパティ値 (または宣言されている [x:Name Directive](../../../desktop-wpf/xaml-services/xname-directive.md)) を持つページの要素に対してのみ、`Handles` を指定できます。 これは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の <xref:System.Windows.FrameworkContentElement.Name%2A> によって、`Handles` 構文に必要な *Instance.Event* 参照形式をサポートするために必要なインスタンス参照が作成されるためです。 <xref:System.Windows.FrameworkContentElement.Name%2A> 参照なしで `Handles` に使用できる唯一の要素は、部分クラスを定義するルート要素インスタンスです。  
  
 `Handles` の後の *Instance.Event* 参照をコンマで区切ることにより、同じハンドラーを複数の要素に割り当てることができます。  
  
 `Handles` を使用して、同じ *Instance.Event* 参照に複数のハンドラーを割り当てることができます。 `Handles` 参照でハンドラーが指定されている順序で重要度を割り当てないでください。同じイベントを処理するハンドラーは任意の順序で呼び出される可能性があることを想定する必要があります。  
  
 宣言で `Handles` と共に追加されたハンドラーを削除するには、<xref:System.Windows.UIElement.RemoveHandler%2A> を呼び出します。  
  
 メンバー テーブルで処理されるイベントを定義するハンドラーをインスタンスに添付している限り、`Handles` を使用してルーティング イベントのハンドラーを添付できます。 ルーティング イベントの場合、`Handles` に添付されたハンドラーは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 属性として添付されたハンドラーと同じルーティング規則に従うか、共通の署名 <xref:System.Windows.UIElement.AddHandler%2A> を使用します。 つまり、イベントが既に処理済みとしてマークされている場合 (イベント データの <xref:System.Windows.RoutedEventArgs.Handled%2A> プロパティが `True` の場合)、そのイベント インスタンスに応答して `Handles` に添付されたハンドラーが呼び出されません。 イベントは、ルート内の別の要素のインスタンス ハンドラーによって処理されるか、現在の要素またはルート上の以前の要素のいずれかを処理するクラスによってマークされる可能性があります。 ペアのトンネルおよびバブル イベントをサポートする入力イベントの場合、トンネリング ルートによってイベント ペアが処理済みとマークされる場合があります。 ルーティング イベントの詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
## <a name="limitations-of-handles-for-adding-handlers"></a>ハンドラーを追加するための "ハンドル" の制限事項  
 `Handles` では、添付イベントのハンドラーを参照できません。 この添付イベント、つまり [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の *typename.eventname* には、`add` アクセサー メソッドを使用する必要があります。 詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
 ルーティング イベントの場合、`Handles` を使用してインスタンス メンバー テーブルにそのイベントが存在するインスタンスにハンドラーを割り当てることができます。 ただし、一般にルーティング イベントでは、親要素のメンバー テーブルにそのイベントがない場合でも、親要素は子要素からのイベントのリスナーになることができます。 属性構文では、*typename.membername* 属性フォームを使用してこれを指定できます。これにより、処理するイベントを実際に定義する型を修飾できます。 たとえば、親 `Page` (`Click` イベントが定義されていない) では、`Button.Click` の形式で属性ハンドラーを割り当てることにより、ボタンクリック イベントをリッスンできます。 ただし、`Handles` では *typename.membername* フォームをサポートしていません。これは、競合する *Instance.Event* フォームをサポートする必要があるためです。 詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
 `Handles` を使用しても、既に処理済みとマークされているイベントに対して呼び出されるハンドラーを添付できません。 代わりに、コードを使用して、<xref:System.Windows.UIElement.AddHandler%28System.Windows.RoutedEvent%2CSystem.Delegate%2CSystem.Boolean%29> の `handledEventsToo` オーバーロードを呼び出す必要があります。  
  
> [!NOTE]
> XAML で同じイベントのイベント ハンドラーを指定する場合は、Visual Basic コードで `Handles` 構文を使用しないでください。 この場合、イベント ハンドラーが 2 回呼び出されます。  
  
## <a name="how-wpf-implements-handles-functionality"></a>WPF で "ハンドル" 機能を実装する方法  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ページがコンパイルされると、中間ファイルによって、<xref:System.Windows.FrameworkContentElement.Name%2A> プロパティ セット (または宣言されている [x:Name Directive](../../../desktop-wpf/xaml-services/xname-directive.md)) を持つページ上のすべての要素に対して `Friend` `WithEvents` 参照を宣言します。 名前付きインスタンスはそれぞれ、`Handles` を介してハンドラーに割り当てることができる要素である可能性があります。  
  
> [!NOTE]
> Visual Studio 内で、IntelliSense には、ページ内の `Handles` 参照に使用できる要素の補完を表示できます。 ただし、中間ファイルですべての `Friends` 参照を設定できるようにするには、1 つのコンパイルの成功が必要になる場合があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.UIElement.AddHandler%2A>
- [ルーティング イベントの処理済みとしてのマーキング、およびクラス処理](marking-routed-events-as-handled-and-class-handling.md)
- [ルーティング イベントの概要](routed-events-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
