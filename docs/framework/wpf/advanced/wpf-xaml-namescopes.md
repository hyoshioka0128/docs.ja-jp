---
title: XAML 名前スコープ
ms.date: 03/30/2017
helpviewer_keywords:
- namescopes [WPF]
- styles [WPF], namescopes in
- templates [WPF], namescopes in
- APIs [WPF], name-related
- name-related APIs
- XAML [WPF], namescopes
- classes [WPF], FrameworkContentElement
ms.assetid: 52bbf4f2-15fc-40d4-837b-bb4c21ead7d4
ms.openlocfilehash: f9d4439c6b102d0d430b5201e3649985daee0b7f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186275"
---
# <a name="wpf-xaml-namescopes"></a>WPF XAML 名前スコープ
XAML 名前スコープは、XAML で定義されているオブジェクトを識別する概念です。 XAML 名前スコープ内の名前を使用すると、オブジェクトの XAML で定義された名前と、オブジェクト ツリー内でそれに対応するインスタンスの間の関係を確立できます。 通常、XAMLアプリケーションの個々の XAML ページ ルートが読み込まれると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] マネージド コード内に XAML 名前スコープが作成されます。 プログラミング オブジェクトとしての XAML 名前スコープは、<xref:System.Windows.Markup.INameScope> インターフェイスによって定義されており、実際のクラス <xref:System.Windows.NameScope> によっても実装されます。  

<a name="Namescopes_in_Loaded_XAML_Applications"></a>
## <a name="namescopes-in-loaded-xaml-applications"></a>読み込まれた XAML アプリケーションでの名前スコープ  
 広範なプログラミングまたはコンピューター サイエンスのコンテキストでは、プログラミングの概念に、オブジェクトにアクセスするために使用できる一意の識別子または名前の原則が含まれることがよくあります。 識別子または名前を使用するシステムでは、名前スコープによって、その名前のオブジェクトが要求された場合にプロセスまたは技法によって検索する境界、または識別名の一意性が強制される境界が定義されます。 これらの一般的な原則は、XAML 名前スコープにも当てはまります。 WPF での XAML 名前スコープは、ページが読み込まれるときに、XAML ページのルート要素に対して作成されます。 ページ ルートから始まって、XAML ページ内で指定されている各名前が、関連する XAML 名前スコープに追加されます。  
  
 WPF XAML では、常に、一般的なルート要素 (<xref:System.Windows.Controls.Page>、<xref:System.Windows.Window> など) である要素によって、XAML 名前スコープが制御されます。 <xref:System.Windows.FrameworkElement> や <xref:System.Windows.FrameworkContentElement> などの要素がマークアップ内のページのルート要素である場合は、<xref:System.Windows.Controls.Page> で動作する XAML 名前スコープを提供できるように、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサによって <xref:System.Windows.Controls.Page> ルートが暗黙的に追加されます。  
  
> [!NOTE]
> [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] マークアップ内のどの要素でも `Name` または `x:Name` 属性が定義されていない場合でも、WPF のビルド アクションでは、XAML 運用環境に対する XAML 名前スコープが作成されます。  
  
 XAML 名前スコープ内で同じ名前を 2 回使用しようとすると、例外が発生します。 コードビハインドを持ち、コンパイルされたアプリケーションの一部である WPF XAML の場合、初期マークアップ コンパイルの間にページに対して生成されたクラスを作成すると、WPF ビルド アクションによってビルド時に例外が発生します。 ビルド アクションによってマークアップ コンパイルされない XAML の場合は、XAML 名前スコープの問題に関連する例外が、XAML の読み込み時に発生する可能性があります。 XAML デザイナーの場合、デザイン時にも XAML 名前スコープの問題が発生する可能性があります。  
  
### <a name="adding-objects-to-runtime-object-trees"></a>ランタイム オブジェクト ツリーへのオブジェクトの追加  
 XAML が解析されるときに、WPF XAML 名前スコープが作成されて定義されます。 オブジェクト ツリーを生成した XAML が解析された後で、そのオブジェクト ツリーにオブジェクトを追加した場合、新しいオブジェクトの `Name` または `x:Name` の値によって、XAML 名前スコープの情報が自動的に更新されることはありません。 XAML が読み込まれた後でオブジェクトの名前を WPF XAML 名前スコープに追加するには、XAML 名前スコープが定義されているオブジェクトで (通常は XAML ページ ルート) <xref:System.Windows.Markup.INameScope.RegisterName%2A> の適切な実装を呼び出す必要があります。 名前が登録されていない場合は、追加されたオブジェクトを <xref:System.Windows.FrameworkElement.FindName%2A> などのメソッドから名前で参照することはできず、その名前をアニメーションの対象として使用することはできません。  
  
 アプリケーション開発者にとって最も一般的なシナリオは、<xref:System.Windows.FrameworkElement.RegisterName%2A> を使用してページの現在のルートの XAML 名前スコープに名前を登録することです。 <xref:System.Windows.FrameworkElement.RegisterName%2A> は、オブジェクトをアニメーションの対象とするストーリーボードの重要なシナリオの一部です。 詳細については、「[ストーリーボードの概要](../graphics-multimedia/storyboards-overview.md)」を参照してください。  
  
 XAML 名前スコープが定義されているオブジェクト以外のオブジェクトで <xref:System.Windows.FrameworkElement.RegisterName%2A> を呼び出した場合でも、オブジェクトが定義されている XAML 名前スコープで <xref:System.Windows.FrameworkElement.RegisterName%2A> を呼び出した場合と同じように、その名前は、呼び出し元オブジェクトが保持されている XAML 名前スコープに登録されます。  
  
