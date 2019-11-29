---
title: x:Key ディレクティブ
ms.date: 03/30/2017
f1_keywords:
- xKey
- Key
- x:Key
helpviewer_keywords:
- x:Key attribute [XAML Services]
- Key attribute in XAML [XAML Services]
- XAML [XAML Services], x:Key attribute
ms.assetid: 1985cd45-f197-42d5-b75e-886add64b248
ms.openlocfilehash: 8321a09db31c9f6d2103a252a195fcdbf8da3e66
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283856"
---
# <a name="xkey-directive"></a>x:Key ディレクティブ
XAML で定義されたディクショナリで作成および参照される要素を一意に識別します。 `x:Key` 値を XAML オブジェクトに追加するのは、リソース ディクショナリ (<xref:System.Windows.ResourceDictionary> など) のリソースを識別するための最も一般的な方法です。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用  
  
```xaml  
<object x:Key="stringKeyValue".../>  
-or-  
<object x:Key="{markupExtensionUsage}".../>  
```  
  
## <a name="xaml-attribute-usage-wpf-specific"></a>XAML 属性の使用方法 (WPF 固有)  
  
```xaml  
<object.Resources>  
  <object x:Key="stringKeyValue".../>  
</object.Resources>  
-or-  
<object.Resources>  
  <object x:Key="{markupExtensionUsage}".../>  
</object.Resources>  
```  
  
## <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|`stringKeyValue`|キーとして使用するテキスト文字列。 テキスト文字列は、 [XamlName 文法](xamlname-grammar.md)に準拠している必要があります。|  
|`markupExtensionUsage`|マークアップ拡張機能の区切り記号 {}には、キーとして使用するオブジェクトを提供するマークアップ拡張機能の使用法が含まれます。 「解説」を参照してください。|  
  
## <a name="remarks"></a>コメント  
 `x:Key` は、XAML リソースディクショナリの概念をサポートします。 言語としての XAML ではリソース ディクショナリの実装は定義されていません。特定の UI フレーム ワークによって定義されています。 WPF での XAML リソースディクショナリの実装方法の詳細については、「 [Xaml リソース](../../desktop-wpf/fundamentals/xaml-resources-define.md)」を参照してください。  
  
 XAML 2006 および WPF では、`x:Key` を属性として指定する必要があります。 文字列ではないキーも使用できますが、文字列ではない値を属性形式で提供するためには、マークアップ拡張機能を使用する必要があります。 XAML 2009 を使用している場合は、`x:Key` を要素として指定して、マークアップ拡張機能の中間を必要とせずに、文字列以外のオブジェクト型によってキー指定されたディクショナリを明示的にサポートすることができます。 このトピックの「XAML 2009」セクションを参照してください。 「解説」の残りの部分は、XAML 2006 の実装に特に適用されます。  
  
 `x:Key` の属性値には、 [XamlName 文法](xamlname-grammar.md)で定義されている任意の文字列を指定できます。また、マークアップ拡張機能を通じて評価されるオブジェクトを指定することもできます。 WPF の例については、「WPF の使用上の注意」を参照してください。  
  
 通常、<xref:System.Collections.IDictionary> の実装である親要素の子要素には、そのディクショナリ内の一意のキー値を指定する `x:Key` 属性を含める必要があります。 フレームワークでは、特定の型の `x:Key` を代用するために、エイリアス化されたキー プロパティを実装する場合があります。このようなプロパティを定義する型には、<xref:System.Windows.Markup.DictionaryKeyPropertyAttribute> 属性を設定する必要があります。  
  
 `x:Key` の指定に相当するコードは、基になる <xref:System.Collections.IDictionary> で使用されるキーです。 たとえば、マークアップで適用される WPF のリソースの `x:Key` は、コードでリソースを WPF の `key` に追加する場合、<xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> の <xref:System.Windows.ResourceDictionary> パラメーターの値と同等です。  
  
## <a name="wpf-usage-notes"></a>WPF の使用上の注意  
 通常、WPF の <xref:System.Collections.IDictionary> などの <xref:System.Windows.ResourceDictionary> の実装である親オブジェクトの子オブジェクトには、`x:Key` 属性を含める必要があります。また、キー値は、そのディクショナリ内で一意である必要があります。 ただし、次のように 2 つの重要な例外があります。  
  
- 一部の WPF 型は、ディクショナリの使用に対して暗黙のキーを宣言します。 たとえば、<xref:System.Windows.Style> が設定された <xref:System.Windows.Style.TargetType%2A> や、<xref:System.Windows.DataTemplate> が設定された <xref:System.Windows.DataTemplate.DataType%2A> は、<xref:System.Windows.ResourceDictionary> に格納して、暗黙のキーを使用できます。  
  
