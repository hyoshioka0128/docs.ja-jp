---
title: WPF と Direct3D9 の相互運用性
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- cpp
helpviewer_keywords:
- WPF [WPF], creating Direct3D9 content
- Direct3D9 [WPF interoperability], creating Direct3D9 content
ms.assetid: 1b14b823-69c4-4e8d-99e4-f6dade58f89a
ms.openlocfilehash: 9ec83c48052e1ef29bb91a6b40b7c76f671bb99f
ms.sourcegitcommit: de17a7a0a37042f0d4406f5ae5393531caeb25ba
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/24/2020
ms.locfileid: "76735185"
---
# <a name="wpf-and-direct3d9-interoperation"></a>WPF と Direct3D9 の相互運用性
Windows Presentation Foundation (WPF) アプリケーションには Direct3D9 コンテンツを含めることができます。 このトピックでは、Direct3D9 コンテンツを作成して WPF と効率的に相互運用する方法について説明します。  
  
> [!NOTE]
> WPF で Direct3D9 コンテンツを使用する場合は、パフォーマンスについても考慮する必要があります。 パフォーマンスを最適化する方法の詳細については、「[Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)」を参照してください。  
  
## <a name="display-buffers"></a>バッファーを表示する  
 <xref:System.Windows.Interop.D3DImage> クラスを使用して、"*バック バッファー*" と "*フロント バッファー*" という 2 つのディスプレイ バッファーを管理します。 バック バッファーは Direct3D9 のサーフェイスです。 <xref:System.Windows.Interop.D3DImage.Unlock%2A> メソッドを呼び出すと、バック バッファーに対する変更がフロント バッファーに転送されます。  
  
 次の図は、バック バッファーとフロント バッファーの関係を示しています。  
  
 ![D3DImage のディスプレイ バッファー](./media/d3dimage-buffers.png "D3DImage_buffers")  
  
## <a name="direct3d9-device-creation"></a>Direct3D9 デバイスの作成  
 Direct3D9 コンテンツをレンダリングするには、Direct3D9 デバイスを作成する必要があります。 デバイスの作成に使用できる Direct3D9 オブジェクトには、`IDirect3D9` と `IDirect3D9Ex` の 2 つがあります。 これらのオブジェクトを使用して、それぞれ `IDirect3DDevice9` デバイスと `IDirect3DDevice9Ex` デバイスを作成します。  
  
 次のいずれかのメソッドを呼び出してデバイスを作成します。  
  
- `IDirect3D9 * Direct3DCreate9(UINT SDKVersion);`  
  
- `HRESULT Direct3DCreate9Ex(UINT SDKVersion, IDirect3D9Ex **ppD3D);`  
  
 Windows Vista 以降のオペレーティング システムでは、Windows ディスプレイ ドライバー モデル (WDDM) を使用するように構成されたディスプレイで `Direct3DCreate9Ex` メソッドを使用します。 他のプラットフォームでは `Direct3DCreate9` メソッドを使用します。  
  
### <a name="availability-of-the-direct3dcreate9ex-method"></a>Direct3DCreate9Ex メソッドの可用性  
 Windows Vista 以降のオペレーティング システムにのみ、d3d9.dll に `Direct3DCreate9Ex` メソッドがあります。 Windows XP でこの関数を直接リンクすると、アプリケーションの読み込みに失敗します。 `Direct3DCreate9Ex` メソッドがサポートされているかどうかを確認するには、DLL を読み込んで proc アドレスを探します。 次のコードは、`Direct3DCreate9Ex` メソッドをテストする方法を示しています。 完全なコード例については、「[チュートリアル: WPF でホストするための Direct3D9 コンテンツの作成](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)」を参照してください。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureD3DObjects](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensured3dobjects)]  
  
### <a name="hwnd-creation"></a>HWND の作成  
 デバイスを作成するには HWND が必要です。 通常、Direct3D9 に使用するダミーの HWND を作成します。 次のコード例は、ダミーの HWND を作成する方法を示しています。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_EnsureHWND](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_ensurehwnd)]  
  
