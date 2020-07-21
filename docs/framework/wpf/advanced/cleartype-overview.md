---
title: ClearType の概要
ms.date: 03/30/2017
helpviewer_keywords:
- typography [WPF], ClearType technology
- ClearType [WPF], technology
ms.assetid: 7e2392e0-75dc-463d-a716-908772782431
ms.openlocfilehash: b76c0cb04e5de498374cbf28c8813fe5c95d41ae
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186165"
---
# <a name="cleartype-overview"></a>ClearType の概要
このトピックでは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で使用されている Microsoft ClearType テクノロジの概要について説明します。  

<a name="overview"></a>
## <a name="technology-overview"></a>テクノロジの概要  
 ClearType は、ラップトップや Pocket PC の画面、フラット パネル モニターなど、既存の LCD (液晶ディスプレイ) でのテキストの読みやすさを向上させるために Microsoft によって開発されたソフトウェア テクノロジです。  ClearType は、LCD 画面の各ピクセル内の個々の垂直カラー ストライプ要素にアクセスすることによって機能します。 ClearType が開発されるまでは、コンピューターで表示可能な最小の詳細レベルは 1 ピクセルでしたが、ClearType を LCD モニターで実行することで、テキストの各部分の幅が 1 ピクセルより小さくても表示できるようになりました。 解像度が上がるとテキスト表示の微細部の鮮明度が高くなるため、長時間にわたって読んでも苦になりません。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で利用可能な ClearType は、Microsoft Windows グラフィックス デバイス インターフェイス (GDI) に含まれるバージョンにいくつかの改良が加えられた最新世代の ClearType です。  
  
<a name="sub-pixel_positioning"></a>
## <a name="sub-pixel-positioning"></a>サブピクセル ポジショニング  
 ClearType の以前のバージョンから大きく改善された点の 1 つに、サブピクセル ポジショニングの使用があります。 GDI に含まれている ClearType の実装とは異なり、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の ClearType では、ピクセルの境界から開始するグリフだけでなく、ピクセルの途中から開始するグリフも表示できます。 グリフの配置の解像度が上がることにより、グリフの間隔や比率の正確さや一貫性が増します。  
  
 次の 2 つの例は、サブピクセル ポジショニングを使用した場合にサブピクセル境界でグリフを開始できることを示しています。 左側の例は、サブピクセル ポジショニングが採用されていない、以前のバージョンの ClearType レンダラーを使用してレンダリングしたものです。 右側の例は、新しいバージョンの ClearType レンダラーで、サブピクセル ポジショニングを使用してレンダリングしたものです。 右側のイメージの **e** と **l** が、それぞれ異なるサブピクセルから開始しているために若干異なってレンダリングされていることに注意してください。 グリフ イメージはハイ コントラストであるため、テキストを標準サイズで画面に表示したときは、この違いはわかりません。 これは、ClearType に組み込まれている高度なカラー フィルター処理によってのみ実現されます。  
  
 ![2 つのバージョンの ClearType を使用して表示されるテキスト](./media/wcpsdk-mmgraphics-text-cleartype-overview-01.png "wcpsdk_mmgraphics_text_cleartype_overview_01")  
ClearType の以前のバージョンと新しいバージョンを使用して表示されるテキスト  
  
 次の 2 つの例では、以前のバージョンの ClearType レンダラーでの出力と、新バージョンの ClearType レンダラーでの出力が比較されています。 右側に示したサブピクセル ポジショニングでは、画面上の文字の間隔が大きく改善されています。特に、サブピクセル 1 個とピクセル 1 個の差がグリフの幅に占める割合の大きい、小さなサイズの場合によくわかります。 2 番目のイメージの方が、文字の間隔が均等に近くなっています。 サブピクセル ポジショニングによるさまざまなメリットがテキスト画面全体の外観に及ぼす効果は大幅に増加しましたが、これは ClearType テクノロジが大きく進歩したことを表しています。  
  
 ![以前のバージョンの ClearType を使用して表示されるテキスト](./media/wcpsdk-mmgraphics-text-cleartype-overview-02.png "wcpsdk_mmgraphics_text_cleartype_overview_02")  
ClearType の以前のバージョンと新しいバージョンを使用したテキスト  
  
<a name="y-direction_antialiasing"></a>
## <a name="y-direction-antialiasing"></a>Y 方向のアンチエイリアシング  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] での ClearType のもう 1 つの改善点は、y 方向のアンチエイリアシングです。 y 方向のアンチエイリアシングが行われない GDI の ClearType では、x 軸上では高い解像度を得られますが、y 軸上では解像度が低くなります。 緩やかな曲線部分の上下では、境界がギザギザになって読みにくくなります。  
  
 次の例では、y 方向のアンチエイリアシングを使用しない場合の効果を示します。 この場合、文字の上下で境界がギザギザになっていることがよくわかります。  
  
 ![緩やかな曲線上にギザギザした境界が付いたテキスト](./media/wcpsdk-mmgraphics-text-cleartype-overview-03.png "wcpsdk_mmgraphics_text_cleartype_overview_03")  
緩やかな曲線上にギザギザした境界が付いたテキスト  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の ClearType には、ギザギザした境界を滑らかにする y 方向レベルのアンチエイリアシング機能があります。 これは、東アジア言語を読みやすくするために特に重要です。これらの言語の表意文字では、緩やかな曲線の量が水平方向と垂直方向でほぼ同じであるからです。  
  
 次の例では、y 方向のアンチエイリアシングの効果を示します。 この場合、文字の上下の曲線が滑らかに表示されています。  
  
 ![ClearType の y 方向アンチエイリアシングを適用したテキスト](./media/wcpsdk-mmgraphics-text-cleartype-overview-04.png "wcpsdk_mmgraphics_text_cleartype_overview_04")  
ClearType の y 方向アンチエイリアシングを適用したテキスト  
  
<a name="hardware_acceleration"></a>
## <a name="hardware-acceleration"></a>ハードウェアの高速化  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の ClearType では、ハードウェア アクセラレーションを利用してパフォーマンスが向上し、CPU の負荷および必要なシステム メモリが削減されます。 グラフィックス カードのピクセル シェーダーおよびビデオ メモリを使用することにより、ClearType では特にアニメーション使用時のテキストのレンダリングが速くなります。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の ClearType では、システム全体の ClearType の設定は変更されません。 Windows で ClearType を無効にすると、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のアンチエイリアシングはグレースケール モードに設定されます。 また、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の ClearType によって、[ClearType Tuner PowerToy](https://www.microsoft.com/typography/ClearTypePowerToy.mspx) の設定が変更されることはありません。  
  
 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のアーキテクチャ設計における決定事項の 1 つに、解像度に依存しないレイアウトによる高解像度 DPI モニターのサポート向上があります。高解像度モニターの普及は進みつつあるからです。 この決定を受けて、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] ではエイリアス化されたテキスト レンダリングや、一部の東アジア言語フォントのビットマップをサポートしないことになりました。これらはどちらも解像度に依存するためです。  
  
<a name="further_information"></a>
## <a name="further-information"></a>詳細情報  
 [ClearType の情報](https://www.microsoft.com/typography/ClearTypeInfo.mspx)  
  
 [ClearType Tuner PowerToy](https://www.microsoft.com/typography/ClearTypePowerToy.mspx)  
  
## <a name="see-also"></a>関連項目

- [ClearType レジストリの設定](cleartype-registry-settings.md)