- WPF は、マージされたリソース ディクショナリの概念をサポートしています。 キーは、マージされたディクショナリ間で共有できます。また、共有されたキーの動作には、<xref:System.Windows.FrameworkContentElement.FindResource%2A> を使用してアクセスできます。 詳細については、「[Merged Resource Dictionaries](../wpf/advanced/merged-resource-dictionaries.md)」を参照してください。  
  
 通常、WPF XAML の実装およびアプリケーション モデルでは、キーの一意性が XAML マークアップ コンパイラによってチェックされることはありません。 その代わり、`x:Key` 値が指定されていない場合や一意でない場合は、読み込み時に XAML パーサー エラーが発生します。 ただし、Visual Studio で WPF のディクショナリを処理すると、デザインフェーズでこのようなエラーが発生することがよくあります。  
  
 ここに示す構文において、<xref:System.Windows.ResourceDictionary> オブジェクトは WPF XAML プロセッサが <xref:System.Windows.FrameworkElement.Resources%2A> コレクションを取得するためのコレクションを生成する方法を暗黙的に決定することに注意してください。 <xref:System.Windows.ResourceDictionary> は、通常はマークアップで要素として明示的に指定されませんが、わかりやすくするために必要に応じて明示的に指定することもできます (その場合、このオブジェクトは、<xref:System.Windows.FrameworkElement.Resources%2A> プロパティ要素とディクショナリに設定される項目間のコレクション オブジェクト要素になります)。 コレクションオブジェクトがほとんど常にマークアップの暗黙的な要素である理由については、「 [XAML 構文の詳細](../wpf/advanced/xaml-syntax-in-detail.md)」を参照してください。  
  
 WPF XAML 実装では、リソース ディクショナリ キーの処理は、<xref:System.Windows.ResourceKey> 抽象クラスによって定義されます。 ただし、WPF XAML プロセッサは、使用方法に基づいてキーごとに別の基になる拡張型を生成します。 たとえば、<xref:System.Windows.DataTemplate> または任意の派生クラスのキーは個別に処理され、異なる <xref:System.Windows.DataTemplateKey> オブジェクトを生成します。  
  
 基本的な XAML 定義では、キーと名前で異なるディレクティブと言語要素 (`x:Key` と `x:Name`) が使用されます。 また、キーと名前は、それらの概念の WPF 定義およびアプリケーションにより異なる状況において使用されます。 詳細については、「 [WPF XAML 名前スコープ](../wpf/advanced/wpf-xaml-namescopes.md)」を参照してください。  
  
 既に説明したように、キー値はマークアップ拡張機能によって指定され、文字列値以外になる場合があります。 WPF シナリオの例として、`x:Key` の値が[ComponentResourceKey](../wpf/advanced/componentresourcekey-markup-extension.md)であることが挙げられます。 特定のコントロールでは、スタイルを完全に置き換えることなく、そのコントロールの外観と動作の一部に影響を与えるカスタム スタイル リソースの型に対応するスタイル キーが公開されます。 このようなキーの例として、<xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A> が挙げられます。  
  
 WPF のマージされたディクショナリ機能では、キーの一意性およびキーの検索動作について考慮を要する点があります。 詳細については、「[Merged Resource Dictionaries](../wpf/advanced/merged-resource-dictionaries.md)」を参照してください。  
  
## <a name="xaml-2009"></a>XAML 2009  
 XAML 2009 緩和されは、常に属性形式で提供される `x:Key` 制限をします。  
  
 WPF では、XAML 2009 機能を使用できますが、マークアップコンパイルされていない XAML にのみ使用できます。 WPF 向けにマークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 のキーワードと機能をサポートしていません。  
  
 XAML 2009 では、次の使用方法を使用して `x:Key` 要素を指定できます。  
  
### <a name="xaml-element-usage-xaml-2009-only"></a>XAML 要素の使用 (XAML 2009 のみ)  
  
```xaml  
<object>  
  <x:Key>  
keyObject  
  </x:Key>  
...  
</object>  
```  
  
### <a name="xaml-values"></a>XAML の値  
  
|||  
|-|-|  
|`keyObject`|専用のディクショナリで指定された `object` のキーとして使用されるオブジェクトの、オブジェクト要素。|  
  
- この種類の使用方法のコンテナー/親は、ここには示しません。 `object` は、特化されたディクショナリの実装を表す object 要素の子である必要があります。 `keyObject` はオブジェクトインスタンス (または値型の値) であることが想定されています。これは、特定の特殊なディクショナリ実装のキーとして適しています。  
  
- WPF は、この使用方法を必要とするディクショナリを実装しません。 オブジェクト キーは XAML 言語のより一般的な機能であり、カスタム ディクショナリのシナリオで XAML でのディクショナリ作成が望まれる場合に有益であることがあります。 リソースに対して文字列以外のキーを使用する暗黙的なスタイルなどの WPF 機能については、別の方法によってキーを確立、または指定することができるので、オブジェクト キーを使用する必要はありません。  
  
- *Keyobject*は、直接のオブジェクトインスタンスではなく、オブジェクト要素形式のマークアップ拡張機能を使用することもできます。  
  
## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意  
 Silverlight の `x:Key` は個別に記載されています。 詳細については、「 [XAML 名前空間 (x:)」を参照してください。言語機能 (Silverlight)](https://go.microsoft.com/fwlink/?LinkId=199081)。  
  
## <a name="see-also"></a>参照

- [XAML リソース](../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [リソースとコード](../wpf/advanced/resources-and-code.md)
- [StaticResource のマークアップ拡張機能](../wpf/advanced/staticresource-markup-extension.md)
