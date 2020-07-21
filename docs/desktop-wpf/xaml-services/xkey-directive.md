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
ms.openlocfilehash: c05f98932ceceeb1530b34a09b1923f2af1378b5
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432756"
---
# <a name="xkey-directive"></a>x:Key ディレクティブ
XAML で定義されたディクショナリで作成および参照される要素を一意に識別します。 `x:Key` 値を XAML オブジェクトに追加するのは、リソース ディクショナリ (<xref:System.Windows.ResourceDictionary> など) のリソースを識別するための最も一般的な方法です。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
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
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`stringKeyValue`|キーとして使用するテキスト文字列。 テキスト文字列は[XamlName 文法](xamlname-grammar.md)に準拠している必要があります。|  
|`markupExtensionUsage`|マークアップ拡張機能の区切り記号{}内で、キーとして使用するオブジェクトを提供するマークアップ拡張機能の使用法。 「解説」を参照してください。|  
  
## <a name="remarks"></a>解説  
 `x:Key` は XAML のリソース ディクショナリの概念をサポートしています。 言語としての XAML ではリソース ディクショナリの実装は定義されていません。特定の UI フレーム ワークによって定義されています。 WPF で XAML リソース ディクショナリを実装する方法の詳細については[、「XAML リソース](../fundamentals/xaml-resources-define.md)」を参照してください。  
  
 XAML 2006 および`x:Key`WPF では、属性として指定する必要があります。 文字列ではないキーも使用できますが、文字列ではない値を属性形式で提供するためには、マークアップ拡張機能を使用する必要があります。 XAML 2009 を使用している`x:Key`場合は、要素として指定して、マークアップ拡張機能の中間を必要とせずに、文字列以外のオブジェクト型でキーをキー設定したディクショナリを明示的にサポートできます。 このトピックの「XAML 2009」のセクションを参照してください。 解説セクションの残りの部分では、XAML 2006 の実装について説明します。  
  
 の属性値は`x:Key`[、XamlName Grammar](xamlname-grammar.md)で定義された任意の文字列を指定することも、マークアップ拡張機能を通じて評価されるオブジェクトにすることもできます。 WPF の例については、「WPF の使用上の注意」を参照してください。  
  
 通常、<xref:System.Collections.IDictionary> の実装である親要素の子要素には、そのディクショナリ内の一意のキー値を指定する `x:Key` 属性を含める必要があります。 フレームワークでは、特定の型の `x:Key` を代用するために、エイリアス化されたキー プロパティを実装する場合があります。このようなプロパティを定義する型には、<xref:System.Windows.Markup.DictionaryKeyPropertyAttribute> 属性を設定する必要があります。  
  
 `x:Key` の指定に相当するコードは、基になる <xref:System.Collections.IDictionary> で使用されるキーです。 たとえば、マークアップで適用される WPF のリソースの `x:Key` は、コードでリソースを WPF の `key` に追加する場合、<xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> の <xref:System.Windows.ResourceDictionary> パラメーターの値と同等です。  
  
## <a name="wpf-usage-notes"></a>WPF の使用上の注意  
 通常、WPF の <xref:System.Collections.IDictionary> などの <xref:System.Windows.ResourceDictionary> の実装である親オブジェクトの子オブジェクトには、`x:Key` 属性を含める必要があります。また、キー値は、そのディクショナリ内で一意である必要があります。 ただし、次のように 2 つの重要な例外があります。  
  
- 一部の WPF 型は、ディクショナリの使用に対して暗黙のキーを宣言します。 たとえば、<xref:System.Windows.Style> が設定された <xref:System.Windows.Style.TargetType%2A> や、<xref:System.Windows.DataTemplate> が設定された <xref:System.Windows.DataTemplate.DataType%2A> は、<xref:System.Windows.ResourceDictionary> に格納して、暗黙のキーを使用できます。  
  
