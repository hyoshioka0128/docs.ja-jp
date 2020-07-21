---
title: バインドのマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- Binding
helpviewer_keywords:
- Binding markup extensions [WPF]
- XAML [WPF], Binding markup extension
ms.assetid: 83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63
ms.openlocfilehash: c6a424e085c7499db08d0a7e6b652f45fb2cdd70
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81644081"
---
# <a name="binding-markup-extension"></a>バインドのマークアップ拡張機能
プロパティ値をデータ バインド値にするのを遅延し、中間式オブジェクトを作成し、実行時に要素とそのバインディングに適用されるデータ コンテキストを解釈します。  
  
## <a name="binding-expression-usage"></a>バインド式の使用  
  
```xaml  
<object property="{Binding}" .../>  
-or-  
<object property="{Binding  bindProp1=value1[, bindPropN=valueN]*}" ...  
/>  
-or-  
<object property="{Binding path}" .../>  
-or  
<object property="{Binding path[, bindPropN=valueN]*}" .../>  
```  
  
## <a name="syntax-notes"></a>構文に関する注意事項  
 これらの構文では、`[]` と `*` はリテラルではありません。 これらは、0 個以上の *bindProp*`=`*value* ペアを使用できることを示す表記の一部であり、それらと前にある *bindProp*`=`*value* ペアの間の区切り記号は `,` です。  
  
 「バインド拡張機能で設定できるバインド プロパティ」セクションで示されているプロパティはすべて、代わりに <xref:System.Windows.Data.Binding> オブジェクト要素の属性を使用して設定できます。 ただし、それは <xref:System.Windows.Data.Binding> のマークアップ拡張を本当に使用しているのではなく、CLR の <xref:System.Windows.Data.Binding> クラスのプロパティを設定する属性の一般的な XAML 処理にすぎません。 つまり、`<Binding` *bindProp1*`="`*value1*`"[` *bindPropN*`="`*valueN*`"]*/>` は、`Binding` 式を使用する代わりに、<xref:System.Windows.Data.Binding> オブジェクト要素の属性を使用するのと同等の構文です。 <xref:System.Windows.Data.Binding> の特定のプロパティの XAML 属性の使用方法については、.NET Framework クラス ライブラリで <xref:System.Windows.Data.Binding> の関連プロパティの「XAML 属性の使用方法」セクションを参照してください。  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`bindProp1, bindPropN`|設定する <xref:System.Windows.Data.Binding> または <xref:System.Windows.Data.BindingBase> プロパティの名前。 すべての <xref:System.Windows.Data.Binding> プロパティを `Binding` 拡張機能で設定できるわけではありません。一部のプロパティは、さらに入れ子になったマークアップ拡張を使用することによってのみ、`Binding` 式内で設定できます。 「バインド拡張機能で設定できるバインド プロパティ」を参照してください。|  
|`value1, valueN`|プロパティに設定する値。 属性値の処理は、最終的には、設定対象の特定の <xref:System.Windows.Data.Binding> プロパティの型とロジックに固有です。|  
|`path`|暗黙的な <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> プロパティを設定するパス文字列。 「[PropertyPath の XAML 構文](propertypath-xaml-syntax.md)」も参照してください。|  
  
## <a name="unqualified-binding"></a>修飾なしの {Binding}  
 「バインド式の使用」で示されている `{Binding}` の使用方法では、既定値の <xref:System.Windows.Data.Binding> オブジェクトが作成されます。それには、初期 <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> の `null` が含まれます。 これは、作成された <xref:System.Windows.Data.Binding> が、実行時データ コンテキストで設定される <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> や <xref:System.Windows.Data.Binding.Source%2A?displayProperty=nameWithType> などのキー データ バインディング プロパティに依存している可能性があるため、多くのシナリオで役立ちます。 データ コンテキストの概念の詳細については、[データ バインディング](../../../desktop-wpf/data/data-binding-overview.md)に関する記事を参照してください。  
  
## <a name="implicit-path"></a>暗黙的なパス  
 `Binding` マークアップ拡張では、<xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> が概念的な "既定のプロパティ" として使用されます。`Path=` は式の中で使用される必要はありません。 暗黙的なパスを使用して `Binding` 式を指定する場合は、<xref:System.Windows.Data.Binding> プロパティが名前で指定されている他のすべての `bindProp`=`value` ペアの前の式の先頭で、暗黙的なパスを指定する必要があります。 たとえば、`{Binding PathString}` などです。`PathString` は、マークアップ拡張の使用によって作成された <xref:System.Windows.Data.Binding> 内の <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> の値として評価される文字列です。 コンマ区切り記号の後で、他の名前付きプロパティを使用して暗黙的なパスを追加できます (例: `{Binding LastName, Mode=TwoWay}`)。  
  
