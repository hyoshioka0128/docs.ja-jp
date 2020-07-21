---
title: インライン スタイルおよびテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- inline templates [WPF]
- styles [WPF], inline
- templates [WPF], inline
- inline styles [WPF]
ms.assetid: 69a1a3f9-acb5-4e2c-9c43-2e376c055ac4
ms.openlocfilehash: b88ef444283f4e1e85009c59b39f3cc41965d300
ms.sourcegitcommit: 944ddc52b7f2632f30c668815f92b378efd38eea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2019
ms.locfileid: "73460003"
---
# <a name="inline-styles-and-templates"></a>インライン スタイルおよびテンプレート
[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] には、リソース内の要素の外観を定義して複数回使用できるようにする方法として、<xref:System.Windows.Style> オブジェクトとテンプレート オブジェクト (<xref:System.Windows.FrameworkTemplate> サブクラス) が用意されています。 このため、型 <xref:System.Windows.Style> と型 <xref:System.Windows.FrameworkTemplate> を取得する [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の属性では、新しいものをインラインで定義するのではなく、既存のスタイルとテンプレートへのリソース参照をほぼ常に作成します。  
  
## <a name="limitations-of-inline-styles-and-templates"></a>インライン スタイルとテンプレートの制限事項  
 [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] では、次の 2 つの方法のいずれかで、スタイルとテンプレートのプロパティを技術的に設定します。 属性構文を使用すると、`<`*object*`Style="{StaticResource`*myResourceKey*`}" .../>` など、リソース内で定義されたスタイルを参照できます。 または、プロパティ要素構文を使用して、次のようにインラインでスタイルを定義することもできます。  
  
 `<` *object* `>`  
  
 `<` *object* `.Style>`  
  
 `<` `Style`  `.../>`  
  
 `</` *object* `.Style>`  
  
 `</` *object* `>`  
  
 属性を使用する方が、より一般的です。 インラインで定義され、リソースで定義されていないスタイルは、必然的に包含要素のみにスコープが設定されます。また、リソース キーがないため、簡単に再利用することはできません。 一般に、リソース定義のスタイルは、高い汎用性と利便性を備え、コード内のプログラム ロジックをマークアップのデザインから分離するという、一般的な [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] プログラミング モデルの原則に準拠しています。  
  
 通常、スタイルまたはテンプレートをインラインで設定する理由はありません。その場所で、そのスタイルまたはテンプレートを使用するのみの場合も同様です。 スタイルまたはテンプレートを取得できる要素のほとんどは、コンテンツ プロパティとコンテンツ モデルもサポートします。 スタイルまたはテンプレートを使用して作成した論理ツリーのみを使用する場合は、ダイレクト マークアップ内の同等の子要素を使用すると、そのコンテンツ プロパティを塗りつぶしやすくなります。 これにより、スタイルとテンプレートのメカニズムが完全にバイパスされます。  
  
 オブジェクトを返すマークアップ拡張によって有効になったその他の構文は、スタイルやテンプレートにも使用できます。 それら 2 つの拡張には、[TemplateBinding](templatebinding-markup-extension.md) および <xref:System.Windows.Data.Binding> というシナリオが考えられます。  
  
## <a name="see-also"></a>関連項目

- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
