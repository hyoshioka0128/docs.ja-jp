---
title: '方法: 中抜きの文字列を作成する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- typography [WPF], linear gradient brush
- outlined text [WPF]
- gradient brush [WPF]
- linear gradient brush [WPF]
- typography [WPF], outline effects
ms.assetid: 4aa3cf6e-1953-4f26-8230-7c1409e5f28d
ms.openlocfilehash: 86bfa396a2aa44eb511c014687501d60e170a396
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278926"
---
# <a name="how-to-create-outlined-text"></a>方法: 中抜きの文字列を作成する

ほとんどの場合、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションでテキスト文字列に装飾を追加するときは、不連続の文字またはグリフのコレクションという観点でテキストを使用します。 たとえば、線状グラデーション ブラシを作成し、<xref:System.Windows.Controls.TextBox> オブジェクトの <xref:System.Windows.Controls.Control.Foreground%2A> プロパティにそれを適用します。 テキスト ボックスを表示または編集すると、テキスト文字列内の現在の文字セットに線状グラデーション ブラシが自動的に適用されます。  
  
 ![線形グラデーション ブラシで表示されるテキスト](./media/how-to-create-outlined-text/text-linear-gradient.jpg)
  
 しかし、テキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換し、他の種類の見た目がリッチなテキストを作成することもできます。 たとえば、テキスト文字列のアウトラインに基づいて <xref:System.Windows.Media.Geometry> オブジェクトを作成できます。  
  
 ![線形グラデーション ブラシを使用するテキスト アウトライン](./media/how-to-create-outlined-text/text-outline-linear-gradient.jpg)  
  
 テキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換すると、テキストは文字の集まりではなくなります。つまり、文字列内の文字を変更することはできません。 ただし、変換されたテキストのストロークおよび塗りつぶしのプロパティを変更することで、テキストの外観を変えることができます。 ストロークは、変換したテキストのアウトラインを参照します。塗りつぶしは、変換したテキストのアウトラインの内側の領域を参照します。  
  
 変換されたテキストのストロークと塗りつぶしを変更することで、視覚効果を作成するいくつかの方法の例を次に示します。  
  
 ![塗りつぶしとストロークに別の色を使用するテキスト](./media/how-to-create-outlined-text/fill-stroke-text-effect.jpg)  
  
 ![ストロークに適用されるイメージ ブラシを含むテキスト](./media/how-to-create-outlined-text/image-brush-application.jpg)
  
 また、変換されたテキストの境界ボックスの四角形 (強調表示) を変更することもできます。 変換されたテキストのストロークと強調表示を変更することで、視覚効果を作成する方法の例を次に示します。  
  
 ![ストロークと強調表示に適用されるイメージ ブラシを含むテキスト](./media/how-to-create-outlined-text/image-brush-text-application.jpg)

## <a name="example"></a>例  
 テキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換するときに重要なのは、<xref:System.Windows.Media.FormattedText> オブジェクトを使用することです。 このオブジェクトを作成したら、<xref:System.Windows.Media.FormattedText.BuildGeometry%2A> メソッドと <xref:System.Windows.Media.FormattedText.BuildHighlightGeometry%2A> メソッドを使用して、テキストを <xref:System.Windows.Media.Geometry> オブジェクトに変換できます。 最初のメソッドでは、書式設定されたテキストのジオメトリが返されます。2 番目のメソッドでは、書式設定されたテキストの境界ボックスのジオメトリが返されます。 次のコード例では、<xref:System.Windows.Media.FormattedText> オブジェクトを作成し、書式設定されたテキストとその境界ボックスのジオメトリを取得する方法を示します。  
  
 [!code-csharp[OutlineTextControlViewer#CreateText](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#createtext)]
 [!code-vb[OutlineTextControlViewer#CreateText](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#createtext)]  
  
 取得した <xref:System.Windows.Media.Geometry> オブジェクトを表示するには、変換されたテキストを表示するオブジェクトの <xref:System.Windows.Media.DrawingContext> にアクセスする必要があります。 これらのコード例では、ユーザー定義のレンダリングをサポートするクラスから派生したカスタム コントロール オブジェクトを作成することによって、このアクセスを実現しています。  
  
 カスタム コントロールで <xref:System.Windows.Media.Geometry> オブジェクトを表示するには、<xref:System.Windows.UIElement.OnRender%2A> メソッドのオーバーライドを指定します。 オーバーライドされたメソッドでは、<xref:System.Windows.Media.DrawingContext.DrawGeometry%2A> メソッドを使用して、<xref:System.Windows.Media.Geometry> オブジェクトを描画する必要があります。  
  
 [!code-csharp[OutlineTextControlViewer#OnRender](~/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs#onrender)]
 [!code-vb[OutlineTextControlViewer#OnRender](~/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb#onrender)]  
  
  カスタム ユーザー コントロール オブジェクトの例のソースについては、[C# の場合は OutlineTextControl.cs](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/OutlineTextControlViewer/CSharp/OutlineTextControl.cs) を、[Visual Basic の場合は OutlineTextControl.vb](https://github.com/dotnet/docs/blob/master/samples/snippets/visualbasic/VS_Snippets_Wpf/OutlineTextControlViewer/visualbasic/outlinetextcontrol.vb) を参照してください。
  
## <a name="see-also"></a>関連項目

- [書式設定されたテキストの描画](drawing-formatted-text.md)
