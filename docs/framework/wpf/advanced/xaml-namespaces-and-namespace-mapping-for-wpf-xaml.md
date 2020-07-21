---
title: XAML 名前空間と名前空間マッピング
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom classes [WPF], mapping namespaces to
- XAML [WPF], namespaces
- namespace mapping [WPF]
- assemblies [WPF], mapping namespaces to
- mapping namespaces [WPF]
- XAML [WPF], namespace mapping
- classes [WPF], mapping namespaces to
- namespaces [WPF]
ms.assetid: 5c0854e3-7470-435d-9fe2-93eec9d3634e
ms.openlocfilehash: 9b01643e8f8d77073595253580ebea60fabfd23b
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/12/2020
ms.locfileid: "79186234"
---
# <a name="xaml-namespaces-and-namespace-mapping-for-wpf-xaml"></a>XAML 名前空間および WPF XAML の名前空間の割り当て
このトピックでは、WPF XAML ファイルのルート タグでよく目にする 2 つの XAML 名前空間マッピングの存在と目的について詳しく説明します。 また、独自のコードや別のアセンブリ内で定義されている要素を使用するために、同様のマッピングを生成する方法についても説明します。  

## <a name="what-is-a-xaml-namespace"></a>XAML 名前空間とは  
 XAML 名前空間は、実際には XML 名前空間の概念を拡張したものです。 XAML 名前空間を指定する手法は、XML 名前空間の構文、URI を名前空間の識別子として使用する規則、同じマークアップ ソースから複数の名前空間を参照するための手段を提供するプレフィックスの使用などに依存します。 XML 名前空間の XAML 定義に追加された主な概念として、XAML 名前空間は、マークアップ使用の一意性の範囲を暗黙的に示し、特定の CLR 名前空間と参照アセンブリによってマークアップ エンティティがサポートされる可能性のある方法にも影響を与えます。 この 2 つ目の考慮事項は、XAML スキーマ コンテキストの概念によっても影響を受けます。 ただし、WPF での XAML 名前空間の使用方法については、一般に、既定の XAML 名前空間、XAML 言語の名前空間、および XAML マークアップによって特定のバッキング CLR 名前空間と参照アセンブリに直接マップされる XAML 名前空間に関して、XAML 名前空間を考えることができます。  
  
<a name="The_WPF_and_XAML_Namespace_Declarations"></a>
## <a name="the-wpf-and-xaml-namespace-declarations"></a>WPF と XAML 名前空間の宣言  
 多くの XAML ファイルのルート タグでの名前空間宣言には、通常、2 つの XML 名前空間宣言があります。 1 つ目の宣言では、WPF クライアントとフレームワークの全体的な XAML 名前空間が既定値としてマップされます。  
  
 `xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"`  
  
 2 つ目の宣言では、別の XAML 名前空間がマップされ、その名前空間が (通常は) `x:` プレフィックスにマップされます。  
  
 `xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"`  
  
 これらの宣言の間には、`x:` プレフィックス マッピングは XAML 言語定義の一部である組み込みをサポートし、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] は、XAML を言語として使用し、XAML 用にオブジェクトのボキャブラリを定義する 1 つの実装である、という関係があります。 WPF のボキャブラリの使用は、XAML の組み込みの使用法よりはるかに一般的であるため、WPF のボキャブラリは既定値としてマップされます。  
  
 この SDK 内の言語機能のプロジェクト テンプレート、サンプル コード、およびドキュメントは、XAML 言語組み込みサポートのマッピングに対する `x:` プレフィックスの規則に従っています。 XAML 名前空間では、基本的な WPF アプリケーションでも必要な、よく使用される多くの機能が定義されています。 たとえば、部分クラスを使用して XAML ファイルにコードビハインドを結合するには、関連する XAML ファイルのルート要素の `x:Class` 属性として、そのクラスを指定する必要があります。 または、キー付きリソースとしてアクセスする XAML ページで定義されているすべての要素で、`x:Key` 属性を設定する必要があります。 XAML のこれらおよび他の側面の詳細については、「[XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)」または「[XAML 構文の詳細](xaml-syntax-in-detail.md)」を参照してください。  
  
