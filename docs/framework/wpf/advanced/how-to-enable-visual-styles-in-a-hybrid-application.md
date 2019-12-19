---
title: '方法 : ハイブリッド アプリケーションで視覚スタイルを有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- visual styles [Windows Forms]
ms.assetid: 95de9b9c-d804-405c-b2d1-49a88c1e0fe1
ms.openlocfilehash: 251c53a8665d2eae7c3b5bb23b0a388009362dcc
ms.sourcegitcommit: 42ed59871db1f29a32b3d8e7abeb20e6eceeda7c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74960114"
---
# <a name="how-to-enable-visual-styles-in-a-hybrid-application"></a>方法 : ハイブリッド アプリケーションで視覚スタイルを有効にする
このトピックでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]ベースのアプリケーションでホストされている [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールで visual スタイルを有効にする方法について説明します。  
  
 アプリケーションが <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドを呼び出すと、ほとんどの [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールで自動的に visual スタイルが使用されます。 詳細については、「[visual スタイルが使用されているコントロールのレンダリング](../../winforms/controls/rendering-controls-with-visual-styles.md)」を参照してください。  
  
 このトピックで説明されているタスクの完全なコード一覧については、「[ハイブリッドアプリケーションでの Visual スタイルの有効化](https://go.microsoft.com/fwlink/?LinkID=159986)」のサンプルを参照してください。  
  
## <a name="enabling-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルの有効化  
  
#### <a name="to-enable-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルを有効にするには  
  
1. `HostingWfWithVisualStyles`という名前の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーションプロジェクトを作成します。  
  
2. ソリューション エクスプローラーで、次のアセンブリへの参照を追加します。  
  
    - WindowsFormsIntegration  
  
    - System.Windows.Forms  
  
3. ツールボックスで <xref:System.Windows.Controls.Grid> アイコンをダブルクリックして、デザインサーフェイスに <xref:System.Windows.Controls.Grid> 要素を配置します。  
  
4. プロパティウィンドウで、<xref:System.Windows.FrameworkElement.Height%2A> の値と <xref:System.Windows.FrameworkElement.Width%2A> プロパティを**Auto**に設定します。  
  
5. デザインビューまたは XAML ビューで、<xref:System.Windows.Window>を選択します。  
  
6. プロパティウィンドウで、 **[イベント]** タブをクリックします。  
  
7. <xref:System.Windows.FrameworkElement.Loaded> イベントをダブルクリックします。
  
8. Mainwindow.xaml または MainWindow.xaml.cs で、<xref:System.Windows.FrameworkElement.Loaded> イベントを処理する次のコードを挿入します。  
  
     [!code-csharp[HostingWfWithVisualStyles#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfWithVisualStyles/CSharp/HostingWfWithVisualStyles/Window1.xaml.cs#11)]
     [!code-vb[HostingWfWithVisualStyles#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfWithVisualStyles/VisualBasic/HostingWfWithVisualStyles/Window1.xaml.vb#11)]  
  
9. F5 キーを押してアプリケーションをビルドし、実行します。  
  
     [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールは、visual スタイルを使用して描画されます。  
  
## <a name="disabling-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルの無効化  
 視覚スタイルを無効にするには、単に <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドの呼び出しを削除します。  
  
#### <a name="to-disable-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルを無効にするには  
  
1. コード エディターで MainWindow.xaml.vb または MainWindow.xaml.cs を開きます。  
  
2. <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドへの呼び出しをコメントアウトします。  
  
3. F5 キーを押してアプリケーションをビルドし、実行します。  
  
     [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールは、既定のシステムスタイルで描画されます。  
  
## <a name="see-also"></a>参照

- <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>
- <xref:System.Windows.Forms.VisualStyles>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [visual スタイルが使用されているコントロールのレンダリング](../../winforms/controls/rendering-controls-with-visual-styles.md)
- [チュートリアル: WPF での Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
