---
title: Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項
titleSuffix: ''
ms.date: 03/30/2017
helpviewer_keywords:
- WPF [WPF], Direct3D9 interop performance
- Direct3D9 [WPF interoperability], performance
ms.assetid: ea8baf91-12fe-4b44-ac4d-477110ab14dd
ms.openlocfilehash: 2445732c27d210a41da26303d6a9ce07ef6fcc94
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76743933"
---
# <a name="performance-considerations-for-direct3d9-and-wpf-interoperability"></a>Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項
<xref:System.Windows.Interop.D3DImage> クラスを使用して、Direct3D9 コンテンツをホストできます。 Direct3D9 コンテンツをホストすると、アプリケーションのパフォーマンスに影響する可能性があります。 このトピックでは、Windows Presentation Foundation (WPF) アプリケーションで Direct3D9 コンテンツをホストするときのパフォーマンスを最適化するためのベスト プラクティスについて説明します。 これらのベスト プラクティスには、Windows Vista、Windows XP、およびマルチモニター ディスプレイを使用している場合の <xref:System.Windows.Interop.D3DImage> の使用方法とベスト プラクティスが含まれています。  
  
> [!NOTE]
> これらのベスト プラクティスを示すコード例については、「[WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)」を参照してください。  
  
## <a name="use-d3dimage-sparingly"></a>D3DImage を慎重に使用する  
 <xref:System.Windows.Interop.D3DImage> インスタンスでホストされている Direct3D9 コンテンツは、純粋な Direct3D アプリケーションほど高速にレンダリングされません。 サーフェイスをコピーしてコマンド バッファーをフラッシュすると、コストのかかる操作になる可能性があります。 <xref:System.Windows.Interop.D3DImage> インスタンスの数が増えるにつれて、より多くのフラッシュが発生し、パフォーマンスが低下します。 そのため、<xref:System.Windows.Interop.D3DImage> は慎重に使用してください。  
  
## <a name="best-practices-on-windows-vista"></a>Windows Vista のベスト プラクティス  
 Windows ディスプレイ ドライバー モデル (WDDM) を使用するように構成されたディスプレイを使う Windows Vista で最高のパフォーマンスを得るには、`IDirect3DDevice9Ex` デバイスに Direct3D9 サーフェイスを作成します。 これにより、サーフェイスの共有が可能になります。 ビデオ カードは、Windows Vista の `D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` および `D3DCAPS2_CANSHARERESOURCE` ドライバー機能をサポートしている必要があります。 その他の設定では、ソフトウェアを介してサーフェイスがコピーされるため、パフォーマンスが大幅に低下します。  
  
> [!NOTE]
> Windows XP Display Driver Model (XDDM) を使用するように Windows Vista のディスプレイが構成されている場合、設定に関係なく、サーフェイスは常にソフトウェアを介してコピーされます。 適切な設定とビデオ カードを使用して WDDM を使用すると、Windows Vista でのパフォーマンスが向上します。これは、サーフェイスのコピーがハードウェアで実行されるためです。  
  
## <a name="best-practices-on-windows-xp"></a>Windows XP のベスト プラクティス  
 Windows XP Display Driver Model (XDDM) を使用する Windows XP で最適なパフォーマンスを得るには、`IDirect3DSurface9::GetDC` メソッドが呼び出されたときに正しく動作するロック可能なサーフェイスを作成します。 内部的には、`BitBlt` メソッドによってハードウェア内のデバイス間でサーフェイスが転送されます。 `GetDC` メソッドは常に XRGB サーフェイス上で機能します。 ただし、クライアント コンピューターで Windows XP SP3 または SP2 が実行されていて、クライアントにもレイヤードウィンドウ機能の修正プログラムがインストールされている場合、このメソッドは ARGB サーフェイス上でのみ機能します。 ビデオ カードは、`D3DDEVCAPS2_CAN_STRETCHRECT_FROM_TEXTURES` ドライバー機能をサポートしている必要があります。  
  
 デスクトップの表示深度が 16 ビットの場合、パフォーマンスが大幅に低下する可能性があります。 32 ビットのデスクトップをお勧めします。  
  
 Windows Vista および Windows XP 用に開発している場合は、Windows XP 上でパフォーマンスをテストします。 Windows XP 上ではビデオ メモリが不足することが問題です。 さらに、Windows XP 上の <xref:System.Windows.Interop.D3DImage> には、追加のビデオ メモリ コピーが必要なため、Windows Vista WDDM よりも多くのビデオ メモリと帯域幅が使用されます。 そのため、同じビデオ ハードウェアの場合、Windows XP のパフォーマンスは Windows Vista のパフォーマンスよりも低くなることが予想されます。  
  
