---
title: '方法: 影付きテキストを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], shadow effects
- shadow effects in text [WPF]
- text [WPF], shadowed
ms.assetid: 6ab9c754-6001-4708-b479-5367f2fd1a35
ms.openlocfilehash: c3e8135372ce4a092552c812cd971cb70bc49bf3
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186842"
---
# <a name="how-to-create-text-with-a-shadow"></a>方法: 影付きテキストを作成する
このセクションの例で、表示されるテキストに影を付ける方法を紹介します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Media.Effects.DropShadowEffect> オブジェクトを使用すると、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] オブジェクトにさまざまなドロップ シャドウ効果を付けることができます。 テキストにドロップ シャドウ効果を適用した例を次に示します。 この場合、影はソフト シャドウです。つまり、影の色がぼやけています。  
  
 ![ぼかし &#61; 0.25 のテキスト シャドウ](./media/how-to-create-text-with-a-shadow/drop-shadow-text-effect.jpg)
  
 <xref:System.Windows.Media.Effects.DropShadowEffect.ShadowDepth%2A> プロパティを設定することで、影の幅を変更できます。 値が `4.0` の場合、影の幅は 4 ピクセルになります。 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> プロパティを変更すると、影の柔らかさ、つまりぼかし具合を調整できます。 値が `0.0` の場合、ぼかしはありません。 ソフト シャドウを付ける方法を次のコード例に示します。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet1](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet1)]  
  
> [!NOTE]
> これらの影効果は、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] テキスト レンダリング パイプラインを通過しません。 結果として、これらの効果の利用時、ClearType が無効になります。  
  
 テキストにハード シャドウ効果を適用した例を次に示します。 この場合、影はぼかされません。  
  
 ![ぼかし &#61; 0 のテキスト シャドウ](./media/how-to-create-text-with-a-shadow/text-shadow-softness.jpg)
  
 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> プロパティを `0.0` に設定してぼかしなしにすると、ハード シャドウを作成できます。 <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> プロパティを変更すると、影の方向を変更できます。 このプロパティの方向値を `0` から `360` の角度に設定します。 次の図では、<xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> プロパティ設定の方向値を確認できます。  
  
 ![シャドウの DropShadow 度の設定](./media/how-to-create-text-with-a-shadow/drop-shadow-degree-setting.png)
  
 ハード シャドウを付ける方法を次のコード例に示します。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet2](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet2)]  
  
## <a name="using-a-blur-effect"></a>ぼかし効果を使用する  
 <xref:System.Windows.Media.Effects.BlurBitmapEffect> を使用して、テキスト オブジェクトの後ろに配置できる影のような効果を作成できます。 テキストに適用されたぼかしビットマップ効果は、全方向に均等にテキストをぼかします。  
  
 テキストにぼかし効果が適用されている例を次に示します。  
  
 ![BlurBitmapEffect を使用するテキスト シャドウ](./media/how-to-create-text-with-a-shadow/text-shadow-blur-effect.jpg)  
  
 ぼかし効果を付ける方法を次のコード例に示します。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet6](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/BlurShadows.xaml#textshadowsnippet6)]  
  
## <a name="using-a-translate-transform"></a>TranslateTransform を使用する  
 <xref:System.Windows.Media.TranslateTransform> を使用して、テキスト オブジェクトの後ろに配置できる影のような効果を作成できます。  
  
 次のコード例では、<xref:System.Windows.Media.TranslateTransform> を使用してテキストに影のような効果を付けています。 この例では、メインのテキストの下にわずかに中心をずらしたコピーが付き、影のような効果を作っています。  
  
 ![TranslateTransform を使用するテキスト シャドウ](./media/how-to-create-text-with-a-shadow/text-transform-shadow-effect.jpg)
  
 TranslateTransform を利用して影のような効果を付ける方法を次のコード例に示します。  
  
 [!code-xaml[TextShadowSnippets#TextShadowSnippet7](~/samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/TransformShadows.xaml#textshadowsnippet7)]