<a name="Mapping_To_Custom_Classes_and_Assemblies"></a>
## <a name="mapping-to-custom-classes-and-assemblies"></a>カスタム クラスとアセンブリへのマッピング  
 標準の WPF および XAML 組み込み XAML 名前空間がプレフィックスにマップされる方法と同じように、`xmlns` プレフィックス宣言内の一連のトークンを使用して、XML 名前空間をアセンブリにマップできます。  
  
 構文では、次の名前付きトークンと値を使用できます。  
  
 `clr-namespace:` 要素として公開するパブリック型が含まれる、アセンブリ内で宣言されている CLR 名前空間。  
  
 `assembly=` 参照されている CLR 名前空間の一部または全部が含まれるアセンブリ。 通常、この値はパスではなくアセンブリの名前だけであり、拡張子 (.dll や .exe など) は含まれません。 そのアセンブリへのパスは、マップしようとしている XAML が含まれるプロジェクト ファイルでプロジェクト参照として設定する必要があります。 バージョン管理と厳密な名前の署名を組み込むには、`assembly` の値を、単純な文字列名ではなく、<xref:System.Reflection.AssemblyName> で定義されている文字列にすることができます。  
  
 `clr-namespace` トークンとその値を区切る文字がコロン (:) であることに注意してください。一方、`assembly` トークンとその値を区切る文字は等号 (=) です。 これら 2 つのトークンの間に使用する文字はセミコロンです。 また、宣言のどこにも空白文字を入れないでください。  
  
### <a name="a-basic-custom-mapping-example"></a>基本的なカスタム マッピングの例  
 次のコードは、カスタム クラスを定義する例です。  
  
```csharp  
namespace SDKSample {  
    public class ExampleClass : ContentControl {  
        public ExampleClass() {  
        ...  
        }  
    }  
}  
```  
  
```vb  
Namespace SDKSample  
    Public Class ExampleClass  
        Inherits ContentControl  
         ...  
        Public Sub New()  
        End Sub  
    End Class  
End Namespace  
```  
  
 このカスタム クラスは、プロジェクトの設定 (図には示されていません) に従って、`SDKSampleLibrary` という名前のライブラリにコンパイルされます。  
  
 このカスタム クラスを参照するには、現在のプロジェクトに対する参照として、それを含める必要もあります。これを行うには、通常、Visual Studio のソリューション エクスプローラーの UI を使用します。  
  
 クラスが含まれるライブラリを作成し、プロジェクトの設定でそれを参照したので、XAML でのルート要素の一部として、次のプレフィックス マッピングを追加できます。  
  
 `xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary"`  
  
 まとめると、次の XAML には、カスタム マッピングと共に一般的な既定のマッピングと x: マッピングがルート タグに含まれており、プレフィックス付き参照を使用して、その UI で `ExampleClass` をインスタンス化します。  
  
```xaml  
<Page x:Class="WPFApplication1.MainPage"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:custom="clr-namespace:SDKSample;assembly=SDKSampleLibrary">  
  ...  
  <custom:ExampleClass/>  
...  
</Page>  
```  
  
### <a name="mapping-to-current-assemblies"></a>現在のアセンブリへのマッピング  
 `assembly` は、参照されている `clr-namespace` が、カスタム クラスを参照しているアプリケーション コードと同じアセンブリ内で定義されている場合は、省略できます。 または、等号の後に文字列トークンを明示せずに `assembly=` を指定しても同じです。  
  
 同じアセンブリ内で定義されている場合、カスタム クラスをページのルート要素として使用することはできません。 部分クラスをマップする必要はありません。アプリケーション内のページの部分クラスではないクラスを、XAML の要素として参照する場合にのみ、それをマップする必要があります。  
  
<a name="Mapping_CLR_Namespaces_to_XML_Namespaces_in_an"></a>
## <a name="mapping-clr-namespaces-to-xml-namespaces-in-an-assembly"></a>アセンブリ内の XML 名前空間に対する CLR 名前空間のマッピング  
 WPF では、複数の CLR 名前空間を 1 つの XAML 名前空間にマップするために XAML プロセッサによって使用される CLR 属性が定義されています。 この属性 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> は、アセンブリを生成するソース コードのアセンブリ レベルに配置します。 WPF アセンブリのソース コードでは、この属性を使用して、<xref:System.Windows> や <xref:System.Windows.Controls> などのさまざまな共通名前空間を、`http://schemas.microsoft.com/winfx/2006/xaml/presentation` 名前空間にマップします。  
  
 <xref:System.Windows.Markup.XmlnsDefinitionAttribute> は、XML/XAML 名前空間名と CLR 名前空間名の 2 つのパラメーターを受け取ります。 複数の <xref:System.Windows.Markup.XmlnsDefinitionAttribute> を使用して、複数の CLR 名前空間を同じ XML 名前空間にマップすることができます。 マップした後は、必要に応じて、それらの名前空間のメンバーを、部分クラスの分離コード ページで適切な `using` ステートメントを指定することにより、完全修飾なしで参照することもできます。 詳細については、「<xref:System.Windows.Markup.XmlnsDefinitionAttribute>」を参照してください。  
  