> [!NOTE]
> XDDM は、Windows XP と Windows Vista の両方で使用できます。ただし、WDDM は Windows Vista でのみ使用できます。  
  
## <a name="general-best-practices"></a>一般的なベスト プラクティス  
 デバイスを作成するときは、`D3DCREATE_MULTITHREADED` 作成フラグを使用します。 これにより、パフォーマンスは低下しますが、WPF レンダリング システムでは、このデバイス上のメソッドを別のスレッドから呼び出します。 2 つのスレッドが同時にデバイスにアクセスしないように、ロック プロトコルに正しく従ってください。  
  
 レンダリングが WPF マネージ スレッドで実行される場合は、`D3DCREATE_FPU_PRESERVE` 作成フラグを使用してデバイスを作成することを強くお勧めします。 この設定がない場合、D3D レンダリングによって WPF 倍精度演算の精度が低下し、レンダリングの問題が発生する可能性があります。  
  
 ハードウェア サポートなしで非 pow2 サーフェイスをタイル表示する場合、または <xref:System.Windows.Interop.D3DImage> を含む <xref:System.Windows.Media.DrawingBrush> または <xref:System.Windows.Media.VisualBrush> をタイル表示する場合を除き、<xref:System.Windows.Interop.D3DImage> のタイル表示は高速です。  
  
## <a name="best-practices-for-multi-monitor-displays"></a>マルチモニター ディスプレイのベスト プラクティス  
 複数のモニターを備えたコンピューターを使用している場合は、前述のベスト プラクティスに従う必要があります。 マルチ モニター構成の場合、パフォーマンスに関するその他の考慮事項もあります。  
  
 バック バッファーを作成すると、特定のデバイスとアダプターに作成されますが、WPF によって任意のアダプターにフロント バッファーが表示される場合があります。 アダプター間でコピーしてフロント バッファーを更新すると、非常にコストが高くなる可能性があります。 複数のビデオ カードと `IDirect3DDevice9Ex` デバイスで WDDM を使用するように構成されている Windows Vista で、フロント バッファーが別のアダプター上にあり、ビデオ カードは同じである場合、パフォーマンスは低下しません。 ただし、複数のビデオ カードを使用する Windows XP と XDDM で、フロント バッファーがバック バッファーとは異なるアダプターに表示される場合は、パフォーマンスが大幅に低下します。 詳細については、「[WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)」を参照してください。  
  
## <a name="performance-summary"></a>パフォーマンスの概要  
 次の表は、オペレーティング システムの機能、ピクセル形式、およびサーフェイスのロックの可否としてのフロント バッファー更新プログラムのパフォーマンスを示しています。 フロント バッファーとバック バッファーは同じアダプター上にあると見なされます。 アダプターの構成にもよりますが、通常、ハードウェア更新プログラムはソフトウェア更新プログラムよりもはるかに高速です。  
  
|サーフェイスのピクセル形式|Windows Vista、WDDM、および 9Ex|その他の Windows Vista の構成|Windows XP SP3 または SP2 および修正プログラム|Windows XP SP2|  
|--------------------------|---------------------------------|----------------------------------------|--------------------------------------|--------------------|  
|D3DFMT_X8R8G8B8 (ロック不可能)|**ハードウェア更新プログラム**|ソフトウェア更新プログラム|ソフトウェア更新プログラム|ソフトウェア更新プログラム|  
|D3DFMT_X8R8G8B8 (ロック可能)|**ハードウェア更新プログラム**|ソフトウェア更新プログラム|**ハードウェア更新プログラム**|**ハードウェア更新プログラム**|  
|D3DFMT_A8R8G8B8 (ロック不可能)|**ハードウェア更新プログラム**|ソフトウェア更新プログラム|ソフトウェア更新プログラム|ソフトウェア更新プログラム|  
|D3DFMT_A8R8G8B8 (ロック可能)|**ハードウェア更新プログラム**|ソフトウェア更新プログラム|**ハードウェア更新プログラム**|ソフトウェア更新プログラム|  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.D3DImage>
- [WPF と Direct3D9 の相互運用性](wpf-and-direct3d9-interoperation.md)
- [チュートリアル: WPF でホストするための Direct3D9 コンテンツの作成](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [チュートリアル: WPF での Direct3D9 コンテンツのホスト](walkthrough-hosting-direct3d9-content-in-wpf.md)
