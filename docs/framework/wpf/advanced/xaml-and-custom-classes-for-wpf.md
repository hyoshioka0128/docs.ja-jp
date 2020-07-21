---
title: XAML とカスタム クラス
ms.date: 03/30/2017
helpviewer_keywords:
- custom classes in XAML [WPF]
- XAML [WPF], custom classes
- classes [WPF], custom classes in XAML
ms.assetid: e7313137-581e-4a64-8453-d44e15a6164a
ms.openlocfilehash: 4cd0ba7fa03d2578f4477c3ccf53188fbbea2dbd
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186265"
---
# <a name="xaml-and-custom-classes-for-wpf"></a>WPF における XAML とカスタム クラス
共通言語ランタイム (CLR) フレームワークで実装されている XAML では、任意の共通言語ランタイム (CLR) 言語でカスタム クラスまたはカスタム構造体を定義し、XAML マークアップを使用してそのクラスにアクセスする機能がサポートされています。 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 定義型とカスタム型の組み合わせを、同じマークアップ ファイル内で使用できます。そのためには、通常、カスタム型を XAML 名前空間プレフィックスにマップします。 このトピックでは、XAML 要素として使用できるようにするために、カスタム クラスが満たす必要のある要件について説明します。  

<a name="Custom_Classes_in_Applications_vs__in_Assemblies"></a>
## <a name="custom-classes-in-applications-or-assemblies"></a>アプリケーションまたはアセンブリでのカスタム クラス  
 XAML で使用されるカスタム クラスは、2 つの異なる方法で定義できます。プライマリ [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] アプリケーションを生成するコードビハインド内または他のコード内で定義する方法と、クラス ライブラリとして使用される実行可能ファイルや DLL などの別のアセンブリ内のクラスとして定義する方法です。 これらの各方法には、固有の利点と欠点があります。  
  
- クラス ライブラリを作成する利点は、そのようなカスタム クラスをさまざまなアプリケーション間で共有できることです。 また、別のライブラリを使用すると、アプリケーションのバージョン管理の問題の制御が簡単になり、使用目的が XAML ページでのルート要素であるクラスの作成が簡単になります。  
  
- アプリケーションでカスタム クラスを定義する利点として、この手法は比較的軽量であり、メイン アプリケーションの実行可能ファイル以外に別のアセンブリを導入した場合に発生する配置およびテストの問題が最小限に抑えられます。  
  
- 定義されているのが同じアセンブリか別のアセンブリかにかかわらず、カスタム クラスを XAML で要素として使用するには、CLR 名前空間と XML 名前空間の間でカスタム クラスをマップする必要があります。 「[XAML 名前空間および WPF XAML の名前空間の割り当て](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください。  
  
<a name="Requirements_for_a_Custom_Class_as_a_XAML_Element"></a>
## <a name="requirements-for-a-custom-class-as-a-xaml-element"></a>XAML 要素としてのカスタム クラスの要件  
 オブジェクト要素としてインスタンス化できるようにするには、クラスが次の要件を満たしている必要があります。  
  
- カスタム クラスはパブリックであり、既定の (パラメーターなしの) パブリック コンストラクターをサポートしている必要があります (構造に関する注意事項については、次のセクションを参照してください)。  
  
- カスタム クラスは入れ子にされたクラスであってはなりません。 入れ子にされたクラスと、CLR の一般的な使用構文の "ドット" は、添付プロパティなど、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] や XAML の他の機能と干渉します。  
  
 オブジェクト要素の構文が有効になるだけでなく、オブジェクトの定義では、そのオブジェクトを値の型として使用する他のパブリック プロパティに対するプロパティ要素の構文も有効になります。 これは、オブジェクトをオブジェクト要素としてインスタンス化でき、そのようなプロパティのプロパティ要素の値を埋めることができるためです。  
  
