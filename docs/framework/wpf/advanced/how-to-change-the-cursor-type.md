---
title: '方法: カーソルの種類を変更する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- mouse pointer [WPF], cursor type
- cursor (mouse pointer)
ms.assetid: 08c945a7-8ab0-4320-acf3-0b4955a344c2
ms.openlocfilehash: 5c9e6931f6addb62a51e44b06a159d4e7b1e5f8a
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61776676"
---
# <a name="how-to-change-the-cursor-type"></a>方法: カーソルの種類を変更する
この例では、特定の要素とアプリケーションでマウスポインターの <xref:System.Windows.Input.Cursor> を変更する方法を示しています。  
  
 この例は、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ファイルとコード ビハインド ファイルで構成されています。  
  
## <a name="example"></a>例  
 希望の <xref:System.Windows.Input.Cursor> を選択する <xref:System.Windows.Controls.ComboBox>、カーソルの変更が 1 つの要素に適用されるかアプリケーション全体に適用されるかを決定する <xref:System.Windows.Controls.RadioButton> の組み、新しいカーソルが適用される <xref:System.Windows.Controls.Border> 要素で構成される、ユーザー インターフェイスが作成されます。  
  
 [!code-xaml[cursors#ChangeCursorsXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml#changecursorsxaml)]  
  
 次のコード ビハインドは、<xref:System.Windows.Controls.ComboBox> でカーソルの種類が変更されたときに呼び出される <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> イベントハンドラーを作成します。  switch ステートメントにより、カーソル名がフィルター処理され、*DisplayArea* という名前の <xref:System.Windows.Controls.Border> が <xref:System.Windows.FrameworkElement.Cursor%2A> プロパティに設定されます。  
  
 カーソルの変更が "アプリケーション全体" に設定されている場合、<xref:System.Windows.Input.Mouse.OverrideCursor%2A> プロパティは <xref:System.Windows.Controls.Border> コントロールの <xref:System.Windows.FrameworkElement.Cursor%2A> プロパティに設定されます。  これにより、アプリケーション全体のカーソルが強制的に変更されます。  
  
 [!code-csharp[cursors#ChangeCursorsSample](~/samples/snippets/csharp/VS_Snippets_Wpf/cursors/CSharp/Window1.xaml.cs#changecursorssample)]
 [!code-vb[cursors#ChangeCursorsSample](~/samples/snippets/visualbasic/VS_Snippets_Wpf/cursors/VisualBasic/Window1.xaml.vb#changecursorssample)]  
  
## <a name="see-also"></a>関連項目

- [入力の概要](input-overview.md)
