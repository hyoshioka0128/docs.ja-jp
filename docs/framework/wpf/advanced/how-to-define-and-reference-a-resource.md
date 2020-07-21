---
title: '方法: リソースを定義および参照する'
ms.date: 03/30/2017
helpviewer_keywords:
- resources [WPF], defining
- defining resources [WPF]
- resources [WPF], referencing
- referencing resources [WPF]
ms.assetid: b86b876b-0a10-489b-9a5d-581ea9b32406
ms.openlocfilehash: e33c86b03d8b18113f3a15b3ab251753958ff5b2
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646507"
---
# <a name="how-to-define-and-reference-a-resource"></a>方法: リソースを定義および参照する

この例では、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の属性を使用してリソースを定義し、それを参照する方法を示します。

## <a name="example"></a>例

次の例では、2 種類のリソースを定義します。<xref:System.Windows.Media.SolidColorBrush> リソースと、いくつかの <xref:System.Windows.Style> リソースです。 <xref:System.Windows.Media.SolidColorBrush> リソースの `MyBrush` は、それぞれが <xref:System.Windows.Media.Brush> 型の値を受け取るいくつかのプロパティの値を提供するために使用されます。 <xref:System.Windows.Style> リソースの `PageBackground`、`TitleText`、`Label` は、特定のコントロールの種類を対象とします。 スタイル リソースがリソース キーによって参照され、[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で定義されているいくつかの特定のコントロール要素の <xref:System.Windows.FrameworkElement.Style%2A> プロパティを設定するために使用されると、スタイルによって対象のコントロールにさまざまなプロパティが設定されます。

`Label` スタイルのセッター内のプロパティの 1 つで、前に定義した `MyBrush` リソースも参照されていることに注意してください。 これは一般的な手法ですが、リソースは指定された順序で解析され、リソース ディクショナリに追加されることに注意することが重要です。 また、[StaticResource マークアップ拡張](staticresource-markup-extension.md)を使用して別のリソース内から参照する場合も、リソースはディクショナリ内で見つかった順序で要求されます。 参照するリソースがリソース コレクション内で定義されている場所が、リソースを要求する場所より前であることを確認します。 必要に応じて、代わりに [DynamicResource マークアップ拡張](dynamicresource-markup-extension.md)を使用して実行時にリソースを参照することで、リソース参照の厳密な作成順序を回避できますが、この DynamicResource 手法はパフォーマンスに影響することに注意する必要があります。 詳細については、[XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。

[!code-xaml[FEResource#XAML](~/samples/snippets/csharp/VS_Snippets_Wpf/FEResource/CS/default.xaml#xaml)]

## <a name="see-also"></a>関連項目

- [XAML リソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