### <a name="structures"></a>構造体  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、カスタム型として定義する構造体を常に、XAML で構築できます。これは、CLR コンパイラによって暗黙的に作成される、構造体に対するパラメーターなしのコンストラクターで、すべてのプロパティ値が既定値に初期化されるためです。 場合によっては、構造体に対する既定の構築動作やオブジェクト要素の使用が、望ましくないことがあります。 これは、構造体は値を設定することが意図されていて、概念的には共用体として機能するためであり、含まれる値が相互に排他的な解釈を持ち、そのどのプロパティも設定できなくなる可能性があります。 <xref:System.Windows.GridLength> は、そのような構造体の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] での例です。 通常、そのような構造体では、構造体の値の異なる解釈やモードを作成する文字列規則を使用して、値を属性形式で表現できるように、型コンバーターを実装する必要があります。 また、構造体では、パラメーターありのコンストラクターを使用してコードを構築するための同様の動作も公開する必要があります。  
  
<a name="Requirements_for_Properties_of_a_Custom_Class_as_XAML"></a>
## <a name="requirements-for-properties-of-a-custom-class-as-xaml-attributes"></a>XAML 属性としてのカスタム クラスのプロパティの要件  
 プロパティでは、値渡し型 (プリミティブなど) を参照するか、XAML プロセッサがアクセスできるパラメーターなしのコンストラクターまたは専用の型コンバーターを持つ型のクラスを使用する必要があります。 CLR XAML の実装では、言語プリミティブのネイティブ サポート、またはバッキング型定義内の型またはメンバーに対する <xref:System.ComponentModel.TypeConverterAttribute> の適用を通じて、XAML プロセッサでこのようなコンバーターが検出されます  
  
 または、プロパティで抽象クラス型やインターフェイスを参照することもできます。 抽象クラスまたはインターフェイスの場合、XAML の解析では、プロパティの値には、インターフェイスを実装する実際のクラス インスタンス、または抽象クラスからの派生型のインスタンスが設定される必要があると、想定されています。  
  
 プロパティの宣言は抽象クラスでもできますが、プロパティに設定できるのは抽象クラスから派生した実際のクラスでだけです。 これは、クラスのオブジェクト要素を作成するには、クラスのパラメーターなしのパブリック コンストラクターが必要になるためです。  
  