### <a name="xaml-namescopes-in-code"></a>コードでの XAML 名前スコープ  
 コードで XAML 名前スコープを作成して使用することができます。 XAML 名前スコープの作成に関係する API と概念は、純粋なコードを使用する場合でも同じです。これは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の XAML プロセッサでは、XAML 自体を処理するときにこれらの API と概念が使用されるためです。 この概念と API は主に、通常は一部または全部が XAML で定義されているオブジェクト ツリー内で、名前によってオブジェクトを検索できるようにするために存在します。  
  
 読み込まれた XAML からではなく、プログラムによって作成されるアプリケーションの場合、インスタンスでの XAML 名前スコープの作成をサポートするには、XAML 名前スコープが定義されているオブジェクトで <xref:System.Windows.Markup.INameScope> を実装するか、オブジェクトが <xref:System.Windows.FrameworkElement> または <xref:System.Windows.FrameworkContentElement> の派生クラスである必要があります。  
  
 また、XAML プロセッサによって読み込まれず、処理されない要素については、オブジェクトに対する XAML 名前スコープが既定で作成または初期化されることはありません。 後で名前を登録するオブジェクトについては、新しい XAML 名前スコープを明示的に作成する必要があります。 XAML 名前スコープを作成するには、静的な <xref:System.Windows.NameScope.SetNameScope%2A> メソッドを呼び出します。 それを所有するオブジェクトを `dependencyObject` パラメーターとして指定し、新しい <xref:System.Windows.NameScope.%23ctor%2A> コンストラクターの呼び出しを `value` パラメーターとして指定します。  
  
 <xref:System.Windows.NameScope.SetNameScope%2A> に対して `dependencyObject` として指定されたオブジェクトが、<xref:System.Windows.Markup.INameScope> の実装、<xref:System.Windows.FrameworkElement>、または <xref:System.Windows.FrameworkContentElement> ではない場合、任意の子要素で <xref:System.Windows.FrameworkElement.RegisterName%2A> を呼び出しても何の効果もありません。 新しい XAML 名前スコープの明示的な作成に失敗した場合、<xref:System.Windows.FrameworkElement.RegisterName%2A> を呼び出すと例外が発生します。  
  
 コードで XAML 名前スコープ API を使用する例については、「[名前のスコープを定義する](../graphics-multimedia/how-to-define-a-name-scope.md)」を参照してください。  
  
