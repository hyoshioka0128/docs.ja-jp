---
title: '方法: PriorityBinding を実装する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data binding [WPF], PriorityBinding class
ms.assetid: d63b65ab-b3e9-4322-9aa8-1450f8d89532
ms.openlocfilehash: 343b0aca4736905f3a0cbff5a0f76b170da0c920
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73459785"
---
# <a name="how-to-implement-prioritybinding"></a>方法: PriorityBinding を実装する
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の <xref:System.Windows.Data.PriorityBinding> は、バインディングのリストを指定することによって機能します。 バインディングのリストは、優先順位が最も高いものから低いものの順に並べられています。 処理時に最も優先順位の高いバインディングから値が正常に返された場合、リスト内の他のバインディングを処理する必要はありません。 最も優先順位の高いバインディングの評価に長い時間がかかっているため、優先順位が高いバインディングから値が正常に返されるまで、次に優先順位が高くて値が正常に返されるバインディングが使用される場合があります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Data.PriorityBinding> 動作を示すため、3 つのプロパティ `FastDP`、`SlowerDP`、`SlowestDP` を含む `AsyncDataSource` オブジェクトが作成されています。  
  
 `FastDP` の get アクセサーでは、`_fastDP` データ メンバーの値が返されます。  
  
 `SlowerDP` の get アクセサーでは、3 秒間待ってから、`_slowerDP` データ メンバーの値が返されます。  
  
 `SlowestDP` の get アクセサーでは、5 秒間待ってから、`_slowestDP` データ メンバーの値が返されます。  
  
> [!NOTE]
> この例は、デモンストレーション目的のみで提供されます。 .NET のガイドラインでは、フィールド セットよりはるかに遅いプロパティは定義しないように推奨されています。 詳細については、「[プロパティとメソッドの選択](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/ms229054(v=vs.100))」を参照してください。  
  
 [!code-csharp[PriorityBinding#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml.cs#1)]
 [!code-vb[PriorityBinding#1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PriorityBinding/VisualBasic/AsyncDataSource.vb#1)]  
  
 <xref:System.Windows.Controls.TextBlock.Text%2A> プロパティは、<xref:System.Windows.Data.PriorityBinding> を使用して上記の `AsyncDS` にバインドされます。  
  
 [!code-xaml[PriorityBinding#2](~/samples/snippets/csharp/VS_Snippets_Wpf/PriorityBinding/CSharp/Window1.xaml#2)]  
  
 バインディング エンジンでは、<xref:System.Windows.Data.Binding> オブジェクトを処理するときに、`SlowestDP` プロパティにバインドされている最初の <xref:System.Windows.Data.Binding> から開始されます。 この <xref:System.Windows.Data.Binding> は処理されても 5 秒間スリープ状態になるため値が正常に返されないので、次の <xref:System.Windows.Data.Binding> 要素が処理されます。 次の <xref:System.Windows.Data.Binding> も 3 秒間スリープするため、値が正常に返されません。 バインディング エンジンは、次に、`FastDP` プロパティにバインドされている <xref:System.Windows.Data.Binding> 要素に移動します。 この <xref:System.Windows.Data.Binding> では、値 "Fast Value" が返されます。 <xref:System.Windows.Controls.TextBlock> に値 "Fast Value" が表示されます。  
  
 3 秒経過すると、`SlowerDP` プロパティから値 "Slower Value" が返されます。 <xref:System.Windows.Controls.TextBlock> に、値 "Slower Value" が表示されます。  
  
 5 秒経過すると、`SlowestDP` プロパティから値 "Slowest Value" が返されます。 そのバインディングは、リストの先頭にあるので最も高い優先順位です。 <xref:System.Windows.Controls.TextBlock> に値 "Slowest Value" が表示されます。  
  
 何をもってバインディングからの戻り値が成功と見なされるかについては、<xref:System.Windows.Data.PriorityBinding> を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.Binding.IsAsync%2A?displayProperty=nameWithType>
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [方法トピック](data-binding-how-to-topics.md)
