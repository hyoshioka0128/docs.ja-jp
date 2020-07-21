---
title: '方法: TextBox のテキストがいつ変更されたかを検出する'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- TextBox control [WPF], detecting text change
- text change [WPF], detecting
- detecting text change [WPF]
ms.assetid: 1c39ee14-e37f-49fb-a0d1-a9824ca13584
ms.openlocfilehash: 8c7744e9e61b8ba796802e54435c0bf9fdbee50e
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855622"
---
# <a name="how-to-detect-when-text-in-a-textbox-has-changed"></a>方法: TextBox のテキストがいつ変更されたかを検出する

この例では、<xref:System.Windows.Controls.TextBox> コントロール内のテキストが変更されるたびに、<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> イベントを使用してメソッドを実行する方法の 1 つを示します。

変更を監視する <xref:System.Windows.Controls.TextBox> コントロールを含む [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の分離コード クラスで、<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> イベントが発生するたびに呼び出すメソッドを挿入します。  このメソッドには、<xref:System.Windows.Controls.TextChangedEventHandler> デリゲートによって予期されるものと一致するシグネチャが必要です。

イベント ハンドラーは、ユーザーまたはプログラムによって <xref:System.Windows.Controls.TextBox> コントロールの内容が変更されるたびに呼び出されます。

> [!NOTE]
> このイベントは、<xref:System.Windows.Controls.TextBox> コントロールが作成され、最初にテキストが入力されたときに発生します。

## <a name="example"></a>例

<xref:System.Windows.Controls.TextBox> コントロールを定義する [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で、イベント ハンドラー メソッド名と一致する値を持つ <xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> 属性を指定します。

[!code-xaml[TextBox_MiscCode#_TextChangedXAML](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml#_textchangedxaml)]

## <a name="example"></a>例

変更を監視する <xref:System.Windows.Controls.TextBox> コントロールを含む [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] の分離コード クラスで、<xref:System.Windows.Controls.Primitives.TextBoxBase.TextChanged> イベントが発生するたびに呼び出すメソッドを挿入します。  このメソッドには、<xref:System.Windows.Controls.TextChangedEventHandler> デリゲートによって予期されるものと一致するシグネチャが必要です。

[!code-csharp[TextBox_MiscCode#_TextChangedEventHandler](~/samples/snippets/csharp/VS_Snippets_Wpf/TextBox_MiscCode/CSharp/Window1.xaml.cs#_textchangedeventhandler)]
[!code-vb[TextBox_MiscCode#_TextChangedEventHandler](~/samples/snippets/visualbasic/VS_Snippets_Wpf/TextBox_MiscCode/VisualBasic/Window1.xaml.vb#_textchangedeventhandler)]

イベント ハンドラーは、ユーザーまたはプログラムによって <xref:System.Windows.Controls.TextBox> コントロールの内容が変更されるたびに呼び出されます。

> [!NOTE]
> このイベントは、<xref:System.Windows.Controls.TextBox> コントロールが作成され、最初にテキストが入力されたときに発生します。

コメント

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Controls.TextChangedEventArgs>
- [TextBox の概要](textbox-overview.md)
- [RichTextBox の概要](richtextbox-overview.md)
