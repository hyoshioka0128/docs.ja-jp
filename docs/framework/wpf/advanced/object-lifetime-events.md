---
title: オブジェクトの有効期間イベント
ms.date: 03/30/2017
helpviewer_keywords:
- events [WPF], ContentRendered
- events [WPF], Deactivated
- events [WPF], Unloaded
- Activated events [WPF]
- events [WPF], Loaded
- Application objects [WPF], lifetime events
- events [WPF], Activated
- ContentRendered events [WPF]
- Deactivated events [WPF]
- events [WPF], Initialized
- events [WPF], Closing
- Unloaded events [WPF]
- exit events [WPF]
- objects' lifetime events [WPF]
- Loaded events [WPF]
- Closing events [WPF]
- events [WPF], Closed
- Initialized events [WPF]
- Closed events [WPF]
- startup events [WPF]
- lifetime events of objects [WPF]
ms.assetid: face6fc7-465b-4502-bfe5-e88d2e729a78
ms.openlocfilehash: 3b761674bd2464ee87e07d9299c805431f8fdeb7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141108"
---
# <a name="object-lifetime-events"></a>オブジェクトの有効期間イベント
このトピックでは、オブジェクトの有効期間における作成、使用、破棄のステージを示す特定の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] イベントについて説明します。  

<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] クラスの既存の依存関係プロパティのコンシューマーの観点から依存関係プロパティを理解しており、「[依存関係プロパティの概要](dependency-properties-overview.md)」というトピックを読んでいることを前提としています。 このトピックの例を理解するには、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] について理解し (「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」を参照)、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションの記述方法を理解していることも必要です。  
  
<a name="intro"></a>
## <a name="object-lifetime-events"></a>オブジェクトの有効期間イベント  
 Microsoft .NET Framework マネージド コードのオブジェクトはすべて、作成、使用、破棄という一連の有効期間のステージを経由します。 また、多くのオブジェクトには、破棄フェーズの一環として発生する有効期間の終了ステージもあります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] オブジェクト (具体的には [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] が要素として識別するビジュアル オブジェクト) にも、共通する一連のオブジェクト有効期間ステージがあります。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プログラミングおよびアプリケーション モデルでは、これらのステージが一連のイベントとして公開されます。 有効期間イベントに関しては、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] に、全般的要素、ウィンドウ要素、ナビゲーション ホスト、アプリケーション オブジェクトの 4 種類の主要オブジェクトがあります。 ウィンドウ要素とナビゲーション ホストは、さらに大きなビジュアル オブジェクト (要素) のグループにも含まれます。 このトピックでは、すべての要素に共通する有効期間イベントについて説明し、次にアプリケーション定義、ウィンドウ要素、またはナビゲーション ホストに適用される特定の有効期間イベントについて説明します。  
  
<a name="common_events"></a>
## <a name="common-lifetime-events-for-elements"></a>要素に関する共通の有効期間イベント  
 任意の WPF フレームワーク レベル要素 (<xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> から派生しているオブジェクト) には、<xref:System.Windows.FrameworkElement.Initialized>、<xref:System.Windows.FrameworkElement.Loaded>、<xref:System.Windows.FrameworkElement.Unloaded> という 3 つの共通する有効期間イベントがあります。  
  
### <a name="initialized"></a>初期化済み  
 <xref:System.Windows.FrameworkElement.Initialized> が最初に発生します。これは、コンストラクターの呼び出しによるオブジェクトの初期化にほぼ対応します。 このイベントは初期化に応答して発生するため、オブジェクトのすべてのプロパティが設定されることが保証されます。 (例外は、動的リソースまたはバインディングなどの式の使用です。これらは評価されない式となります。)すべてのプロパティが設定されるという要件の結果、マークアップで定義される入れ子の要素によって発生する一連の <xref:System.Windows.FrameworkElement.Initialized> は、要素ツリーの最下位の要素から始まって、ルート方向の親要素に向かう順序で発生するように見えます。 この順序に従うのは、親子のリレーションシップおよびコンテインメントがプロパティであるためです。その結果、親のプロパティを設定する子要素も完全に初期化されるまで、親は初期化を報告できません。  
  
 <xref:System.Windows.FrameworkElement.Initialized> イベントへの応答としてハンドラーを記述する際は、ハンドラーが接続される要素ツリー (論理ツリーまたはビジュアル ツリーのいずれか) の他のすべての要素、特に親要素が作成された保証がないことを考慮する必要があります。 メンバー変数が null である可能性や、基になるバインディングによってデータ ソースがまだ設定されていない可能性があります (式レベルでも)。  
  
