---
title: XAML 概要
description: .NET Core の Windows Presentation Foundation (WPF) によって XAML 言語がどのように構造化および実装されるかについて説明します。
author: adegeo
ms.date: 08/08/2019
ms.author: adegeo
dev_langs:
- csharp
- vb
helpviewer_keywords:
- user interfaces [XAML]
- classes [XAML]
- root element [XAML]
- XAML [WPF], about XAML
- base classes [XAML]
- routed events [WPF]
- code-behind files [WPF], XAML
- collection properties [XAML]
- events [XAML]
- property element [XAML]
- content models [XAML]
- Extensible Application Markup Language (see XAML)
- attribute syntax [XAML]
ms.openlocfilehash: 4ccf107bd56be33d9b195d97ae5edf1a6b85117f
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325699"
---
# <a name="xaml-overview-in-wpf"></a>WPF の XAML の概要

この記事では、XAML 言語の機能について説明し、XAML を使用して Windows Presentation Foundation (WPF) アプリを作成する方法を示します。 この記事では特に、WPF によって実装される XAML について説明します。 XAML 自体は、WPF よりも包括的な言語の概念です。

[!INCLUDE [desktop guide under construction](../../../includes/desktop-guide-preview-note.md)]

## <a name="what-is-xaml"></a>XAML とは

XAML は宣言型マークアップ言語です。 XAML は .NET Core プログラミング モデルに適用されるので、.NET Core アプリの UI を簡単に作成できます。 表示される UI 要素を宣言型 XAML マークアップで作成し、部分クラス定義を通じてマークアップに結合される分離コード ファイルを使用して、UI 定義をランタイム ロジックから分離させることができます。 XAML は、アセンブリで定義される特定のバッキング型のセットにおけるオブジェクトのインスタンス化を直接表します。 これは、バッキング型システムへのこのような直接の結びつきのない一般的にインタープリタ型言語である、他のほとんどのマークアップ言語とは異なります。 XAML を使用すると、別々の関係者が異なるツールを使用してアプリの UI やロジックを扱うことができるワークフローが可能になります。

XAML ファイルは、テキストとして表された場合、通常 `.xaml` 拡張子を持つ XML ファイルです。 ファイルは任意の XML エンコードでエンコードできますが、UTF-8 としてエンコードするのが一般的です。

次の例は、UI の一部としてボタンを作成する方法を示しています。 この例は、XAML が一般的な UI プログラミング メタファーを表す方法を簡単に紹介することを目的としています (完全なサンプルではありません)。

