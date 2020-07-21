---
title: '方法: システム パラメーター キーを使用する'
ms.date: 03/30/2017
helpviewer_keywords:
- resource keys [WPF], SystemParameters class
- classes [WPF], SystemParameters
ms.assetid: 77571283-d16c-45bb-9f69-cafbbf72b21e
ms.openlocfilehash: edacb4b98ab01f081f668dc3374f6588492210d9
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/22/2019
ms.locfileid: "69918367"
---
# <a name="how-to-use-system-parameters-keys"></a>方法: システム パラメーター キーを使用する
システム リソースは、開発者がシステム設定と一貫性のあるビジュアルを作成できるようにするために、多くのシステム メトリックをリソースとして公開します。 <xref:System.Windows.SystemParameters> は、システム パラメーター値および値にバインドされるリソース キーの両方を含むクラスです (<xref:System.Windows.SystemParameters.FullPrimaryScreenHeight%2A>、<xref:System.Windows.SystemParameters.FullPrimaryScreenHeightKey%2A> など)。 システム パラメーター メトリックは、静的なリソースとしても、動的なリソースとしても使用できます。 アプリケーションの実行時にパラメーター メトリックを自動的に更新する場合は、動的リソースを使用します。それ以外の場合は、静的リソースを使用します。  
  
> [!NOTE]
> 動的リソースのプロパティ名には、キーワード *Key* が追加されています。  
  
 次の例では、ボタンのスタイル設定やカスタマイズを行うために、システム パラメーター動的リソースにアクセスして使用する方法を示します。 この [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の例では、ボタンの幅と高さに <xref:System.Windows.SystemParameters> の値を割り当てて、ボタンのサイズを設定します。  
  
## <a name="example"></a>例  
 [!code-xaml[SystemRes_snip#ParameterDynamicResources](~/samples/snippets/csharp/VS_Snippets_Wpf/SystemRes_snip/CSharp/MyApp.xaml#parameterdynamicresources)]  
  
## <a name="see-also"></a>関連項目

- [システム ブラシで領域を塗りつぶす](../graphics-multimedia/how-to-paint-an-area-with-a-system-brush.md)
- [SystemFonts を使用する](how-to-use-systemfonts.md)
- [SystemParameters を使用する](how-to-use-systemparameters.md)
