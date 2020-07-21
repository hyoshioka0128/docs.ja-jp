---
title: 基本要素の概要
ms.date: 03/30/2017
helpviewer_keywords:
- base elements [WPF]
ms.assetid: 2c997092-72c6-4767-bc84-74267f4eee72
ms.openlocfilehash: f6519675ebf3624152e1077e7582f04e38b1dce9
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81644041"
---
# <a name="base-elements-overview"></a>基本要素の概要
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] のクラスの大部分は、SDK のドキュメントで一般に基本要素クラスと呼ばれている 4 つのクラスから派生しています。 このようなクラスとしては、<xref:System.Windows.UIElement>、<xref:System.Windows.FrameworkElement>、<xref:System.Windows.ContentElement>、<xref:System.Windows.FrameworkContentElement> があります。 <xref:System.Windows.DependencyObject> クラスも関連がありますが、これは <xref:System.Windows.UIElement> と <xref:System.Windows.ContentElement> の両方に共通する基底クラスであるためです  

<a name="base_apis"></a>
## <a name="base-element-apis-in-wpf-classes"></a>WPF クラスの基本要素 API  
 <xref:System.Windows.UIElement> および <xref:System.Windows.ContentElement> は、どちらも <xref:System.Windows.DependencyObject> から派生していますが、その方法は多少異なります。 このレベルでの相違点は、<xref:System.Windows.UIElement> や <xref:System.Windows.ContentElement> がユーザー インターフェイスで使用される方法と、それらがアプリケーション内で使用される目的に関するものです。 <xref:System.Windows.UIElement> のクラス階層構造内には <xref:System.Windows.Media.Visual> も存在します。これは、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] の基礎となる低レベルのグラフィックス サポートを公開するクラスです。 <xref:System.Windows.Media.Visual> では、独立した四角形の画面領域を定義することにより、レンダリングのフレームワークが提供されます。 実際には、<xref:System.Windows.UIElement> では比較的大きなオブジェクト モデルがサポートされており、四角形の画面領域として記述できる領域にレンダリングおよびレイアウトされるように設計されている要素のためのものです。そのコンテンツ モデルは、さまざまな要素の組み合わせが可能なように、意図的にオープンに作られています。 <xref:System.Windows.ContentElement> は <xref:System.Windows.Media.Visual> から派生していません。そのモデルでは、<xref:System.Windows.ContentElement> は、リーダーやビューアーなど、他のものによって処理されます。これらのリーダーやビューアーなどでは、要素が解釈され、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] で処理される完全な <xref:System.Windows.Media.Visual> が生成されます。 一部の <xref:System.Windows.UIElement> クラスは、コンテンツ ホストとなるように設計されています。それらのクラスでは、1 つ以上の <xref:System.Windows.ContentElement> クラスに対して、ホスティングとレンダリングが提供されます (そのようなクラスの例として、<xref:System.Windows.Controls.DocumentViewer> があります)。 <xref:System.Windows.ContentElement> は、比較的小さなオブジェクト モデルを持ち、<xref:System.Windows.UIElement> 内にホストされるテキスト、情報、またはドキュメントのコンテンツ向けに使用されることの多い要素の基底クラスとして使用されます。  
  
### <a name="framework-level-and-core-level"></a>フレームワークレベルとコアレベル  
 <xref:System.Windows.UIElement> は <xref:System.Windows.FrameworkElement> の基底クラスとして機能し、<xref:System.Windows.ContentElement> は <xref:System.Windows.FrameworkContentElement> の基底クラスとして機能します。 この次のレベルのクラスが存在する理由は、WPF フレームワーク レベルとは異なる WPF コア レベルをサポートするためです。この区分は、PresentationCore と PresentationFramework アセンブリ間での API の区分にも存在します。 WPF フレームワーク レベルは、表示のためのレイアウト マネージャーの実装など、アプリケーションの基本的ニーズに対して、より完全なソリューションを提供します。 WPF コア レベルは、アセンブリの追加によるオーバーヘッドを引き起こすことなく [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の大部分を使用する方法を提供します。 これらのレベルの区別は、ほとんどの通常のアプリケーション開発シナリオでほとんど問題になりません。一般には、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API を 1 つのものと見なして、WPF フレームワーク レベルと WPF コア レベルの違いについて意識する必要はありません。 アプリケーション設計で WPF フレームワーク レベルの機能の大部分を置き換えることにした場合、たとえば開発中のソリューション全体に、独自の[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)] の構成およびレイアウトが既に実装されている場合には、これらのレベルの区分に関する理解が必要となる可能性があります。  
  
