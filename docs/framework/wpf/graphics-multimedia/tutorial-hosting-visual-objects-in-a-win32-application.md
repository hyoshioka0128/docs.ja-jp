---
title: 'チュートリアル: Win32 アプリケーションでのビジュアル オブジェクトのホスト'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- visual objects in Win32 code [WPF]
- Win32 code [WPF], visual objects in
- hosting [WPF], visual objects in Win32 code
ms.assetid: f0e1600c-3217-43d5-875d-1864fa7fe628
ms.openlocfilehash: d04357e0770bbf8eebe8f40a86a19ddc9baae3ab
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79187424"
---
# <a name="tutorial-hosting-visual-objects-in-a-win32-application"></a>チュートリアル: Win32 アプリケーションでのビジュアル オブジェクトのホスト
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] は、アプリケーションの作成に適した環境を提供します。 ただし、Win32 コードにかなりの投資がある場合は、コードを書き換えるより、アプリケーションに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の機能を追加するほうがより効果的であることがあります。 アプリケーションで同時に使用される Win32 と [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のグラフィックス サブシステムをサポートするために、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、Win32 ウィンドウ内でオブジェクトをホストするための機構が提供されています。  
  
 このチュートリアルでは、Win32 ウィンドウで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のビジュアル オブジェクトをホストするサンプル アプリケーション ([Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)) の記述方法について説明します。  

<a name="requirements"></a>
## <a name="requirements"></a>必要条件  
 このチュートリアルは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] と Win32 プログラミングの基礎知識があることを前提としています。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のプログラミングの基本的な概要については、「[チュートリアル: 初めての WPF デスクトップ アプリケーション](../getting-started/walkthrough-my-first-wpf-desktop-application.md)」を参照してください。 Win32 のプログラミングの概要については、この主題に関する数多くの書籍、特に「*Programming Windows*」(Charles Petzold 著) を参照してください。  
  
> [!NOTE]
> このチュートリアルには、関連するサンプルからのコード例が多数含まれています。 しかし、読みやすくするため、完全なサンプル コードは含まれていません。 完全なサンプル コードについては、「[Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)」を参照してください。  
  
<a name="creating_the_host_win32_window"></a>
## <a name="creating-the-host-win32-window"></a>ホストの Win32 ウィンドウを作成する  
 Win32 のウィンドウで [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のオブジェクトをホストするときに鍵となるのは、<xref:System.Windows.Interop.HwndSource> クラスです。 このクラスは、Win32 ウィンドウ内の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] オブジェクトをラップして、それらを子ウィンドウとして [!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] に組み込めるようにします。  
  
 次の例は、<xref:System.Windows.Interop.HwndSource> オブジェクトを、ビジュアル オブジェクトの Win32 コンテナー ウィンドウとして作成するためのコードを示しています。 Win32 ウィンドウのウィンドウ スタイル、位置、およびその他のパラメーターを設定するには、<xref:System.Windows.Interop.HwndSourceParameters> オブジェクトを使用します。  
  
 [!code-csharp[VisualsHitTesting#101](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#101)]
 [!code-vb[VisualsHitTesting#101](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#101)]  
  
> [!NOTE]
> <xref:System.Windows.Interop.HwndSourceParameters.ExtendedWindowStyle%2A> プロパティの値を WS_EX_TRANSPARENT に設定することはできません。 つまり、ホストの Win32 ウィンドウを透明にすることはできません。 このため、ホストの Win32 ウィンドウの背景色は、その親ウィンドウと同じ背景色に設定されます。  
  
<a name="adding_visual_objects_to_the_host_win32_window"></a>
## <a name="adding-visual-objects-to-the-host-win32-window"></a>ホストの Win32 ウィンドウにビジュアル オブジェクトを追加する  
 ビジュアル オブジェクトのホストの Win32 コンテナー ウィンドウを作成したら、それにビジュアル オブジェクトを追加できます。 ビジュアル オブジェクトの変換 (アニメーションなど) が、ホストの Win32 ウィンドウの四角形領域の境界を超えて拡張されていないことを確認してください。  
  
 次の例は、<xref:System.Windows.Interop.HwndSource> オブジェクトを作成し、それにビジュアル オブジェクトを追加するためのコードを示したものです。  
  
> [!NOTE]
> <xref:System.Windows.Interop.HwndSource> オブジェクトの <xref:System.Windows.Interop.HwndSource.RootVisual%2A> プロパティは、ホストの Win32 ウィンドウに追加された最初のビジュアル オブジェクトに設定されます。 ルート ビジュアル オブジェクトは、ビジュアル オブジェクト ツリーの最上位ノードを定義します。 ホストの Win32 ウィンドウに追加された後続のビジュアル オブジェクトは、子オブジェクトとして追加されます。  
  
 [!code-csharp[VisualsHitTesting#100](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#100)]
 [!code-vb[VisualsHitTesting#100](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#100)]  
  
<a name="implementing_the_win32_message_filter"></a>
## <a name="implementing-the-win32-message-filter"></a>Win32 メッセージ フィルターを実装する  
 ビジュアル オブジェクトのホストの Win32 ウィンドウには、アプリケーション キューからウィンドウに送信されたメッセージを処理するための、ウィンドウ メッセージ フィルター プロシージャが必要です。 ウィンドウ プロシージャは、Win32 システムからメッセージを受信します。 これらは入力メッセージか、またはウィンドウ管理メッセージです。 必要に応じて、メッセージをウィンドウ プロシージャで処理したり、既定の処理用のシステムにメッセージを渡すことができます。  
  
 ビジュアル オブジェクトの親として定義された <xref:System.Windows.Interop.HwndSource> オブジェクトは、開発者が提供したウィンドウ メッセージ フィルター プロシージャを参照する必要があります。 <xref:System.Windows.Interop.HwndSource> オブジェクトを作成する際には、ウィンドウ プロシージャを参照するように <xref:System.Windows.Interop.HwndSourceParameters.HwndSourceHook%2A> プロパティを設定します。  
  
 [!code-csharp[VisualsHitTesting#102](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#102)]
 [!code-vb[VisualsHitTesting#102](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#102)]  
  
 次の例に示すは、左右のマウス ボタンのアップ メッセージを処理するためのコードです。 マウス ヒット位置の座標値は、`lParam` パラメーターの値に含まれます。  
  
 [!code-csharp[VisualsHitTesting#103](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
<a name="processing_the_win32_messages"></a>
## <a name="processing-the-win32-messages"></a>Win32 メッセージを処理する  
 次のコード例は、ホストの Win32 ウィンドウに含まれているビジュアル オブジェクトの階層に対して、ヒット テストがどのように実行されるかを示したものです。 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> メソッドを使用して、ヒット テストを実行するルート ビジュアル オブジェクトと座標値を指定することにより、ビジュアル オブジェクトのジオメトリ内にポイントがあるかどうかを識別できます。 この場合、ルート ビジュアル オブジェクトは <xref:System.Windows.Interop.HwndSource> オブジェクトの <xref:System.Windows.Interop.HwndSource.RootVisual%2A> プロパティの値です。  
  
 [!code-csharp[VisualsHitTesting#104](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 ビジュアル オブジェクトに対するヒット テストについて詳しくは、「[ビジュアル層でのヒット テスト](hit-testing-in-the-visual-layer.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.HwndSource>
- [Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)
- [ビジュアル層でのヒット テスト](hit-testing-in-the-visual-layer.md)