- WPF は、マージされたリソース ディクショナリの概念をサポートしています。 キーは、マージされたディクショナリ間で共有できます。また、共有されたキーの動作には、<xref:System.Windows.FrameworkContentElement.FindResource%2A> を使用してアクセスできます。 詳細については、「[Merged Resource Dictionaries](../../framework/wpf/advanced/merged-resource-dictionaries.md)」を参照してください。  
  
 通常、WPF XAML の実装およびアプリケーション モデルでは、キーの一意性が XAML マークアップ コンパイラによってチェックされることはありません。 その代わり、`x:Key` 値が指定されていない場合や一意でない場合は、読み込み時に XAML パーサー エラーが発生します。 ただし、WPF 用のディクショナリの Visual Studio の処理では、多くの場合、デザイン 段階でこのようなエラーに注意できます。  
  
 ここに示す構文において、<xref:System.Windows.ResourceDictionary> オブジェクトは WPF XAML プロセッサが <xref:System.Windows.FrameworkElement.Resources%2A> コレクションを取得するためのコレクションを生成する方法を暗黙的に決定することに注意してください。 <xref:System.Windows.ResourceDictionary> は、通常はマークアップで要素として明示的に指定されませんが、わかりやすくするために必要に応じて明示的に指定することもできます (その場合、このオブジェクトは、<xref:System.Windows.FrameworkElement.Resources%2A> プロパティ要素とディクショナリに設定される項目間のコレクション オブジェクト要素になります)。 コレクション オブジェクトがマークアップの暗黙的な要素である理由については[、「XAML 構文の詳細](../../framework/wpf/advanced/xaml-syntax-in-detail.md)」を参照してください。  
  
 WPF XAML 実装では、リソース ディクショナリ キーの処理は、<xref:System.Windows.ResourceKey> 抽象クラスによって定義されます。 ただし、WPF XAML プロセッサは、使用方法に基づいてキーごとに別の基になる拡張型を生成します。 たとえば、<xref:System.Windows.DataTemplate> または任意の派生クラスのキーは個別に処理され、異なる <xref:System.Windows.DataTemplateKey> オブジェクトを生成します。  
  
 基本的な XAML 定義では、キーと名前で異なるディレクティブと言語要素 (`x:Key` と `x:Name`) が使用されます。 また、キーと名前は、それらの概念の WPF 定義およびアプリケーションにより異なる状況において使用されます。 詳細については、「 [WPF XAML 名前スコープ](../../framework/wpf/advanced/wpf-xaml-namescopes.md)」を参照してください。  
  
 既に説明したように、キー値はマークアップ拡張機能によって指定され、文字列値以外になる場合があります。 WPF のシナリオの例としては、`x:Key`の値が[ComponentResourceKey](../../framework/wpf/advanced/componentresourcekey-markup-extension.md)である可能性があります。 特定のコントロールでは、スタイルを完全に置き換えることなく、そのコントロールの外観と動作の一部に影響を与えるカスタム スタイル リソースの型に対応するスタイル キーが公開されます。 このようなキーの例として、<xref:System.Windows.Controls.ToolBar.ButtonStyleKey%2A> が挙げられます。  
  
 WPF のマージされたディクショナリ機能では、キーの一意性およびキーの検索動作について考慮を要する点があります。 詳細については、「[Merged Resource Dictionaries](../../framework/wpf/advanced/merged-resource-dictionaries.md)」を参照してください。  
  
## <a name="xaml-2009"></a>XAML 2009  
 XAML 2009 では、属性`x:Key`形式で常に提供される制限が緩和されます。  
  
 WPF では、XAML 2009 の機能を使用できますが、マークアップ コンパイルされていない XAML に対してのみ使用できます。 WPF 向けにマークアップ コンパイルされた XAML、および XAML の BAML 形式は、現在、XAML 2009 のキーワードと機能をサポートしていません。  
  
 XAML 2009 では、次`x:Key`の使用方法で要素を指定できます。  
  
### <a name="xaml-element-usage-xaml-2009-only"></a>XAML 要素の使用 (XAML 2009 のみ)  
  
```xaml  
<object>  
  <x:Key>  
keyObject  
  </x:Key>  
...  
</object>  
```  
  
### <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`keyObject`|専用のディクショナリで指定された `object` のキーとして使用されるオブジェクトの、オブジェクト要素。|  
  
- この種類の使用方法のコンテナー/親は、ここには示しません。 `object` は、専用のディクショナリの実装を表すオブジェクト要素の子であると想定されます。 `keyObject` は、その専用のディクショナリの実装のキーとして適切なオブジェクト インスタンス (または値の型の値) であると想定されます。  
  
- WPF は、この使用方法を必要とするディクショナリを実装しません。 オブジェクト キーは XAML 言語のより一般的な機能であり、カスタム ディクショナリのシナリオで XAML でのディクショナリ作成が望まれる場合に有益であることがあります。 リソースに対して文字列以外のキーを使用する暗黙的なスタイルなどの WPF 機能については、別の方法によってキーを確立、または指定することができるので、オブジェクト キーを使用する必要はありません。  
  
- `keyObject`直接オブジェクト インスタンスではなく、オブジェクト要素形式でのマークアップ拡張機能の使用も可能です。  
  
## <a name="silverlight-usage-notes"></a>Silverlight の使用上の注意  
 Silverlight 用の `x:Key` に関しては、別途ドキュメントが用意されています。 詳細については[、「XAML 名前空間 (x:)」を参照してください。言語機能 (シルバーライト)](https://docs.microsoft.com/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc188995(v=vs.95))  
  
## <a name="see-also"></a>関連項目

- [XAML リソース](../fundamentals/xaml-resources-define.md)
- [リソースとコード](../../framework/wpf/advanced/resources-and-code.md)
- [StaticResource のマークアップ拡張機能](../../framework/wpf/advanced/staticresource-markup-extension.md)