## <a name="designer-namespaces-and-other-prefixes-from-xaml-templates"></a>XAML テンプレートからのデザイナー名前空間とその他のプレフィックス  
 WPF XAML に対して開発環境ツールやデザイン ツールを使用している場合、XAML マークアップ内に他の定義済みの XAML 名前空間やプレフィックスがあることに気付く場合があります。  
  
 Visual Studio 用の WPF デザイナーでは、通常はプレフィックス `d:` にマップされるデザイナー名前空間が使用されます。 さらに最近の WPF 用プロジェクト テンプレートでは、Visual Studio 用 WPF デザイナーと他のデザイン環境の間での XAML の交換をサポートするため、この XAML 名前空間があらかじめマップされている場合があります。 このデザイン XAML 名前空間は、デザイナーの XAML ベースの UI をラウンドトリップする間もデザイン状態を持続させるために使用されます。 また、デザイナーで実行時データ ソースを有効にする `d:IsDataSource` などの機能にも使用されます。  
  
 マップされていると思われるもう 1 つのプレフィックスは `mc:` です。 `mc:` は、マークアップの互換性のためのものであり、必ずしも XAML 固有ではないマークアップ互換性パターンが利用されています。 ある程度まで、マークアップ互換性機能を使用して、フレームワーク間や、バッキング実装の他の境界間での XAML の交換、XAML スキーマ コンテキスト間での作業、デザイナーでの制限されたモードに対する互換性の提供などを行うことができます。 マークアップ互換性の概念と WPF との関係の詳細については、「[マークアップの互換性 (mc:) 言語機能](markup-compatibility-mc-language-features.md)」を参照してください。  
  
## <a name="wpf-and-assembly-loading"></a>WPF とアセンブリの読み込み  
 WPF の XAML スキーマ コンテキストは WPF アプリケーション モデルと統合され、そのモデルでは CLR で定義された <xref:System.AppDomain> の概念が使用されています。 WPF での <xref:System.AppDomain> と他の要素の使用に基づいて、実行時またはデザイン時に、XAML スキーマ コンテキストによって、アセンブリの読み込み方法または型の検索方法が解釈される流れを、次に示します。  
  
1. 最後に読み込まれたアセンブリから始めて、<xref:System.AppDomain> を反復処理し、既に読み込まれているアセンブリから、名前のすべての部分が一致するものを検索します。  
  
2. 名前が修飾されている場合は、修飾された名前に対して <xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> を呼び出します。  
  
3. 修飾された名前の短い名前と公開キー トークンが、マークアップの読み込み元のアセンブリと一致する場合は、そのアセンブリを返します。  
  
4. 短い名前と公開キー トークンを使用して、<xref:System.Reflection.Assembly.Load%28System.String%29?displayProperty=nameWithType> を呼び出します。  
  
5. 名前が修飾されていない場合は、<xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=nameWithType> を呼び出します。  
  
 Loose XAML では、ステップ 3 は使用されません。読み込み元のアセンブリはありません。  
  
 WPF 用にコンパイルされた XAML (XamlBuildTask で生成されたもの) では、<xref:System.AppDomain> から既に読み込まれているアセンブリは使用されません (ステップ 1)。 また、XamlBuildTask の出力で名前を修飾してはならないため、ステップ 5 は適用されません。  
  
 (PresentationBuildTask によって生成される) コンパイル済みの BAML ではすべてのステップが使用されますが、BAML には修飾されていないアセンブリ名を含めることはできません。  
  
## <a name="see-also"></a>関連項目

- [XML 名前空間について](https://docs.microsoft.com/previous-versions/aa468565(v=msdn.10))
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
