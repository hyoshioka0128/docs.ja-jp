---
title: ThemeDictionary のマークアップ拡張機能
ms.date: 03/30/2017
f1_keywords:
- ThemeDictionaryExtension
- ThemeDictionary
helpviewer_keywords:
- ThemeDictionary markup extension [WPF]
- XAML [WPF], ThemeDictionary markup extension
ms.assetid: aa75e10b-13dd-4989-972d-51bab63a05e2
ms.openlocfilehash: 450956de1c7498bf2b92096b38ad2f64745a0b2d
ms.sourcegitcommit: 839777281a281684a7e2906dccb3acd7f6a32023
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "82141097"
---
# <a name="themedictionary-markup-extension"></a>ThemeDictionary のマークアップ拡張機能
カスタム コントロールの作成者またはサードパーティのコントロールを統合するアプリケーションに、コントロールのスタイル設定に使用するテーマ固有のリソース ディクショナリを読み込む方法を提供します。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xml  
<object property="{ThemeDictionary assemblyUri}" ... />  
```  
  
## <a name="xaml-object-element-usage"></a>XAML オブジェクト要素の使用方法  
  
```xml  
<object>  
  <object.property>  
    <ThemeDictionary AssemblyName="assemblyUri"/>  
  <object.property>  
<object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|`assemblyUri`|テーマの情報が格納されているアセンブリの URI (Uniform Resource Identifier)。 通常、これは大きなパッケージ内のアセンブリを参照するパック URI です。 アセンブリ リソースとパック URI によって、配置の問題が簡単になります。 詳細については、「[WPF におけるパッケージの URI](../app-development/pack-uris-in-wpf.md)」を参照してください。|  
  
## <a name="remarks"></a>Remarks  
 この拡張機能では、1 つの特定のプロパティ値、つまり <xref:System.Windows.ResourceDictionary.Source%2A?displayProperty=nameWithType> の値を設定することだけが意図されています。  
  
 この拡張機能を使用すると、単一リソースのみのアセンブリを指定できます。それには、Windows Aero テーマがユーザーのシステムに適用されている場合にのみ使用されるスタイル、Luna テーマがアクティブになっている場合にのみ使用される他のスタイル、などが含まれます。 この拡張機能を使用することで、必要に応じて、コントロール固有のリソース ディクショナリの内容を自動的に無効にし、別のテーマに合わせて再度読み込むことができます。  
  
 `assemblyUri` の文字列 (<xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> プロパティの値) は、特定のテーマに適用されるディクショナリを識別する名前付け規則の基礎となります。 `ThemeDictionary` に対する <xref:System.Windows.Markup.MarkupExtension.ProvideValue%2A> のロジックにより、プリコンパイル済みのリソース アセンブリに含まれる、特定のテーマ ディクショナリのバリエーションを指す Uniform Resource Identifier (URI) を生成することによって、規則が完成されます。 この規則、または一般的なコントロールのスタイル設定およびページやアプリケーション レベルのスタイル設定とのテーマの相互作用の概念については、ここでは説明しません。 `ThemeDictionary` を使用する基本的なシナリオは、アプリケーション レベルで宣言された `ResourceDictionary` の <xref:System.Windows.ResourceDictionary.Source%2A> プロパティを指定する場合です。 ダイレクト URI ではなく `ThemeDictionary` 拡張を使用してアセンブリの URI を指定すると、システム テーマが変更されるたびに適用される無効化ロジックが拡張ロジックによって提供されます。  
  
 属性構文は、このマークアップ拡張機能で使用される最も一般的な構文です。 `ThemeDictionary` 識別子文字列の後に設定される文字列トークンは、基になる <xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> 拡張クラスの <xref:System.Windows.ThemeDictionaryExtension> 値として割り当てられます。  
  
 `ThemeDictionary` は、オブジェクト要素構文でも使用できます。 この場合は、<xref:System.Windows.ThemeDictionaryExtension.AssemblyName%2A> プロパティの値を指定する必要があります。  
  
 `ThemeDictionary` は、<xref:System.Windows.Markup.StaticExtension.Member%2A> プロパティをプロパティおよび値のペアとして指定する詳細出力属性使用でも使用できます。  
  
```xml  
<object property="{ThemeDictionary AssemblyName=assemblyUri}" ... />  
```  
  
 詳細出力の使用は、複数の設定可能プロパティを持つ拡張機能や、一部のプロパティがオプションである場合に役立ちます。 `ThemeDictionary` には、必須の設定可能プロパティが 1 つしか存在しないため、このような詳細出力の使用は一般的ではありません。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] の [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサの実装では、このマークアップ拡張の処理は <xref:System.Windows.ThemeDictionaryExtension> クラスによって定義されています。  
  
 `ThemeDictionary` はマークアップ拡張機能です。 一般にマークアップ拡張機能を実装するのは、属性値をリテラル値やハンドラー名以外にエスケープする要件が存在し、その要件の適用範囲がグローバルで、特定の型やプロパティに型コンバーターを適用するだけにとどまらない場合です。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のすべてのマークアップ拡張では、それぞれの属性構文で { と } の 2 つの記号が使用されます。これは規約であり、これに従って [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、マークアップ拡張で属性を処理する必要があることが認識されます。 詳細については、「[マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目

- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [マークアップ拡張機能と WPF XAML](markup-extensions-and-wpf-xaml.md)
- [WPF アプリケーションのリソース ファイル、コンテンツ ファイル、およびデータ ファイル](../app-development/wpf-application-resource-content-and-data-files.md)
