---
title: '方法: Win32 ホスト コンテナーを使用してヒット テストを実行する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hit tests [WPF], using Win32 host containers
- visual objects [WPF], hit tests on
- Win32 host containers [WPF], hit tests using
ms.assetid: 9491f7f3-d8ba-4573-a888-2f064d1349dc
ms.openlocfilehash: a86c1c36f75fa232d52731959371268a8b2593d7
ms.sourcegitcommit: 700ea803fb06c5ce98de017c7f76463ba33ff4a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77452806"
---
# <a name="how-to-hit-test-using-a-win32-host-container"></a>方法: Win32 ホスト コンテナーを使用してヒット テストを実行する
ビジュアル オブジェクトのホスト ウィンドウ コンテナーを提供することで、Win32 ウィンドウにビジュアル オブジェクトを作成できます。 格納されているビジュアル オブジェクト用のイベント処理機能を提供するには、ホスト ウィンドウ コンテナーのメッセージ フィルター ループに渡されるメッセージを処理します。 「[チュートリアル: Win32 アプリケーションでのビジュアル オブジェクトのホスト](tutorial-hosting-visual-objects-in-a-win32-application.md)」を参照し、Win32 ウィンドウでビジュアル オブジェクトをホストする方法の詳細を確認してください。  
  
## <a name="example"></a>例  
 次のコードでは、ビジュアル オブジェクトのホスト コンテナーとして使用される Win32 ウィンドウにマウス イベント ハンドラーを設定する方法を示します。  
  
 [!code-csharp[VisualsHitTesting#103](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyWindow.cs#103)]
 [!code-vb[VisualsHitTesting#103](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyWindow.vb#103)]  
  
 トラッピング固有のマウス イベントに対応してヒット テストを設定する方法を次の例に示します。  
  
 [!code-csharp[VisualsHitTesting#104](~/samples/snippets/csharp/VS_Snippets_Wpf/VisualsHitTesting/CSharp/MyCircle.cs#104)]
 [!code-vb[VisualsHitTesting#104](~/samples/snippets/visualbasic/VS_Snippets_Wpf/VisualsHitTesting/VisualBasic/MyCircle.vb#104)]  
  
 <xref:System.Windows.Interop.HwndSource> オブジェクトは、Win32 ウィンドウ内の [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] コンテンツを表します。 <xref:System.Windows.Interop.HwndSource> オブジェクトの <xref:System.Windows.Interop.HwndSource.RootVisual%2A> プロパティの値は、ビジュアル ツリー階層内の最上位ノードを表します。  
  
 Win32 ホスト コンテナーを使用するオブジェクトのヒット テストのサンプル全体については、「[Win32 相互運用によるヒット テストのサンプル](https://github.com/microsoft/WPF-Samples/tree/master/Visual%20Layer/VisualsHitTesting)」をご覧ください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Interop.HwndSource>
- [ビジュアル層でのヒット テスト](hit-testing-in-the-visual-layer.md)
- [チュートリアル: Win32 アプリケーションでのビジュアル オブジェクトのホスト](tutorial-hosting-visual-objects-in-a-win32-application.md)