<a name="Namescopes_in_Styles_and_Templates"></a>
## <a name="xaml-namescopes-in-styles-and-templates"></a>スタイルとテンプレートでの XAML 名前スコープ  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のスタイルとテンプレートを使用すると、簡単な方法でコンテンツを再利用したり、再適用したりすることができます。 ただし、スタイルやテンプレートには、テンプレート レベルで XAML 名が定義されている要素が含まれる場合もあります。 その同じテンプレートが 1 ページで複数回使用される可能性があります。 このため、スタイルとテンプレートのどちらでも、スタイルまたはテンプレートが適用されるオブジェクト ツリー内の場所に関係がないように、独自の XAML 名前スコープを定義します。  
  
 次に例を示します。  
  
 [!code-xaml[XamlOvwSupport#NameScopeTemplates](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page6.xaml#namescopetemplates)]  
  
 ここでは、同じテンプレートを 2 つの異なるボタンに適用します。 テンプレートに個別の XAML 名前スコープがない場合は、テンプレートで使用されている名前 `TheBorder` により、XAML 名前スコープで名前の競合が発生します。 テンプレートのインスタンス化ごとに独自の XAML 名前スコープがあるため、この例では、インスタンス化されるテンプレートの各 XAML 名前スコープには、名前が 1 つだけ含まれます。  
  
 また、スタイルでも独自の XAML 名前スコープを定義します。これは主に、ストーリーボードの一部に特定の名前を割り当てることができるようにするためです。 これらの名前を使用すると、テンプレートがコントロールのカスタマイズの一部として再定義された場合でも、その名前の要素を対象とするコントロール固有の動作が有効になります。  
  
 個別の XAML 名前スコープがあるため、テンプレートでの名前付き要素の検索は、ページ内でテンプレート化されていない名前付き要素を見つける場合より困難です。 最初に、テンプレートが適用されているコントロールの <xref:System.Windows.Controls.Control.Template%2A> プロパティ値を取得することで、適用されているテンプレートを特定する必要があります。 次に、テンプレート バージョンの <xref:System.Windows.FrameworkTemplate.FindName%2A> を呼び出し、テンプレートが適用されたコントロールを 2 番目のパラメーターとして渡します。  
  
 コントロールの作成者が、適用されるテンプレートの特定の名前付き要素は、コントロール自体で定義されている動作のターゲットであるという規則を設けている場合は、コントロールの実装コードから <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> メソッドを使用できます。 <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> メソッドは保護されているので、コントロールの作成者だけがアクセスできます。  
  
 テンプレート内から作業していて、テンプレートが適用されている XAML 名前スコープにアクセスする必要がある場合は、<xref:System.Windows.FrameworkElement.TemplatedParent%2A> の値を取得し、そこで <xref:System.Windows.FrameworkElement.FindName%2A> を呼び出します。 テンプレート内での作業の例としては、適用されるテンプレートの要素からイベントが発生するイベント ハンドラーの実装を作成している場合があります。  
  
<a name="Namescopes_and_Name_related_APIs"></a>
## <a name="xaml-namescopes-and-name-related-apis"></a>XAML 名前スコープと名前関連の API  
 <xref:System.Windows.FrameworkElement> には、<xref:System.Windows.FrameworkElement.FindName%2A>、<xref:System.Windows.FrameworkElement.RegisterName%2A>、<xref:System.Windows.FrameworkElement.UnregisterName%2A> の各メソッドがあります。 これらのメソッドを呼び出すオブジェクトが XAML 名前スコープを所有している場合、メソッドでは、関連する XAML 名前スコープのメソッドが呼び出されます。 それ以外の場合は、親要素で XAML 名前スコープを所有しているかどうかがチェックされ、XAML 名前スコープが見つかるまで、このプロセスが再帰的に繰り返されます (XAML プロセッサの動作により、ルートには XAML 名前スコープがあることが保証されます)。 <xref:System.Windows.FrameworkContentElement> の動作も似ていますが、XAML 名前スコープを所有する <xref:System.Windows.FrameworkContentElement> がないという点が異なります。 呼び出しを最終的に <xref:System.Windows.FrameworkElement> の親要素に転送できるよう、メソッドは <xref:System.Windows.FrameworkContentElement> に存在します。  
  
 <xref:System.Windows.NameScope.SetNameScope%2A> は、新しい XAML 名前スコープを既存のオブジェクトにマップするために使用されます。 <xref:System.Windows.NameScope.SetNameScope%2A> を複数回呼び出して XAML 名前スコープをリセットまたはクリアすることができますが、これは一般的な使用方法ではありません。 また、通常、<xref:System.Windows.NameScope.GetNameScope%2A> はコードからは使用されません。  
  
### <a name="xaml-namescope-implementations"></a>XAML 名前スコープの実装  
 次のクラスでは、<xref:System.Windows.Markup.INameScope> が直接実装されています。  
  
- <xref:System.Windows.NameScope>  
  
- <xref:System.Windows.Style>  
  
- <xref:System.Windows.ResourceDictionary>  
  
- <xref:System.Windows.FrameworkTemplate>  
  
 <xref:System.Windows.ResourceDictionary> では、XAML の名前または名前スコープは使用されません。ディクショナリの実装であるため、代わりにキーが使用されます。 <xref:System.Windows.ResourceDictionary> で <xref:System.Windows.Markup.INameScope> が実装されている唯一の理由は、実際の XAML 名前スコープと <xref:System.Windows.ResourceDictionary> によるキーの処理方法の違いを明確にするのに役立つ例外をユーザー コードに対して生成することができることと、XAML 名前スコープが親要素によって <xref:System.Windows.ResourceDictionary> に適用されないようにするためです。  
  
 <xref:System.Windows.FrameworkTemplate> と <xref:System.Windows.Style> では、明示的なインターフェイス定義によって <xref:System.Windows.Markup.INameScope> が実装されています。 明示的に実装することで、これらの XAML 名前スコープは <xref:System.Windows.Markup.INameScope> インターフェイスからアクセスされたときに従来のように動作することができます。これは、XAML 名前スコープと [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内部プロセスの通信方法です。 ただし、明示的なインターフェイス定義は、<xref:System.Windows.FrameworkTemplate> および <xref:System.Windows.Style> の従来の API サーフェイスの一部ではありません。これは、<xref:System.Windows.FrameworkTemplate> や <xref:System.Windows.Style> で <xref:System.Windows.Markup.INameScope> メソッドを直接呼び出す必要はほとんどなく、代わりに <xref:System.Windows.FrameworkElement.GetTemplateChild%2A> などの他の API を使用するためです。  
  
 次のクラスでは、<xref:System.Windows.NameScope?displayProperty=nameWithType> ヘルパー クラスを使用し、<xref:System.Windows.NameScope.NameScope%2A?displayProperty=nameWithType> 添付プロパティを使用してその XAML 名前スコープの実装に接続することにより、独自の XAML 名前スコープが定義されています。  
  
- <xref:System.Windows.FrameworkElement>  
  
- <xref:System.Windows.FrameworkContentElement>  
  
## <a name="see-also"></a>関連項目

- [XAML 名前空間および WPF XAML の名前空間の割り当て](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)
- [x:Name ディレクティブ](../../../desktop-wpf/xaml-services/xname-directive.md)
