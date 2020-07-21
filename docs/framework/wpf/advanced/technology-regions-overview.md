---
title: 技術領域の概要
ms.date: 03/30/2017
helpviewer_keywords:
- window regions [WPF]
- Win32 code [WPF], WPF interoperation
- Win32 code [WPF], airspace
- airspace [WPF]
- interoperability [WPF], airspace
- Win32 code [WPF], window regions
ms.assetid: b7cc350f-b9e2-48b1-be14-60f3d853222e
ms.openlocfilehash: 0b6ad222737f992da3074770fb5a2bff17860c00
ms.sourcegitcommit: 9a97c76e141333394676bc5d264c6624b6f45bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75740294"
---
# <a name="technology-regions-overview"></a>技術領域の概要
WPF、Win32、DirectX などのアプリケーションで複数の表示テクノロジを使用する場合、共通のトップレベル ウィンドウ内のレンダリング領域を共有する必要があります。 このトピックでは、WPF 相互運用アプリケーションの表示と入力に影響する可能性がある問題について説明します。  
  
## <a name="regions"></a>領域  
 トップレベル ウィンドウ内では、相互運用アプリケーションのテクノロジの 1 つを構成する各 HWND に独自の領域 ("空域" とも呼ばれます) があることを概念化することができます。 ウィンドウ内の個々のピクセルは 1 つの HWND に属し、それによってその HWND の領域が構成されます (厳密に言えば、複数の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] HWND がある場合は複数の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 領域がありますが、この説明の目的として、存在するのは 1 つのみと想定してください)。 この領域は、すべてのレイヤーまたは他のウィンドウは、アプリケーションの有効期間中にそのピクセル上にレンダリングされる場合、同じレンダリングレベル テクノロジに含まれる必要があることを意味します。 Win32 で [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ピクセルをレンダリングしようとすると、望ましくない結果が生じるため、可能な限り相互運用 API によって禁止されます。  
  
### <a name="region-examples"></a>領域の例  
 次の図は、Win32、DirectX、および [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] が混在するアプリケーションを示しています。 各テクノロジには個別の重複しないピクセル セットが使用されているので、領域に関する問題はありません。  
  
 ![Win32、DirectX、および WPF が混在するアプリケーションの例。](./media/technology-regions-overview/win32-directx-windows-presentation-foundation-application.png)  
  
 このアプリケーションでは、マウス ポインターの位置を使用して、これら 3 つの領域のいずれかにレンダリングされるアニメーションが作成されるとします。 アニメーションにどのようなテクノロジが使われたかにかかわらず、そのテクノロジは他の 2 つの領域に違反しています。 次の図は、Win32 領域上に WPF の円をレンダリングする試行を示しています。  
  
 ![Win32 領域上に WPF の円をレンダリングする試行。](./media/technology-regions-overview/render-windows-presentation-foundation-circle-over-win32-region.png)  
  
 もう 1 つの違反は、異なるテクノロジ間で透明度またはアルファ ブレンドを使用しようとする場合です。  次の図の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ボックスは Win32 および DirectX 領域に違反しています。 その [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]ボックスのピクセルは半透明なので、DirectX と [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の両方によって共同で所有される必要がありますが、それは不可能です。  そのため、これはもう 1 つの違反であり、構築できません。  
  
 ![Win32 および DirectX 領域に違反する WPF ボックスを示す図。](./media/technology-regions-overview/windows-foundation-presentation-box-violate-win32-directx-region.png)  
  
 前述した 3 つの例では四角形の領域を使用しましたが、異なるシェイプも考えられます。  たとえば、穴のある領域も使用できます。 次の図は、四角形の穴がある Win32 領域を示しています。これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 領域と DirectX 領域を合わせたサイズです。  
  
 ![四角形の穴がある Win32 領域を示す図。](./media/technology-regions-overview/win32-region-rectangular-hole.png)  
  
 領域は、完全に四角形以外にすることや、Win32 HRGN (領域) で記述できる任意のシェイプにすることができます。  
  
 ![四角形以外の領域を示す図。](./media/technology-regions-overview/nonrectangular-win32-region.png)  
  
## <a name="transparency-and-top-level-windows"></a>透明度とトップレベル ウィンドウ  
 Windows のウィンドウ マネージャーでは、実際には Win32 HWND のみが処理されます。 そのため、すべての [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Window> は HWND です。 <xref:System.Windows.Window> HWND は、すべての HWND の一般的な規則に従う必要があります。 その HWND 内で、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コードでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API 全体がサポートするあらゆることを実行できます。 ただし、デスクトップ上の他の HWND との相互作用の場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は Win32 処理とレンダリング規則に従う必要があります。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、Win32 API (四角形以外のウィンドウには HRGN、ピクセル単位のアルファにはレイヤード ウィンドウ) を使用することで、四角形以外のウィンドウをサポートしています。  
  
 定数アルファ キーとカラー キーはサポートされていません。  Win32 レイヤード ウィンドウ機能は、プラットフォームによって異なります。  
  
 レイヤード ウィンドウは、ウィンドウ内のすべてのピクセルに適用するアルファ値を指定することにより、ウィンドウ全体を半透明にすることができます  (Win32 では実際にはピクセル単位のアルファをサポートしていますが、このモードでは、ダイアログやドロップダウンを含め、子 HWND を自分で描画する必要があるため、これを実際のプログラムで使用するのは非常に困難です)。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では HRGN をサポートしています。ただし、この機能用のマネージド API はありません。 プラットフォームの呼び出しと <xref:System.Windows.Interop.HwndSource> を使用して、関連する Win32 API を呼び出すことができます。 詳細については、「[マネージド コードからのネイティブ関数の呼び出し](/cpp/dotnet/calling-native-functions-from-managed-code)」を参照してください。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] レイヤード ウィンドウは、オペレーティング システムによって機能が異なります。 これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] にレンダリングに DirectX が使用され、レイヤード ウィンドウが DirectX レンダリングではなく主に GDI レンダリング用に設計されたためです。  
  
- WPF では、ハードウェア アクセラレータによるレイヤード ウィンドウをサポートしています。  
  
- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では透明カラー キーをサポートしていません。これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では要求された正確な色のレンダリングを保証できないためです。レンダリングにハードウェア アクセラレータが使用される場合は特にそうです。  
  
## <a name="see-also"></a>関連項目

- [WPF と Win32 の相互運用性](wpf-and-win32-interoperation.md)
- [チュートリアル: Win32 での WPF クロックのホスト](walkthrough-hosting-a-wpf-clock-in-win32.md)
- [WPF での Win32 コンテンツのホスト](hosting-win32-content-in-wpf.md)
