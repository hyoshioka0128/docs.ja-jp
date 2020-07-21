---
title: ビットマップ効果の概要
ms.date: 03/30/2017
helpviewer_keywords:
- bitmap effects [WPF]
ms.assetid: 23cb338e-4b59-4b52-b294-96431f9c9568
ms.openlocfilehash: 4a5e73f21d4ce4988f56c139d13038dca902b5b1
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187000"
---
# <a name="bitmap-effects-overview"></a>ビットマップ効果の概要
ビットマップ効果を使用すると、設計者と開発者は、レンダリングされる Windows Presentation Foundation (WPF) コンテンツに視覚効果を適用できます。 たとえば、ビットマップ効果では、<xref:System.Windows.Media.Effects.DropShadowBitmapEffect> 効果またはぼかし効果をイメージやボタンに簡単に適用できます。  
  
> [!IMPORTANT]
> .NET Framework 4 以降では、<xref:System.Windows.Media.Effects.BitmapEffect> クラスが廃止されています。 <xref:System.Windows.Media.Effects.BitmapEffect> クラスを使用しようとすると、廃止に関する例外が発生します。 <xref:System.Windows.Media.Effects.BitmapEffect> クラスの廃止されていない代替クラスは、<xref:System.Windows.Media.Effects.Effect> クラスです。 ほとんどの場合、<xref:System.Windows.Media.Effects.Effect> クラスの方がはるかに高速です。  

<a name="wpf_effects"></a>
## <a name="wpf-bitmap-effects"></a>WPF のビットマップ効果  
 ビットマップ効果 (<xref:System.Windows.Media.Effects.BitmapEffect> オブジェクト) は、簡単なピクセル処理操作です。 ビットマップ効果は、入力として <xref:System.Windows.Media.Imaging.BitmapSource> を受け取り、効果 (ぼかしやドロップ シャドウなど) を適用した後で、新しい <xref:System.Windows.Media.Imaging.BitmapSource> を生成します。 各ビットマップ効果では、フィルター処理プロパティを制御できるプロパティが公開されています (<xref:System.Windows.Media.Effects.BlurBitmapEffect> の <xref:System.Windows.Media.Effects.BlurBitmapEffect.Radius%2A> など)。  
  
 特殊なケースとして、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、効果をライブ <xref:System.Windows.Media.Visual> オブジェクトのプロパティとして設定できます (<xref:System.Windows.Controls.Button> や <xref:System.Windows.Controls.TextBox> など)。 ピクセル処理は、実行時に適用されてレンダリングされます。 この場合、レンダリング時に、<xref:System.Windows.Media.Visual> が同等の <xref:System.Windows.Media.Imaging.BitmapSource> に自動的に変換され、<xref:System.Windows.Media.Effects.BitmapEffect> への入力としてフィードされます。 出力は、<xref:System.Windows.Media.Visual> オブジェクトの既定のレンダリング動作を置き換えます。 このため、<xref:System.Windows.Media.Effects.BitmapEffect> オブジェクトでは、ビジュアル オブジェクトがソフトウェアのみでレンダリングされるよう強制されます。つまり、効果の適用時にハードウェア アクセラレーションは利用されません。  
  
- <xref:System.Windows.Media.Effects.BlurBitmapEffect> は、オブジェクトのピントが外れた表示をシミュレートします。  
  
- <xref:System.Windows.Media.Effects.OuterGlowBitmapEffect> は、オブジェクトの周囲に色の付いた光輪を作成します。  
  
- <xref:System.Windows.Media.Effects.DropShadowBitmapEffect> は、オブジェクトの後ろに影を作成します。  
  
- <xref:System.Windows.Media.Effects.BevelBitmapEffect> は、指定された曲線に従ってイメージの表面を浮き上がらせるベベルを作成します。  
  
- <xref:System.Windows.Media.Effects.EmbossBitmapEffect> は、人工光源からの奥行きと質感の印象を与えるために、<xref:System.Windows.Media.Visual> のバンプ マッピングを作成します。  
  
> [!NOTE]
> WPF のビットマップ効果は、ソフトウェア モードでレンダリングされます。 効果を適用するオブジェクトも、ソフトウェアでレンダリングされます。 大きなビジュアルにビットマップ効果を使うとき、またはビットマップ効果のプロパティをアニメーション化するときに、パフォーマンスが最も低下します。 このような方法ではビットマップ効果をまったく使ってはならないということではありませんが、注意を払い、十分にテストを行って、ユーザー エクスペリエンスが期待どおりになることを確認する必要があります。  
  
> [!NOTE]
> WPF のビットマップ効果は、部分信頼の実行をサポートしていません。 ビットマップ効果を使うには、アプリケーションが完全な信頼のアクセス許可を持つ必要があります。  
  
<a name="applyeffects"></a>
## <a name="how-to-apply-an-effect"></a>効果を適用する方法  
 <xref:System.Windows.Media.Effects.BitmapEffect> は <xref:System.Windows.Media.Visual> のプロパティです。 したがって、<xref:System.Windows.Controls.Button>、<xref:System.Windows.Controls.Image>、<xref:System.Windows.Media.DrawingVisual>、<xref:System.Windows.UIElement> などのビジュアル オブジェクトには、プロパティを設定するだけで簡単に効果を適用できます。 <xref:System.Windows.UIElement.BitmapEffect%2A> を 1 つの <xref:System.Windows.Media.Effects.BitmapEffect> オブジェクトに設定することも、<xref:System.Windows.Media.Effects.BitmapEffectGroup> オブジェクトを使用して複数の効果を連鎖させることもできます。  
  
 次の例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で <xref:System.Windows.Media.Effects.BitmapEffect> を適用する方法を示します。  
  
 [!code-xaml[EffectsGallery_snip#BlurSimpleExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blursimpleexample.xaml#blursimpleexampleinline)]  
  
 次の例では、コードで <xref:System.Windows.Media.Effects.BitmapEffect> を適用する方法を示します。  
  
 [!code-csharp[EffectsGallery_snip#CodeBehindBlurCodeBehindExampleInline](~/samples/snippets/csharp/VS_Snippets_Wpf/EffectsGallery_snip/CSharp/blurcodebehindexample.xaml.cs#codebehindblurcodebehindexampleinline)]  
  
> [!NOTE]
> <xref:System.Windows.Media.Effects.BitmapEffect> を <xref:System.Windows.Controls.DockPanel> や <xref:System.Windows.Controls.Canvas> などのレイアウト コンテナーに適用すると、すべての子要素を含む、要素つまりビジュアル オブジェクトのビジュアル ツリーに効果が適用されます。  
  
<a name="customeffects"></a>
## <a name="creating-custom-effects"></a>カスタム効果の作成  
 WPF では、マネージド WPF アプリケーションで使用できるカスタム効果を作成するためのアンマネージド インターフェイスも提供されています。 カスタム ビットマップ効果の作成に関する参考資料については、「[Unmanaged WPF Bitmap Effect](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh)」(アンマネージ WPF ビットマップ効果) ドキュメントをご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Effects.BitmapEffectGroup>
- <xref:System.Windows.Media.Effects.BitmapEffectInput>
- <xref:System.Windows.Media.Effects.BitmapEffectCollection>
- [アンマネージ WPF ビットマップ効果](https://docs.microsoft.com/previous-versions/windows/desktop/wibe/-wibe-lh)
- [イメージングの概要](imaging-overview.md)
- [セキュリティ](../security-wpf.md)
- [WPF グラフィックス レンダリングの概要](wpf-graphics-rendering-overview.md)
- [2D グラフィックスとイメージング](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
