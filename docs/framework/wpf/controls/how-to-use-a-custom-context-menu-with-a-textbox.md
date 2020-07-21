---
title: '方法: TextBox でカスタム コンテキスト メニューを使用する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- context menus [WPF], custom
- menus [WPF], custom
- custom context menus [WPF]
- TextBox control [WPF], custom content menus
ms.assetid: 842d3cd5-6fa0-4be4-8d90-6c7466213b1c
ms.openlocfilehash: b0507c6fa37f0f51f9e12ebe5f908c39c25b50d9
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61699176"
---
# <a name="how-to-use-a-custom-context-menu-with-a-textbox"></a>方法: TextBox でカスタム コンテキスト メニューを使用する
この例からは、<xref:System.Windows.Controls.TextBox> 用の単純なカスタム コンテキスト メニューを定義し、実装する方法がわかります。  
  
## <a name="example"></a>例  
 次の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] の例では、カスタム コンテキスト メニューを含む <xref:System.Windows.Controls.TextBox> コントロールが定義されます。  
  
 このコンテキスト メニューは <xref:System.Windows.Controls.ContextMenu> 要素を利用して定義されています。  コンテキスト メニュー自体は一連の <xref:System.Windows.Controls.MenuItem> 要素と <xref:System.Windows.Controls.Separator> 要素で構成されています。  各 <xref:System.Windows.Controls.MenuItem> 要素によってコンテキスト メニューのコマンドが定義されます。<xref:System.Windows.Controls.HeaderedItemsControl.Header%2A> 属性によって、メニュー コマンドの表示テキストが定義されます。<xref:System.Windows.Controls.MenuItem.Click> 属性によって、各メニュー項目のハンドラー メソッドが指定されます。  <xref:System.Windows.Controls.Separator> 要素は、前のメニュー項目とそれに続くメニュー項目の間に分割線を表示するだけのものです。  
  
 [!code-xaml[TextBox_ContextMenu#_TextBox_ContextMenuXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml#_textbox_contextmenuxaml)]  
  
## <a name="example"></a>例  
 次の例では、前のコンテキスト メニュー定義の実装コードと、コンテキスト メニューを有効にし、無効にするコードを示します。  <xref:System.Windows.Controls.ContextMenu.Opened> イベントは、<xref:System.Windows.Controls.TextBox> の現在の状態に基づき、特定のコマンドの有効と無効を動的に切り替えるために使用されます。  
  
 既定のコンテキスト メニューを復元するには、<xref:System.Windows.DependencyObject.ClearValue%2A> メソッドを使用し、<xref:System.Windows.FrameworkElement.ContextMenu%2A> プロパティの値を消去します。  コンテキスト メニューを完全に無効にするには、<xref:System.Windows.FrameworkElement.ContextMenu%2A> プロパティを null 参照に設定します (Visual Basic の `Nothing`)。  
  
 [!code-csharp[TextBox_ContextMenu#_TextBox_ContextMenu](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_ContextMenu/CSharp/Window1.xaml.cs#_textbox_contextmenu)]
 [!code-vb[TextBox_ContextMenu#_TextBox_ContextMenu](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_ContextMenu/VisualBasic/Window1.xaml.vb#_textbox_contextmenu)]  
  
## <a name="see-also"></a>関連項目

- [コンテキスト メニューでスペル チェックを使用する](how-to-use-spell-checking-with-a-context-menu.md)
- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
