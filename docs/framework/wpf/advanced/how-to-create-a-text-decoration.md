---
title: '方法: 文字の装飾を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- fonts [WPF], baseline
- text [WPF], decorations
- fonts [WPF], underline
- fonts [WPF], overline
- strikethrough type [WPF]
- fonts [WPF], strikethrough
- overline type [WPF]
- underline type [WPF]
- typography [WPF], text decorations
- baseline type [WPF]
ms.assetid: cf3cb4e7-782a-4be7-b2d4-e0935e21e4e0
ms.openlocfilehash: cf3b3c3bcb75153a0be4f7ced03b38134b79a930
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79185924"
---
# <a name="how-to-create-a-text-decoration"></a>方法: 文字の装飾を作成する
<xref:System.Windows.TextDecoration> オブジェクトは、テキストに追加できるビジュアルな装飾です。 文字の装飾には、下線、ベースライン、取り消し線、上線の 4 種類があります。 次の例では、テキストに対する相対的なテキスト装飾の位置を示します。  
  
 ![テキスト装飾の種類の図](./media/how-to-create-a-text-decoration/text-decoration-types.gif)  
  
 テキストにテキスト装飾を追加するには、<xref:System.Windows.TextDecoration> オブジェクトを作成して、そのプロパティを変更します。 テキスト装飾を表示する場所 (下線など) を指定するには、<xref:System.Windows.TextDecoration.Location%2A> プロパティを使用します。 塗りつぶしやグラデーションの色など、テキスト装飾の外観を指定するには、<xref:System.Windows.TextDecoration.Pen%2A> プロパティを使用します。 <xref:System.Windows.TextDecoration.Pen%2A> プロパティの値を指定しない場合、修飾は既定で、テキストと同じ色になります。 <xref:System.Windows.TextDecoration> オブジェクトを定義したら、それを対象のテキスト オブジェクトの <xref:System.Windows.TextDecorations> コレクションに追加します。  
  
 次の例では、線状グラデーション ブラシと破線ペンのスタイルに設定されたテキスト装飾を示します。  
  
 ![線形グラデーション下線を使用したテキスト装飾](./media/how-to-create-a-text-decoration/text-decoration-gradient.png)  
  
 <xref:System.Windows.Documents.Hyperlink> オブジェクトは、インライン レベルのフロー コンテンツ要素であり、フロー コンテンツ内のハイパーリンクをホストすることができます。 既定では、<xref:System.Windows.Documents.Hyperlink> では下線を表示するために <xref:System.Windows.TextDecoration> オブジェクトが使用されます。 <xref:System.Windows.TextDecoration> オブジェクトをインスタンス化するときは大きな負荷がかかる場合があり、<xref:System.Windows.Documents.Hyperlink> オブジェクトの数が多い場合は特にそうです。 <xref:System.Windows.Documents.Hyperlink> 要素を広範に使用する場合は、<xref:System.Windows.ContentElement.MouseEnter> イベントなどのイベントをトリガーするときにのみ下線を表示することを検討する必要があります。  
  
 次の例では、"My MSN" のリンクに対する下線は動的であり、<xref:System.Windows.ContentElement.MouseEnter> イベントがトリガーされたときにだけ表示されます。  
  
 ![TextDecorations を表示するハイパーリンク](./media/how-to-create-a-text-decoration/text-decorations-hyperlinks.png)  

 詳細については、「[方法: ハイパーリンクに下線を引くかどうかを指定する](how-to-specify-whether-a-hyperlink-is-underlined.md)」を参照してください。  
  
## <a name="example"></a>例  
 次のコード例の下線テキスト装飾では、既定のフォント値が使用されています。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets1)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets1)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets1)]  
  
 次のコード例の下線テキスト装飾は、ペンに対する単色ブラシで作成されています。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets2)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets2)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets2)]  
  
 次のコード例の下線テキスト装飾は、破線のペンに対する線状グラデーション ブラシで作成されています。  
  
 [!code-csharp[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml.cs#textdecorationsnippets3)]
 [!code-vb[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextDecorationSnippets/visualbasic/window1.xaml.vb#textdecorationsnippets3)]
 [!code-xaml[TextDecorationSnippets#TextDecorationSnippets3](~/samples/snippets/csharp/VS_Snippets_Wpf/TextDecorationSnippets/CSharp/Window1.xaml#textdecorationsnippets3)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.TextDecoration>
- <xref:System.Windows.Documents.Hyperlink>
- [ハイパーリンクに下線を引くかどうかを指定する](how-to-specify-whether-a-hyperlink-is-underlined.md)
