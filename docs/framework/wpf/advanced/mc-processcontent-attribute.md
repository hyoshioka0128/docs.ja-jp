---
title: mc:ProcessContent 属性
ms.date: 03/30/2017
helpviewer_keywords:
- mc:ProcessContent attribute
- XAML [WPF], mc:ProcessContent attribute
ms.assetid: 2689b2c8-b4dc-4b71-b9bd-f95e619122d7
ms.openlocfilehash: bcf55668bdc70902e346c401549a88f6ccb9072e
ms.sourcegitcommit: 011314e0c8eb4cf4a11d92078f58176c8c3efd2d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2020
ms.locfileid: "77095126"
---
# <a name="mcprocesscontent-attribute"></a>mc:ProcessContent 属性
[mc:Ignorable 属性](mc-ignorable-attribute.md)を指定することで直接の親要素が [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサによって無視される場合でも、関連する親要素によってコンテンツが処理される必要がある [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] 要素を指定します。 `mc:ProcessContent` 属性は、カスタムの名前空間マッピングと [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] のバージョン管理の両方で、マークアップ互換性をサポートします。  
  
## <a name="xaml-attribute-usage"></a>XAML 属性の使用方法  
  
```xaml  
<object  
  xmlns:ignorablePrefix="ignorableUri"  
  xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"  
  mc:Ignorable="ignorablePrefix"...  
  mc:ProcessContent="ignorablePrefix:ThisElementCanBeIgnored"  
>  
    <ignorablePrefix:ThisElementCanBeIgnored>  
        [content]  
    </ignorablePrefix:ThisElementCanBeIgnored>  
</object>  
```  
  
## <a name="xaml-values"></a>XAML 値  
  
|||  
|-|-|  
|*ignorablePrefix*|XML 1.0 仕様に従う有効なプレフィックス文字列。|  
|*ignorableUri*|XML 1.0 仕様に従う、名前空間を指定するための有効な URI。|  
|*ThisElementCanBeIgnored*|基になる型を解決できない場合に、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] プロセッサ実装によって無視できる要素。|  
|*[content]*|*ThisElementCanBeIgnored* は無視可能とマークされています。 プロセッサによってその要素が無視された場合、 *[content]* は *object* によって処理されます。|  
  
## <a name="remarks"></a>Remarks  
 既定で [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、無視された要素内のコンテンツは無視されます。 `mc:ProcessContent` を使用して特定の要素を指定すると、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] プロセッサでは、無視された要素内のコンテンツが引き続き処理されます。 通常、これは、コンテンツが複数のタグ内に入れ子にされ、少なくとも 1 つのタグが無視可能で、少なくとも 1 つは無視可能ではない場合に使用されます。ません。  
  
 スペース区切りを使用して、属性に複数のプレフィックスを指定できます (例: `mc:ProcessContent="ignore:Element1 ignore:Element2"`)。  
  
 `http://schemas.openxmlformats.org/markup-compatibility/2006` 名前空間には、SDK のこの領域ではドキュメント化されていない他の要素と属性を定義します。 詳細については、[XML マークアップ互換性仕様](https://docs.microsoft.com/office/open-xml/introduction-to-markup-compatibility#markup-compatibility-in-the-open-xml-file-formats-specification)に関するページを参照してください。  
  
## <a name="see-also"></a>関連項目

- [mc:Ignorable 属性](mc-ignorable-attribute.md)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
