---
title: ComponentResourceKey マークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- ComponentResourceKey
- ComponentResourceKeyExtension
helpviewer_keywords:
- ComponentResourceKey markup extension [WPF]
- XAML [WPF], ComponentResourceKey markup extension
ms.assetid: d6bcdbe6-61b3-40a7-b381-4e02185b5a85
ms.openlocfilehash: f86b7000b97bbc1287347947a9244c24a7de74c2
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141139"
---
# <a name="componentresourcekey-markup-extension"></a>ComponentResourceKey マークアップ拡張機能
外部アセンブリから読み込まれるリソースのキーを定義して参照します。 これにより、リソース検索では、アセンブリ内の明示的なリソース ディクショナリやクラスではなく、アセンブリ内の対象の型を指定できます。  
  
## <a name="xaml-attribute-usage-setting-key-compact"></a>XAML 属性の使用方法 (キーの設定、コンパクト)  
  
```xml  
<object x:Key="{ComponentResourceKey {x:Type targetTypeName}, targetID}" ... />  
```  
  
## <a name="xaml-attribute-usage-setting-key-verbose"></a>XAML 属性の使用方法 (キーの設定、詳細)  
  
```xml  
<object x:Key="{ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}" ... />  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-compact"></a>XAML 属性の使用方法 (リソースの要求、コンパクト)  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey {x:Type targetTypeName}, targetID}}" ... />  
```  
  
## <a name="xaml-attribute-usage-requesting-resource-verbose"></a>XAML 属性の使用方法 (リソースの要求、詳細)  
  
```xml  
<object property="{DynamicResource {ComponentResourceKey TypeInTargetAssembly={x:Type targetTypeName}, ResourceID=targetID}}" ... />  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`targetTypeName`|リソース アセンブリで定義されているパブリック共通言語ランタイム (CLR) 型の名前。|  
|`targetID`|リソースのキー。 リソースを検索すとき、`targetID` はリソースの [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)に似ています。|  
  
## <a name="remarks"></a>Remarks  
 上記の使用方法で示されているように、{`ComponentResourceKey`} マークアップ拡張は次の 2 つの場所で使用されています。  
  
- コントロールの作成者によって提供される、テーマ リソース ディクショナリ内のキーの定義。  
  
- コントロールを再テンプレート化するが、コントロールのテーマによって提供されるリソースのプロパティ値を使用したい場合の、アセンブリのテーマ リソースへのアクセス。  
  
 テーマのコンポーネント リソースを参照する場合は、通常、`{StaticResource}` ではなく `{DynamicResource}` を使用することをお勧めします。 これは、使用方法で示されています。 `{DynamicResource}` が推奨されるのは、テーマ自体がユーザーによって変更される場合があるためです。 コントロールの作成者が意図するテーマのサポートに最も近いコンポーネント リソースが必要な場合は、コンポーネントのリソース参照を動的にできる必要もあります。  
  
 <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> では、リソースが実際に定義されているターゲット アセンブリに存在する型が示されてます。 `ComponentResourceKey` は、<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> が定義されている場所の正確な情報とは関係なく定義および使用できますが、最終的には参照されているアセンブリを使用して型を解決する必要があります。  
  
 <xref:System.Windows.ComponentResourceKey> の一般的な使用方法は、そのときにクラスのメンバーとして公開されるキーを定義することです。 この使用方法では、マークアップ拡張ではなく <xref:System.Windows.ComponentResourceKey> クラスのコンストラクターを使用します。 詳細については、<xref:System.Windows.ComponentResourceKey> に関する記事、または「[コントロールの作成の概要](../controls/control-authoring-overview.md)」の「テーマ リソース用のキーの定義と参照」セクションを参照してください。  
  
 キーの設定とキー付きリソースの参照の両方で、通常は、属性構文が `ComponentResourceKey` マークアップ拡張に使用されます。  
  
 示されているコンパクト構文は、<xref:System.Windows.ComponentResourceKey.%23ctor%2A> コンストラクターのシグネチャと、マークアップ拡張の位置指定パラメーターの使用に依存しています。 `targetTypeName` と `targetID` を指定する順序が重要です。 詳細構文は、<xref:System.Windows.ComponentResourceKey.%23ctor%2A> のパラメーターなしのコンストラクターに依存し、オブジェクト要素の真の属性構文に似た方法で <xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> と <xref:System.Windows.ComponentResourceKey.ResourceId%2A> が設定されます。 詳細構文では、プロパティが設定される順序は重要ではありません。 これら 2 つの代替手段 (コンパクトと詳細) の関係とメカニズムについては、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」で詳しく説明されています。  
  
 技術的には、`targetID` の値はどのようなオブジェクトでもよく、文字列である必要はありません。 ただし、WPF での最も一般的な使用方法は、`targetID` の値を文字列の形式と揃えることであり、そのような文字列が [XamlName 文法](../../../desktop-wpf/xaml-services/xamlname-grammar.md)において有効である場所です。  
  
 `ComponentResourceKey` は、オブジェクト要素構文で使用できます。 この場合、拡張機能を正しく初期化するには、<xref:System.Windows.ComponentResourceKey.TypeInTargetAssembly%2A> プロパティと <xref:System.Windows.ComponentResourceKey.ResourceId%2A> プロパティの両方の値を指定する必要があります。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] リーダーの実装では、このマークアップ拡張の処理は <xref:System.Windows.ComponentResourceKey> クラスによって定義されています。  
  
 `ComponentResourceKey` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のすべてのマークアップ拡張では、それぞれの属性構文で { と } の 2 つの記号が使用されます。これは規約であり、これに従って [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、マークアップ拡張で属性を処理する必要があることが認識されます。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.ComponentResourceKey>
- <xref:System.Windows.Controls.ControlTemplate>
- [コントロールの作成の概要](../controls/control-authoring-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
