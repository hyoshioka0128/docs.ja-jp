---
title: '方法: ルーティング イベントを処理する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], handling
- bubbling events [WPF]
ms.assetid: 157787b4-f469-4047-8777-5b034145f32e
ms.openlocfilehash: edb3d6724af89b7e85986c50b579084e3c4e5070
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62001508"
---
# <a name="how-to-handle-a-routed-event"></a>方法: ルーティング イベントを処理する
バブル イベントの動作と、ルーティング イベント データを処理できるハンドラーを作成する方法を次の例に示します。  
  
## <a name="example"></a>例  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、要素は、要素ツリー構造体に配置されます。 親要素は、要素ツリー内で最初に子要素が発生させたイベントの処理に参加できます。 これは、イベント ルーティングにより可能です。  
  
 ルーティング イベントは通常、バブルまたはトンネルの 2 つのルーティング方法のいずれかに従います。 この例では、バブル イベントに焦点を当て、<xref:System.Windows.Controls.Primitives.ButtonBase.Click?displayProperty=nameWithType> イベントを使用して、ルーティングの動作を示します。  
  
 次の例では、2 つの <xref:System.Windows.Controls.Button> コントロールを作成し、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 属性構文を使用して、イベント ハンドラーを共通の親要素 (この例では <xref:System.Windows.Controls.StackPanel>) にアタッチします。 この例では、各 <xref:System.Windows.Controls.Button> 子要素の個々のイベント ハンドラーをアタッチするのではなく、属性構文を使用してイベント ハンドラーを <xref:System.Windows.Controls.StackPanel> 親要素にアタッチします。 このイベント処理パターンは、ハンドラーがアタッチされる要素の数を減らすための手法としてイベント ルーティングを使用する方法を示します。 各 <xref:System.Windows.Controls.Button> のすべてのバブル イベントが親要素を通じてルーティングされます。  
  
 親 <xref:System.Windows.Controls.StackPanel> 要素では、属性として指定された <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベント名が <xref:System.Windows.Controls.Button> クラスに名前を付けることによって部分的に修飾されていることにご注意ください。 <xref:System.Windows.Controls.Button> クラスは、メンバーの一覧に <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントが含まれる <xref:System.Windows.Controls.Primitives.ButtonBase> 派生クラスです。 イベント ハンドラーをアタッチするためのこの部分修飾手法が必要になるのは、ルーティング イベント ハンドラーがアタッチされる要素のメンバー一覧に、処理されているイベントが存在しない場合です。  
  
 [!code-xaml[RoutedEventHandle#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml#xaml)]  
  
 次の例では、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントを処理します。  この例では、イベントを処理する要素とイベントを発生させる要素を報告します。 ユーザーがいずれかのボタンをクリックすると、イベント ハンドラーが実行されます。  
  
 [!code-csharp[RoutedEventHandle#Handler](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventHandle/CSharp/default.xaml.cs#handler)]
 [!code-vb[RoutedEventHandle#Handler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventHandle/VisualBasic/MainWindow.xaml.vb#handler)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.RoutedEvent>
- [入力の概要](input-overview.md)
- [ルーティング イベントの概要](routed-events-overview.md)
- [方法トピック](events-how-to-topics.md)
- [XAML 構文の詳細](xaml-syntax-in-detail.md)
