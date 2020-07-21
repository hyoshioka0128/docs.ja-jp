---
title: パフォーマンスの最適化:ハードウェアの活用
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], performance
- hardware rendering pipeline [WPF]
- rendering tiers [WPF]
- graphics rendering tiers [WPF]
- graphics [WPF], rendering tiers
- software rendering pipeline [WPF]
ms.assetid: bfb89bae-7aab-4cac-a26c-a956eda8fce2
ms.openlocfilehash: a47a4aae785d817904c30fe7c865a1c033eb3cca
ms.sourcegitcommit: eb9ff6f364cde6f11322e03800d8f5ce302f3c73
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68709221"
---
# <a name="optimizing-performance-taking-advantage-of-hardware"></a>パフォーマンスの最適化:ハードウェアの活用
[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の内部アーキテクチャには、ハードウェアとソフトウェアの 2 つのレンダリング パイプラインがあります。 このトピックでは、アプリケーションのパフォーマンスの最適化に関する意思決定に役立つ、これらのレンダリング パイプラインについて説明します。  
  
## <a name="hardware-rendering-pipeline"></a>ハードウェア レンダリング パイプライン  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のパフォーマンスを判断するうえで最も重要な要因の 1 つは、レンダリング バインドであることです。レンダリングが必要なピクセルが多いほど、パフォーマンス コストは高くなります。 ただし、グラフィックス処理装置 (GPU) にオフロードできるレンダリングが多いほど、パフォーマンスが向上します。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション ハードウェア レンダリング パイプラインは、Microsoft DirectX バージョン 7.0 以上をサポートするハードウェアで Microsoft DirectX の機能を最大限に活用します。 Microsoft DirectX バージョン 7.0 および PixelShader 2.0 以降の機能をサポートするハードウェアでは、さらに最適化を行うことができます。  
  
## <a name="software-rendering-pipeline"></a>ソフトウェア レンダリング パイプライン  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ソフトウェア レンダリング パイプラインは、完全に CPU バインドです。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、CPU の SSE および SSE2 命令セットを利用して、最適化された、完全な機能を備えたソフトウェア ラスタライザーを実装します。 ソフトウェアへのフォールバックは、ハードウェア レンダリング パイプラインを使用してアプリケーションの機能をレンダリングできないときはいつでもシームレスに行われます。  
  
 ソフトウェア モードでレンダリングするときに発生する最大のパフォーマンスの問題は、フィル レートに関連しています。これは、レンダリングするピクセル数として定義されています。 ソフトウェア レンダリング モードのパフォーマンスに懸念がある場合は、ピクセルが再描画される回数を最小限に抑えるようにしてください。 たとえば、青色の背景を持つアプリケーションがあり、その後、少し透明な画像がその上にレンダリングされる場合、アプリケーションのすべてのピクセルを 2 回レンダリングすることになります。 その結果、アプリケーションをその画像とともにレンダリングすると、青の背景しかない場合と比べて 2 倍の時間がかかります。  
  
### <a name="graphics-rendering-tiers"></a>グラフィックスの描画層  
 アプリケーションが実行されるハードウェア構成を予測することは、非常に困難な場合があります。 しかし、アプリケーションがさまざまなハードウェア構成を最大限に活用できるように、異なるハードウェアで実行されているときに機能をシームレスに切り替えられるような設計を検討することもできます。  
  
 これを実現するために、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、実行時にシステムのグラフィックス機能を決定する機能が用意されています。 グラフィックス機能は、ビデオ カードを 3 つのレンダリング機能階層のいずれかに分類することで決定されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、アプリケーションがレンダリング機能階層に対してクエリを実行できるようにする API を公開しています。 その後、ハードウェアでサポートされている描画層に基づき、アプリケーションが実行時にさまざまなコード パスを取ります。  
  
 描画層に最も影響を与えるグラフィックス ハードウェアの機能:  
  
- **ビデオ RAM** グラフィックス ハードウェアのビデオ メモリの量で、グラフィックスの構築に利用できるバッファーのサイズと数が決まります。  
  
- **ピクセル シェーダー** ピクセル シェーダーは、ピクセル単位で効果を計算するグラフィックス処理機能です。 表示されるグラフィックスの解像度によっては、各表示フレームの処理に数百万単位のピクセルが必要になることがあります。  
  
- **頂点シェーダー** 頂点シェーダーは、オブジェクトの頂点データに数学演算を実行するグラフィックス処理機能です。  
  
- **マルチテクスチャ サポート** マルチテクスチャ サポートとは、3D グラフィックス オブジェクトにブレンド操作を実行するとき、2 つ以上の異なるテクスチャを適用できる機能のことです。 マルチテクスチャ サポートの度合いは、グラフィックス ハードウェア上のマルチテクスチャ ユニットの数で決まります。  
  
 ピクセル シェーダー、頂点シェーダー、マルチテクスチャの機能は、特定の DirectX バージョン レベルを定義するために使用されます。これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で異なる描画層を定義するために使用されます。  
  
 グラフィックス ハードウェアの機能により [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションのレンダリング能力が決まります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] システムには次の 3 つの描画層があります。  
  
- **描画層 0** グラフィックス ハードウェアの高速化はありません。 DirectX のバージョン レベルはバージョン 7.0 より前です。  
  
- **描画層 1** 部分的にグラフィックス ハードウェアが高速化されます。 DirectX のバージョン レベルは、バージョン 7.0 以上、バージョン9.0 **未満**です。  
  
- **描画層 2** ほとんどのグラフィックス機能でグラフィックス ハードウェア高速が利用されます。 DirectX のバージョン レベルは、バージョン 9.0 以上です。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の描画層の詳細については、「[グラフィックスの描画層](graphics-rendering-tiers.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [WPF アプリケーションのパフォーマンスの最適化](optimizing-wpf-application-performance.md)
- [アプリケーション パフォーマンスの計画](planning-for-application-performance.md)
- [レイアウトとデザイン](optimizing-performance-layout-and-design.md)
- [2D グラフィックスとイメージング](optimizing-performance-2d-graphics-and-imaging.md)
- [オブジェクトの動作](optimizing-performance-object-behavior.md)
- [アプリケーション リソース](optimizing-performance-application-resources.md)
- [[テキスト]](optimizing-performance-text.md)
- [データ バインディング](optimizing-performance-data-binding.md)
- [パフォーマンスに関するその他の推奨事項](optimizing-performance-other-recommendations.md)