### <a name="present-parameters"></a>Present パラメーター  
 デバイスの作成にも `D3DPRESENT_PARAMETERS` 構造体が必要ですが、重要なのは一部のパラメーターのみです。 これらのパラメーターは、メモリ フットプリントを最小限に抑えるために選択されます。  
  
 `BackBufferHeight` フィールドと `BackBufferWidth` フィールドを 1 に設定します。 これらを 0 に設定すると、HWND のディメンションに設定されます。  
  
 Direct3D9 に使用されるメモリの破損を防ぎ、Direct3D9 によって FPU 設定が変更されないようにするために、常に `D3DCREATE_MULTITHREADED` フラグと `D3DCREATE_FPU_PRESERVE` フラグを設定してください。  
  
 次のコードは、`D3DPRESENT_PARAMETERS` 構造体を初期化する方法を示しています。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_Init](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_init)]  
  
## <a name="creating-the-back-buffer-render-target"></a>バック バッファー レンダー ターゲットの作成  
 Direct3D9 コンテンツを <xref:System.Windows.Interop.D3DImage> で表示するには、Direct3D9 サーフェイスを作成し、<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> メソッドを呼び出してそれを割り当てます。  
  
### <a name="verifying-adapter-support"></a>アダプター サポートの確認  
 サーフェイスを作成する前に、必要なサーフェイスのプロパティがすべてのアダプターでサポートされていることを確認します。 1 つのアダプターのみにレンダリングする場合でも、システム内の任意のアダプターに WPF ウィンドウが表示されることがあります。 WPF によってサーフェイスが使用可能なアダプター間で移動される可能性があるため、常にマルチアダプター構成を処理する Direct3D9 コードを書き、すべてのアダプターのサポートを確認する必要があります。  
  
 次のコード例は、Direct3D9 のサポートについてシステム上のすべてのアダプターを確認する方法を示しています。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_TestSurfaceSettings](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_testsurfacesettings)]  
  
### <a name="creating-the-surface"></a>サーフェイスの作成  
 サーフェイスを作成する前に、デバイスの機能がターゲット オペレーティング システム上で良好なパフォーマンスをサポートしていることを確認します。 詳細については、「[Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)」を参照してください。  
  
 デバイスの機能を確認したら、サーフェイスを作成できます。 次のコード例は、レンダー ターゲットを作成する方法を示しています。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#Renderer_CreateSurface](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderer.cpp#renderer_createsurface)]  
  
### <a name="wddm"></a>WDDM  
 WDDM を使用するように構成されている Windows Vista 以降のオペレーティング システムでは、レンダー ターゲット テクスチャを作成し、レベル 0 の サーフェイスを <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> メソッドに渡すことができます。 Windows XP では、ロック可能なレンダー ターゲット テクスチャを作成できず、パフォーマンスが低下するため、このアプローチは推奨されません。  
  
