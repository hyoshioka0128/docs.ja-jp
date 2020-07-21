---
title: '方法: カスタム ルーティング イベントを作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- routed events [WPF], creating
- events [WPF], routing
ms.assetid: b79f459a-1c3f-4045-b2d4-1659cc8eaa3c
ms.openlocfilehash: cbfb88af4e35e3f090248982bb14d6b7a3a03cef
ms.sourcegitcommit: 24a4a8eb6d8cfe7b8549fb6d823076d7c697e0c6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2019
ms.locfileid: "68401471"
---
# <a name="how-to-create-a-custom-routed-event"></a>方法: カスタム ルーティング イベントを作成する
カスタム イベントでイベント ルーティングをサポートするには、<xref:System.Windows.EventManager.RegisterRoutedEvent%2A> メソッドを使用して <xref:System.Windows.RoutedEvent> を登録する必要があります。 この例では、カスタム ルーティング イベント作成の基本を紹介します。  
  
## <a name="example"></a>例  
 次の例に示すように、最初に、<xref:System.Windows.EventManager.RegisterRoutedEvent%2A> メソッドを使用して <xref:System.Windows.RoutedEvent> を登録します。 <xref:System.Windows.RoutedEvent> 静的フィールドの名前は、***Event*** という接尾辞で終わる決まりになっています。 この例では、イベントの名前は `Tap` です。イベントのルーティング方法は <xref:System.Windows.RoutingStrategy.Bubble> です。 登録呼び出し後、イベントの add-and-remove 共通言語ランタイム (CLR) イベント アクセサーを指定できます。  
  
 この特別な例では `OnTap` 仮想メソッド経由でイベントが発生していますが、イベントの発生や変更に対するイベントの反応の仕方はニーズによって変わります。  
  
 また、この例では、基本的に <xref:System.Windows.Controls.Button> のサブクラス全体を実装しています。このサブクラスは別個のアセンブリとして構築され、別個の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ページでカスタム クラスとしてインスタンス化されます。 これはサブクラス化されたコントロールを他のコントロールで構成されたツリーに挿入できるという概念を示すものです。この状況では、このようなコントロールのカスタム イベントには、あらゆるネイティブ [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 要素とまったく同じイベント ルーティング機能が与えられます。  
  
 [!code-csharp[RoutedEventCustom#CustomClass](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/SDKSampleLibrary/class1.cs#customclass)]
 [!code-vb[RoutedEventCustom#CustomClass](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RoutedEventCustom/VB/SDKSampleLibrary/Class1.vb#customclass)]  
  
 [!code-xaml[RoutedEventCustom#Page](~/samples/snippets/csharp/VS_Snippets_Wpf/RoutedEventCustom/CSharp/RoutedEventCustomApp/default.xaml#page)]  
  
 トンネル イベントは同じように作成されますが、<xref:System.Windows.RoutedEvent.RoutingStrategy%2A> は登録呼び出しで <xref:System.Windows.RoutingStrategy.Tunnel> に設定されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のトンネル イベントには接頭辞として "Preview" という単語が付く決まりになっています。  
  
 バブリング イベントの動作例については、「[ルーティング イベントを処理する](how-to-handle-a-routed-event.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [ルーティング イベントの概要](routed-events-overview.md)
- [入力の概要](input-overview.md)
- [コントロールの作成の概要](../controls/control-authoring-overview.md)
