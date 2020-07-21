---
title: プレビュー イベント
ms.date: 03/30/2017
helpviewer_keywords:
- Preview events [WPF]
- suppressing events [WPF]
- events [WPF], Preview
- events [WPF], suppressing
ms.assetid: b5032308-aa9c-4d02-af11-630ecec8df7e
ms.openlocfilehash: 75165df94aa8b508ef85cf970933efb98b9d62ca
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61772880"
---
# <a name="preview-events"></a>プレビュー イベント
プレビュー イベントは、トンネリング イベントとも呼ばれ、ルートの方向がアプリケーション ルートからイベントを発生させた要素に向かって移動し、イベント データのソースとして報告されるルーティング イベントです。 すべてのイベント シナリオでプレビュー イベントがサポートされている、または必要とされているわけではありません。このトピックでは、プレビュー イベントが存在する状況、アプリケーションまたはコンポーネントでそれらを処理する方法、カスタム コンポーネントまたはクラスでプレビュー イベントを作成することが適切な場合について説明します。  
  
## <a name="preview-events-and-input"></a>プレビュー イベントと入力  
 一般的にプレビュー イベントを処理するときは、イベント データで処理されるイベントをマークすることにご注意ください。 発生させた要素 (イベント データでソースとして報告される要素) 以外の要素でプレビュー イベントを処理すると、発生した元のイベントを処理する機会が要素に提供されないという影響があります。 これが望ましい結果になる場合もあります。問題の要素がコントロールの合成内のリレーションシップに存在する場合は特にそうです。  
  
 特に入力イベントの場合、プレビュー イベントでもイベント データ インスタンスが同等のバブリング イベントと共有されます。 入力イベントを処理済みとマークするためにプレビュー イベント クラス ハンドラーを使用する場合、バブリング入力イベント クラス ハンドラーは呼び出されません。 また、イベントを処理済みとマークするためにプレビュー イベント インスタンス ハンドラーを使用する場合、通常、バブリング イベントのハンドラーは呼び出されません。 イベントが処理済みとしてマークされている場合でも、呼び出すオプションを使用してクラス ハンドラーまたはインスタンス ハンドラーを登録またはアタッチできますが、この手法は一般的には使用されません。  
  
 クラス処理とプレビュー イベントとの関係の詳細については、「[ルーティング イベントの処理済みとしてのマーキング、およびクラス処理](marking-routed-events-as-handled-and-class-handling.md)」を参照してください。  
  
### <a name="working-around-event-suppression-by-controls"></a>コントロールによるイベント抑制の回避  
 プレビュー イベントが一般的に使用されるシナリオの 1 つとして、入力イベントの複合コントロール処理があります。 場合によっては、コントロールの作成者が、おそらく、より多くの情報を伝達する、またはより具体的な動作を意味するコンポーネント定義のイベントを置き換える目的で、特定のイベントがコントロールから発生しないように抑制することがあります。 たとえば、マウスをキャプチャし、常に <xref:System.Windows.Controls.Button> 自体によって発生する <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを発生させるために、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] <xref:System.Windows.Controls.Button> を使用して、<xref:System.Windows.Controls.Button> またはその複合要素によって発生する <xref:System.Windows.UIElement.MouseLeftButtonDown> および <xref:System.Windows.UIElement.MouseRightButtonDown> バブリング イベントを抑制することができます。 イベントとそのデータはルートに沿って続行されますが、<xref:System.Windows.Controls.Button> によってイベント データは <xref:System.Windows.RoutedEventArgs.Handled%2A> とマークされるため、`handledEventsToo` ケースで動作する必要があることを明確に示すイベントのハンドラーのみが呼び出されます。  アプリケーションのルートに向かう他の要素に、コントロール抑制イベントを処理する機会がまだ必要な場合、代替手段の 1 つは、`true` に指定された `handledEventsToo` を使って、コード内でハンドラーをアタッチすることです。 ただし、多くの場合、より簡単な手法は、処理するルーティング方向を変更して、入力イベントと同等のプレビューにすることです。 たとえば、コントロールによって <xref:System.Windows.UIElement.MouseLeftButtonDown> が抑制されている場合は、代わりに <xref:System.Windows.UIElement.PreviewMouseLeftButtonDown> のハンドラーをアタッチしてみてください。 この手法は、<xref:System.Windows.UIElement.MouseLeftButtonDown> などの基本要素の入力イベントに対してのみ機能します。 これらの入力イベントでは、トンネルおよびバブルのペアが使用され、両方のイベントが発生し、イベント データが共有されます。  
  
 これらの手法にはそれぞれに副作用または制限事項があります。 プレビュー イベントを処理することの副作用は、その時点でイベントを処理すると、バブリング イベントの処理が想定されているハンドラーが無効になる可能性があることです。そのため、制限事項は、まだルートのプレビュー部分にある間にイベントに処理済みとマークすることが、通常は推奨されないということです。 `handledEventsToo` 手法の制限事項は、属性として [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で `handledEventsToo` ハンドラーを指定できないことです。ハンドラーがアタッチされる要素へのオブジェクト参照を取得した後、コードにイベント ハンドラーを登録する必要があります。  
  
## <a name="see-also"></a>関連項目

- [ルーティング イベントの処理済みとしてのマーキング、およびクラス処理](marking-routed-events-as-handled-and-class-handling.md)
- [ルーティング イベントの概要](routed-events-overview.md)
