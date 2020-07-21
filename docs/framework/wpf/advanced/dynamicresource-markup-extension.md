---
title: DynamicResource のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- DynamicResource
- DynamicResourceExtension
helpviewer_keywords:
- XAML [WPF], DynamicResource markup extension
- DynamicResource markup extensions [WPF]
ms.assetid: 7324f243-03af-4c2b-b0db-26ac6cdfcbe4
ms.openlocfilehash: 579fae46a7c53a61b728d7526ef397eb371abb74
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141070"
---
# <a name="dynamicresource-markup-extension"></a>DynamicResource のマークアップ拡張機能
定義されているリソースの値が山処すあれるように遅延するすることによって、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のプロパティ属性の値を提供します。 そのリソース検索動作は、実行時の検索に類似しています。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xml  
<object property="{DynamicResource key}" ... />  
```  
  
## <a name="xaml-property-element-usage"></a>XAML プロパティ要素の使用  
  
```xml  
<object>  
  <object.property>  
    <DynamicResource ResourceKey="key" ... />  
  </object.property>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`key`|要求されたリソースのキー。 このキーは、リソースがマークアップで作成された場合は [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)によって最初に割り当てられ、リソースがコードで作成された場合は <xref:System.Windows.ResourceDictionary.Add%2A?displayProperty=nameWithType> を呼び出すときに `key` パラメーターとして提供されています。|  
  
## <a name="remarks"></a>Remarks  
 `DynamicResource` では、初期コンパイル中に一時式が作成されます。そのため、オブジェクトを構築するために要求されたリソース値が実際に必要になるまで、リソースの検索が遅延されます。 これは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] ページが読み込まれた後になる可能性があります。 リソースの値は、現在のページ スコープから始まるすべてのアクティブなリソース ディクショナリに対するキー検索に基づいて検出され、コンパイル時のプレースホルダー式の代わりに使用されます。  
  
> [!IMPORTANT]
> 依存関係プロパティの優先順位に関しては、`DynamicResource` 式は動的リソース参照が適用される位置と同じです。 以前はローカル値として `DynamicResource` 式が使用されていたプロパティに対してローカル値を設定した場合、`DynamicResource` は完全に削除されます。 詳細については、「[依存関係プロパティ値の優先順位](dependency-property-value-precedence.md)」を参照してください。  
  
 特定のリソース アクセス シナリオは、[StaticResource マークアップ拡張](staticresource-markup-extension.md)ではなく `DynamicResource` に特に適しています。 `DynamicResource` と `StaticResource` の相対的な利点とパフォーマンスへの影響については、[XAML のリソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
 指定する <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> は、ページ、アプリケーション、使用可能なコントロール テーマと外部リソース、またはシステム リソースのいずれかのレベルで [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)によって決定される既存のリソースに対応している必要があります。リソースの検索は、この順序で行われます。 静的リソースと動的リソースのリソース検索の詳細については、[XAML のリソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。  
  
 リソース キーは、[XamlName 文法](../../../desktop-wpf/xaml-services/xamlname-grammar.md)で定義されている任意の文字列の可能性があります。 リソース キーは、<xref:System.Type> などの他のオブジェクト型の場合もあります。 <xref:System.Type> キーは、テーマによってコントロールのスタイルを設定する方法の基礎になります。 詳しくは、「[コントロールの作成の概要](../controls/control-authoring-overview.md)」を参照してください。  
  
 <xref:System.Windows.FrameworkElement.FindResource%2A> などのリソース値を検索するための API は、`DynamicResource` によって使用されているものと同じリソース検索ロジックに従います。  
  
 リソースを参照する別の宣言的な方法は、[StaticResource マークアップ拡張](staticresource-markup-extension.md)として機能します。  
  
 属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `DynamicResource` 識別子文字列の後に設定される文字列トークンは、基になる <xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> 拡張クラスの <xref:System.Windows.DynamicResourceExtension> 値として割り当てられます。  
  
 `DynamicResource` は、オブジェクト要素構文で使用できます。 この場合は、<xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> プロパティの値を指定する必要があります。  
  
 `DynamicResource` は、<xref:System.Windows.DynamicResourceExtension.ResourceKey%2A> プロパティをプロパティおよび値のペアとして指定する詳細出力属性使用でも使用できます。  
  
```xml  
<object property="{DynamicResource ResourceKey=key}" ... />  
```  
  
 詳細出力の使用は、複数の設定可能プロパティを持つ拡張機能や、一部のプロパティがオプションである場合に役立ちます。 `DynamicResource` には、必須の設定可能プロパティが 1 つしか存在しないため、このような詳細出力の使用は一般的ではありません。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの実装では、このマークアップ拡張の処理は <xref:System.Windows.DynamicResourceExtension> クラスによって定義されています。  
  
 `DynamicResource` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のすべてのマークアップ拡張では、それぞれの属性構文で { と } の 2 つの記号が使用されます。これは規約であり、これに従って [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、マークアップ拡張で属性を処理する必要があることが認識されます。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [リソースとコード](resources-and-code.md)
- [x:Key ディレクティブ](../../../desktop-wpf/xaml-services/xkey-directive.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [StaticResource のマークアップ拡張機能](staticresource-markup-extension.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