### <a name="loaded"></a>読み込み  
 次に、<xref:System.Windows.FrameworkElement.Loaded> が発生します。 <xref:System.Windows.FrameworkElement.Loaded> イベントが発生するのは、最終的な描画の前、ただし描画に必要なすべての値がレイアウト システムによって計算された後です。 <xref:System.Windows.FrameworkElement.Loaded> は、要素を含む論理ツリーが完全である場合にのみ発生し、HWND とレンダリング サーフェイスを提供するプレゼンテーション ソースに接続されます。 標準データ バインディング (他のプロパティや直接定義したデータ ソースなどのローカル ソースへのバインディング) は、<xref:System.Windows.FrameworkElement.Loaded> の前に発生します。 非同期データ バインディング (外部ソースまたは動的ソース) が発生する可能性もありますが、非同期であるという性質の定義から、その保証はできません。  
  
 <xref:System.Windows.FrameworkElement.Loaded> イベントを発生させるメカニズムは、<xref:System.Windows.FrameworkElement.Initialized> とは異なります。 <xref:System.Windows.FrameworkElement.Initialized> イベントは、要素単位で発生し、完全な要素ツリーによる直接の調整はありません。 これに対し、<xref:System.Windows.FrameworkElement.Loaded> イベントは、要素ツリー (特に、論理ツリー) 全体にわたる調整動作として発生します。 ツリーのすべての要素が読み込まれたと見なされる状態になると、<xref:System.Windows.FrameworkElement.Loaded> イベントは、最初にルート要素で発生します。 次に、<xref:System.Windows.FrameworkElement.Loaded> イベントは、各子要素で連続して発生します。  
  
> [!NOTE]
> この動作は、表面上は、ルーティング イベントのトンネリングに似ているとも言えます。 ただし、イベントからイベントへと伝達される情報はありません。 各要素は常に <xref:System.Windows.FrameworkElement.Loaded> イベントを処理することができ、イベント データを処理済みとしてマークしても、その要素以外への影響はありません。  
  
### <a name="unloaded"></a>アンロードされました  
 最後に <xref:System.Windows.FrameworkElement.Unloaded> が発生します。これは、プレゼンテーション ソースまたは削除中のビジュアル親によって開始されます。 <xref:System.Windows.FrameworkElement.Unloaded> が発生して処理されるときには、(<xref:System.Windows.FrameworkElement.Parent%2A> プロパティによって決定される) イベント ソースの親である要素、または論理ツリーまたはビジュアル ツリーの上方向にある任意の要素が既に設定解除されている可能性があります。これは、データ バインディング、リソース参照、スタイルが、通常の、または判明している最後の実行時の値に設定されていない可能性があることを意味します。  
  
<a name="application_model_elements"></a>
## <a name="lifetime-events-application-model-elements"></a>有効期間イベント アプリケーション モデルの要素  
 要素の共通の有効期間イベントに基づいて構築されたアプリケーション モデル要素には、<xref:System.Windows.Application>、<xref:System.Windows.Window>、<xref:System.Windows.Controls.Page>、<xref:System.Windows.Navigation.NavigationWindow>、<xref:System.Windows.Controls.Frame> があります。 これらの要素は、共通の有効期間イベントを拡張して、特定の目的に関連するイベントを追加します。 これらの詳細については、次のトピックで説明しています。  
  
- <xref:System.Windows.Application>:[アプリケーション管理の概要](../app-development/application-management-overview.md)。  
  
- <xref:System.Windows.Window>:[WPF ウィンドウの概要](../app-development/wpf-windows-overview.md)。  
  
- <xref:System.Windows.Controls.Page>、<xref:System.Windows.Navigation.NavigationWindow>、および <xref:System.Windows.Controls.Frame>:[ナビゲーションの概要](../app-development/navigation-overview.md)。  
  
## <a name="see-also"></a>関連項目

- [依存関係プロパティ値の優先順位](dependency-property-value-precedence.md)
- [ルーティング イベントの概要](routed-events-overview.md)
