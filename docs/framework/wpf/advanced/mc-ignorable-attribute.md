---
title: mc:Ignorable 属性
ms.date: 03/30/2017
helpviewer_keywords:
- mc XML namespace prefix [WPF]
- mc:Ignorable attribute
- XML [WPF], mc namespace prefix
- XAML [WPF], mc:Ignorable attribute
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: acd9a6ef-b7ca-4146-abb6-60f3b366e9ec
ms.openlocfilehash: e14ab0ebc7d44e2792307b16c7c0581ff7a71bc6
ms.sourcegitcommit: 22be09204266253d45ece46f51cc6f080f2b3fd6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73740830"
---
# <a name="mcignorable-attribute"></a>mc:Ignorable 属性
マークアップ ファイルで検出されたどの XML 名前空間プレフィックスを [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサで無視できるかを指定します。 `mc:Ignorable` 属性は、カスタム名前空間のマッピングと [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のバージョン管理の両方で、マークアップ互換性をサポートします。  
  
## <a name="xaml-attribute-usage-single-prefix"></a>XAML 属性の使用 (1 つのプレフィックス)  
  
```xaml  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-attribute-usage-two-prefixes"></a>XAML 属性の使用 (2 つのプレフィックス)  
  
```xaml  
<object  
  xmlns:ignorablePrefix1="ignorableUri"  
  xmlns:ignorablePrefix2="ignorableUri2"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix1 ignorablePrefix2"...>  
    <ignorablePrefix1:ThisElementCanBeIgnored/>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|"*ignorablePrefix、ignorablePrefix1 など*"|XML 1.0 仕様に従って有効なプレフィックス文字列。|  
|*ignorableUri*|XML 1.0 仕様に従って名前空間を指定するための有効な URI。|  
|*ThisElementCanBeIgnored*|基になる型を解決できない場合に、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] プロセッサ実装によって無視できる要素。|  
  
## <a name="remarks"></a>Remarks  
 `mc` XML 名前空間プレフィックスは、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]互換性名前空間`http://schemas.openxmlformats.org/markup-compatibility/2006`をマッピングするときに使用する推奨プレフィックス規則です。  
  
 要素名のプレフィックス部分が `mc:Ignorable` として識別される要素または属性は、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサによって処理されるときにエラーを発生させません。 その属性が、基になる型またはプログラミング コンストラクトに解決できない場合、その要素は無視されます。 ただし、無視された要素でも、その要素が処理されなかったことの副作用として、追加の要素要件について別の解析エラーを生成する可能性があることにご注意ください。 たとえば、特定の要素コンテンツモデルでは、子要素が 1 つだけ必要になる場合がありますが、指定された子要素が `mc:Ignorable` プレフィックスに含まれており、指定された子要素を型に解決できない場合、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサによってエラーが発生する可能性があります。  
  
 `mc:Ignorable` は、識別子文字列への名前空間マッピングのみに適用されます。 `mc:Ignorable` は、アセンブリへの名前空間マッピングには適用されません。アセンブリは、CLR 名前空間とアセンブリを指定します (またはアセンブリとして現在の実行可能ファイルを既定とします)。  
  
 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサを実装する場合、`mc:Ignorable`として識別されるプレフィックスで修飾された要素または属性について、プロセッサ実装で、解析または処理エラーが発生しないようにする必要があります。 しかし、それでも、前に示した 1 つの子要素の例のように、要素が読み込めない、または処理できないために生じる二次的な結果として、プロセッサ実装で例外が発生する可能性があります。  
  
 既定では、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサは、無視された要素内のコンテンツを無視します。 ただし、追加の属性 [mc:ProcessContent 属性](mc-processcontent-attribute.md)を指定して、次に使用可能な親要素によって、無視された要素内のコンテンツの処理を続行するように要求することができます。  
  
 属性には、1 つ以上の空白文字を区切りとして使用して、複数のプレフィックスを指定できます (例: `mc:Ignorable="ignore1 ignore2"`)。  

 `http://schemas.openxmlformats.org/markup-compatibility/2006` 名前空間は、SDK のこの領域ではドキュメント化されていない他の要素および属性を定義します。 詳細については、[XML マークアップ互換性仕様](/office/open-xml/introduction-to-markup-compatibility#markup-compatibility-in-the-open-xml-file-formats-specification)に関するセクションを参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Markup.XamlReader>
- [PresentationOptions:Freeze 属性](presentationoptions-freeze-attribute.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [WPF のドキュメント](documents-in-wpf.md)
