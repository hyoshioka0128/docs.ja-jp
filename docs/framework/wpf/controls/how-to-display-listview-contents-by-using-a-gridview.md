---
title: '方法: GridView を使用して ListView コンテンツを表示する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], displaying contents with GridView
- GridView [WPF], displaying ListView contents
ms.assetid: 5bc1e767-ab46-4f14-bd41-3d5d39e1d000
ms.openlocfilehash: 9b467c95d541c326a41d1ed4bd9eb5c87e25bd5c
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910495"
---
# <a name="how-to-display-listview-contents-by-using-a-gridview"></a>方法: GridView を使用して ListView コンテンツを表示する
この例からは、<xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.GridView> 表示モードを定義する方法がわかります。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.GridViewColumn> オブジェクトを指定することによって <xref:System.Windows.Controls.GridView> の表示モードを定義できます。 次の例では、<xref:System.Windows.Controls.ListView> コントロールに指定されているデータ コンテンツにバインドされる <xref:System.Windows.Controls.GridViewColumn> オブジェクトを定義する方法を示します。 この <xref:System.Windows.Controls.GridView> の例では、<xref:System.Windows.Controls.ListView> コントロールの <xref:System.Windows.Controls.ItemsControl.ItemsSource%2A> として設定される `EmployeeInfoDataSource` の `FirstName`、`LastName`、`EmployeeNumber` フィールドにマッピングされる 3 つの <xref:System.Windows.Controls.GridViewColumn> オブジェクトが指定されます。  
  
 [!code-xaml[ListViewCode#ListViewEmployee](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewCode/CSharp/Window1.xaml#listviewemployee)]  
  
 この例がどのように表示されるかを次の図に示します。  
  
 ![GridView の出力が表示された ListView のスクリーンショット。](./media/gridview-overview/listview-gridview-output.jpg)  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
- [方法トピック](listview-how-to-topics.md)
