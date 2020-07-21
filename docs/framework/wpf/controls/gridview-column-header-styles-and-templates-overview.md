---
title: GridView の列ヘッダー スタイルおｙびテンプレートの概要
ms.date: 03/30/2017
helpviewer_keywords:
- column headers [WPF], customizing
- ListView controls [WPF], GridView column header styles
- controls [WPF], ListView
- headers [WPF], customizing
- GridView view mode [WPF], customizing column headers
ms.assetid: 74835674-a39e-4ab5-9418-ad7f6ab7b956
ms.openlocfilehash: 83643d8acea706bad439683702e4228d240b97bc
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61911366"
---
# <a name="gridview-column-header-styles-and-templates-overview"></a>GridView の列ヘッダー スタイルおｙびテンプレートの概要
この概要では、<xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.GridView> ビュー モードで、列ヘッダーのカスタマイズに使用するプロパティの優先順位について説明します。  
  
## <a name="customizing-a-column-header-in-a-gridview"></a>GridView での列ヘッダーのカスタマイズ  
 <xref:System.Windows.Controls.GridView> の列ヘッダーのコンテンツ、レイアウト、およびスタイルを定義するプロパティは、多くの関連するクラスにあります。 これらのプロパティの一部には、類似した機能または同じ機能があります。  
  
 次の表の行では、同じ機能を実行するプロパティのグループを示しています。 これらのプロパティを使用すると、<xref:System.Windows.Controls.GridView> で列ヘッダーをカスタマイズできます。 関連するプロパティの優先順位は右から左で、最も右の列のプロパティが最も優先順位が高くなります。 たとえば、<xref:System.Windows.Controls.GridViewColumnHeader> オブジェクトに対して <xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> が設定されていて、関連付けられている <xref:System.Windows.Controls.GridViewColumn> に <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A> が設定されている場合、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> が優先されます。 このシナリオでは、<xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A> による影響はありません。  
  
 **GridView の列ヘッダーの関連プロパティ**  
  
|||||  
|-|-|-|-|  
|**クラス**|<xref:System.Windows.Controls.GridView>|<xref:System.Windows.Controls.GridViewColumn>|<xref:System.Windows.Controls.GridViewColumnHeader>|  
|**コンテキスト メニューのプロパティ**|<xref:System.Windows.Controls.GridView.ColumnHeaderContextMenu%2A>|利用不可|<xref:System.Windows.FrameworkElement.ContextMenu%2A>|  
|**ToolTip**<br /><br /> **プロパティ**|<xref:System.Windows.Controls.GridView.ColumnHeaderToolTip%2A>|利用不可|<xref:System.Windows.FrameworkElement.ToolTip%2A>|  
|**ヘッダー テンプレート**<br /><br /> **プロパティ**|<xref:System.Windows.Controls.GridView.ColumnHeaderTemplate%2A> <sup>1</sup>/<br /><br /> <xref:System.Windows.Controls.GridView.ColumnHeaderTemplateSelector%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderTemplate%2A> <sup>1</sup>/<br /><br /> <xref:System.Windows.Controls.GridViewColumn.HeaderTemplateSelector%2A>|<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> <sup>1</sup>/<br /><br /> <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A>|  
|**スタイル プロパティ**|<xref:System.Windows.Controls.GridView.ColumnHeaderContainerStyle%2A>|<xref:System.Windows.Controls.GridViewColumn.HeaderContainerStyle%2A>|<xref:System.Windows.FrameworkElement.Style%2A>|  
  
 <sup>1</sup>**ヘッダー テンプレートのプロパティ**では、テンプレートとテンプレート セレクターの両プロパティを設定した場合、テンプレート プロパティが優先されます。 たとえば、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> と <xref:System.Windows.Controls.ContentControl.ContentTemplateSelector%2A> の両プロパティを設定した場合、<xref:System.Windows.Controls.ContentControl.ContentTemplate%2A> プロパティが優先されます。  
  
## <a name="see-also"></a>関連項目

- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
