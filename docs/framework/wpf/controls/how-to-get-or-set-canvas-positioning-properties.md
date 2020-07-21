---
title: '方法: Canvas の配置プロパティを取得または設定する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Canvas control [WPF], setting positioning properties
ms.assetid: 1636b950-2b5a-4507-8a10-c5034cc58b1c
ms.openlocfilehash: 06508e1198736ccb1cbda41641dff4bc634ef82b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61910482"
---
# <a name="how-to-get-or-set-canvas-positioning-properties"></a>方法: Canvas の配置プロパティを取得または設定する
この例からは、<xref:System.Windows.Controls.Canvas> 要素の配置メソッドを利用し、子コンテンツを配置する方法がわかります。 この例では、<xref:System.Windows.Controls.ListBoxItem> のコンテンツを利用して配置値を表し、値を <xref:System.Double> のインスタンスに変換しています。このインスタンスは、配置に必須の引数です。 値はその後、文字列に再変換され、<xref:System.Windows.Controls.Canvas.GetLeft%2A> メソッドを利用することで <xref:System.Windows.Controls.TextBlock> 要素にテキストとして表示されます。  
  
## <a name="example"></a>例  
 次の例では、選択できる <xref:System.Windows.Controls.ListBoxItem> 要素が 11 ある <xref:System.Windows.Controls.ListBox> 要素が作成されます。 <xref:System.Windows.Controls.Primitives.Selector.SelectionChanged> イベントによって `ChangeLeft` カスタム メソッドがトリガーされます。これは、後続のコード ブロックによって定義されます。  
  
 各 <xref:System.Windows.Controls.ListBoxItem> によって <xref:System.Double> が表されます。これは、<xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Canvas.SetLeft%2A> メソッドで受け取られる引数の 1 つです。 <xref:System.Windows.Controls.ListBoxItem> を利用して <xref:System.Double> のインスタンスを表すには、まず、正しいデータ型に <xref:System.Windows.Controls.ListBoxItem> を変換する必要があります。  
  
 [!code-xaml[CanvasPositioningProperties#1](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml#1)]  
  
 ユーザーが <xref:System.Windows.Controls.ListBox> 選択を変更すると、`ChangeLeft` カスタム メソッドが呼び出されます。 このメソッドでは、<xref:System.Windows.Controls.ListBoxItem> が <xref:System.Windows.LengthConverter> オブジェクトに渡されます。このオブジェクトによって、<xref:System.Windows.Controls.ListBoxItem> の <xref:System.Windows.Controls.ContentControl.Content%2A> が <xref:System.Double> のインスタンスに変換されます (この値は、<xref:System.Windows.Controls.Control.ToString%2A> メソッドを利用することで <xref:System.String> に既に変換されていることに注目してください)。 この値は次に、`text1` オブジェクトの位置を変更するため、<xref:System.Windows.Controls.Canvas> の <xref:System.Windows.Controls.Canvas.SetLeft%2A> メソッドと <xref:System.Windows.Controls.Canvas.GetLeft%2A> メソッドに戻されます。  
  
 [!code-csharp[CanvasPositioningProperties#2](~/samples/snippets/csharp/VS_Snippets_Wpf/CanvasPositioningProperties/CSharp/Window1.xaml.cs#2)]
 [!code-vb[CanvasPositioningProperties#2](~/samples/snippets/visualbasic/VS_Snippets_Wpf/CanvasPositioningProperties/VisualBasic/Window1.xaml.vb#2)]  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.Canvas>
- <xref:System.Windows.Controls.ListBoxItem>
- <xref:System.Windows.LengthConverter>
- [パネルの概要](panels-overview.md)
