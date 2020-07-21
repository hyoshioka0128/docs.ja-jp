---
title: '方法: ドラッグされた GridView 列ヘッダーのスタイルを作成する'
ms.date: 03/30/2017
helpviewer_keywords:
- ListView controls [WPF], styling
ms.assetid: 0b999645-0313-4b33-80b9-19ece08b5459
ms.openlocfilehash: dbcdd38e0397b8e637aff962420a2959f33203df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910885"
---
# <a name="how-to-create-a-style-for-a-dragged-gridview-column-header"></a>方法: ドラッグされた GridView 列ヘッダーのスタイルを作成する
この例からは、ユーザーが列の位置を変更するとき、ドラッグした <xref:System.Windows.Controls.GridViewColumnHeader> の外観を変更する方法がわかります。  
  
## <a name="example"></a>例  
 その表示モードに <xref:System.Windows.Controls.GridView> が使用される <xref:System.Windows.Controls.ListView> で列ヘッダーを別の場所にドラッグすると、列が新しい位置に移動します。 列ヘッダーをドラッグしている間、元のヘッダー以外に、フロート状態のヘッダーのコピーが表示されます。 <xref:System.Windows.Controls.GridView> の列ヘッダーは <xref:System.Windows.Controls.GridViewColumnHeader> によって表されます。  
  
 このフロート状態と元のヘッダーの両方の外観をカスタマイズするには、<xref:System.Windows.Controls.ControlTemplate.Triggers%2A> を設定して <xref:System.Windows.Controls.GridViewColumnHeader> <xref:System.Windows.Style> を変更します。 これらの <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> は、<xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> プロパティ値が `true` で、<xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> プロパティ値が <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating> のときに適用されます。  
  
 マウスが <xref:System.Windows.Controls.GridViewColumnHeader> の上にあるとき、ユーザーがマウス ボタンを押したままにすると、<xref:System.Windows.Controls.Primitives.ButtonBase.IsPressed%2A> プロパティ値が `true` に変わります。 同様に、ユーザーがドラッグ操作を開始すると、<xref:System.Windows.Controls.GridViewColumnHeader.Role%2A> プロパティが <xref:System.Windows.Controls.GridViewColumnHeaderRole.Floating> に変わります。  
  
 次の例に、ユーザーが列を新しい位置にドラッグするときに、フロート状態と元のヘッダーの <xref:System.Windows.Controls.Control.Foreground%2A> 色と <xref:System.Windows.Controls.Control.Background%2A> 色を変えるように <xref:System.Windows.Controls.ControlTemplate.Triggers%2A> を設定する方法を示します。  
  
 [!code-xaml[ListViewHeaderRoleStyle#GVCHControlTemplateStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplatestart)]  
[!code-xaml[ListViewHeaderRoleStyle#ControlTemplateTriggersStart](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersstart)]  
[!code-xaml[ListViewHeaderRoleStyle#IsPressed](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#ispressed)]  
[!code-xaml[ListViewHeaderRoleStyle#Floating](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#floating)]  
[!code-xaml[ListViewHeaderRoleStyle#ControlTemplateTriggersEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#controltemplatetriggersend)]  
[!code-xaml[ListViewHeaderRoleStyle#GVCHControlTemplateEnd](~/samples/snippets/csharp/VS_Snippets_Wpf/ListViewHeaderRoleStyle/CS/Window1.xaml#gvchcontroltemplateend)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.GridViewColumnHeader>
- <xref:System.Windows.Controls.GridViewColumnHeaderRole>
- <xref:System.Windows.Controls.ListView>
- <xref:System.Windows.Controls.GridView>
- [方法トピック](listview-how-to-topics.md)
- [ListView の概要](listview-overview.md)
- [GridView の概要](gridview-overview.md)
