---
title: メニューのスタイルとテンプレート
ms.date: 03/30/2017
helpviewer_keywords:
- styles [WPF], Menu
- ControlTemplate [WPF], Menu
- Menu [WPF], styles and templates
- states [WPF], Menu
- templates [WPF], Menu
- parts [WPF], Menu
ms.assetid: b89da183-9b87-42c6-ac53-731a42c7b09e
ms.openlocfilehash: 3ce0be1fdeeee1465c2facb414cc7a081b268eb5
ms.sourcegitcommit: 17ee6605e01ef32506f8fdc686954244ba6911de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74283473"
---
# <a name="menu-styles-and-templates"></a>メニューのスタイルとテンプレート
このトピックでは、<xref:System.Windows.Controls.Menu> コントロールのスタイルとテンプレートについて説明します。 <xref:System.Windows.Controls.ControlTemplate>の既定値を変更して外観を制御します。 詳細については、「[コントロールのためにテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)」をご覧ください。  
  
## <a name="menu-parts"></a>Menu のパーツ  
 <xref:System.Windows.Controls.Menu> コントロールに名前付きパーツはありません。  
  
 <xref:System.Windows.Controls.Menu> の <xref:System.Windows.Controls.ControlTemplate> を作成する場合、テンプレートで、<xref:System.Windows.Controls.ScrollViewer> 内に <xref:System.Windows.Controls.ItemsPresenter> を含めることができます (<xref:System.Windows.Controls.ItemsPresenter> により、<xref:System.Windows.Controls.Menu> の各項目が表示されます。<xref:System.Windows.Controls.ScrollViewer> で、コントロール内のスクロールを有効にします)。  <xref:System.Windows.Controls.ItemsPresenter> が <xref:System.Windows.Controls.ScrollViewer> の直接の子でない場合は、<xref:System.Windows.Controls.ItemsPresenter> に `ItemsPresenter` という名前を付ける必要があります。  
  
## <a name="menu-states"></a>Menu の状態  
 次の表は、<xref:System.Windows.Controls.Menu> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがある `true` です。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがない `true` です。|  
  
## <a name="menuitem-parts"></a>MenuItem のパーツ  
 次の表は、<xref:System.Windows.Controls.Menu> コントロールの名前付きパーツの一覧を示します。  
  
|パーツ|種類|説明|  
|-|-|-|  
|PART_Popup|<xref:System.Windows.Controls.Primitives.Popup>|サブメニューの領域。|  
  
 <xref:System.Windows.Controls.MenuItem> の <xref:System.Windows.Controls.ControlTemplate> を作成する場合、テンプレートで、<xref:System.Windows.Controls.ScrollViewer> 内に <xref:System.Windows.Controls.ItemsPresenter> を含めることができます (<xref:System.Windows.Controls.ItemsPresenter> により、<xref:System.Windows.Controls.MenuItem> の各項目が表示されます。<xref:System.Windows.Controls.ScrollViewer> で、コントロール内のスクロールを有効にします)。  <xref:System.Windows.Controls.ItemsPresenter> が <xref:System.Windows.Controls.ScrollViewer> の直接の子でない場合は、<xref:System.Windows.Controls.ItemsPresenter> に `ItemsPresenter` という名前を付ける必要があります。  
  
## <a name="menuitem-states"></a>MenuItem の状態  
 次の表は、<xref:System.Windows.Controls.MenuItem> コントロールの表示状態の一覧を示します。  
  
|VisualState 名|VisualStateGroup 名|説明|  
|-|-|-|  
|有効|ValidationStates|このコントロールで <xref:System.Windows.Controls.Validation> クラスを使用し、<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは `false` です。|  
|InvalidFocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがある `true` です。|  
|InvalidUnfocused|ValidationStates|<xref:System.Windows.Controls.Validation.HasError%2A?displayProperty=nameWithType> 添付プロパティは、コントロールにフォーカスがない `true` です。|  
  
## <a name="menu-and-menuitem-controltemplate-example"></a>Menu および MenuItem の ControlTemplate の例  
 次の例は、<xref:System.Windows.Controls.Menu> コントロールの <xref:System.Windows.Controls.ControlTemplate> を定義する方法を示しています。  
  
 [!code-xaml[ControlTemplateExamples#Menu](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menu)]  
  
 次の例は、<xref:System.Windows.Controls.MenuItem> コントロールの <xref:System.Windows.Controls.ControlTemplate> を定義する方法を示しています。  
  
 [!code-xaml[ControlTemplateExamples#MenuItem](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuitem)]  
  
 次の例は、前の例で使用した `MenuScrollViewer` を定義しています。  
  
 [!code-xaml[ControlTemplateExamples#MenuScrollViewer](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/menu.xaml#menuscrollviewer)]  
  
 <xref:System.Windows.Controls.ControlTemplate> の例では、次のリソースを 1 つ以上使用します。  
  
 [!code-xaml[ControlTemplateExamples#Resources](~/samples/snippets/csharp/VS_Snippets_Wpf/ControlTemplateExamples/CS/resources/shared.xaml#resources)]  
  
 完全なサンプルについては、[Styling with ControlTemplates Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Styles%20&%20Templates/IntroToStylingAndTemplating)を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.FrameworkElement.Style%2A>
- <xref:System.Windows.Controls.ControlTemplate>
- [コントロールのスタイルとテンプレート](control-styles-and-templates.md)
- [コントロールのカスタマイズ](control-customization.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [コントロールのためのテンプレートを作成する](../../../desktop-wpf/themes/how-to-create-apply-template.md)