## <a name="handling-device-state"></a>デバイスの状態の処理  
 <xref:System.Windows.Interop.D3DImage> クラスを使用して、"*バック バッファー*" と "*フロント バッファー*" という 2 つのディスプレイ バッファーを管理します。 バック バッファーは、Direct3D サーフェイスです。  <xref:System.Windows.Interop.D3DImage.Unlock%2A> メソッドを呼び出すと、バック バッファーに対する変更はフロント バッファーに転送され、そのハードウェア上に表示されます。 場合によっては、フロント バッファーが使用できなくなります。 この使用できなくなる状況は、画面ロック、全画面専用の Direct3D アプリケーション、ユーザー切り替え、またはその他のシステム アクティビティが原因で発生する可能性があります。 これが発生した場合、<xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> イベントを処理することで WPF アプリケーションに通知されます。  フロント バッファーが使用できなくなった場合のアプリケーションの応答は、ソフトウェア レンダリングへのフォールバックが WPF で有効かどうかによって変わります。 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> メソッドには、WPF がソフトウェア レンダリングにフォールバックするかどうかを指定するパラメーターを受け取るオーバーロードがあります。  
  
 <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%29> オーバーロードを呼び出すか、`enableSoftwareFallback` パラメーターを `false` に設定して <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> オーバーロードを呼び出すと、フロント バッファーが使用できなくなり、何も表示されなくなったときに、レンダリング システムではバック バッファーへの参照が解放されます。 フロント バッファーを再び使用できるようになると、レンダリング システムによって <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> イベントが発生し、WPF アプリケーションに通知されます。  <xref:System.Windows.Interop.D3DImage.IsFrontBufferAvailableChanged> イベントのイベント ハンドラーを作成し、有効な Direct3D サーフェイスを使用してもう一度レンダリングを再開できます。 レンダリングを再開するには、<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> を呼び出す必要があります。  
  
 `enableSoftwareFallback` パラメーターを `true` に設定して <xref:System.Windows.Interop.D3DImage.SetBackBuffer%28System.Windows.Interop.D3DResourceType%2CSystem.IntPtr%2CSystem.Boolean%29> オーバーロードを呼び出すと、フロント バッファーが使用できなくなったときにレンダリング システムにバック バッファーへの参照が保持されます。そのため、バッファーを再び使用できるようになったときに <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> を呼び出す必要はありません。  
  
 ソフトウェア レンダリングを有効にすると、ユーザーのデバイスが使用できなくなる場合がありますが、レンダリング システムには Direct3D サーフェイスへの参照が保持されます。 Direct3D9 デバイスが使用できないかどうかを確認するには、`TestCooperativeLevel` メソッドを呼び出します。 Direct3D9Ex デバイスを確認するには、`CheckDeviceState` メソッドを呼び出します。これは、`TestCooperativeLevel` メソッドが非推奨になり、常に成功が返されるためです。 ユーザー デバイスが使用できなくなった場合は、<xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> を呼び出して、バック バッファーへの WPF の参照を解放します。  デバイスをリセットする必要がある場合は、`backBuffer` パラメーターを `null` に設定して <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> を呼び出し、次に `backBuffer` を有効な Direct3D サーフェイスに設定して <xref:System.Windows.Interop.D3DImage.SetBackBuffer%2A> をもう一度呼び出します。  
  
 マルチアダプターのサポートを実装する場合にのみ、`Reset` メソッドを呼び出して無効なデバイスから復旧します。 それ以外の場合は、すべての Direct3D9 インターフェイスを解放して、完全に再作成します。 アダプターのレイアウトが変更された場合、変更前に作成された Direct3D9 オブジェクトは更新されません。  
  
## <a name="handling-resizing"></a>サイズ変更の処理  
 <xref:System.Windows.Interop.D3DImage> がネイティブ サイズ以外の解像度で表示されている場合、<xref:System.Windows.Media.Effects.SamplingMode.Bilinear> が <xref:System.Windows.Media.BitmapScalingMode.Fant> の代わりに使用されている場合を除き、現在の <xref:System.Windows.Media.RenderOptions.BitmapScalingMode%2A> に従って拡大縮小されます。  
  
 より高い忠実性が必要な場合は、<xref:System.Windows.Interop.D3DImage> のコンテナーのサイズが変わったときに新しいサーフェイスを作成する必要があります。  
  
 サイズ変更を処理するには、3 つの方法があります。  
  
- レイアウト システムに参加し、サイズが変更されたときに新しいサーフェイスを作成します。 ビデオ メモリが使い果たされたり、フラグメント化されたりする可能性があるため、あまり多くのサーフェイスを作成しないでください。  
  
- サイズ変更イベントが一定期間発生しなくなるまで待ってから、新しいサーフェイスを作成します。  
  
- コンテナーのサイズを毎秒数回チェックする <xref:System.Windows.Threading.DispatcherTimer> を作成します。  
  
