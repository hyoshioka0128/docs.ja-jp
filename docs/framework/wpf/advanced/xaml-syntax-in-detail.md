---
title: XAML 構文の詳細
ms.date: 03/30/2017
helpviewer_keywords:
- XML [WPF], namespaces
- XAML [WPF], parsing of attributes
- parsing of attributes [WPF]
- XAML [WPF], markup extensions
- attached properties [WPF]
- tag syntax [XAML]
- markup extensions [WPF]
- XAML [WPF], object element syntax
- XAML [WPF], syntax terminology
- attached events [WPF]
- lookup semantics [WPF]
- XAML [WPF], attached events
- XAML [WPF], content syntax
- XAML [WPF], lookup semantics
- content syntax [WPF]
- object element syntax [WPF]
- syntax terminology [XAML]
- XAML [WPF], attached properties
- attributes [XAML], parsing
- XAML [WPF], tag syntax
- XAML [WPF], attribute syntax
- property element syntax [WPF]
- terminology [XAML]
- namespaces [WPF], XML
- attribute syntax [XAML]
- XAML [WPF], property element syntax
ms.assetid: 67cce290-ca26-4c41-a797-b68aabc45479
ms.openlocfilehash: 5f8bb862ce443fd7397036b10f69cda65a6960bc
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646142"
---
# <a name="xaml-syntax-in-detail"></a>XAML 構文の詳細
このトピックでは、XAML 構文の要素について説明するために使用される用語を定義します。 これらの用語は、このドキュメントの他の部分で頻繁に使用されます。WPF のドキュメントと、System.Xaml レベルでの XAML 言語サポートによって有効にされる XAML および XAML の基本的な概念を使用する他のフレームワークの両方で使用されます。 このトピックは、[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md) に関するトピックで説明されている基本的な用語を拡充したものです。  