<a name="subclassing_elements"></a>
## <a name="choosing-which-element-to-derive-from"></a>派生元の要素を選択する  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を拡張したカスタム クラスを作成するための最も実際的な方法は、既存のクラス階層から必要な機能を可能な限り得ることのできる、いずれかの [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスから派生させることです。 このセクションでは、継承元とするクラスの選択に役立つように、最も重要な要素クラスのうちの 3 つのクラスが提供する機能を示します。  
  
 コントロールを実装する場合には ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスから派生させる理由としてはこれが実際のところ最も一般的なものですが)、実用的なコントロールであるクラス、コントロール ファミリの基本クラス、または少なくとも <xref:System.Windows.Controls.Control> 基底クラスから派生させるのが一般的です。 いくつかのガイドラインと実際の例については、「[コントロールの作成の概要](../controls/control-authoring-overview.md)」を参照してください。  
  
 コントロールを作成しているのではなく、階層の上位にあるクラスから派生する必要がある場合は、各基本要素クラスに定義された特性に関するガイドを意図した、以下のセクションを参照してください。  
  
 <xref:System.Windows.DependencyObject> から派生するクラスを作成すると、次の機能が継承されます。  
  
- <xref:System.Windows.DependencyObject.GetValue%2A> と <xref:System.Windows.DependencyObject.SetValue%2A> のサポート、およびプロパティ システム全体のサポート。  
  
- 依存関係プロパティと、依存関係プロパティとして実装されている添付プロパティを使用する機能。  
  
 <xref:System.Windows.UIElement> から派生するクラスを作成する場合は、<xref:System.Windows.DependencyObject> によって提供される機能以外に、次の機能を継承します。  
  
- アニメーション化されたプロパティ値の基本的なサポート。 詳しくは、「 [アニメーションの概要](../graphics-multimedia/animation-overview.md)」をご覧ください。  
  
- 基本的な入力イベントのサポートと、コマンド実行のサポート。 詳細については、「[入力の概要](input-overview.md)」および「[コマンド実行の概要](commanding-overview.md)」を参照してください。  
  
- レイアウト システムに情報を提供するためにオーバーライドできる仮想メソッド。  
  
 <xref:System.Windows.FrameworkElement> から派生するクラスを作成する場合は、<xref:System.Windows.UIElement> によって提供される機能以外に、次の機能を継承します。  
  
- スタイル設定とストーリーボードのサポート。 詳細については、「<xref:System.Windows.Style>」および「[ストーリーボードの概要](../graphics-multimedia/storyboards-overview.md)」を参照してください。  
  
- データ バインディングのサポート。 詳しくは、「 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」をご覧ください。  
  
- 動的リソース参照のサポート。 詳細については、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」を参照してください。  
  
- プロパティ値継承のサポート、および、データ バインディング、スタイル、またはレイアウトのフレームワークの実装などのフレームワーク サービスのプロパティに関する条件をレポートする場合に役立つ、メタデータ内の他のフラグ。 詳細については、「[フレームワーク プロパティ メタデータ](framework-property-metadata.md)」を参照してください。  
  
- 論理ツリーの概念。 詳細については、「[WPF のツリー](trees-in-wpf.md)」を参照してください。  
  
- レイアウトに影響を与えるプロパティの変更を検出できる <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> オーバーライドなど、レイアウト システムの実際的な WPF フレームワーク レベルの実装のサポート。  
  
 <xref:System.Windows.ContentElement> から派生するクラスを作成する場合は、<xref:System.Windows.DependencyObject> によって提供される機能以外に、次の機能を継承します。  
  
- アニメーションのサポート。 詳しくは、「 [アニメーションの概要](../graphics-multimedia/animation-overview.md)」をご覧ください。  
  
- 基本的な入力イベントのサポートと、コマンド実行のサポート。 詳細については、「[入力の概要](input-overview.md)」および「[コマンド実行の概要](commanding-overview.md)」を参照してください。  
  
 <xref:System.Windows.FrameworkContentElement> から派生するクラスを作成する場合は、<xref:System.Windows.ContentElement> によって提供される機能以外に、次の機能を使用できます。  
  
- スタイル設定とストーリーボードのサポート。 詳細については、「<xref:System.Windows.Style>」および「[アニメーションの概要](../graphics-multimedia/animation-overview.md)」を参照してください。  
  
- データ バインディングのサポート。 詳しくは、「 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)」をご覧ください。  
  
- 動的リソース参照のサポート。 詳しくは、「[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)」を参照してください。  
  
