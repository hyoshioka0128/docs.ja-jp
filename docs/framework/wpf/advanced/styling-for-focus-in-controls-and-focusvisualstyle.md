---
title: コントロールのフォーカスのスタイルと FocusVisualStyle
ms.date: 03/30/2017
helpviewer_keywords:
- keyboard focus [WPF]
- focus [WPF], visual styling
- styles [WPF], focus visual style
ms.assetid: 786ac576-011b-4d72-913b-558deccb9b35
ms.openlocfilehash: fda7ed12d232af5a7cfb8eb43cbb09eb793da171
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79141200"
---
# <a name="styling-for-focus-in-controls-and-focusvisualstyle"></a>コントロールのフォーカスのスタイルと FocusVisualStyle
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では、キーボード フォーカスを受け取ったときにコントロールの外観を変更するためのメカニズムが、並列的に 2 つ用意されています。 1 つ目のメカニズムは、コントロールに適用されるスタイルやテンプレート内で、<xref:System.Windows.UIElement.IsKeyboardFocused%2A> などのプロパティに対するプロパティ セッターを使用する方法です。 2 つ目のメカニズムは、<xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> プロパティの値として個別のスタイルを指定する方法です。"フォーカス表示スタイル" を使用すると、コントロールやその他の UI 要素のビジュアル ツリーを置き換えて変更するのではなく、コントロール上に描画する装飾用の独立したビジュアル ツリーを作成することができます。 このトピックでは、これらの各メカニズムがどのような場合に適しているかについて説明します。  

<a name="Purpose"></a>
## <a name="the-purpose-of-focus-visual-style"></a>フォーカス表示スタイルの目的  
 フォーカス表示スタイルは、UI 要素へのキーボード ナビゲーションに基づいてビジュアルなユーザー フィードバックを表示するための、共通の "オブジェクト モデル" を提供する機能です。 これは、コントロールに新しいテンプレートを適用したり、特定のテンプレート構成を把握したりしなくても利用できます。  
  
 ただし、フォーカス表示スタイル機能はコントロール テンプレートを把握せずに動作するので、フォーカス表示スタイルを使用したコントロールに表示できるビジュアル フィードバックは、必然的に限定されます。 この機能によって実際に行われることは、テンプレートを使用したコントロールのレンダリングによって作成されたビジュアル ツリーの上に、別のビジュアル ツリー (装飾) を重ね合わせるという処理です。 この個別のビジュアル ツリーは、<xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> プロパティに従ったスタイルを使用して定義します。  
  
<a name="Default"></a>
## <a name="default-focus-visual-style-behavior"></a>既定のフォーカス表示スタイル動作  
 フォーカス表示スタイルは、フォーカス アクションがキーボードによって開始された場合にのみ機能します。 マウス操作やプログラムによるフォーカス変更の場合、フォーカス表示スタイルのモードは無効になります。 各フォーカス モードの違いについて詳しくは、「[フォーカスの概要](focus-overview.md)」を参照してください。  
  
 コントロールのテーマには、既定のフォーカス表示スタイル動作があり、その動作が、そのテーマ内のすべてのコントロールのフォーカス表示スタイルになります。 このテーマ スタイルは、静的キー <xref:System.Windows.SystemParameters.FocusVisualStyleKey%2A> の値によって識別されます。 アプリケーション レベルで独自のフォーカス表示スタイルを宣言すると、この既定のスタイル動作が置き換えられます。 テーマ全体を定義する場合は、その同じキーを使用して、テーマ全体の既定動作のスタイルを定義する必要があります。  
  
 テーマ内では、通常、既定のフォーカス表示スタイルは非常にシンプルなものです。 大まかに表すと、次のようになります。  
  
```xaml  
<Style x:Key="{x:Static SystemParameters.FocusVisualStyleKey}">  
  <Setter Property="Control.Template">  
    <Setter.Value>  
      <ControlTemplate>  
        <Rectangle StrokeThickness="1"  
          Stroke="Black"  
          StrokeDashArray="1 2"  
          SnapsToDevicePixels="true"/>  
      </ControlTemplate>  
    </Setter.Value>  
  </Setter>  
</Style>  
```  
  
<a name="When"></a>
## <a name="when-to-use-focus-visual-styles"></a>フォーカス表示スタイルをいつ使用するか  
 基本的な考え方として、コントロールに適用されるフォーカス表示スタイルの外観は、各コントロール間で一貫している必要があります。 一貫性を維持するための 1 つの方法として、フォーカス表示スタイルを変更するのは、テーマ全体を構成する場合だけに限定するという方法があります。その場合、テーマ内で定義されている各コントロールに、まったく同じフォーカス表示スタイルを使用することもできますし、見た目の共通性を維持しながら、コントロールごとにスタイルのバリエーションを持たせることもできます。 また、ページや UI の要素のうち、キーボードでのフォーカス取得が可能なすべて要素について、同じスタイル (または類似のスタイル) を使ってスタイルを指定することもできます。  
  
 テーマに属していない個々のコントロール スタイルに対して <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> を設定することは、フォーカス表示スタイルの本来の用途ではありません。 表示動作がコントロール間で一貫していないと、キーボードのフォーカスに関してユーザーが混乱する可能性があるからです。 キーボード フォーカスに関する動作として、テーマ全体での一貫性から外れたものを特定のコントロールに意図的に指定したい場合は、個別の入力状態プロパティ (<xref:System.Windows.UIElement.IsFocused%2A> や <xref:System.Windows.UIElement.IsKeyboardFocused%2A> など) に対応したスタイルのトリガーを使用する方がアプローチとして適しています。  
  
 フォーカス表示スタイルは、キーボード フォーカス専用です。 そのため、フォーカス表示スタイルはユーザー補助機能の一種と言えます。 あらゆるタイプのフォーカス (マウス、キーボード、またはプログラム) を対象に UI を変更したい場合は、フォーカス表示スタイルを使用するのではなく、一般的なフォーカス プロパティ (<xref:System.Windows.UIElement.IsFocused%2A> や <xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> など) の値によって動作するスタイルやテンプレートで、セッターやトリガーを使用するようにしてください。  
  