## <a name="binding-properties-that-can-be-set-with-the-binding-extension"></a>バインド拡張機能で設定できるバインド プロパティ  
 このトピックで示す構文では、`bindProp`=`value` という一般的な近い表現が使用されています。これは、<xref:System.Windows.Data.BindingBase> または <xref:System.Windows.Data.Binding> には、`Binding` のマークアップ拡張および式構文を使用して設定できる、読み取りおよび書き込みプロパティが多数あるためです。 暗黙の <xref:System.Windows.Data.Binding.Path%2A?displayProperty=nameWithType> を除き、それらは任意の順序で設定できます。 (`Path=` を明示的に指定することもでき、その場合は任意の順序で設定できます)。 基本的に、コンマで区切られた `bindProp`=`value` のペアを使用して、以下の一覧の 0 個以上のプロパティを設定できます。  
  
 これらのプロパティ値の一部では、XAML のテキスト構文のネイティブな型変換がサポートされていないオブジェクト型が必要であり、したがって属性値として設定するにはマークアップ拡張が必要です。 各プロパティの詳細については、.NET Framework クラス ライブラリにある XAML 属性の使用方法に関するセクションを参照してください。マークアップ拡張をさらに使用しても使用しなくても、XAML 属性の構文に使用する文字列は、基本的に、`Binding` 式で指定する値と同じです。ただし、`Binding` 式の各 `bindProp`=`value` を引用符で囲まないでください。  
  
- <xref:System.Windows.Data.BindingBase.BindingGroupName%2A>: 使用可能なバインド グループを識別する文字列。 これは、比較的高度なバインド概念です。<xref:System.Windows.Data.BindingBase.BindingGroupName%2A> のリファレンス ページを参照してください。  
  
- <xref:System.Windows.Data.Binding.BindsDirectlyToSource%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。  
  
- <xref:System.Windows.Data.Binding.Converter%2A>: 式で文字列 `bindProp`=`value` を使用して設定できます。ただし、そのためには、[StaticResource マークアップ拡張](staticresource-markup-extension.md)など、値のオブジェクト参照が必要です。 この場合の値は、カスタム コンバーター クラスのインスタンスです。  
  
- <xref:System.Windows.Data.Binding.ConverterCulture%2A>: 標準ベースの識別子として式で設定できます。<xref:System.Windows.Data.Binding.ConverterCulture%2A> のリファレンス トピックを参照してください。  
  
- <xref:System.Windows.Data.Binding.ConverterParameter%2A>: 式で文字列 `bindProp`=`value` を使用して設定できます。ただし、これは渡されるパラメーターの型によって異なります。 値に参照型を渡す場合は、入れ子になった [StaticResource マークアップ拡張](staticresource-markup-extension.md)などのオブジェクト参照が必要です。  
  
- <xref:System.Windows.Data.Binding.ElementName%2A>: <xref:System.Windows.Data.Binding.RelativeSource%2A> および <xref:System.Windows.Data.Binding.Source%2A> に対して相互に排他的です。これらの各バインド プロパティでは、特定のバインディング方法が表されます。 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)に関する記事を参照してください。  
  
- <xref:System.Windows.Data.BindingBase.FallbackValue%2A>: 式で文字列 `bindProp`=`value` を使用して設定できます。ただし、これは渡される値の型によって異なります。 参照型を渡す場合は、入れ子になった [StaticResource マークアップ拡張](staticresource-markup-extension.md)などのオブジェクト参照が必要です。  
  
- <xref:System.Windows.Data.Binding.IsAsync%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。  
  
- <xref:System.Windows.Data.Binding.Mode%2A>: *value* は <xref:System.Windows.Data.BindingMode> 列挙型の定数名です。 たとえば、`{Binding Mode=OneWay}` のようにします。  
  
- <xref:System.Windows.Data.Binding.NotifyOnSourceUpdated%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。  
  
- <xref:System.Windows.Data.Binding.NotifyOnTargetUpdated%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。  
  
- <xref:System.Windows.Data.Binding.NotifyOnValidationError%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。  
  
- <xref:System.Windows.Data.Binding.Path%2A>: データ オブジェクトまたは一般的なオブジェクト モデルへのパスを記述する文字列。 この形式では、このトピックでは適切に説明できないオブジェクト モデルをトラバースするためのさまざまな規則が提供されます。 「[PropertyPath の XAML 構文](propertypath-xaml-syntax.md)」を参照してください。  
  
- <xref:System.Windows.Data.Binding.RelativeSource%2A>: <xref:System.Windows.Data.Binding.ElementName%2A> および <xref:System.Windows.Data.Binding.Source%2A> に対して相互に排他的です。これらの各バインド プロパティでは、特定のバインディング方法が表されます。 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)に関する記事を参照してください。 値を指定するには、入れ子になった [RelativeSource マークアップ拡張](relativesource-markupextension.md)を使用する必要があります。  
  
- <xref:System.Windows.Data.Binding.Source%2A>: <xref:System.Windows.Data.Binding.RelativeSource%2A> および <xref:System.Windows.Data.Binding.ElementName%2A> に対して相互に排他的です。これらの各バインド プロパティでは、特定のバインディング方法が表されます。 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)に関する記事を参照してください。 入れ子になった拡張機能を使用する必要があります。通常は、キー付きリソース ディクショナリからオブジェクト データ ソースを参照する [StaticResource マークアップ拡張](staticresource-markup-extension.md)を使用します。  
  