### <a name="typeconverter-enabled-attribute-syntax"></a>TypeConverter が有効な属性の構文  
 クラス レベルで専用の属性付き型コンバーターを提供する場合、適用される型変換により、その型をインスタンス化する必要がある任意のプロパティの属性構文が有効になります。 型コンバーターがあるだけでは、型をオブジェクト要素で使用できるようにはなりません。その型に対してパラメーターなしのコンストラクターが存在する場合にだけ、オブジェクト要素で使用できるようになります。 そのため、型コンバーターが有効になっているプロパティは、通常、型自体でもオブジェクト要素構文がサポートされている場合を除き、プロパティ構文では使用できません。 例外として、プロパティ要素構文を指定できますが、プロパティ要素には文字列が含まれています。 その使用は実質的に属性構文の使用に相当するものであり、このような使用方法は、属性値のより堅牢な空白処理が必要な場合を除き、一般的ではありません。 たとえば、次の例では、文字列を受け取るプロパティ要素の使用法と、それと同等の属性の使用法を示します。  
  
 [!code-xaml[XamlOvwSupport#GoofyTCPE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe)]  
  
 [!code-xaml[XamlOvwSupport#GoofyTCPE2](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofytcpe2)]  
  
 属性構文は許可されていても、オブジェクト要素を含むプロパティ要素構文は XAML で許可されていないプロパティの例は、<xref:System.Windows.Input.Cursor> 型を受け取るさまざまなプロパティです。 <xref:System.Windows.Input.Cursor> クラスには専用の型コンバーター <xref:System.Windows.Input.CursorConverter> がありますが、パラメーターなしのコンストラクターは公開されていないため、実際の <xref:System.Windows.Input.Cursor> 型は参照型であっても、<xref:System.Windows.FrameworkElement.Cursor%2A> プロパティは属性構文を使用してのみ設定できます。  
  
### <a name="per-property-type-converters"></a>プロパティごとの型コンバーター  
 代わりの方法として、プロパティ自体のプロパティ レベルで型コンバーターを宣言できます。 これにより、適切な型に基づいて <xref:System.ComponentModel.TypeConverter.ConvertFrom%2A> 操作に対する入力として属性の入力文字列値を処理することにより、インラインでプロパティの型のオブジェクトをインスタンス化する "ミニ言語" が有効になります。 通常、これが行われるのは便利なアクセサーを提供することが目的であり、XAML でプロパティを設定できるようにするためだけではありません。 ただし、パラメーターなしのコンストラクターまたは属性付きの型コンバーターが提供されない既存の CLR 型を使用したい場合は、属性に対して型コンバーターを使用することもできます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] API で <xref:System.Globalization.CultureInfo> 型を受け取る特定のプロパティは、そのようなものの例です。 この場合、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、既存の Microsoft .NET Framework の <xref:System.Globalization.CultureInfo> 型を使用して、以前のバージョンのフレームワークで使用されていた互換性と移行のシナリオにより適切に対応してましたが、<xref:System.Globalization.CultureInfo> 型では、XAML プロパティ値として直接使用できるために必要なコンストラクターまたは型レベルの変換はサポートされていませんでした。  
  
 XAML で使用するプロパティを公開するときは常に (特に、コントロールを作成する場合)、依存関係プロパティを使用してそのプロパティをバッキングすることをよく検討する必要があります。 <xref:System.Windows.DependencyProperty> バッキングを使用するとパフォーマンスを向上させることができるため、XAML プロセッサの既存の [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 実装を使用する場合、これが特に当てはまります。 依存関係プロパティでは、ユーザーが XAML でアクセス可能なプロパティに対して期待するプロパティ システム機能がプロパティに対して公開されます。 これには、アニメーション、データ バインディング、スタイルのサポートなどの機能が含まれます。 詳細については、「[カスタム依存関係プロパティ](custom-dependency-properties.md)」および「[XAML 読み込みと依存関係プロパティ](xaml-loading-and-dependency-properties.md)」を参照してください。  
  
### <a name="writing-and-attributing-a-type-converter"></a>型コンバーターの記述と属性化  
 場合によっては、プロパティ型の型変換を提供するために、カスタム <xref:System.ComponentModel.TypeConverter> 派生クラスを記述する必要があります。 XAML での使用をサポートできる型コンバーターから派生させる方法、そのような型コンバーターを作成する手順、および <xref:System.ComponentModel.TypeConverterAttribute> を適用する方法については、「[TypeConverters および XAML](typeconverters-and-xaml.md)」を参照してください。  
  
<a name="Requirements_for_Events_of_a_Custom_Class_as_XAML"></a>
## <a name="requirements-for-xaml-event-handler-attribute-syntax-on-events-of-a-custom-class"></a>カスタム クラスのイベントでの XAML イベント ハンドラー属性構文に対する要件  
 CLR イベントとして使用できるようにするには、パラメーターなしのコンストラクターをサポートするクラスで、または派生クラスでイベントにアクセスできる抽象クラスで、イベントをパブリック イベントとして公開する必要があります。 ルーティング イベントとして簡単に使用するためには、CLR イベントで明示的な `add` メソッドと `remove` メソッドを実装する必要があります。これらのメソッドでは、CLR イベントのシグネチャのハンドラーを追加および削除し、それらのハンドラーを <xref:System.Windows.UIElement.AddHandler%2A> および <xref:System.Windows.UIElement.RemoveHandler%2A> メソッドに転送します。 これらのメソッドでは、イベントがアタッチされるインスタンス上のルーティング イベント ハンドラー ストアにハンドラーを追加したり、ストアからハンドラーを削除したりします。  
  
> [!NOTE]
> <xref:System.Windows.UIElement.AddHandler%2A> を使用してルーティング イベントにハンドラーを直接登録することができ、ルーティング イベントを公開する CLR イベントを意図的に定義しないでおくことができます。 イベントによってハンドラーをアタッチするための XAML 属性構文は有効にならず、生成されたクラスで提供されるその型の機能の XAML ビューは透過性が低いため、通常、この方法は推奨されません。  
  
<a name="Collection_Properties"></a>
## <a name="writing-collection-properties"></a>コレクションのプロパティの記述  
 コレクション型を受け取るプロパティには、コレクションに追加されるオブジェクトを指定できる XAML 構文があります。 この構文には、2 つの注目すべき機能があります。  
  
- オブジェクト要素構文では、コレクション オブジェクトであるオブジェクトを指定する必要はありません。 コレクション型を受け取るプロパティを XAML で指定するたびに、そのコレクション型は暗黙的に存在します。  
  
- マークアップでのコレクション プロパティの子要素は、コレクションのメンバーになるように処理されます。 通常、コレクションのメンバーにコードでアクセスするには、`Add` などのリストおよびディクショナリ メソッドまたはインデクサーを使用します。 ただし、XAML の構文では、メソッドまたはインデクサーはサポートされていません (例外: XAML 2009 ではメソッドがサポートされていますが、XAML 2009 を使用すると、WPF の可能な使用方法が制限されます。「[XAML 2009 言語機能](../../../desktop-wpf/xaml-services/xaml-2009-language-features.md)」を参照してください)。 コレクションが要素のツリーを構築するための非常に一般的な要件であることは明らかであり、宣言型の XAML でこれらのコレクションを設定する何らかの方法が必要です。 したがって、コレクション プロパティの子要素は、コレクション プロパティ型の値であるコレクションにそれを追加することで処理されます。  
  
 .NET Framework XAML サービスの実装、したがって WPF XAML プロセッサでは、コレクション プロパティを構成するものに対して次の定義が使用されます。 プロパティのプロパティ型では、次のいずれかが実装されている必要があります。  
  
- <xref:System.Collections.IList> の実装。  
  
- <xref:System.Collections.IDictionary> または同等の汎用 (<xref:System.Collections.Generic.IDictionary%602>) の実装。  
  
- <xref:System.Array> からの派生 (XAML での配列の詳細については、「[x:Array のマークアップ拡張機能](../../../desktop-wpf/xaml-services/xarray-markup-extension.md)」を参照)。  
  
- <xref:System.Windows.Markup.IAddChild> の実装 ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] によって定義されているインターフェイス)。  
  
 CLR でのこれらの各型には `Add` メソッドがあり、オブジェクト グラフの作成時に基になるコレクションに項目を追加するために、XAML プロセッサによって使用されます。  
  
> [!NOTE]
> `List` および `Dictionary` のジェネリック インターフェイス (<xref:System.Collections.Generic.IList%601> および <xref:System.Collections.Generic.IDictionary%602>) は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] XAML プロセッサによるコレクションの検出に対してはサポートされていません。 ただし、<xref:System.Collections.Generic.List%601> を基底クラスとして使用するか (<xref:System.Collections.IList> が直接実装されているため)、<xref:System.Collections.Generic.Dictionary%602> を基底クラスとして使用すること (<xref:System.Collections.IDictionary> が直接実装されているため) ができます。  
  
 コレクションを受け取るプロパティを宣言するときは、そのプロパティ値が型の新しいインスタンスで初期化される方法に注意してください。 プロパティを依存関係プロパティとして実装していない場合は、コレクション型のコンストラクターを呼び出すバッキング フィールドをプロパティで使用するのが適切です。 プロパティが依存関係プロパティである場合は、既定の型コンストラクターの一部として、コレクション プロパティを初期化することが必要な場合があります。 これは、依存関係プロパティではその既定値がメタデータから取得され、通常は、コレクション プロパティの初期値を静的な共有コレクションにするのは望ましくないためです。 含まれる型のインスタンスごとに、コレクション インスタンスが存在している必要があります。 詳細については、「[カスタム依存関係プロパティ](custom-dependency-properties.md)」を参照してください。  
  
 コレクション プロパティのカスタム コレクション型を実装できます。 コレクション プロパティは暗黙的に処理されるため、カスタム コレクション型を XAML で暗黙的に使用するために、パラメーターなしのコンストラクターを提供する必要はありません。 ただし、必要に応じて、コレクション型にパラメーターなしのコンストラクターを提供することもできます。 これは、有益な方法です。 パラメーターなしのコンストラクターを指定しない場合、コレクションをオブジェクト要素として明示的に宣言することはできません。 マークアップの作成者は、マークアップのスタイルとして、コレクションを明示的にすることを好む場合があります。 また、パラメーターなしのコンストラクターを使用すると、プロパティ値としてコレクション型を使用する新しいオブジェクトを作成するときに、初期化の要件を簡単にできます。  
  
<a name="XAMLCONtent"></a>
## <a name="declaring-xaml-content-properties"></a>XAML のコンテンツ プロパティの宣言  
 XAML 言語では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] コンテンツ プロパティの概念が定義されています。 オブジェクト構文で使用できる各クラスは、XAML コンテンツ プロパティを 1 つだけ持つことができます。 クラスの XAML コンテンツ プロパティとしてプロパティを宣言するには、クラス定義の一部として <xref:System.Windows.Markup.ContentPropertyAttribute> を適用します。 目的の XAML コンテンツ プロパティの名前を、属性の <xref:System.Windows.Markup.ContentPropertyAttribute.Name%2A> として指定します。 プロパティは、<xref:System.Reflection.PropertyInfo> などのリフレクション コンストラクトとしてではなく、名前で文字列として指定されます。  
  
 コレクション プロパティを XAML コンテンツ プロパティとして指定できます。 この結果、そのプロパティを使用して、コレクション オブジェクト要素またはプロパティ要素タグを介在させることなく、オブジェクト要素で 1 つ以上の子要素を使用できます。 これらの要素は、XAML コンテンツ プロパティの値として処理され、バッキング コレクションのインスタンスに追加されます。  
  
 既存の XAML コンテンツ プロパティの一部では、`Object` のプロパティ型が使用されます。 これにより、XAML コンテンツ プロパティで、<xref:System.String> などのプリミティブの値や、単一の参照オブジェクトの値を取得できるようになります。 このモデルに従う場合は、型の決定と、可能な型の処理を、型で行う必要があります。 <xref:System.Object> コンテンツ タイプを使用する一般的な理由は、オブジェクト コンテンツを文字列として追加する簡単な手段 (既定のプレゼンテーション処理を受けます) のサポートと、既定以外のプレゼンテーションや追加データを指定するオブジェクト コンテンツを追加する高度な手段のサポートの両方です。  
  
<a name="Serializing"></a>
## <a name="serializing-xaml"></a>XAML のシリアル化  
 コントロールを作成する場合など、特定のシナリオでは、XAML でインスタンス化できるすべてのオブジェクト表現を、同等の XAML マークアップにシリアル化できるようにしたい場合もあります。 このトピックでは、シリアル化の要件については説明しません。 「[コントロールの作成の概要](../controls/control-authoring-overview.md)」および「[要素のツリーおよびシリアル化](element-tree-and-serialization.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [カスタム依存関係プロパティ](custom-dependency-properties.md)
- [コントロールの作成の概要](../controls/control-authoring-overview.md)
- [基本要素の概要](base-elements-overview.md)
- [XAML 読み込みと依存関係プロパティ](xaml-loading-and-dependency-properties.md)
