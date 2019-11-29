---
title: 'チュートリアル: WPF での Windows フォーム コントロールのホスト'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting Windows Forms control in WPF [WPF]
ms.assetid: 9cb88415-39b0-4c46-80c4-ff325b674286
ms.openlocfilehash: e353c35e9989e5887e038371672adbb6c2d3598d
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73976525"
---
# <a name="walkthrough-hosting-a-windows-forms-control-in-wpf"></a>チュートリアル: WPF での Windows フォーム コントロールのホスト

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、豊富な機能セットを備えたさまざまなコントロールが用意されています。 ただし、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] のページで [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールを使用することが必要になる場合があります。 たとえば、既存の [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールに多大な投資を行っている場合や、独自の機能を提供する [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールがある場合があります。

このチュートリアルでは、コードを使用して [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページで [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] <xref:System.Windows.Forms.MaskedTextBox?displayProperty=nameWithType> コントロールをホストする方法について説明します。

このチュートリアルで示されているタスクの完全なコード一覧については、「 [WPF の Windows フォームコントロールのホスト](https://go.microsoft.com/fwlink/?LinkID=160057)」を参照してください。

## <a name="prerequisites"></a>必要条件

このチュートリアルを完了するには Visual Studio が必要です。

## <a name="hosting-the-windows-forms-control"></a>Windows フォームコントロールのホスト

### <a name="to-host-the-maskedtextbox-control"></a>MaskedTextBox コントロールをホストするには

1. `HostingWfInWpf`という名前の WPF アプリケーションプロジェクトを作成します。

2. 次のアセンブリへの参照を追加します。

    - WindowsFormsIntegration

    - System.Windows.Forms

3. WPF デザイナーで Mainwindow.xaml を開きます。

4. <xref:System.Windows.Controls.Grid> 要素に `grid1`という名前を指定します。

     [!code-xaml[HostingWfInWPF#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml#1)]

5. デザインビューまたは XAML ビューで、<xref:System.Windows.Window> 要素を選択します。

6. プロパティウィンドウで、 **[イベント]** タブをクリックします。

7. <xref:System.Windows.FrameworkElement.Loaded> イベントをダブルクリックします。

8. <xref:System.Windows.FrameworkElement.Loaded> イベントを処理する次のコードを挿入します。

     [!code-csharp[HostingWfInWPF#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#10)]
     [!code-vb[HostingWfInWPF#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#10)]

9. ファイルの先頭に、次の `Imports` または `using` ステートメントを追加します。

     [!code-csharp[HostingWfInWPF#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfInWPF/CSharp/HostingWfInWPF/Window1.xaml.cs#11)]
     [!code-vb[HostingWfInWPF#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfInWPF/VisualBasic/HostingWfInWpf/Window1.xaml.vb#11)]

10. **F5** キーを押してアプリケーションをビルドし、実行します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: WPF での XAML を使用した Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf-by-using-xaml.md)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [Windows フォーム コントロールおよび同等の WPF コントロール](windows-forms-controls-and-equivalent-wpf-controls.md)
- [WPF サンプルでの Windows フォームコントロールのホスト](https://go.microsoft.com/fwlink/?LinkID=160057)