- <xref:System.Windows.Data.BindingBase.StringFormat%2A>: バインドされるデータの文字列形式規則を記述する文字列。 これは、比較的高度なバインド概念です。<xref:System.Windows.Data.BindingBase.StringFormat%2A> のリファレンス ページを参照してください。  
  
- <xref:System.Windows.Data.BindingBase.TargetNullValue%2A>: 式で文字列 `bindProp`=`value` を使用して設定できます。ただし、これは渡されるパラメーターの型によって異なります。 値に参照型を渡す場合は、入れ子になった [StaticResource マークアップ拡張](staticresource-markup-extension.md)などのオブジェクト参照が必要です。  
  
- <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>: *value* は <xref:System.Windows.Data.UpdateSourceTrigger> 列挙型の定数名です。 たとえば、`{Binding UpdateSourceTrigger=LostFocus}` のようにします。 特定のコントロールでは、このバインド プロパティの既定値が異なる可能性があります。 以下を参照してください。<xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A>  
  
- <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。 「解説」を参照してください。  
  
- <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A>:ブール値。`true` または `false` を使用できます。 既定値は、`false` です。 「解説」を参照してください。  
  
- <xref:System.Windows.Data.Binding.XPath%2A>: XML データ ソースの XMLDOM へのパスを記述する文字列。 [XMLDataProvider と XPath クエリを使用した XML データへのバインド](../data/how-to-bind-to-xml-data-using-an-xmldataprovider-and-xpath-queries.md)に関する記事を参照してください。  
  
 `Binding` マークアップ拡張と `{Binding}` 式の形式を使用して設定できない <xref:System.Windows.Data.Binding> のプロパティを次に示します。  
  
- <xref:System.Windows.Data.Binding.UpdateSourceExceptionFilter%2A>: このプロパティには、コールバックの実装への参照が必要です。 イベント ハンドラー以外のコールバックおよびメソッドは、XAML 構文では参照できません。  
  
- <xref:System.Windows.Data.Binding.ValidationRules%2A>: プロパティは、<xref:System.Windows.Controls.ValidationRule> オブジェクトのジェネリック コレクションを受け取ります。 これは、<xref:System.Windows.Data.Binding> オブジェクト要素のプロパティ要素として表すことができますが、`Binding` 式で使用するためにすぐに利用できる属性解析手法はありません。 <xref:System.Windows.Data.Binding.ValidationRules%2A> のリファレンス トピックを参照してください。  
  
- <xref:System.Windows.Data.Binding.XmlNamespaceManager%2A>  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]
> 依存関係プロパティの優先順位に関しては、`Binding` 式はローカルに設定された値と同じです。 以前は `Binding` 式であったプロパティに対してローカル値を設定した場合、`Binding` は完全に削除されます。 詳細については、「[依存関係プロパティ値の優先順位](dependency-property-value-precedence.md)」を参照してください。  
  
 基本レベルでのデータ バインディングの記述については、このトピックでは説明しません。 [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)に関する記事を参照してください。  
  
> [!NOTE]
> <xref:System.Windows.Data.MultiBinding> と <xref:System.Windows.Data.PriorityBinding> では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 拡張構文はサポートされていません。 代わりに、プロパティ要素を使用します。 <xref:System.Windows.Data.MultiBinding> および <xref:System.Windows.Data.PriorityBinding> のリファレンス トピックを参照してください。  
  
 XAML のブール値では大文字と小文字が区別されません。 たとえば、`{Binding NotifyOnValidationError=true}` でも `{Binding NotifyOnValidationError=True}` でも指定できます。  
  
 データの検証を伴うバインドは、通常、`{Binding ...}` 式としてではなく、明示的な `Binding` 要素によって指定されます。また、式で <xref:System.Windows.Data.Binding.ValidatesOnDataErrors%2A> または <xref:System.Windows.Data.Binding.ValidatesOnExceptions%2A> を設定することは一般的ではありません。 これは、コンパニオン プロパティ <xref:System.Windows.Data.Binding.ValidationRules%2A> は式形式では簡単に設定できないためです。 詳細については、[バインディングの検証の実装](../data/how-to-implement-binding-validation.md)に関する記事を参照してください。  
  
 `Binding` はマークアップ拡張機能です。 一般にマークアップ拡張を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティで属性化された型コンバーターにとどまらない場合です。 XAML のすべてのマークアップ拡張機能では、それぞれの属性構文で `{` と `}` の 2 つの記号を使用します。これは規約であり、これに従って XAML プロセッサは、マークアップ拡張機能で文字列コンテンツを処理する必要があることを認識します。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
 `Binding` は例外的なマークアップ拡張であり、WPF の XAML 実装に対する拡張機能を実装する <xref:System.Windows.Data.Binding> クラスで、XAML に関係のない他のいくつかのメソッドとプロパティも実装されています。 他のメンバーは、XAML マークアップ拡張として機能するだけでなく、<xref:System.Windows.Data.Binding> を多くのデータ バインディング シナリオに対応できる、より汎用的で自己完結型のクラスにすることを目的としています。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Data.Binding>
- [データ バインディングの概要](../../../desktop-wpf/data/data-binding-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