## <a name="multi-monitor-optimization"></a>マルチモニターの最適化  
 レンダリング システムによって <xref:System.Windows.Interop.D3DImage> が別のモニターに移動されると、パフォーマンスが大幅に低下する可能性があります。  
  
 WDDM では、モニターが同じビデオ カード上にあり、`Direct3DCreate9Ex` を使用している限り、パフォーマンスが低下することはありません。 モニターが別のビデオ カード上にある場合は、パフォーマンスが低下します。 Windows XP では、パフォーマンスは常に低下します。  
  
 <xref:System.Windows.Interop.D3DImage> が別のモニターに移動された場合は、対応するアダプターに新しいサーフェイスを作成して、良好なパフォーマンスを復元することができます。  
  
 パフォーマンスの低下を回避するには、マルチモニター ケース専用のコードを書きます。 次の一覧は、マルチモニター コードを書く 1 つの方法を示しています。  
  
1. `Visual.ProjectToScreen` メソッドを使用して、画面空間内の <xref:System.Windows.Interop.D3DImage> のポイントを見つけます。  
  
2. `MonitorFromPoint` GDI メソッドを使用して、ポイントが表示されているモニターを見つけます。  
  
3. `IDirect3D9::GetAdapterMonitor` メソッドを使用して、モニターがオンになっている Direct3D9 アダプターを見つけます。  
  
4. アダプターがバック バッファーを使用するアダプターと同じでない場合は、新しいモニター上に新しいバック バッファーを作成し、それを <xref:System.Windows.Interop.D3DImage> バック バッファーに割り当てます。  
  
> [!NOTE]
> <xref:System.Windows.Interop.D3DImage> が複数のモニターに使用される場合、WDDM と `IDirect3D9Ex` が同じアダプター上にある場合を除き、パフォーマンスは低下します。 この状況でパフォーマンスを向上させる方法はありません。  
  
 次のコード例は、現在のモニターを見つける方法を示しています。  
  
 [!code-cpp[System.Windows.Interop.D3DImage#RendererManager_SetAdapter](~/samples/snippets/cpp/VS_Snippets_Wpf/System.Windows.Interop.D3DImage/cpp/renderermanager.cpp#renderermanager_setadapter)]  
  
 <xref:System.Windows.Interop.D3DImage> コンテナーのサイズまたは位置が変わったときにモニターを更新するか、1 秒あたり数回更新される `DispatcherTimer` を使用してモニターを更新します。  
  
## <a name="wpf-software-rendering"></a>WPF のソフトウェア レンダリング  
 次の状況では、ソフトウェアの UI スレッドに対して WPF が同期的にレンダリングされます。  
  
- 印刷  
  
- <xref:System.Windows.Media.Effects.BitmapEffect>  
  
- <xref:System.Windows.Media.Imaging.RenderTargetBitmap>  
  
 このような状況のいずれかが発生すると、レンダリング システムから <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> メソッドが呼び出され、ハードウェア バッファーがソフトウェアにコピーされます。 既定の実装では、サーフェイスを使用して `GetRenderTargetData` メソッドが呼び出されます。 この呼び出しは、ロックおよびロック解除パターンの外部で発生するため、失敗する可能性があります。 この場合、`CopyBackBuffer` メソッドから `null` が返され、画像は表示されません。  
  
 <xref:System.Windows.Interop.D3DImage.CopyBackBuffer%2A> メソッドをオーバーライドして基本実装を呼び出し、`null` が返される場合は、プレースホルダー <xref:System.Windows.Media.Imaging.BitmapSource> を返すことができます。  
  
 基本実装を呼び出すのではなく、独自のソフトウェア レンダリングを実装することもできます。  
  
> [!NOTE]
> WPF が完全にソフトウェアでレンダリングされている場合、WPF にはフロント バッファーがないため、<xref:System.Windows.Interop.D3DImage> は表示されません。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.D3DImage>
- [Direct3D9 および WPF の相互運用性のパフォーマンスに関する考慮事項](performance-considerations-for-direct3d9-and-wpf-interoperability.md)
- [チュートリアル: WPF でホストするための Direct3D9 コンテンツの作成](walkthrough-creating-direct3d9-content-for-hosting-in-wpf.md)
- [チュートリアル: WPF での Direct3D9 コンテンツのホスト](walkthrough-hosting-direct3d9-content-in-wpf.md)