- プロパティ値継承のサポート、および、データ バインディング、スタイル、またはレイアウトのフレームワークの実装などのフレームワーク サービスのプロパティに関する条件をレポートする場合に役立つ、メタデータ内の他のフラグ。 詳細については、「[フレームワーク プロパティ メタデータ](framework-property-metadata.md)」を参照してください。  
  
- レイアウト システムの変更 (たとえば <xref:System.Windows.FrameworkElement.ArrangeOverride%2A>) へのアクセスは継承されません。 レイアウト システムの実装は、<xref:System.Windows.FrameworkElement> でのみ利用できます。 ただし、レイアウトに影響を与えるプロパティの変更を検出し、それらの変更を任意のコンテンツ ホストに報告できる <xref:System.Windows.FrameworkElement.OnPropertyChanged%2A> オーバーライドは継承されます。  
  
 さまざまなクラスに関してコンテンツ モデルがドキュメント化されています。 派生元として適切なクラスを見つける必要がある場合、クラスのコンテンツ モデルは、考慮する必要がある項目の候補の 1 つです。 詳細については、「[WPF のコンテンツ モデル](../controls/wpf-content-model.md)」を参照してください。  
  
<a name="other_base_classes"></a>
## <a name="other-base-classes"></a>他の基本クラス  
  
### <a name="dispatcherobject"></a>DispatcherObject  
 <xref:System.Windows.Threading.DispatcherObject> では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] スレッド モデルのサポートが提供されており、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション用に作成されたすべてのオブジェクトを <xref:System.Windows.Threading.Dispatcher> に関連付けられるようになります。 <xref:System.Windows.UIElement>、<xref:System.Windows.DependencyObject>、または <xref:System.Windows.Media.Visual> から派生させない場合でも、このスレッド モデルのサポートを可能にするために <xref:System.Windows.Threading.DispatcherObject> から派生させることを検討してください。 詳細については、「[スレッド モデル](threading-model.md)」を参照してください。  
  
### <a name="visual"></a>ビジュアル  
 <xref:System.Windows.Media.Visual> では、四角形に近い表示形式を必要とする 2D オブジェクトの概念が実装されています。 <xref:System.Windows.Media.Visual> の実際のレンダリングは他のクラスで行われます (単一のクラスですべての操作が完結しません) が、<xref:System.Windows.Media.Visual> クラスでは、レンダリング プロセスのさまざまなレベルで使用される既知の型が提供されます。 <xref:System.Windows.Media.Visual> ではヒット テストが実装されていますが、ヒット テストの結果を報告するイベントは公開されていません (このイベントは <xref:System.Windows.UIElement> にあります)。 詳細については、「[ビジュアル層のプログラミング](../graphics-multimedia/visual-layer-programming.md)」を参照してください。  
  
### <a name="freezable"></a>Freezable  
 <xref:System.Windows.Freezable> では、不変オブジェクトが必要なときやパフォーマンス上の理由で望ましいときにオブジェクトのコピーを生成する手段を提供することにより、可変オブジェクト上で不変性がシミュレートされます。 <xref:System.Windows.Freezable> 型は、ジオメトリ、ブラシ、アニメーションなどの特定のグラフィックス要素に使用できる共通の基盤です。 <xref:System.Windows.Freezable> は <xref:System.Windows.Media.Visual> ではありません。これには、別のオブジェクトのプロパティ値を設定するために <xref:System.Windows.Freezable> が適用されるときにサブプロパティとなるプロパティを格納できます。これらのサブプロパティは、レンダリングに影響することがあります。 詳細については、「[Freezable オブジェクトの概要](freezable-objects-overview.md)」を参照してください。  
  
 <xref:System.Windows.Media.Animation.Animatable>  
  
 <xref:System.Windows.Media.Animation.Animatable> は、<xref:System.Windows.Freezable> 派生クラスであり、このクラスによってアニメーション コントロール層とユーティリティ メンバーが追加され、現在のアニメーション プロパティを非アニメーション プロパティから区別できるようになります。  
  
### <a name="control"></a>Control  
 <xref:System.Windows.Controls.Control> は、あるテクノロジではコントロールと呼ばれ、別のテクノロジではコンポーネントと呼ばれるオブジェクトの種類の基底クラスとして意図されています。 一般に [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] コントロール クラスは、UI コントロールを直接表すクラスか、コントロールの複合に密接に参加するクラスです。 <xref:System.Windows.Controls.Control> で主に提供される機能は、コントロールのテンプレート作成です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Control>
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [コントロールの作成の概要](../controls/control-authoring-overview.md)
- [WPF アーキテクチャ](wpf-architecture.md)
