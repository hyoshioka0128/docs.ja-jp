---
title: StaticResource のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- StaticResource
- StaticResourceExtension
helpviewer_keywords:
- XAML [WPF], StaticResource markup extension
- StaticResource markup extensions [WPF]
ms.assetid: 97af044c-71f1-4617-9a94-9064b68185d2
ms.openlocfilehash: c160322fb3834fcd705c0482f5e55c8da32d143b
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141252"
---
# <a name="staticresource-markup-extension"></a>StaticResource のマークアップ拡張機能
既に定義されているリソースへの参照を検索することによって、任意の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロパティ属性の値を提供します。 そのリソースに対する検索動作は、読み込み時の検索に似ています。これにより、現在の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページおよび他のアプリケーション ソースのマークアップから以前に読み込まれたリソースが検索され、実行時オブジェクトのプロパティ値としてそのリソース値が生成されます。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xml  
<object property="{StaticResource key}" ... />  
```  
  
## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法  
  
```xml  
<object>  
  <object.property>  
<StaticResource ResourceKey="key" ... />  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`key`|要求されたリソースのキー。 このキーは、リソースがマークアップで作成された場合は [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)によって最初に割り当てられ、リソースがコードで作成された場合は <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> を呼び出すときに `key` パラメーターとして提供されています。|  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]
> `StaticResource` では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ファイル内で構文的にさらに定義されているリソースへの前方参照を試行することはできません。 それを試みることはサポートされておらず、このような参照が失敗しない場合でも、前方参照を試行すると、<xref:System.Windows.ResourceDictionary> を表す内部ハッシュ テーブルが検索されるときに、読み込み時間のパフォーマンスが低下します。 最良の結果を得るには、前方参照を回避できるように、リソース ディクショナリの構成を調整します。 前方参照を回避できない場合は、代わりに [DynamicResource マークアップ拡張](dynamicresource-markup-extension.md)を使用します。  
  
 指定する <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> は、ページ、アプリケーション、使用可能なコントロール テーマと外部リソース、またはシステム リソースのいずれかのレベルで [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)によって示される既存のリソースに対応している必要があります。 リソースの検索は、その順序で行われます。 静的リソースと動的リソースのリソース検索動作の詳細については、[XAML のリソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
 リソース キーは、[XamlName 文法](../../../desktop-wpf/xaml-services/xamlname-grammar.md)で定義されている任意の文字列の可能性があります。 リソース キーは、<xref:System.Type> などの他のオブジェクト型の場合もあります。 <xref:System.Type> キーは、暗黙的なスタイル キーにより、テーマによってコントロールのスタイルを設定する方法の基礎になります。 詳しくは、「[コントロールの作成の概要](../controls/control-authoring-overview.md)」を参照してください。  
  
 リソースを参照する別の宣言的な方法は、[DynamicResource マークアップ拡張](dynamicresource-markup-extension.md)として機能します。  
  
 属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `StaticResource` 識別子文字列の後に設定される文字列トークンは、基になる <xref:System.Windows.StaticResourceExtension.ResourceKey%2A> 拡張クラスの <xref:System.Windows.StaticResourceExtension> 値として割り当てられます。  
  
 `StaticResource` は、オブジェクト要素構文で使用できます。 この場合は、<xref:System.Windows.StaticResourceExtension.ResourceKey%2A> プロパティの値を指定する必要があります。  
  
 `StaticResource` は、<xref:System.Windows.StaticResourceExtension.ResourceKey%2A> プロパティをプロパティおよび値のペアとして指定する詳細出力属性使用でも使用できます。  
  
```xml  
<object property="{StaticResource ResourceKey=key}" ... />  
```  
  
 詳細出力の使用は、複数の設定可能プロパティを持つ拡張機能や、一部のプロパティがオプションである場合に役立ちます。 `StaticResource` には、必須の設定可能プロパティが 1 つしか存在しないため、このような詳細出力の使用は一般的ではありません。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの実装では、このマークアップ拡張の処理は <xref:System.Windows.StaticResourceExtension> クラスによって定義されています。  
  
 `StaticResource` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のすべてのマークアップ拡張では、それぞれの属性構文で { と } の 2 つの記号が使用されます。これは規約であり、これに従って [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、マークアップ拡張で属性を処理する必要があることが認識されます。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [リソースとコード](resources-and-code.md)
