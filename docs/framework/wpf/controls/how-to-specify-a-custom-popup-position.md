---
title: '方法: ポップアップのカスタム位置を指定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Popup control [WPF], specifying custom position
ms.assetid: 28c24f39-d3aa-4ee2-b950-384b4a5dab92
ms.openlocfilehash: b48dedc044b418062642af5c5bb40afab78a3c97
ms.sourcegitcommit: 1c1a1f9ec0bd1efb3040d86a79f7ee94e207cca5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2020
ms.locfileid: "80635748"
---
# <a name="how-to-specify-a-custom-popup-position"></a>方法: ポップアップのカスタム位置を指定する
この例では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティが <xref:System.Windows.Controls.Primitives.PlacementMode.Custom> に設定されているときに、<xref:System.Windows.Controls.Primitives.Popup> コントロールのカスタム位置を指定する方法を示します。  
  
## <a name="example"></a>例  
 <xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティが <xref:System.Windows.Controls.Primitives.PlacementMode.Custom> に設定されていると、<xref:System.Windows.Controls.Primitives.Popup> では定義されている <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> デリゲートのインスタンスが呼び出されます。 このデリゲートでは、ターゲット領域の左上隅と <xref:System.Windows.Controls.Primitives.Popup> の左上隅を基準として、一連の可能なポイントが返されます。 <xref:System.Windows.Controls.Primitives.Popup> は、視認性が最もよい場所に配置されます。  
  
 次の例では、<xref:System.Windows.Controls.Primitives.Popup.Placement%2A> プロパティを <xref:System.Windows.Controls.Primitives.PlacementMode.Custom> に設定することで <xref:System.Windows.Controls.Primitives.Popup> の位置を定義する方法が示されています。 また、<xref:System.Windows.Controls.Primitives.Popup> を配置するために <xref:System.Windows.Controls.Primitives.CustomPopupPlacementCallback> デリゲートを作成して割り当てる方法も示されています。  コールバック デリゲートでは、2 つの <xref:System.Windows.Controls.Primitives.CustomPopupPlacement> オブジェクトが返されます。  最初の位置では <xref:System.Windows.Controls.Primitives.Popup> が画面の端で見えなくなる場合、<xref:System.Windows.Controls.Primitives.Popup> は 2 番目の位置に配置されます。  
  
 [!code-xaml[PopupCustomPlacement#CustomPlacement](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml#customplacement)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateInstance](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegateinstance)]
 [!code-vb[PopupCustomPlacement#DelegateInstance](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegateinstance)]  
  
 [!code-csharp[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/csharp/VS_Snippets_Wpf/PopupCustomPlacement/CSharp/Window1.xaml.cs#delegatedefinition)]
 [!code-vb[PopupCustomPlacement#DelegateDefinition](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PopupCustomPlacement/visualbasic/window1.xaml.vb#delegatedefinition)]  
  
 サンプル全体については、[ポップアップ配置のサンプル](https://github.com/dotnet/docs/tree/master/samples/snippets/csharp/VS_Snippets_Wpf/PopupPositionSnippet/CS)を参照してください。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Primitives.Popup>
- [ポップアップの概要](popup-overview.md)
- [ハウツー記事](popup-how-to-topics.md)