<a name="the_xaml_language_specification"></a>
## <a name="the-xaml-language-specification"></a>XAML 言語仕様  
 ここで定義されている XAML 構文の用語は、XAML 言語仕様でも定義または参照されています。 XAML は XML に基づく言語であり、XML 構造ルールに従うか、それを拡張しています。 一部の用語は、XML 言語または XML ドキュメント オブジェクト モデルを説明するときに一般的に使用される用語と共通であるか、またはそれが基になっています。  
  
 XAML 言語仕様の詳細については、Microsoft ダウンロード センターから [\[MS-XAML\]](https://download.microsoft.com/download/0/A/6/0A6F7755-9AF5-448B-907D-13985ACCF53E/[MS-XAML].pdf) をダウンロードしてください。  
  
<a name="xaml_and_clr"></a>
## <a name="xaml-and-clr"></a>XAML と CLR  
 XAML はマークアップ言語です。 名前のとおり、共通言語ランタイム (CLR) によってランタイムを実行できるようになります。 XAML 自体は、CLR ランタイムによって直接使用される共通言語の 1 つではありません。 そうではなく、XAML は独自の型システムをサポートするものと考えることができます。 WPF によって使用される特定の XAML 解析システムは、CLR と CLR 型システムが基になっています。 XAML の型は、WPF の XAML が解析されるときに、実行時の表現をインスタンス化するために、CLR の型にマップされます。 このため、このドキュメントの構文に関する残りの部分には、CLR 型システムへの参照が含まれています。ただし、XAML 言語仕様での同等の構文の説明には含まれません。 (XAML 言語仕様レベルによると、XAML 型は他の任意の型システムにマップでき、それは CLR である必要はありませんが、それには別の XAML パーサーを作成して使用する必要があります)。  
  
#### <a name="members-of-types-and-class-inheritance"></a>型のメンバーとクラスの継承  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 型の XAML メンバーであるプロパティとイベントは、多くの場合、基本型から継承されます。 たとえば、`<Button Background="Blue" .../>` について考えてみます。 クラス定義、リフレクション結果、またはドキュメントを見ると、<xref:System.Windows.Controls.Control.Background%2A> プロパティは、<xref:System.Windows.Controls.Button> クラスで直接宣言されているプロパティではありません。 そうではなく、<xref:System.Windows.Controls.Control.Background%2A> は基底クラス <xref:System.Windows.Controls.Control> から継承されています。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の XAML 要素のクラス継承動作は、XML マークアップのスキーマで適用される解釈とは大きく異なります。 クラスの継承は複雑になる可能性があります。中間の基底クラスが抽象型の場合、またはインターフェイスが関係している場合は特にそうです。 これは、DTD 形式や XSD 形式などの XML プログラミングで通常使用されるスキーマ型を使用して、XAML の要素とその使用可能な属性のセットを正確かつ完全に表現することが困難な理由の 1 つです。 もう 1 つの理由は、XAML 言語自体の機能拡張および型マッピング機能により、許容される型とメンバーを完全かつ一意的に表現することが不可能なためです。  
  
<a name="object_element_syntax"></a>
## <a name="object-element-syntax"></a>オブジェクト要素構文  
 "*オブジェクト要素構文*" は、XML 要素を宣言することで CLR のクラスまたは構造体をインスタンス化する XAML マークアップ構文です。 この構文は、HTML などの他のマークアップ言語の要素構文に似ています。 オブジェクト要素構文は、左山かっこ (\<) で始まり、インスタンス化されるクラスまたは構造体の型名が続きます。 型名の後には、0 個以上の空白を挿入できます。また、0 個以上の属性をオブジェクト要素で宣言することもできます。属性名 = "値" のペアを区切るには、1 つ以上のスペースを使用します。 最後に、次のいずれかが満たされている必要があります。  
  
- 要素とタグは、スラッシュ (/) とその直後の右山かっこ (>) によって閉じられる必要があります。  
  
- 開始タグは、右山かっこ (>) によって終了する必要があります。 開始タグの後には、他のオブジェクト要素、プロパティ要素、または内部テキストを記述できます。 厳密にここに含めることができる内容については、通常、要素のオブジェクト モデルによって制限されます。 適切な入れ子および他の開始および終了タグのペアとのバランスのため、オブジェクト要素に対応する終了タグが存在する必要もあります。  
  
 .NET によって実装される XAML には、オブジェクト要素から型、属性からプロパティまたはイベント、および XAML 名前空間から CLR 名前空間とアセンブリへのマップに関する一連の規則があります。 WPF と .NET では、XAML オブジェクト要素は参照されているアセンブリで定義されている .NET 型にマップされ、属性はそれらの型のメンバーにマップされます。 XAML で CLR 型を参照する場合は、その型の継承されたメンバーにもアクセスできます。  
  
 たとえば、次の例は、<xref:System.Windows.Controls.Button> クラスの新しいインスタンスをインスタンス化し、<xref:System.Windows.FrameworkElement.Name%2A> 属性とその属性の値を指定するオブジェクト要素構文です。  
  
 [!code-xaml[XAMLOvwSupport#SyntaxOE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxoe)]  
  
 次の例は、XAML コンテンツ プロパティ構文も含まれるオブジェクト要素構文です。 中に含まれる内部テキストは、<xref:System.Windows.Controls.TextBox> の XAML コンテンツ プロパティ <xref:System.Windows.Controls.TextBox.Text%2A> を設定するために使用されます。  
  
 [!code-xaml[XAMLOvwSupport#ThisIsATextBox](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#thisisatextbox)]  
  
### <a name="content-models"></a>コンテンツ モデル  
 クラスでは構文に関して XAML オブジェクト要素としての使用がサポートされている場合がありますが、その要素がアプリケーションまたはページで正しく機能するのは、コンテンツ モデルまたは要素ツリー全体の予想される位置に配置されている場合だけです。 たとえば、<xref:System.Windows.Controls.MenuItem> は通常、<xref:System.Windows.Controls.Menu> などの <xref:System.Windows.Controls.Primitives.MenuBase> 派生クラスの子としてのみ配置する必要があります。 特定の要素のコンテンツ モデルは、XAML 要素として使用できるコントロールおよび他の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] クラスのクラス ページの解説の一部として説明されています。  
  
<a name="properties_of_object_elements"></a>
## <a name="properties-of-object-elements"></a>オブジェクト要素のプロパティ  
 XAML のプロパティは、さまざまな構文で設定できます。 特定のプロパティに使用できる構文は、設定するプロパティの基になる型システムの特性によって異なります。  
  
 プロパティの値を設定することにより、オブジェクトが実行時オブジェクト グラフに存在するときの機能または特性が追加されます。 オブジェクト要素から作成されるオブジェクトの初期状態は、パラメーターなしのコンストラクターの動作に基づきます。 通常、アプリケーションでは、特定のオブジェクトの完全に既定のインスタンス以外のものを使用します。  
  
<a name="attribute_syntax_properties"></a>
## <a name="attribute-syntax-properties"></a>属性構文 (プロパティ)  
 属性構文は、既存のオブジェクト要素の属性を宣言することによってプロパティの値を設定する XAML マークアップ構文です。 属性名は、関連するオブジェクト要素の基になっているクラスのプロパティの CLR メンバー名と一致している必要があります。 属性名の後に代入演算子 (=) を記述します。 属性値は、引用符で囲まれた文字列である必要があります。  
  
> [!NOTE]
> 代替引用符を使用することにより、属性内でリテラルの引用符を使用できます。 たとえば、二重引用符が含まれる文字列を宣言する手段として、単一引用符を使用できます。 単一引用符と二重引用符のどちらを使用する場合でも、属性値の文字列の開始と終了には、一致するペアを使用する必要があります。 また、特定の XAML 構文での文字制限を回避するために使用できるエスケープ シーケンスやその他の手法もあります。 「[XML 文字エンティティと XAML](../../../desktop-wpf/xaml-services/xml-character-entities.md)」を参照してください。  
  
 属性構文を使用して設定するには、プロパティはパブリックで、書き込み可能である必要があります。 バッキング型システムでのプロパティの値は、値型であるか、または関連するバッキング型にアクセスするときに XAML プロセッサによってインスタンス化または参照できる参照型である必要があります。  
  
 WPF XAML イベントの場合、属性名として参照されるイベントはパブリックであり、パブリック デリゲートを持つ必要があります。  
  
 プロパティまたはイベントは、含む側のオブジェクト要素によってインスタンス化されるクラスまたは構造体のメンバーである必要があります。  
  
### <a name="processing-of-attribute-values"></a>属性値の処理  
 開始と終了の引用符に含まれる文字列値は、XAML プロセッサによって処理されます。 プロパティの既定の処理動作は、基になる CLR プロパティの型によって決まります。  
  
 属性値は、次のいずれかの方法により、この処理順序で設定されます。  
  
1. XAML プロセッサで、中かっこまたは <xref:System.Windows.Markup.MarkupExtension> から派生したオブジェクト要素が検出された場合は、値を文字列として処理するのではなく、参照されているマークアップ拡張が最初に評価され、マークアップ拡張によって返されるオブジェクトが値として使用されます。 多くの場合、マークアップ拡張によって返されるオブジェクトは、既存のオブジェクトへの参照、または実行時まで評価が延期される式であり、新しくインスタンス化されたオブジェクトではありません。  
  
2. プロパティが属性付きの <xref:System.ComponentModel.TypeConverter> で宣言されている場合、またはプロパティの値の型が属性付きの <xref:System.ComponentModel.TypeConverter> で宣言されている場合は、属性の文字列値が変換入力として型コンバーターに送信され、コンバーターからは新しいオブジェクト インスタンスが返されます。  
  
3. <xref:System.ComponentModel.TypeConverter> がない場合は、プロパティ型への直接変換が試みられます。 この最終的なレベルは、XAML 言語プリミティブ型間のパーサー ネイティブ値での直接変換、または列挙型の名前付き定数の名前のチェック (その場合、パーサーは一致した値にアクセスします) です。  
  
#### <a name="enumeration-attribute-values"></a>列挙属性の値  
 XAML の列挙は、本質的に XAML パーサーによって処理され、列挙型のメンバーは、列挙型の名前付き定数の 1 つの文字列名を指定することによって指定する必要があります。  
  
 フラグ以外の列挙値に対するネイティブな動作では、属性値の文字列が処理されて、列挙値のいずれかに解決されます。 コードでのように <*列挙型*>.<*値*> の形式で列挙型を指定することはありません。 代わりに "*値*" だけを指定し、"*列挙型*" は設定するプロパティの型によって推論されます。 <*列挙型*>.<*値*> の形式で属性を指定した場合は、正しく解決されません。  
  
 フラグ列挙型の動作は、<xref:System.Enum.Parse%2A?displayProperty=nameWithType> メソッドに基づきます。 各値をコンマで区切ることにより、フラグ列挙型に複数の値を指定できます。 ただし、フラグではない列挙値を組み合わせることはできません。 たとえば、コンマ構文を使用して、非フラグ列挙型の複数の条件に対して動作する <xref:System.Windows.Trigger> を作成することはできません。  
  
```xaml  
<!--This will not compile, because Visibility is not a flagwise enumeration.-->  
...  
<Trigger Property="Visibility" Value="Collapsed,Hidden">  
  <Setter ... />  
</Trigger>  
...  
```  
  
 XAML で設定可能な属性をサポートするフラグ列挙型は、WPF ではほとんど使用されません。 ただし、そのような列挙型の 1 つは <xref:System.Windows.Media.StyleSimulations> です。 たとえば、コンマ区切りのフラグ属性構文を使用して、<xref:System.Windows.Documents.Glyphs> クラスの解説に記載されている例を変更することができます。`StyleSimulations = "BoldSimulation"` を `StyleSimulations = "BoldSimulation,ItalicSimulation"` にすることができます。 <xref:System.Windows.Input.KeyBinding.Modifiers%2A?displayProperty=nameWithType> は、複数の列挙値を指定できるもう 1 つのプロパティです。 ただし、このプロパティは、<xref:System.Windows.Input.ModifierKeys> 列挙型で独自の型コンバーターがサポートされているため、特別なケースになります。 修飾子の型コンバーターでは、コンマ (,) ではなくプラス記号 (+) が区切り記号として使用されます。 この変換では、"Ctrl + Alt" など、Microsoft Windows プログラミングでキーの組み合わせを表す従来の構文がサポートされています。  
  
### <a name="properties-and-event-member-name-references"></a>プロパティとイベント メンバー名の参照  
 属性を指定するときは、含む側のオブジェクト要素に対してインスタンス化した CLR 型のメンバーとして存在する任意のプロパティまたはイベントを参照できます。  
  
 または、含む側のオブジェクト要素とは無関係に、添付プロパティまたは添付イベントを参照できます。 (添付プロパティについては、次のセクションで説明します)。  
  
 <*型名*>.<*イベント*> という部分修飾名を使用して、既定の名前空間でアクセスできる任意のオブジェクトから、任意のイベントを指定することもできます。この構文では、子要素からのイベント ルーティングをハンドラーで処理することが想定されているにも関わらず、親要素のメンバー テーブルにそのイベントがない場合の、ルーティング イベントに対するハンドラーのアタッチがサポートされています。 この構文は添付イベントの構文に似ていますが、ここでのイベントは添付イベントではありません。 この場合は、修飾名を持つイベントを参照しています。 詳細については、「[ルーティング イベントの概要](routed-events-overview.md)」を参照してください。  
  
 一部のシナリオでは、属性の値として属性名ではなくプロパティ名が指定されることがあります。 そのプロパティ名には、<*所有者の型*>.<*依存プロパティ名*> の形式で指定されたプロパティなど、修飾子が含まれる場合もあります。 このシナリオは、XAML でスタイルやテンプレートを作成する場合によく見られます。 属性値として指定されたプロパティ名の処理規則は異なり、設定されているプロパティの型、または特定の WPF サブシステムの動作によって管理されます。 詳細については、「[スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」を参照してください。  
  
 プロパティ名のもう 1 つの使用方法は、属性値でプロパティとプロパティの関係が記述されている場合です。 この機能は、データ バインディングとストーリーボード ターゲットに対して使用され、<xref:System.Windows.PropertyPath> クラスとその型コンバーターによって有効になります。 参照セマンティクスの詳細については、「[PropertyPath の XAML 構文](propertypath-xaml-syntax.md)」を参照してください。  
  
<a name="property_element_syntax"></a>
## <a name="property-element-syntax"></a>プロパティ要素の構文  
 "*プロパティ要素の構文*" は、要素の基本的な XML 構文規則とは少し異なる構文です。 XML では、属性の値は事実上は文字列であり、唯一可能なバリエーションは、使用される文字列エンコード形式です。 XAML では、プロパティの値として他のオブジェクト要素を割り当てることができます。 この機能は、プロパティ要素の構文によって有効になります。 プロパティは、要素タグ内の属性として指定されるのではなく、<*要素型名*>.<*プロパティ名*> という形式の開始要素タグを使用して指定され、プロパティの値がその中で指定されて、プロパティ要素が閉じられます。  
  
 具体的には、構文は左山かっこ (\<) で始まり、その直後に、プロパティ要素の構文が含まれているクラスまたは構造体の型名が続きます。 それ以降は、1 つのドット (.)、プロパティの名前、右山かっこ (>) の順になります。 属性構文と同様に、そのプロパティは、指定された型の宣言されたパブリック メンバー内に存在する必要があります。 プロパティに割り当てられる値は、プロパティ要素内に格納されています。 プロパティ要素の構文では値として指定されたオブジェクトを処理することが想定されているため、通常、値は 1 つ以上のオブジェクト要素として指定します。 最後に、同じ <*要素型名*>.<*プロパティ名*> の組み合わせを指定する同等の終了タグを指定し、適切な入れ子および他の要素タグとのバランスにする必要があります。  
  
 たとえば、次に示すのは、<xref:System.Windows.Controls.Button> の <xref:System.Windows.FrameworkElement.ContextMenu%2A> プロパティに対するプロパティ要素の構文です。  
  
 [!code-xaml[XAMLOvwSupport#ContextMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#contextmenu)]  
  
 また、指定されるプロパティの型が <xref:System.String> などのプリミティブ値の型である場合、または名前が指定された列挙型である場合は、プロパティ要素内の値を内部テキストとして指定することもできます。 これらの 2 つの使用方法は、いずれの場合もさらに単純な属性構文を使用できるため、あまり一般的ではありません。 文字列でプロパティ要素を指定する 1 つのシナリオは、XAML コンテンツ プロパティではなくても、UI テキストの表現に使用され、ラインフィードなどの特定の空白文字要素をその UI テキストで表示する必要があるプロパティの場合です。 属性の構文では改行を保持できませんが、プロパティ要素の構文では、重要な空白の保持がアクティブになっている場合は保持できます (詳細については、「[XAML での空白の処理](../../../desktop-wpf/xaml-services/white-space-processing.md)」を参照してください)。 もう 1 つのシナリオは、[x:Uid ディレクティブ](../../../desktop-wpf/xaml-services/xuid-directive.md)をプロパティ要素に適用し、その中の値を、WPF 出力 BAML または他の手法でローカライズする必要がある値としてマークできるようにする場合です。  
  
 プロパティ要素は、WPF 論理ツリーでは表されません。 プロパティ要素は、プロパティを設定するための特定の構文であり、その基になるインスタンスまたはオブジェクトがある要素ではありません。 (論理ツリーの概念の詳細については、「[WPF のツリー](trees-in-wpf.md)」を参照してください)。  
  
 属性とプロパティ要素の両方の構文がサポートされているプロパティの場合は、通常、2 つの構文は同じ結果になりますが、空白文字の処理などの微妙な点は構文によって多少異なります。  
  
<a name="collection_syntax"></a>
## <a name="collection-syntax"></a>コレクションの構文  
 XAML の仕様では、値の型がコレクションであるプロパティを XAML プロセッサの実装で識別する必要があります。 .NET での一般的な XAML プロセッサの実装は、マネージド コードと CLR に基づいており、次のいずれかを使用してコレクション型を識別します。  
  
- 型で <xref:System.Collections.IList> が実装されている。  
  
- 型で <xref:System.Collections.IDictionary> が実装されている。  
  
- 型が <xref:System.Array> から派生している (XAML での配列の詳細については、「[x:Array のマークアップ拡張機能](../../../desktop-wpf/xaml-services/xarray-markup-extension.md)」を参照)。  
  
 プロパティの型がコレクションである場合、推論されるコレクション型を、マークアップでオブジェクト要素として指定する必要はありません。 代わりに、コレクションの項目になることが予想される要素を、プロパティ要素の 1 つ以上の子要素として指定します。 そのような各項目は、読み込み中にオブジェクトに対して評価され、暗黙的なコレクションの `Add` メソッドを呼び出すことによってコレクションに追加されます。 たとえば、<xref:System.Windows.Style> の <xref:System.Windows.Style.Triggers%2A> プロパティは特殊なコレクション型 <xref:System.Windows.TriggerCollection> になり、その型では <xref:System.Collections.IList> が実装されています。 マークアップで <xref:System.Windows.TriggerCollection> オブジェクト要素をインスタンス化する必要はありません。 代わりに、1 つ以上の <xref:System.Windows.Trigger> 項目を `Style.Triggers` プロパティ要素内の要素として指定します。ここで、<xref:System.Windows.Trigger> (または派生クラス) は、厳密に型指定された暗黙の <xref:System.Windows.TriggerCollection> に対する項目型として想定される型です。  
  
 [!code-xaml[XAMLOvwSupport#SyntaxPECollection](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#syntaxpecollection)]  
  
 プロパティは、コレクション型と、その型および派生型に対する XAML コンテンツ プロパティの両方にすることができます。詳細については、このトピックの次のセクションで説明します。  
  
 暗黙的なコレクション要素では、マークアップに要素として出現しない場合でも、論理ツリー表現にメンバーが作成されます。 通常、親の型のコンストラクターでは、そのプロパティの 1 つであるコレクションのインスタンス化が実行され、初期状態が空のコレクションがオブジェクト ツリーの一部になります。  
  
> [!NOTE]
> リストとディクショナリのジェネリック インターフェイス (<xref:System.Collections.Generic.IList%601> および <xref:System.Collections.Generic.IDictionary%602>) は、コレクションの検出に対してはサポートされていません。 ただし、<xref:System.Collections.Generic.List%601> を基底クラスとして使用するか (<xref:System.Collections.IList> が直接実装されているため)、<xref:System.Collections.Generic.Dictionary%602> を基底クラスとして使用すること (<xref:System.Collections.IDictionary> が直接実装されているため) ができます。  
  
 コレクション型に関する .NET のリファレンス ページでは、コレクションのオブジェクト要素を意図的に省略したこの構文が、XAML 構文のセクションで暗黙のコレクション構文として示されていることがあります。  
  
 ルート要素を除き、別の要素の子要素として入れ子になっている XAML ファイル内のすべてのオブジェクト要素は、実際には、その親要素の暗黙的なコレクション プロパティのメンバー、または親要素の XAML コンテンツ プロパティの値を指定する要素の、どちらか一方または両方です (XAML コンテンツ プロパティについては、次のセクションで説明します)。 つまり、マークアップ ページでの親要素と子要素の関係は、実際には、ルートに 1 つのオブジェクトがあり、ルートの下にあるすべてのオブジェクト要素は、親のプロパティ値を提供する単一のインスタンスであるか、または親のコレクション型プロパティ値でもあるコレクション内の項目の 1 つです。 この単一ルートの概念は XML に共通しており、多くの場合、<xref:System.Windows.Markup.XamlReader.Load%2A> などの XAML を読み込む API の動作で強化されます。  
  
 次に示すのは、明示的に指定されているコレクション (<xref:System.Windows.Media.GradientStopCollection>) に対するオブジェクト要素の構文の例です。  
  
```xaml  
<LinearGradientBrush>  
  <LinearGradientBrush.GradientStops>  
    <GradientStopCollection>  
      <GradientStop Offset="0.0" Color="Red" />  
      <GradientStop Offset="1.0" Color="Blue" />  
    </GradientStopCollection>  
  </LinearGradientBrush.GradientStops>  
</LinearGradientBrush>  
```  
  
 コレクションを明示的に宣言することが常に可能なわけではないことに注意してください。 たとえば、前に示した <xref:System.Windows.Style.Triggers%2A> の例で <xref:System.Windows.TriggerCollection> を明示的に宣言しようとすると、失敗します。 コレクションを明示的に宣言するには、コレクション クラスでパラメーターなしのコンストラクターがサポートされていて、<xref:System.Windows.TriggerCollection> にパラメーターなしのコンストラクターが存在していない必要があります。  
  
<a name="xaml_content_properties"></a>
## <a name="xaml-content-properties"></a>XAML コンテンツのプロパティ  
 XAML コンテンツの構文は、クラス宣言の一部として <xref:System.Windows.Markup.ContentPropertyAttribute> が指定されているクラスでのみ有効な構文です。 <xref:System.Windows.Markup.ContentPropertyAttribute> では、その型の要素 (派生クラスを含む) に対するコンテンツ プロパティであるプロパティ名が参照されます。 XAML プロセッサによって処理される場合、オブジェクト要素の開始タグと終了タグの間にある子要素または内部テキストは、そのオブジェクトの XAML コンテンツ プロパティの値として割り当てられます。 コンテンツ プロパティに対して明示的なプロパティ要素を指定することは許可されていますが、一般に、.NET リファレンスの XAML 構文のセクションでは、この使用方法は示されていません。 明示的で詳細な手法は、マークアップのわかりやすさやマークアップのスタイルに関して場合によっては価値がありますが、通常、コンテンツ プロパティの目的は、直感的に親子として関連付けられる要素を直接入れ子にできるように、マークアップを効率化することです。 要素の他のプロパティに対するプロパティ要素タグは、XAML 言語の厳密な定義では "コンテンツ" として割り当てられません。これらは、XAML パーサーの処理順序でそれより前に処理され、"コンテンツ" とは見なされません。  
  
### <a name="xaml-content-property-values-must-be-contiguous"></a>XAML コンテンツ プロパティの値は連続している必要がある  
 XAML コンテンツ プロパティの値は、そのオブジェクト要素の他のプロパティ要素の完全に前または完全に後のいずれかに指定する必要があります。 これは、XAML コンテンツ プロパティの値が文字列として指定されているか、または 1 つ以上のオブジェクトとして指定されているに関わらず当てはまります。 たとえば、次のようなマークアップは解析されません。  
  
```xaml  
<Button>I am a
  <Button.Background>Blue</Button.Background>  
  blue button</Button>  
```  
  
 コンテンツ プロパティのプロパティ要素構文を使用してこの構文が明示的に作成されている場合、コンテンツ プロパティが 2 回設定されるため、これは基本的に無効です。  
  
```xaml  
<Button>  
  <Button.Content>I am a </Button.Content>  
  <Button.Background>Blue</Button.Background>  
  <Button.Content> blue button</Button.Content>  
</Button>  
```  
  
 同じように無効な例は、コンテンツ プロパティがコレクションであり、子要素とプロパティ要素が混在している場合です。  
  
```xaml  
<StackPanel>  
  <Button>This example</Button>  
  <StackPanel.Resources>  
    <SolidColorBrush x:Key="BlueBrush" Color="Blue"/>  
  </StackPanel.Resources>  
  <Button>... is illegal XAML</Button>  
</StackPanel>  
```  
  
<a name="content_properties_and_collection_syntax_combined"></a>
## <a name="content-properties-and-collection-syntax-combined"></a>コンテンツ プロパティとコレクション構文の組み合わせ  
 複数のオブジェクト要素をコンテンツとして受け入れるには、コンテンツ プロパティの型が明示的なコレクション型である必要があります。 コレクション型に対するプロパティ要素の構文と同様に、XAML プロセッサではコレクション型である型を識別する必要があります。 要素に XAML コンテンツ プロパティがあり、XAML コンテンツ プロパティの型がコレクションである場合は、暗黙的なコレクション型をオブジェクト要素としてマークアップで指定する必要はなく、XAML コンテンツ プロパティをプロパティ要素として指定する必要もありません。 そのため、マークアップの明白なコンテンツ モデルでは、複数の子要素をコンテンツとして割り当てることができます。 <xref:System.Windows.Controls.Panel> 派生クラスのコンテンツ構文を次に示します。 すべての <xref:System.Windows.Controls.Panel> 派生クラスでは、XAML コンテンツ プロパティは <xref:System.Windows.Controls.Panel.Children%2A> として設定され、これには <xref:System.Windows.Controls.UIElementCollection> 型の値が必要です。  
  
 [!code-xaml[XAMLOvwSupport#SyntaxContent](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page5.xaml#syntaxcontent)]  
  
 マークアップには <xref:System.Windows.Controls.Panel.Children%2A> のプロパティ要素も <xref:System.Windows.Controls.UIElementCollection> の要素も必要ないことに注意してください。 これは XAML の設計機能であり、これにより、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] を定義する再帰的包含要素が、プロパティ要素タグやコレクション オブジェクトを介在させることなく、直接的な親子要素関係を持つ入れ子になった要素のツリーとして表現されます。 実際には、設計上、<xref:System.Windows.Controls.UIElementCollection> をマークアップでオブジェクト要素として明示的に指定することはできません。 唯一の用途が暗黙のコレクションである <xref:System.Windows.Controls.UIElementCollection> では、パラメーターなしのパブリック コンストラクターは公開されず、オブジェクト要素としてインスタンス化することはできません。  
  
### <a name="mixing-property-elements-and-object-elements-in-an-object-with-a-content-property"></a>コンテンツ プロパティがあるオブジェクトでのプロパティ要素とオブジェクト要素の混合  
 XAML の仕様では、オブジェクト要素内の XAML コンテンツ プロパティを格納するために使用されるオブジェクト要素は連続している必要があり、混合されていてはならない、ということを XAML プロセッサで適用できることが宣言されています。 プロパティ要素とコンテンツの混合に対するこの制限は、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の XAML プロセッサによって適用されます。  
  
 オブジェクト要素内の最初の即時マークアップとして、子オブジェクト要素を指定することができます。 その後、プロパティ要素を導入できます。 または、1 つ以上のプロパティ要素を指定し、次にコンテンツを指定し、さらにプロパティ要素を指定することもできます。 ただし、コンテンツの後でプロパティ要素を指定したら、それ以上コンテンツを指定することはできず、追加できるのはプロパティ要素だけです。  
  
 このコンテンツとプロパティ要素の順序に関する要件は、コンテンツとして使用される内部テキストには適用されません。 ただし、プロパティ要素と内部テキストが混在している場合、大きな空白をマークアップで視覚的に検出するのは困難であるため、内部テキストを連続させるのは、やはり適切なマークアップ スタイルです。  
  
<a name="xaml_namespaces"></a>
## <a name="xaml-namespaces"></a>XAML 名前空間  
 これまでの構文の例では、既定の XAML 名前空間以外の XAML 名前空間は指定されていません。 一般的な [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 名前空間が既定の XAML 名前空間として指定されます。 既定の XAML 名前空間以外の XAML 名前空間を指定した場合でも、同様の構文を使用できます。 ただし、その場合は、既定の XAML 名前空間内でアクセスできないクラスの名前を指定するすべての場所で、そのクラス名の前に、対応する CLR 名前空間にマップされる XAML 名前空間のプレフィックスを付ける必要があります。 たとえば、`<custom:Example/>` は、`Example` クラスのインスタンスをインスタンス化するためのオブジェクト要素構文です。そのクラス (および場合によっては、バッキング型を含む外部アセンブリ情報) を含む CLR 名前空間は、これより前に `custom` プレフィックスにマップされています。  
  
 XAML 名前空間の詳細については、「[XAML 名前空間および WPF XAML の名前空間の割り当て](xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください。  
  
<a name="markup_extensions"></a>
## <a name="markup-extensions"></a>マークアップ拡張機能  
 XAML で定義されているマークアップ拡張のプログラミング エンティティを使用すると、文字列属性値またはオブジェクト要素の通常の XAML プロセッサ処理をエスケープして、処理をバッキング クラスに延期することができます。 属性構文を使用するときに XAML プロセッサに対してマークアップ拡張を示す文字は左中かっこ ({) で、その後に右中かっこ (}) 以外の任意の文字が続きます。 左中かっこの後の最初の文字列では、特定の拡張機能の動作を提供するクラスを参照する必要があります。部分文字列 "Extension" が真のクラス名の一部である場合、参照ではその部分文字列を省略できます。 その後には 1 つのスペースを使用でき、それ以降は、右中かっこが検出されるまで、各文字が拡張機能の実装により入力として使用されます。  
  
 .NET XAML の実装では、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] および他のフレームワークやテクノロジによってサポートされているすべてのマークアップ拡張の基底として、<xref:System.Windows.Markup.MarkupExtension> 抽象クラスが使用されます。 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] で明示的に実装されているマークアップ拡張の目的は、多くの場合、他の既存のオブジェクトを参照する手段を提供すること、または実行時に評価されるオブジェクトへの遅延参照を行うことです。 たとえば、特定のプロパティが通常受け取る値の代わりに `{Binding}` マークアップ拡張を指定することにより、簡単な WPF データ バインディングが実現されます。 WPF マークアップ拡張の多くでは、通常は属性構文を使用できない場所で、プロパティに対して属性構文を使用できます。 たとえば、<xref:System.Windows.Style> オブジェクトは、入れ子になった一連のオブジェクトとプロパティが含まれる比較的複雑な型です。 WPF のスタイルは、通常、<xref:System.Windows.ResourceDictionary> のリソースとして定義された後、リソースを要求する 2 つの WPF マークアップ拡張のいずれかを使用して参照されます。 マークアップ拡張では、プロパティ値の評価がリソース参照まで延期され、次の例に示すように、属性構文で <xref:System.Windows.Style> 型を使用して <xref:System.Windows.FrameworkElement.Style%2A> プロパティの値を提供できます。  
  
 `<Button Style="{StaticResource MyStyle}">My button</Button>`  
  
 ここで、`StaticResource` は、マークアップ拡張の実装を提供する <xref:System.Windows.StaticResourceExtension> クラスを示します。 次の文字列 `MyStyle` は、既定以外の <xref:System.Windows.StaticResourceExtension> コンストラクターに対する入力として使用されます。この場合、拡張文字列から取得されるパラメーターでは、要求される <xref:System.Windows.ResourceKey> が宣言されています。 `MyStyle` は、リソースとして定義されている <xref:System.Windows.Style> の [x:Key](../../../desktop-wpf/xaml-services/xkey-directive.md) 値であると想定されます。 [StaticResource マークアップ拡張](staticresource-markup-extension.md)を使用すると、読み込み時に静的リソース参照ロジックを使用して、<xref:System.Windows.Style> プロパティ値を提供するためにリソースを使用することが要求されます。  
  
 マークアップ拡張機能の詳細については、 「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。 一般的な .NET XAML の実装で有効になるマークアップ拡張と他の XAML プログラミング機能のリファレンスについては、「[XAML 名前空間 (x:) 言語機能](../../../desktop-wpf/xaml-services/namespace-language-features.md)」を参照してください。 WPF 固有のマークアップ拡張については、「[WPF XAML 拡張機能](wpf-xaml-extensions.md)」を参照してください。  
  
<a name="attached_properties"></a>
## <a name="attached-properties"></a>アタッチされるプロパティ  
 添付プロパティは XAML で導入されたプログラミング概念であり、プロパティを特定の型で所有および定義しながら、任意の要素の属性またはプロパティ要素として設定できます。 添付プロパティで想定されている主なシナリオは、すべての要素で広範にオブジェクト モデルを共有する必要なしに、マークアップ構造内の子要素で、親要素に情報を報告できるようにすることです。 逆に、親要素で添付プロパティを使用すると、子要素に情報を報告できます。 添付プロパティの目的と、独自の添付プロパティを作成する方法の詳細については、「[添付プロパティの概要](attached-properties-overview.md)」を参照してください。  
  
 添付プロパティで使用する構文は、<*型名*>.<*プロパティ名*> の組み合わせをやはり指定する点では、プロパティ要素の構文と一見似ています。 次の 2 つの重要な違いがあります。  
  
- 属性構文を使用して添付プロパティを設定する場合でも、<*型名*>.<*プロパティ名*> の組み合わせを使用できます。 属性構文でプロパティ名を修飾する必要があるのは、添付プロパティの場合だけです。  
  
- プロパティ要素構文を添付プロパティに対して使用することもできます。 ただし、一般的なプロパティ要素構文で指定する <*型名*> は、プロパティ要素が含まれるオブジェクト要素です。 添付プロパティを参照している場合の <*型名*> は、添付プロパティが定義されているクラスであり、それを含んでいるオブジェクト要素ではありません。  
  
<a name="attached_events"></a>
## <a name="attached-events"></a>アタッチされるイベント  
 添付イベントは、XAML で導入されたもう 1 つのプログラミング概念であり、特定の型でイベントを定義しながら、任意のオブジェクト要素にハンドラーを添付できます。 WOF の実装では、多くの場合、添付イベントが定義される型は、サービスが定義されている静的な型であり、それらの添付イベントは、サービスを公開する型のルーティング イベント エイリアスによって公開されることがあります。 添付イベントのハンドラーは、属性の構文によって指定されます。 添付イベントと同様に、属性構文も添付イベントで <*型名*>.<*イベント名*> を使用できるように拡張されています。ここで、<*型名*> は添付イベントのインフラストラクチャに対して `Add` および `Remove` イベント ハンドラー アクセサーを提供するクラスであり、<*イベント名*> はイベントの名前です。  
  
<a name="anatomy_of_a_xaml_page_root_element"></a>
## <a name="anatomy-of-a-xaml-root-element"></a>XAML ルート要素の構造  
 次の表は、一般的な XAML ルート要素の内容です。ルート要素の特定の属性が示されています。  
  
|||  
|-|-|  
|`<Page`|ルート要素のオブジェクト要素の開始|  
|`xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`|既定の ([!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]) XAML 名前空間|  
|`xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`|XAML 言語の XAML 名前空間|  
|`x:Class="ExampleNamespace.ExampleCode"`|部分クラスに対して定義されているコードビハインドにマークアップを接続する部分クラスの宣言|  
|`>`|ルートのオブジェクト要素の終了。 要素に子要素が含まれているため、オブジェクトはまだ閉じられません|  
  
<a name="optional_and_nonrecommended_xaml_usages"></a>
## <a name="optional-and-nonrecommended-xaml-usages"></a>XAML のオプションの使用方法と推奨されない使用方法  
 以下のセクションで説明する XAML の使用方法は、XAML プロセッサによって技術的にはサポートされていますが、冗長さや他の審美的問題が発生し、XAML ソースが含まれるアプリケーションを開発するときに、ユーザーが XAML ファイルを読みにくくなります。  
  
### <a name="optional-property-element-usages"></a>プロパティ要素のオプションの使用方法  
 プロパティ要素のオプションの使用方法には、XAML プロセッサによって暗黙的に考慮される要素コンテンツ プロパティの明示的な記述が含まれます。 たとえば、<xref:System.Windows.Controls.Menu> のコンテンツを宣言する場合、XAML プロセッサの暗黙の動作 (<xref:System.Windows.Controls.Menu> のすべての子要素は <xref:System.Windows.Controls.MenuItem> である必要があり、<xref:System.Windows.Controls.ItemsControl.Items%2A> コレクションに配置される) を使用する代わりに、<xref:System.Windows.Controls.Menu> の <xref:System.Windows.Controls.ItemsControl.Items%2A> コレクションを `<Menu.Items>` プロパティ要素タグとして明示的に宣言し、各 <xref:System.Windows.Controls.MenuItem> を `<Menu.Items>` 内に配置することができます。 このオプションの使用方法は、場合によっては、マークアップで表されるオブジェクト構造を視覚的に明確にするのに、役立つことがあります。 または、場合によっては、プロパティ要素を明示的に使用すると、属性値内の入れ子になったマークアップ拡張のように、技術的には機能するものの、視覚的にはわかりにくいマークアップを回避できます。  
  
### <a name="full-typenamemembername-qualified-attributes"></a>typeName.memberName の完全修飾属性  
 属性の <*型名*>.<*メンバー名*> の形式は、実際には単なるルーティング イベントのケースより汎用的に機能します。 ただし、マークアップのスタイルと読みやすさだけが理由の場合は、他の状況では、その形式は過剰であり、回避する必要があります。 次の例の <xref:System.Windows.Controls.Control.Background%2A> 属性に対する 3 つの参照は、まったく同じになります。  
  
 [!code-xaml[XAMLOvwSupport#TypeNameProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenameprop)]  
  
 `Button.Background` は、<xref:System.Windows.Controls.Button> でのそのプロパティに対する修飾された参照が正常であり (<xref:System.Windows.Controls.Control.Background%2A> は Control から継承されています)、<xref:System.Windows.Controls.Button> はオブジェクト要素または基底クラスのクラスであるため、機能します。 `Control.Background` は、<xref:System.Windows.Controls.Control> クラスで実際に <xref:System.Windows.Controls.Control.Background%2A> が定義されていて、<xref:System.Windows.Controls.Control> は <xref:System.Windows.Controls.Button> 基底クラスであるため、機能します。  
  
 ただし、その次の <*型名*>.<*メンバー名*> の形式の例は機能せず、そのため次のようにコメントされています。  
  
 [!code-xaml[XAMLOvwSupport#TypeNameBadProp](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#typenamebadprop)]  
  
 <xref:System.Windows.Controls.Label> は <xref:System.Windows.Controls.Control> のもう 1 つの派生クラスであり、<xref:System.Windows.Controls.Label> オブジェクト要素内で `Label.Background` を指定してあれば、この使用方法は動作したはずです。 しかし、<xref:System.Windows.Controls.Label> は <xref:System.Windows.Controls.Button> のクラスまたは基底クラスではないため、指定された XAML プロセッサの動作では、`Label.Background` は添付プロパティとして処理されます。 `Label.Background` は使用可能な添付プロパティではないため、この使用方法は失敗します。  
  
### <a name="basetypenamemembername-property-elements"></a>baseTypeName.memberName プロパティ要素  
 属性構文に対して <*型名*>.<*メンバー名*> の形式が動作するのと同じように、プロパティ要素構文に対しては <*基底型名*>.<*メンバー名*> という構文が機能します。 たとえば、次のような構文は機能します。  
  
 [!code-xaml[XAMLOvwSupport#GoofyPE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#goofype)]  
  
 ここでは、プロパティ要素は `Button` に含まれていますが、`Control.Background` として指定されています。  
  
 ただし、属性に対する <*型名*>.<*メンバー名*> の形式と同じように、<*基底型名*>.<*メンバー名*> はマークアップのスタイルとして不適切であるため、回避する必要があります。  
  
## <a name="see-also"></a>関連項目

- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [XAML 名前空間 (x:) 言語機能](../../../desktop-wpf/xaml-services/namespace-language-features.md)
- [WPF XAML 拡張機能](wpf-xaml-extensions.md)
- [依存関係プロパティの概要](dependency-properties-overview.md)
- [TypeConverters および XAML](typeconverters-and-xaml.md)
- [WPF における XAML とカスタム クラス](xaml-and-custom-classes-for-wpf.md)
