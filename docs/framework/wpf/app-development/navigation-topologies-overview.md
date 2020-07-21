---
title: ナビゲーション トポロジの概要
ms.date: 03/30/2017
helpviewer_keywords:
- linear topology [WPF]
- fixed hierarchical topology [WPF]
- fixed linear topology [WPF]
- topologies [WPF]
- navigation topologies [WPF]
- dynamically-generated topology
ms.assetid: 5d5ee837-629a-4933-869a-186dc22ac43d
ms.openlocfilehash: 08f6342095706e5ffe9479f5236457d21474152a
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79174200"
---
# <a name="navigation-topologies-overview"></a>ナビゲーション トポロジの概要
<a name="introduction"></a> この概要では、WPF のナビゲーション トポロジを紹介します。 3 つの一般的なナビゲーション トポロジをサンプルと共に説明します。  
  
> [!NOTE]
> このトピックを読む前に、ページ関数を使用した WPF の構造化ナビゲーションの概念を理解している必要があります。 これらのトピックの詳細については、「[構造化ナビゲーションの概要](structured-navigation-overview.md)」を参照してください。  
  
 このトピックは、次のセクションで構成されています。  
  
- [ナビゲーション トポロジ](#Navigation_Topologies)  
  
- [構造化ナビゲーション トポロジ](#Structured_Navigation_Topologies)  
  
- [固定線形トポロジを介したナビゲーション](#Navigation_over_a_Fixed_Linear_Topology)  
  
- [固定階層トポロジを介した動的ナビゲーション](#Dynamic_Navigation_over_a_Fixed_Hierarchical_Topology)  
  
- [動的に生成されたトポロジを介したナビゲーション](#Navigation_over_a_Dynamically_Generated_Topology)  
  
<a name="Navigation_Topologies"></a>
## <a name="navigation-topologies"></a>ナビゲーション トポロジ  
 WPF では、ナビゲーションには、一般に、クリックされると他のページにナビゲートするハイパーリンク (<xref:System.Windows.Documents.Hyperlink>) を持つページ (<xref:System.Windows.Controls.Page>) で構成されます。 ナビゲート先のページは、Uniform Resource Identifier (URI) によって識別されます (「[WPF におけるパッケージの URI](pack-uris-in-wpf.md)」を参照)。 ページ、ハイパーリンク、および Uniform Resource Identifier (URI) を表示する次のような簡単な例を考えてみます。  
  
 [!code-xaml[NavigationTopologiesOverviewSnippets#Page1](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationTopologiesOverviewSnippets/CS/Page1.xaml#page1)]  
  
 [!code-xaml[NavigationTopologiesOverviewSnippets#Page2](~/samples/snippets/csharp/VS_Snippets_Wpf/NavigationTopologiesOverviewSnippets/CS/Page2.xaml#page2)]  
  
 これらのページは "*ナビゲーション トポロジ*" に配置され、その構造はページ間をどのような方法で移動できるかによって決まります。 このナビゲーション トポロジは、単純なシナリオに適していますが、ナビゲーションはより複雑なトポロジを必要とすることもあり、アプリケーションの実行中にしか定義できないものもあります。  
  
 このトピックでは、"*固定線形*"、"*固定階層*"、および "*動的生成*" という 3 つの一般的なナビゲーション トポロジについて説明 します。 各ナビゲーション トポロジについて、次の図に示されているような [!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を持つサンプルによって説明します。  
  
 ![データ項目を含むタスク ページとナビゲーション ボタン。](./media/navigation-topologies-overview/navigation-topology-data-items.png)  
  
<a name="Structured_Navigation_Topologies"></a>
## <a name="structured-navigation-topologies"></a>構造化ナビゲーション トポロジ  
 ナビゲーション トポロジには、大きく分けて次の 2 種類があります。  
  
- **固定トポロジ**: コンパイル時に定義され、実行時に変化しません。 固定トポロジは、シーケンスが固定されたページを線形的または階層的にナビゲートする場合に役立ちます。  
  
- **動的トポロジ**: ユーザー、アプリケーション、またはシステムから収集された入力に基づいて実行時に定義されます。 動的トポロジは、ページがさまざまなシーケンスでナビゲートされる可能性があるときに便利です。  
  
 ナビゲーション トポロジの作成にはページを使用することもできますが、これらのサンプルではページ関数を使用しています。その理由は、ページ関数に用意されている追加サポートによって、トポロジのページ間でデータをやり取りする機能のサポートを簡略化できるためです。  
  
<a name="Navigation_over_a_Fixed_Linear_Topology"></a>
## <a name="navigation-over-a-fixed-linear-topology"></a>固定線形トポロジを介したナビゲーション  
 固定線形トポロジは、シーケンスが固定されている 1 つ以上のウィザード ページの構造に似ています。 次の図では、固定線形トポロジを持つウィザードの高レベルの構造とフローを示します。  
  
 ![固定線形トポロジを示す図。](./media/navigation-topologies-overview/navigation-topology-fixed-linear.png)  
  
 固定線形トポロジを使用するナビゲーションの一般的な動作は、次のとおりです。  
  
- 呼び出し元ページから起動ページにナビゲートします。起動ページでは、ウィザードを初期化し、ウィザードの最初のページにナビゲートします。 呼び出し元ページからウィザードの最初のページを直接呼び出すこともできるため、起動ページ ([!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のない <xref:System.Windows.Navigation.PageFunction%601>) は必須ではありません。 ただし、起動ページを使用すると、ウィザードの初期化プロセスを簡略化でき、特に初期化が複雑な場合に便利です。  
  
- ユーザーは、[戻る] ボタンと [進む] ボタン (またはハイパーリンク) を使用して、ページ間を移動できます。  
  
- ユーザーは、履歴を使用してページ間を移動できます。  
  
- ユーザーは、[キャンセル] ボタンを押すことによって、任意のウィザード ページからウィザードをキャンセルできます。  
  
- ユーザーは、ウィザードの最後のページで [完了] ボタンを押すことによって、ウィザードを受け入れることができます。  
  
- ウィザードがキャンセルされると、ウィザードは適切な結果を返し、データは返しません。  
  
- ユーザーがウィザードを受け入れた場合、ウィザードは適切な結果を返し、収集したデータを返します。  
  
- ウィザードが完了すると (受け入れられた場合も、キャンセルされた場合も)、ウィザードを構成するページは履歴から削除されます。 これにより、ウィザードの各インスタンスが分離され、異常なデータや状態の発生を防ぎます。  
  
<a name="Dynamic_Navigation_over_a_Fixed_Hierarchical_Topology"></a>
## <a name="dynamic-navigation-over-a-fixed-hierarchical-topology"></a>固定階層トポロジを介した動的ナビゲーション  
 一部のアプリケーションでは、次の図に示されているように、ページから複数のページにナビゲートできる場合があります。
  
 ![複数のページに移動できるページを示す図。](./media/navigation-topologies-overview/navigation-topology-multiple-pages.png)  
  
 この構造は固定階層トポロジと呼ばれ、通常、階層内を移動するシーケンスは、アプリケーションまたはユーザーによって実行時に決定されます。 実行時に、他の複数のページにナビゲートできる階層内の各ページは、移動先ページを決定するために必要なデータを収集します。 次の図は、前の図に基づくいくつかの可能なナビゲーション シーケンスを示しています。  
  
 ![可能なナビゲーション シーケンスを示す図。](./media/navigation-topologies-overview/navigation-topology-fixed-hierarchical.png)  
  
 固定階層構造内のページのシーケンスは実行時に決定されますが、ユーザー エクスペリエンスは固定線形トポロジの場合と同じです。  
  
- 呼び出し元ページから起動ページにナビゲートします。起動ページでは、ウィザードを初期化し、ウィザードの最初のページにナビゲートします。 呼び出し元ページからウィザードの最初のページを直接呼び出すこともできるため、起動ページ ([!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のない <xref:System.Windows.Navigation.PageFunction%601>) は必須ではありません。 ただし、起動ページを使用すると、ウィザードの初期化プロセスを簡略化でき、特に初期化が複雑な場合に便利です。  
  
- ユーザーは、[戻る] ボタンと [進む] ボタン (またはハイパーリンク) を使用して、ページ間を移動できます。  
  
- ユーザーは、履歴を使用してページ間を移動できます。  
  
- ユーザーは、履歴をたどって戻ることで、ナビゲーション シーケンスを変更できます。  
  
- ユーザーは、[キャンセル] ボタンを押すことによって、任意のウィザード ページからウィザードをキャンセルできます。  
  
- ユーザーは、ウィザードの最後のページで [完了] ボタンを押すことによって、ウィザードを受け入れることができます。  
  
- ウィザードがキャンセルされると、ウィザードは適切な結果を返し、データは返しません。  
  
- ユーザーがウィザードを受け入れた場合、ウィザードは適切な結果を返し、収集したデータを返します。  
  
- ウィザードが完了すると (受け入れられた場合も、キャンセルされた場合も)、ウィザードを構成するページは履歴から削除されます。 これにより、ウィザードの各インスタンスが分離され、異常なデータや状態の発生を防ぎます。  
  
<a name="Navigation_over_a_Dynamically_Generated_Topology"></a>
## <a name="navigation-over-a-dynamically-generated-topology"></a>動的に生成されたトポロジを介したナビゲーション  
 一部のアプリケーションでは、複数のページ間を移動するシーケンスの決定にユーザー、アプリケーション、または外部データが必要になり、実行時にしか決定できない場合があります。 次の図では、基本となるナビゲーション シーケンスを持つ一連のページを示します。  
  
 ![基本となるナビゲーション シーケンスを持つ一連のページ。](./media/navigation-topologies-overview/navigation-topology-dynamically-generated.png)  
  
 次の図では、実行時にユーザーによって選択されたナビゲーション シーケンスを示します。  
  
 ![実行時に選択されたナビゲーション シーケンスを示す図。](./media/navigation-topologies-overview/navigation-topology-sequence-chosen-run-time.png)  
  
 このナビゲーション シーケンスは、動的生成トポロジと呼ばれます。 ユーザーにとっては、他のナビゲーション トポロジと同様に、ユーザー エクスペリエンスは前述のトポロジと同じです。  
  
- 呼び出し元ページから起動ページにナビゲートします。起動ページでは、ウィザードを初期化し、ウィザードの最初のページにナビゲートします。 呼び出し元ページからウィザードの最初のページを直接呼び出すこともできるため、起動ページ ([!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] のない <xref:System.Windows.Navigation.PageFunction%601>) は必須ではありません。 ただし、起動ページを使用すると、ウィザードの初期化プロセスを簡略化でき、特に初期化が複雑な場合に便利です。  
  
- ユーザーは、[戻る] ボタンと [進む] ボタン (またはハイパーリンク) を使用して、ページ間を移動できます。  
  
- ユーザーは、履歴を使用してページ間を移動できます。  
  
- ユーザーは、[キャンセル] ボタンを押すことによって、任意のウィザード ページからウィザードをキャンセルできます。  
  
- ユーザーは、ウィザードの最後のページで [完了] ボタンを押すことによって、ウィザードを受け入れることができます。  
  
- ウィザードがキャンセルされると、ウィザードは適切な結果を返し、データは返しません。  
  
- ユーザーがウィザードを受け入れた場合、ウィザードは適切な結果を返し、収集したデータを返します。  
  
- ウィザードが完了すると (受け入れられた場合も、キャンセルされた場合も)、ウィザードを構成するページは履歴から削除されます。 これにより、ウィザードの各インスタンスが分離され、異常なデータや状態の発生を防ぎます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Page>
- <xref:System.Windows.Navigation.PageFunction%601>
- <xref:System.Windows.Navigation.NavigationService>
- [構造化ナビゲーションの概要](structured-navigation-overview.md)