<a name="How"></a>
## <a name="how-to-create-a-focus-visual-style"></a>フォーカス表示スタイルの作成方法  
 フォーカス表示スタイル用に作成するスタイルでは、常に <xref:System.Windows.Style.TargetType%2A> を <xref:System.Windows.Controls.Control> にします。 このスタイルは、主に <xref:System.Windows.Controls.ControlTemplate> で構成される必要があります。 ターゲットの種類として、そのフォーカス表示スタイルが <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A> に割り当てられている種類を指定することはしないでください。  
  
 ターゲットの種類は常に <xref:System.Windows.Controls.Control> となるので、すべてのコントロールに共通するプロパティを使用してスタイルを設定する必要があります (<xref:System.Windows.Controls.Control> クラスとその基本クラスのプロパティを使用します)。 テンプレートを作成する際には、UI 要素へのオーバーレイとして正しく機能すると共に、コントロールの機能領域が不明瞭にならないようにする必要があります。 つまり、ビジュアル フィードバックがコントロールの余白の外側に表示されるようにするか、一時的な (または目立ち過ぎない) 効果として表示されるようにして、フォーカス表示スタイルが適用されたコントロールに対するヒット テストの邪魔にならないようにする必要があります。 テンプレートのバインドで使用できるプロパティのうち、オーバーレイ テンプレートのサイズや位置を決定するのに役立つものとしては、<xref:System.Windows.FrameworkElement.ActualHeight%2A>、<xref:System.Windows.FrameworkElement.ActualWidth%2A>、<xref:System.Windows.FrameworkElement.Margin%2A>、<xref:System.Windows.Controls.Control.Padding%2A> があります。  
  
<a name="Alternatives"></a>
## <a name="alternatives-to-using-a-focus-visual-style"></a>フォーカス表示スタイルの代替手段  
 1 つのコントロールだけにスタイルを設定する場合や、コントロール テンプレートをより細かく制御したい場合など、フォーカス表示スタイルを使用するのが適切でない場合でも、フォーカスの変化に応じて表示動作を作成できるプロパティは他にもたくさんあります。  
  
 トリガー、セッター、およびイベント セッターについては、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」で詳しく説明しています。 ルーティング イベントの処理については、「[ルーティング イベントの概要](routed-events-overview.md)」で説明しています。  
  
### <a name="iskeyboardfocused"></a>IsKeyboardFocused  
 キーボード フォーカスに特化して対応したい場合は、<xref:System.Windows.UIElement.IsKeyboardFocused%2A> 依存関係プロパティをプロパティ <xref:System.Windows.Trigger> に使用することができます。 1 つのコントロールだけを対象にする場合で、他のコントロールのキーボード フォーカス動作とは見た目が調和しない可能性がある場合は、スタイルまたはテンプレートでプロパティ トリガーを使用すると、キーボード フォーカス動作をより効果的に定義することができます。  
  
 これに似たもう 1 つの依存関係プロパティとして、<xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> も使用できます。これは、キーボード フォーカスが複合的なコントロール領域や機能領域内にあることを視覚的に示したい場合に適しています。 たとえば、複数のコントロールをグループ化したパネルがある場合、<xref:System.Windows.UIElement.IsKeyboardFocusWithin%2A> トリガーを配置すれば、キーボード フォーカスがそのパネル内の個別の要素にまで絞られていない場合でも、そのパネルの表示が変わるようにすることができます。  
  
 また、<xref:System.Windows.UIElement.GotKeyboardFocus> イベントと <xref:System.Windows.UIElement.LostKeyboardFocus> イベント (およびプレビュー版での同等機能) を使用することもできます。 これらのイベントは、<xref:System.Windows.EventSetter> の基礎として使用できます。また、分離コード内のイベントのハンドラーを記述することもできます。  
  
### <a name="other-focus-properties"></a>その他のフォーカス プロパティ  
 フォーカス変更のあらゆる原因に対応して表示動作を生成したい場合は、セッターやトリガーのベースとして <xref:System.Windows.UIElement.IsFocused%2A> 依存関係プロパティを使用するか、<xref:System.Windows.UIElement.GotFocus> または <xref:System.Windows.UIElement.LostFocus> イベントを <xref:System.Windows.EventSetter> に使用するようにしましょう。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement.FocusVisualStyle%2A>
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [フォーカスの概要](focus-overview.md)
- [入力の概要](input-overview.md)
