---
title: '方法: カスタム コンテキスト メニューを RichTextBox に配置する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- custom context menus [WPF], positioning
- positioning custom context menus [WPF]
- RichTextBox control [WPF], positioning custom context menus
- context menus [WPF], positioning
ms.assetid: bf77c930-a546-4573-9a56-9af345ba189a
ms.openlocfilehash: f9407f59c3daafd09fa5b84006f33ef2f3ebd31f
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61770826"
---
# <a name="how-to-position-a-custom-context-menu-in-a-richtextbox"></a>方法: カスタム コンテキスト メニューを RichTextBox に配置する
この例では、カスタム コンテキスト メニューを <xref:System.Windows.Controls.RichTextBox> に配置する方法を示します。  
  
 **RichTextBox** のカスタム コンテキスト メニューを実装する場合、コンテキスト メニューの配置の処理を行う必要があります。  既定では、**RichTextBox** の中央でカスタム コンテキスト メニューが開きます。  
  
## <a name="example"></a>例  
 既定の配置時の動作をオーバーライドするには、<xref:System.Windows.FrameworkContentElement.ContextMenuOpening> イベントのリスナーを追加します。  次の例では、プログラムによってこれを実行する方法を説明します。  
  
 [!code-csharp[RichTextBox_ContextMenu#_AddListener](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_addlistener)]
 [!code-vb[RichTextBox_ContextMenu#_AddListener](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_addlistener)]  
  
## <a name="example"></a>例  
 次の例は、対応する <xref:System.Windows.FrameworkContentElement.ContextMenuOpening> イベント リスナーの実装を示しています。  
  
 [!code-csharp[RichTextBox_ContextMenu#_ListenerBody](~/samples/snippets/csharp/VS_Snippets_Wpf/RichTextBox_ContextMenu/CSharp/app.xaml.cs#_listenerbody)]
 [!code-vb[RichTextBox_ContextMenu#_ListenerBody](~/samples/snippets/visualbasic/VS_Snippets_Wpf/RichTextBox_ContextMenu/VisualBasic/app.xaml.vb#_listenerbody)]  
  
## <a name="see-also"></a>関連項目

- [RichTextBox の概要](richtextbox-overview.md)
- [TextBox の概要](textbox-overview.md)