[!code-xaml[XAMLOvwSupport#DirtSimple](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]

## <a name="xaml-syntax-in-brief"></a>XAML 構文の概要

次のセクションでは、XAML 構文の基本的な形式について説明し、簡潔なマークアップの例を示します。 これらのセクションは、各構文形式に関する完全な情報 (これらがバッキング型システムでどのように表されるかなど) を提供するものではありません。 XAML 構文の詳細については、「[XAML 構文の詳細](../../framework/wpf/advanced/xaml-syntax-in-detail.md)」を参照してください。

次のいくつかのセクションに含まれる内容の大部分は、XML 言語になじみがある方には初歩的なものになります。 これは、XAML の基本的な設計原則の 1 つによる結果です。 XAML 言語では独自の概念が定義されていますが、これらの概念は XML 言語およびマークアップ形式内で作用します。

### <a name="xaml-object-elements"></a>XAML オブジェクト要素

オブジェクト要素は、通常、型のインスタンスを宣言します。 この型は、言語として XAML を使用するテクノロジによって参照されるアセンブリ内で定義されます。

オブジェクト要素の構文は必ず、始め山かっこ (`<`) で開始します。 この後に、インスタンスを作成する型の名前が続きます。 (この名前には、後で説明する概念であるプレフィックスを含めることができます)。この後、必要に応じて、オブジェクト要素の属性を宣言できます。 オブジェクト要素タグを完了するには、終わり山かっこ (`>`) で終了します。 代わりに、スラッシュと終わり山かっこを続けて入力 (`/>`) してタグを完了することで、コンテンツのない自己終了形式を使用することもできます。 たとえば、前に示したマークアップ スニペットをもう一度見てください。

[!code-xaml[XAMLOvwSupport#DirtSimple](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#dirtsimple)]

これは、2 つのオブジェクト要素を指定しています。`<StackPanel>` (コンテンツを含み、後に終了タグ) と `<Button .../>` (複数の属性を持つ自己終了形式) です。 オブジェクト要素 `StackPanel` および `Button` はそれぞれ、WPF によって定義されかつ WPF アセンブリの一部であるクラスの名前にマップされます。 オブジェクト要素タグを指定する場合は、基になる型の新しいインスタンスを作成するための XAML 処理の命令を作成します。 各インスタンスは、XAML の解析および読み込み時に基になる型のパラメーターなしのコンストラクターを呼び出すことによって作成されます。

### <a name="attribute-syntax-properties"></a>属性構文 (プロパティ)

オブジェクトのプロパティは、多くの場合、オブジェクト要素の属性として表現できます。 属性構文では、設定するオブジェクト プロパティの名前を指定し、その後に代入演算子 (=) を付けます。 属性の値は、常に引用符で囲まれた文字列として指定されます。

属性構文は、最も簡素化されたプロパティ設定の構文であり、過去にマークアップ言語を使用したことのある開発者が最も直感的に使用できる構文です。 たとえば、次のマークアップは、`Content` として指定された表示テキストに加えて、赤色のテキストと青色の背景が設定されたボタンを作成します。

[!code-xaml[XAMLOvwSupport#BlueRedButton](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbutton)]

### <a name="property-element-syntax"></a>プロパティ要素構文

オブジェクト要素の一部のプロパティでは、属性構文は使用できません。これは、プロパティ値を指定するために必要なオブジェクトまたは情報を、属性構文の引用符および文字列制限内で適切に表現できないためです。 このような場合は、プロパティ要素構文として知られる別の構文を使用できます。

プロパティ要素の開始タグの構文は `<TypeName.PropertyName>` です。 通常、そのタグの内容は、プロパティがその値として受け取る型のオブジェクト要素です。 内容を指定した後は、終了タグでプロパティ要素を閉じる必要があります。 終了タグの構文は `</TypeName.PropertyName>` です。

属性構文を使用できる場合は、通常、属性構文を使用する方が便利であり、よりコンパクトなマークアップが可能になりますが、これは多くの場合、技術的な制限ではなく、スタイルの問題にすぎません。 次の例では、前の属性構文の例で設定されているものと同じプロパティを示していますが、今回は `Button` のすべてのプロパティにプロパティ要素構文を使用しています。

[!code-xaml[XAMLOvwSupport#BlueRedButtonPE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/Page1.xaml#blueredbuttonpe)]

### <a name="collection-syntax"></a>コレクション構文

XAML 言語には、より人間が読みやすいマークアップを生成するための最適化がいくつか含まれています。 このような最適化の 1 つは、特定のプロパティがコレクション型を受け取る場合、そのプロパティの値内の子要素としてマークアップで宣言する項目がコレクションの一部になるということです。 この場合、子オブジェクト要素のコレクションは、コレクション プロパティに設定される値です。

次の例は、<xref:System.Windows.Media.GradientBrush.GradientStops%2A> プロパティの値を設定するためのコレクション構文を示しています。

```xaml
<LinearGradientBrush>
  <LinearGradientBrush.GradientStops>
    <!-- no explicit new GradientStopCollection, parser knows how to find or create -->
    <GradientStop Offset="0.0" Color="Red" />
    <GradientStop Offset="1.0" Color="Blue" />
  </LinearGradientBrush.GradientStops>
</LinearGradientBrush>
```

### <a name="xaml-content-properties"></a>XAML コンテンツのプロパティ

XAML では言語機能が指定され、これにより、クラスはそのプロパティの 1 つだけを XAML "_コンテンツ_" プロパティに指定できます。 そのオブジェクト要素の子要素は、そのコンテンツ プロパティの値を設定するために使用されます。 つまり、そのコンテンツ プロパティを一意にするために、XAML マークアップでそのプロパティを設定するときにプロパティ要素を省略し、マークアップ内でより可視的な親/子メタファーを生成することができます。

たとえば、<xref:System.Windows.Controls.Border> で <xref:System.Windows.Controls.Decorator.Child%2A> の "_コンテンツ_" プロパティを指定します。 次の 2 つの <xref:System.Windows.Controls.Border> 要素は、同一に扱われます。 1 つ目は、コンテンツ プロパティ構文を利用して、`Border.Child` プロパティ要素を省略しています。 2 つ目は `Border.Child` を明示的に示しています。

```xaml
<Border>
  <TextBox Width="300"/>
</Border>
<!--explicit equivalent-->
<Border>
  <Border.Child>
    <TextBox Width="300"/>
  </Border.Child>
</Border>
```

XAML 言語の規則として、XAML コンテンツ プロパティの値は、そのオブジェクト要素の他のプロパティ要素の完全に前または完全に後のいずれかに指定する必要があります。 たとえば、次のマークアップはコンパイルされません。

```xaml
<Button>I am a
  <Button.Background>Blue</Button.Background>
  blue button</Button>
```

XAML 構文の詳細については、「[XAML 構文の詳細](../../framework/wpf/advanced/xaml-syntax-in-detail.md)」を参照してください。

### <a name="text-content"></a>テキスト コンテンツ

少数の XAML 要素では、テキストをそのコンテンツとして直接処理できます。 これを有効にするには、次のいずれかのケースが満たされている必要があります。

- クラスでコンテンツ プロパティを宣言する必要があり、そのコンテンツ プロパティは文字列に割り当て可能な型である必要があります (型は <xref:System.Object> である場合もあります)。 たとえば、任意の <xref:System.Windows.Controls.ContentControl> がそのコンテンツ プロパティとして <xref:System.Windows.Controls.ContentControl.Content%2A> を使用し、それが型 <xref:System.Object> である場合、これは <xref:System.Windows.Controls.Button> などの <xref:System.Windows.Controls.ContentControl> で次の使用法をサポートします: `<Button>Hello</Button>`。

- 型で型コンバーターを宣言する必要があります。この場合、テキスト コンテンツは、その型コンバーターの初期化テキストとして使用されます。 たとえば、`<Brush>Blue</Brush>` は `Blue` のコンテンツ値をブラシに変換します。 このケースは、実際にはあまり一般的ではありません。

- 型は、既知の XAML 言語プリミティブである必要があります。

### <a name="content-properties-and-collection-syntax-combined"></a>コンテンツ プロパティとコレクション構文の組み合わせ

次の例について考えます。

```xaml
<StackPanel>
  <Button>First Button</Button>
  <Button>Second Button</Button>
</StackPanel>
```

ここでは、各 <xref:System.Windows.Controls.Button> は <xref:System.Windows.Controls.StackPanel> の子要素です。 これは、2 つの異なる理由から 2 つのタグを省略している、簡素化された直感的なマークアップです。

- **省略された StackPanel.Children プロパティ要素:** <xref:System.Windows.Controls.StackPanel> は <xref:System.Windows.Controls.Panel> から派生します。 <xref:System.Windows.Controls.Panel> で <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=nameWithType> をその XAML コンテンツ プロパティとして定義します。

- **省略された UIElementCollection オブジェクト要素:** <xref:System.Windows.Controls.Panel.Children%2A?displayProperty=nameWithType> プロパティは、<xref:System.Collections.IList> を実装する型 <xref:System.Windows.Controls.UIElementCollection> を取ります。 コレクションの要素タグは、<xref:System.Collections.IList> などのコレクションの処理に関する XAML ルールに基づいて省略できます。 (この場合、<xref:System.Windows.Controls.UIElementCollection> はパラメーターなしのコンストラクターを公開しないため、実際にはインスタンス化できません。そのため、<xref:System.Windows.Controls.UIElementCollection> オブジェクト要素はコメントアウトされて示されています。)

```xaml
<StackPanel>
  <StackPanel.Children>
    <!--<UIElementCollection>-->
    <Button>First Button</Button>
    <Button>Second Button</Button>
    <!--</UIElementCollection>-->
  </StackPanel.Children>
</StackPanel>
```

### <a name="attribute-syntax-events"></a>属性構文 (イベント)

属性構文は、プロパティではなくイベントであるメンバーにも使用できます。 この場合、属性の名前はイベントの名前です。 XAML のイベントの WPF 実装では、属性の値は、そのイベントのデリゲートを実装するハンドラーの名前です。 たとえば、次のマークアップは、マークアップで作成された <xref:System.Windows.Controls.Button> に <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントのハンドラーを割り当てます。

[!code-xaml[XAMLOvwSupport#ButtonWithCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]

WPF のイベントおよび XAML には、属性構文のこの例以外にも多くのものがあります。 たとえば、ここで参照されている `ClickHandler` は何を表し、どのように定義されているのか疑問に思うかもしれません。 これについては、この記事の後半の「[イベントと XAML コードビハインド](#events-and-xaml-code-behind)」セクションで説明します。

## <a name="case-and-white-space-in-xaml"></a>XAML の大文字と小文字の区別と空白

一般に、XAML では大文字と小文字が区別されます。 バッキング型を解決するために、WPF XAML では、CLR で大文字と小文字が区別されるのと同じ規則によって大文字と小文字を区別します。 オブジェクト要素、プロパティ要素、および属性名はすべて、アセンブリ内の基になる型または型のメンバーと名前で比較されるときに、大文字と小文字の区別を使用して指定する必要があります。 XAML 言語のキーワードとプリミティブでも、大文字と小文字が区別されます。 値の大文字と小文字は、必ずしも区別されるとは限りません。 値の大文字と小文字が区別されるかどうかは、値を受け取るプロパティに関連付けられている型コンバーターの動作、またはプロパティ値の型によって異なります。 たとえば、<xref:System.Boolean> 型を受け取るプロパティは、`true` または `True` を同等の値として受け取ることができますが、これは、<xref:System.Boolean> への文字列のネイティブ WPF XAML パーサーの型変換で、これらが同等として既に許可されているためです。

WPF XAML プロセッサおよびシリアライザーは、すべての重要でない空白を無視または削除し、意味のある空白をすべて正規化します。 これは、XAML 仕様の既定の空白に対する動作の推奨事項と一致します。 この動作が重要であるのは、XAML コンテンツ プロパティ内で文字列を指定するときのみです。 簡単に言うと、XAML は空白、改行、およびタブの各文字を空白に変換し、隣接する文字列のいずれかの端で 1 つの空白を保持します (見つかった場合)。 XAML の空白の処理に関する完全な説明については、この記事では扱いません。 詳細については、「[XAML での空白の処理](../xaml-services/white-space-processing.md)」を参照してください。

## <a name="markup-extensions"></a>マークアップ拡張機能

マークアップ拡張は、XAML 言語の概念です。 属性構文の値を指定するために使用する場合、中かっこ (`{` と `}`) は、マークアップ拡張の使用を示します。 この使用法は、リテラル文字列または文字列変換可能な値のいずれかとしての属性値の一般的な扱いを回避するように、XAML 処理に指示します。

WPF アプリのプログラミングで使用される最も一般的なマークアップ拡張は、データ バインディング式に使用される [`Binding`](../../framework/wpf/advanced/binding-markup-extension.md) と、リソース参照の [`StaticResource`](../../framework/wpf/advanced/staticresource-markup-extension.md) および [`DynamicResource`](../../framework/wpf/advanced/dynamicresource-markup-extension.md) です。 マークアップ拡張を使用すると、プロパティが一般に属性構文をサポートしていない場合でも、属性構文を使用してそのプロパティの値を指定できます。 マークアップ拡張では、多くの場合、中間式の型を使用して、値の保留や、実行時にのみ存在する他のオブジェクトの参照などの機能が有効化されます。

たとえば、次のマークアップは、属性構文を使用して <xref:System.Windows.FrameworkElement.Style%2A> プロパティの値を設定します。 <xref:System.Windows.FrameworkElement.Style%2A> プロパティは、既定では属性構文の文字列によってインスタンス化できなかった <xref:System.Windows.Style> クラスのインスタンスを受け取ります。 ただし、この場合、属性は特定のマークアップ拡張 `StaticResource` を参照します。 このマークアップ拡張が処理されると、リソース ディクショナリのキー付きリソースとして前にインスタンス化されていたスタイルへの参照が返されます。

[!code-xaml[FEResourceSH_snip#XAMLOvwShortResources](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources)]
[!code-xaml[FEResourceSH_snip#XAMLOvwShortResources2](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources2)]
[!code-xaml[FEResourceSH_snip#XAMLOvwShortResources3](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResourceSH_snip/CS/page1.xaml#xamlovwshortresources3)]

WPF で特別に実装されている XAML のすべてのマークアップ拡張のリファレンス一覧については、「[WPF XAML 拡張機能](../../framework/wpf/advanced/wpf-xaml-extensions.md)」を参照してください。 System.Xaml によって定義され、.NET Core XAML の実装でより広範に使用できるマークアップ拡張のリファレンス一覧については、「[XAML 名前空間 (x:)言語機能](../xaml-services/namespace-language-features.md)」を参照してください。 マークアップ拡張の概念の詳細については、 「[マークアップ拡張機能と WPF XAML](../../framework/wpf/advanced/markup-extensions-and-wpf-xaml.md)」を参照してください。

## <a name="type-converters"></a>型コンバーター

「[XAML 構文の概要](#xaml-syntax-in-brief)」セクションでは、属性値を文字列によって設定できる必要があると記載しました。 文字列を他のオブジェクト型またはプリミティブ値に変換する方法の基本的でネイティブな処理は、<xref:System.DateTime> や <xref:System.Uri> などの特定の型のネイティブ処理に加えて、<xref:System.String> 型自体に基づきます。 ただし、WPF の型やそれらの型のメンバーの多くは、より複雑なオブジェクト型のインスタンスを文字列および属性として指定できるように、基本的な文字列属性処理動作を拡張します。

<xref:System.Windows.Thickness> 構造体は、XAML の使用に対して型変換が有効になっている型の例です。 <xref:System.Windows.Thickness> は、入れ子になった四角形内の測定値を示し、<xref:System.Windows.FrameworkElement.Margin%2A> などのプロパティの値として使用されます。 型コンバーターを <xref:System.Windows.Thickness> に配置すると、<xref:System.Windows.Thickness> を使用するすべてのプロパティが属性として指定できるため、それらを XAML で簡単に指定できます。 次の例では、型変換と属性構文を使用して、<xref:System.Windows.FrameworkElement.Margin%2A> の値を指定しています。

[!code-xaml[XAMLOvwSupport#MarginTCE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#margintce)]

前の属性構文の例は、次のより詳細な構文の例と同じです。ここで、<xref:System.Windows.FrameworkElement.Margin%2A> は代わりに、<xref:System.Windows.Thickness> オブジェクト要素を含むプロパティ要素構文を通じて設定されています。 <xref:System.Windows.Thickness> の 4 つの主なプロパティは、新しいインスタンスの属性として設定されています。

[!code-xaml[XAMLOvwSupport#MarginVerbose](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#marginverbose)]

> [!NOTE]
> 型自体にパラメーターなしのコンストラクターがないため、サブクラスを伴わずにその型にプロパティを設定する唯一のパブリックな方法が型変換であるオブジェクトの数も限られています。 たとえば <xref:System.Windows.Input.Cursor> です。

型変換の詳細については、「[TypeConverters および XAML](../../framework/wpf/advanced/typeconverters-and-xaml.md)」を参照してください。

## <a name="xaml-root-elements-and-xaml-namespaces"></a>XAML ルート要素と XAML 名前空間

XAML ファイルは、整形式の XML ファイルであると同時に有効な XAML ファイルであるためには、ルート要素を 1 つだけ持つ必要があります。 一般的な WPF のシナリオでは、WPF アプリ モデルで顕著な意味を持つルート要素を使用します (たとえば、ページの場合は <xref:System.Windows.Window> や <xref:System.Windows.Controls.Page>、外部辞書の場合は <xref:System.Windows.ResourceDictionary>、アプリ定義の場合は <xref:System.Windows.Application>)。 次の例は、<xref:System.Windows.Controls.Page> のルート要素を使用して、WPF ページの一般的な XAML ファイルのルート要素を示しています。

[!code-xaml[XAMLOvwSupport#RootOnly](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly)]
[!code-xaml[XAMLOvwSupport#RootOnly2](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page2.xaml#rootonly2)]

また、ルート要素には、`xmlns` および `xmlns:x` 属性が含まれます。 これらの属性は XAML プロセッサに対して、マークアップが要素として参照するバッキング型の型定義を含む XAML 名前空間を示します。 `xmlns` 属性は、具体的に既定の XAML 名前空間を示します。 既定の XAML 名前空間内では、マークアップ内のオブジェクト要素をプレフィックスなしで指定できます。 ほとんどの WPF アプリ シナリオと、SDK の WPF セクションに示されているほとんどすべての例では、既定の XAML 名前空間は WPF 名前空間 `http://schemas.microsoft.com/winfx/2006/xaml/presentation` にマップされます。 `xmlns:x` 属性は、XAML 言語の名前空間 `http://schemas.microsoft.com/winfx/2006/xaml` をマップする追加の XAML 名前空間を示します。

名前スコープの使用とマッピングに対するスコープを定義する `xmlns` のこの使用法は、XML 1.0 仕様と一致しています。 XAML 名前スコープが XML 名前スコープと異なるのは、XAML 名前スコープが、型の解決および XAML の解析に関して、名前スコープの要素がどのように型によってサポートされるかについても何かを示すという点だけです。

`xmlns` 属性は、各 XAML ファイルのルート要素でのみ厳密に必要です。 `xmlns` 定義は、ルート要素のすべての子孫要素に適用されます (この動作も、`xmlns` の XML 1.0 仕様と同じです)。また、`xmlns` 属性はルートの下の他の要素でも許可され、定義している要素の子孫要素に適用されます。 ただし、XAML 名前空間を頻繁に定義または再定義すると、XAML マークアップ スタイルが読みにくくなる可能性があります。

XAML プロセッサの WPF 実装には、WPF コア アセンブリを認識するインフラストラクチャが含まれています。 WPF コア アセンブリには、既定の XAML 名前空間への WPF マッピングをサポートする型が含まれていることがわかっています。 これは、プロジェクト ビルド ファイルの一部である構成と、WPF ビルドおよびプロジェクト システムによって有効になります。 そのため、WPF アセンブリからの XAML 要素を参照するために必要なことは、既定の XAML 名前空間を既定の `xmlns` として宣言することだけです。

### <a name="the-x-prefix"></a>x: プレフィックス

前のルート要素の例では、XAML の言語コンストラクトをサポートする専用の XAML 名前空間である XAML 名前空間 `http://schemas.microsoft.com/winfx/2006/xaml` をマップするために、プレフィックス `x:` が使用されていました。 この `x:` プレフィックスは、プロジェクトのテンプレート、例、およびこの SDK 全体のドキュメントで、この XAML 名前空間をマップするために使用されています。 XAML 言語の XAML 名前空間には、XAML で頻繁に使用するプログラミング コンストラクトがいくつか含まれています。 次に、ユーザーが使用する最も一般的な `x:` プレフィックスのプログラミング コンストラクトの一覧を示します。

- [x:Key](../xaml-services/xkey-directive.md):<xref:System.Windows.ResourceDictionary> (または、他のフレームワークの同様のディクショナリの概念) のリソースごとに一意のキーを設定します。 `x:Key` は、一般的な WPF アプリのマークアップに見られる `x:` の使用の 90% を占めます。

- [x:Class](../xaml-services/xclass-directive.md):XAML ページにコードビハインドを提供するクラスの CLR 名前空間とクラス名を指定します。 WPF プログラミング モデルごとにコードビハインドをサポートするには、このようなクラスが必要です。そのため、リソースがない場合でも、ほとんどの場合、`x:` がマップされていることがわかります。

- [x:Name](../xaml-services/xname-directive.md):オブジェクト要素が処理された後にランタイム コードに存在するインスタンスのランタイム オブジェクト名を指定します。 一般に、[x:Name](../xaml-services/xname-directive.md) には、WPF で定義された同等のプロパティをよく使用します。 このようなプロパティは、特に CLR バッキング プロパティにマップされるため、初期化された XAML から名前付き要素を見つけるためにランタイム コードをよく使用するアプリのプログラミングにはより便利です。 そのようなプロパティの中で最も一般的なものは <xref:System.Windows.FrameworkElement.Name%2A?displayProperty=nameWithType> です。 [x:Name](../xaml-services/xname-directive.md) は、同等の WPF フレームワーク レベルの <xref:System.Windows.FrameworkElement.Name%2A> プロパティが特定の型でサポートされていない場合でも使用できます。 これは、特定のアニメーション シナリオで発生します。

- [x:Static](../xaml-services/xstatic-markup-extension.md):本来なら XAML と互換性のあるプロパティではない静的な値を返す参照を有効にします。

- [x:Type](../xaml-services/xtype-markup-extension.md):型名に基づいて <xref:System.Type> 参照を作成します。 これは、<xref:System.Windows.Style.TargetType%2A?displayProperty=nameWithType> などの <xref:System.Type> を受け取る属性を指定するために使用されますが、[x:Type](../xaml-services/xtype-markup-extension.md) マークアップ拡張の使用がオプションであるように、プロパティに文字列から <xref:System.Type> へのネイティブ変換が含まれることがよくあります。

`x:` プレフィックス/XAML 名前空間には、あまり一般的ではない追加のプログラミング コンストラクトがあります。 詳細については、「[XAML 名前空間 (x:)言語機能](../xaml-services/namespace-language-features.md)」を参照してください。

## <a name="custom-prefixes-and-custom-types-in-xaml"></a>XAML のカスタム プレフィックスとカスタム型

独自のカスタム アセンブリの場合、または **PresentationCore**、**PresentationFramework** および **WindowsBase** の WPF コア以外のアセンブリの場合は、カスタム `xmlns` マッピングの一部としてアセンブリを指定できます。 その後、試みている XAML の使用をサポートするように型が正しく実装されていれば、XAML でそのアセンブリから型を参照することができます。

次に、カスタム プレフィックスが XAML マークアップでどのように機能するかの基本的な例を示します。 プレフィックス `custom` は、ルート要素タグで定義され、特定のアセンブリ (パッケージ化されてアプリで使用可能なもの) にマップされます。 このアセンブリには `NumericUpDown` 型が含まれています。これは、一般的な XAML の使用をサポートするために実装され、WPF XAML コンテンツ モデル内のこの特定のポイントでその挿入を許可するクラスの継承を使用します。 この `NumericUpDown` コントロールのインスタンスは、プレフィックスを使用してオブジェクト要素として宣言されます。これにより、XAML パーサーは、どの XAML 名前空間に型が含まれているか、したがって型定義を含むバッキング アセンブリがどこにあるかを認識します。

```xaml
<Page
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:custom="clr-namespace:NumericUpDownCustomControl;assembly=CustomLibrary"
    >
  <StackPanel Name="LayoutRoot">
    <custom:NumericUpDown Name="numericCtrl1" Width="100" Height="60"/>
...
  </StackPanel>
</Page>
```

XAML のカスタム型の詳細については、「[WPF における XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)」を参照してください。

アセンブリ内の XML 名前空間とコード名前空間がどのように関連しているかの詳細については、「[XAML 名前空間および WPF XAML の名前空間の割り当て](../../framework/wpf/advanced/xaml-namespaces-and-namespace-mapping-for-wpf-xaml.md)」を参照してください。

## <a name="events-and-xaml-code-behind"></a>イベントと XAML コードビハインド

ほとんどの WPF アプリは、XAML マークアップとコードビハインドの両方で構成されています。 プロジェクト内で、XAML は `.xaml` ファイルとして記述され、Microsoft Visual Basic や C# などの CLR 言語が分離コード ファイルの記述に使用されます。 XAML ファイルが WPF プログラミングおよびアプリケーションのモデルの一部としてマークアップ コンパイルされている場合、XAML ファイルの XAML 分離コード ファイルの場所は、XAML のルート要素の `x:Class` 属性として名前空間とクラスを指定することによって識別されます。

ここまでの例でいくつかのボタンを確認しましたが、これらのボタンのいずれにも論理的な動作はまだ関連付けられていませんでした。 オブジェクト要素の動作を追加するための主要なアプリケーション レベルの方法は、要素クラスの既存のイベントを使用し、実行時にそのイベントが発生したときに呼び出されるイベントの特定のハンドラーを記述することです。 イベント名と、使用するハンドラーの名前はマークアップで指定されますが、ハンドラーを実装するコードはコードビハインドで定義されます。

[!code-xaml[XAMLOvwSupport#ButtonWithCodeBehind](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml#buttonwithcodebehind)]

[!code-csharp[XAMLOvwSupport#ButtonWithCodeBehindHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page3.xaml.cs#buttonwithcodebehindhandler)]
[!code-vb[XAMLOvwSupport#ButtonWithCodeBehindHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#buttonwithcodebehindhandler)]

分離コード ファイルは CLR 名前空間 `ExampleNamespace` を使用し、その名前空間内の部分クラスとして `ExamplePage` を宣言していることに注意してください。 これは、`ExampleNamespace`.`ExamplePage` の `x:Class` 属性値と同等です。 これはマークアップ ルートで指定されました。 WPF マークアップ コンパイラは、ルート要素型からクラスを派生させることによって、コンパイルされた XAML ファイルの部分クラスを作成します。 また同じ部分クラスを定義するコードビハインドを指定すると、結果として得られるコードは、コンパイル済みアプリの同じ名前空間とクラス内で結合されます。

WPF でのコードビハインド プログラミングの要件の詳細については、「[WPF でのコードビハインド、イベント ハンドラー、および部分クラスの要件](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md#code-behind-event-handler-and-partial-class-requirements-in-wpf)」を参照してください。

別個の分離コード ファイルを作成したくない場合は、XAML ファイルでコードをインライン化することもできます。 ただし、インライン コードは、かなりの制限がある汎用性の低い手法です。 詳細については、「[WPF における分離コードと XAML](../../framework/wpf/advanced/code-behind-and-xaml-in-wpf.md)」を参照してください。

### <a name="routed-events"></a>ルーティング イベント

WPF の基本となる特有のイベント機能は、ルーティング イベントです。 ルーティング イベントを使用すると、要素がツリー リレーションシップを介して接続されていれば、要素は別の要素によって発生したイベントを処理できます。 XAML 属性を使用してイベント処理を指定する場合、ルーティング イベントは、任意の要素 (この特定のイベントをクラス メンバー テーブルに一覧表示しない要素を含む) に対してリッスンおよび処理することができます。 これは、イベント名属性を所有クラス名で修飾することで実現します。 たとえば、進行中の `StackPanel` / `Button` の例の親 `StackPanel` は、属性値としてハンドラー名を使用して、`StackPanel` オブジェクト要素に属性 `Button.Click` を指定することによって、子要素ボタンの <xref:System.Windows.Controls.Primitives.ButtonBase.Click> イベントのハンドラーを登録できます。 詳細については、「[ルーティング イベントの概要](../../framework/wpf/advanced/routed-events-overview.md)」を参照してください。

## <a name="xaml-named-elements"></a>XAML の名前付き要素

既定では、XAML オブジェクト要素を処理することによってオブジェクト グラフに作成されたオブジェクト インスタンスには、一意識別子もオブジェクト参照もありません。 これに対して、コードでコンストラクターを呼び出す場合は、そのほとんどにおいて、コンストラクターの結果を使用して、作成されたインスタンスに変数を設定するため、後でコード内でインスタンスを参照できます。 マークアップ定義によって作成されたオブジェクトへの標準化されたアクセスを実現するために、XAML では [x:Name 属性](../xaml-services/xname-directive.md)を定義します。 任意のオブジェクト要素に `x:Name` 属性の値を設定できます。 コードビハインドでは、選択した識別子が、作成されたインスタンスを参照するインスタンス変数に相当します。 あらゆる点で、名前付き要素はオブジェクト インスタンスのように機能します (名前がそのインスタンスを参照します)。そして、コードビハインドによってその名前付き要素が参照され、アプリ内での実行時のやり取りを処理することができます。 インスタンスと変数の間のこの接続は、WPF XAML マークアップ コンパイラによって行われます。具体的には、この記事では詳しく説明しない <xref:System.Windows.Markup.IComponentConnector.InitializeComponent%2A> などの機能やパターンに関連しています。

WPF フレームワーク レベルの XAML 要素は、<xref:System.Windows.FrameworkElement.Name%2A> プロパティを継承します。これは、XAML で定義された `x:Name` 属性に相当します。 その他のクラスの中には、一般的に `Name` プロパティとして定義される `x:Name` のプロパティ レベルの同等のものを提供するものもあります。 一般に、選択した要素または型のメンバー テーブルに `Name` プロパティを見つけられない場合は、代わりに `x:Name` を使用します。 `x:Name` の値は、特定のサブシステム、または <xref:System.Windows.FrameworkElement.FindName%2A> などのユーティリティ メソッドのいずれかによって実行時に使用できる XAML 要素に識別子を提供します。

次の例では、<xref:System.Windows.Controls.StackPanel> 要素で <xref:System.Windows.FrameworkElement.Name%2A> を設定します。 次に、その <xref:System.Windows.Controls.StackPanel> 内の <xref:System.Windows.Controls.Button> のハンドラーが、<xref:System.Windows.FrameworkElement.Name%2A> によって設定されたそのインスタンス参照 `buttonContainer` を通じて <xref:System.Windows.Controls.StackPanel> を参照します。

[!code-xaml[XAMLOvwSupport#NamedE](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede)]
[!code-xaml[XAMLOvwSupport#NamedE2](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml#namede2)]

[!code-csharp[XAMLOvwSupport#NameCode](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page7.xaml.cs#namecode)]
[!code-vb[XAMLOvwSupport#NameCode](~/samples/snippets/visualbasic/VS_Snippets_Wpf/XAMLOvwSupport/VisualBasic/Page1.xaml.vb#namecode)]

変数と同じように、インスタンスの XAML 名はスコープの概念によって管理されるので、予測可能な特定のスコープ内で名前が一意になるように強制することができます。 ページを定義する主要なマークアップは、1 つの一意の XAML 名前スコープを示し、XAML 名前スコープの境界はそのページのルート要素です。 ただし、他のマークアップ ソースは、スタイルやスタイル内のテンプレートなど、実行時にページとやり取りすることができ、多くの場合、このようなマークアップ ソースには、ページの XAML 名前スコープと必ずしも接続しない独自の XAML 名前スコープがあります。 `x:Name` および XAML 名前スコープの詳細については、「<xref:System.Windows.FrameworkElement.Name%2A>」、「[x:Name ディレクティブ](../xaml-services/xname-directive.md)」、または「[WPF XAML 名前スコープ](../../framework/wpf/advanced/wpf-xaml-namescopes.md)」を参照してください。

## <a name="attached-properties-and-attached-events"></a>添付プロパティと添付イベント

XAML では、特定のプロパティまたはイベントを、設定されている要素の型の定義にそのプロパティまたはイベントが存在するかどうかに関係なく、任意の要素に指定できるようにする言語機能が指定されます。 この機能のプロパティのバージョンは添付プロパティと呼ばれ、イベントのバージョンは添付イベントと呼ばれます。 概念的には、添付プロパティと添付イベントは、任意の XAML 要素またはオブジェクト インスタンスに設定できるグローバル メンバーと考えることができます。 ただし、その要素またはクラス、あるいはより大規模なインフラストラクチャでは、添付値のバッキング プロパティ ストアがサポートされている必要があります。

XAML の添付プロパティは、通常、属性構文を介して使用されます。 属性構文では、形式 `ownerType.propertyName` で添付プロパティを指定します。

一見すると、これはプロパティ要素の使用法に似ていますが、この場合、指定する `ownerType` は、添付プロパティが設定されるオブジェクト要素とは常に異なる型です。 `ownerType` は、添付プロパティ値を取得または設定するために XAML プロセッサで必要とされるアクセサー メソッドを提供する型です。

添付プロパティの最も一般的なシナリオは、子要素が親要素にプロパティ値を報告できるようにすることです。

次の例は、<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 添付プロパティを示しています。 <xref:System.Windows.Controls.DockPanel> クラスは、<xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> のアクセサーを定義しているため、添付プロパティを所有しています。 また、<xref:System.Windows.Controls.DockPanel> クラスには、その子要素を反復処理して、特に <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> の設定値がないか各要素を検査するロジックが含まれています。 値が検出されると、その値は子要素を配置するためにレイアウト中に使用されます。 <xref:System.Windows.Controls.DockPanel.Dock%2A?displayProperty=nameWithType> 添付プロパティとこの配置機能の使用は、実際には <xref:System.Windows.Controls.DockPanel> クラスの使用のきっかけとなるシナリオです。

[!code-xaml[XAMLOvwSupport#DockAP](~/samples/snippets/csharp/VS_Snippets_Wpf/XAMLOvwSupport/CSharp/page8.xaml#dockap)]

WPF では、添付プロパティのほとんどまたはすべてが依存関係プロパティとしても実装されます。 詳細については、「[添付プロパティの概要](../../framework/wpf/advanced/attached-properties-overview.md)」を参照してください。

添付イベントは、属性構文の同様の `ownerType.eventName` 形式を使用します。 非添付イベントと同様に、XAML の添付イベントの属性値で、イベントが要素で処理されるときに呼び出されるハンドラー メソッドの名前を指定します。 WPF XAML での添付イベントの使用は、あまり一般的ではありません。 詳細については、「[添付イベントの概要](../../framework/wpf/advanced/attached-events-overview.md)」を参照してください。

## <a name="base-types-and-xaml"></a>基本型と XAML

基になる WPF XAML とその XAML 名前空間は、XAML のマークアップ要素に加えて、CLR オブジェクトに対応する型のコレクションです。 ただし、すべてのクラスを要素にマップできるわけではありません。 <xref:System.Windows.Controls.Primitives.ButtonBase> などの抽象クラスや、特定の非抽象基本クラスは、CLR オブジェクト モデルの継承に使用されます。 基底クラス (抽象のものも含む) は、具象 XAML 要素のそれぞれがその階層内の基底クラスからメンバーを継承するので、XAML 開発にとって引き続き重要です。 多くの場合、これらのメンバーには、要素の属性として設定できるプロパティや、処理できるイベントが含まれます。 <xref:System.Windows.FrameworkElement> は、WPF フレームワーク レベルでの WPF の具象基底 UI クラスです。 UI を設計するときは、さまざまなシェイプ、パネル、デコレーター、またはコントロール クラスを使用しますが、これらはすべて <xref:System.Windows.FrameworkElement> から派生します。 関連する基底クラスである <xref:System.Windows.FrameworkContentElement> では、<xref:System.Windows.FrameworkElement> 内の API を意図的にミラー化する API を使用して、フロー レイアウト プレゼンテーションに適したドキュメント指向の要素がサポートされています。 要素レベルの属性と CLR オブジェクト モデルの組み合わせにより、特定の XAML 要素とその基になる型に関係なく、ほとんどの具象 XAML 要素に設定できる一般的なプロパティのセットが提供されます。

## <a name="xaml-security"></a>XAML におけるセキュリティ

XAML は、オブジェクトのインスタンス化と実行を直接表すマークアップ言語です。 そのため、XAML で作成された要素は、生成された同等のコードと同じように、システム リソース (ネットワーク アクセス、ファイル システム IO など) を操作できます。 完全に信頼されたアプリに読み込まれた XAML は、ホスト アプリと同じようにシステム リソースにアクセスできます。

### <a name="code-access-security-cas-in-wpf"></a>WPF におけるコード アクセス セキュリティ (CAS)

**このセクションが該当するのは .NET Framework のみです。 .NET Core の WPF では、CAS をサポートしていません。 詳細については、[コード アクセス セキュリティの相違点](../migration/differences-from-net-framework.md#code-access-security)に関する記事を参照してください。**

.NET Framework の WPF では、コード アクセス セキュリティ (CAS) がサポートされています。 これは、インターネット ゾーンで実行されている WPF コンテンツの実行アクセス許可が制限されていることを意味します。 "Loose XAML" (XAML ビューアーによって読み込み時に解釈される、コンパイルされていない XAML のページ) と XBAP は、通常、このインターネット ゾーンで実行され、同じアクセス許可セットを使用します。 ただし、完全に信頼されたアプリケーションリに読み込まれた XAML は、ホスト アプリケーションと同じようにシステム リソースにアクセスできます。 詳細については、「[WPF 部分信頼セキュリティ](../../framework/wpf/wpf-partial-trust-security.md)」を参照してください。

## <a name="loading-xaml-from-code"></a>コードからの XAML の読み込み

XAML は、すべての UI を定義するために使用できますが、XAML で UI の一部だけを定義することが適切な場合もあります。 この機能を使用すると、部分的なカスタマイズ、情報のローカル ストレージ、XAML を使用したビジネスオブジェクトの提供、または想定される各種シナリオが可能になります。 これらのシナリオにとって重要なのは、<xref:System.Windows.Markup.XamlReader> クラスとその <xref:System.Windows.Markup.XamlReader.Load%2A> メソッドです。 入力は XAML ファイルであり、出力は、そのマークアップから作成されたオブジェクトの実行時ツリーのすべてを表すオブジェクトです。 そして、そのオブジェクトを、アプリに既に存在する別のオブジェクトのプロパティとして挿入できます。 このプロパティが、最終的な表示機能を備え、かつ新しいコンテンツがアプリに追加されたことを実行エンジンに通知する、コンテンツ モデル内の適切なプロパティであれば、XAML に読み込むことで、実行中のアプリのコンテンツを簡単に変更できます。 .NET Framework の場合、この機能は通常、完全に信頼されたアプリケーションでのみ使用できます。これは、実行時にアプリケーションにファイルを読み込むことで、セキュリティ上の明らかな影響が発生するためです。

## <a name="see-also"></a>関連項目

- [XAML 構文の詳細](../../framework/wpf/advanced/xaml-syntax-in-detail.md)
- [WPF における XAML とカスタム クラス](../../framework/wpf/advanced/xaml-and-custom-classes-for-wpf.md)
- [XAML 名前空間 (x:)言語機能](../xaml-services/namespace-language-features.md)
- [WPF XAML 拡張機能](../../framework/wpf/advanced/wpf-xaml-extensions.md)
- [基本要素の概要](../../framework/wpf/advanced/base-elements-overview.md)
- [WPF のツリー](../../framework/wpf/advanced/trees-in-wpf.md)
