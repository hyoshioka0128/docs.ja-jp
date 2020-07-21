---
title: '方法: ハイブリッド アプリケーションで視覚スタイルを有効にする'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hybrid applications [WPF interoperability]
- visual styles [Windows Forms]
ms.assetid: 95de9b9c-d804-405c-b2d1-49a88c1e0fe1
ms.openlocfilehash: dd52313e9100f9c6a1141b53ccc5a23a4b54410a
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76789920"
---
# <a name="how-to-enable-visual-styles-in-a-hybrid-application"></a>方法: ハイブリッド アプリケーションで視覚スタイルを有効にする
ここでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションでホストされている Windows フォーム コントロールで視覚スタイルを有効にする方法について説明します。  
  
 アプリケーションから <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドを呼び出す場合、ほとんどの Windows フォーム コントロールには自動的に視覚スタイルが使用されます。 詳細については、「[visual スタイルが使用されているコントロールのレンダリング](../../winforms/controls/rendering-controls-with-visual-styles.md)」を参照してください。  
  
 このトピックで示すタスクの完全なコード一覧については、[ハイブリッド アプリケーションでの視覚スタイルの有効化のサンプル](https://go.microsoft.com/fwlink/?LinkID=159986)を参照してください。  
  
## <a name="enabling-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルの有効化  
  
#### <a name="to-enable-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルを有効にするには  
  
1. `HostingWfWithVisualStyles` という名前の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アプリケーション プロジェクトを作成します。  
  
2. ソリューション エクスプローラーで、次のアセンブリへの参照を追加します。  
  
    - WindowsFormsIntegration  
  
    - System.Windows.Forms  
  
3. ツールボックスで、<xref:System.Windows.Controls.Grid> アイコンをダブルクリックして、<xref:System.Windows.Controls.Grid> 要素をデザイン サーフェイスに配置します。  
  
4. プロパティ ウィンドウで、<xref:System.Windows.FrameworkElement.Height%2A> プロパティと <xref:System.Windows.FrameworkElement.Width%2A> プロパティの値を **[自動]** に設定します。  
  
5. デザイン ビューまたは XAML ビューで、<xref:System.Windows.Window> を選択します。  
  
6. プロパティ ウィンドウの **[イベント]** タブをクリックします。  
  
7. <xref:System.Windows.FrameworkElement.Loaded> イベントをダブルクリックします。
  
8. MainWindow.xaml.vb または MainWindow.xaml.cs に、<xref:System.Windows.FrameworkElement.Loaded> イベントを処理する次のコードを挿入します。  
  
     [!code-csharp[HostingWfWithVisualStyles#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWfWithVisualStyles/CSharp/HostingWfWithVisualStyles/Window1.xaml.cs#11)]
     [!code-vb[HostingWfWithVisualStyles#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWfWithVisualStyles/VisualBasic/HostingWfWithVisualStyles/Window1.xaml.vb#11)]  
  
9. F5 キーを押してアプリケーションをビルドし、実行します。  
  
     Windows フォーム コントロールは、視覚スタイルを使用して描画されます。  
  
## <a name="disabling-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルの無効化  
 視覚スタイルを無効にするには、単に <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドの呼び出しを削除します。  
  
#### <a name="to-disable-windows-forms-visual-styles"></a>Windows フォーム視覚スタイルを無効にするには  
  
1. コード エディターで MainWindow.xaml.vb または MainWindow.xaml.cs を開きます。  
  
2. <xref:System.Windows.Forms.Application.EnableVisualStyles%2A> メソッドの呼び出しをコメント アウトします。  
  
3. F5 キーを押してアプリケーションをビルドし、実行します。  
  
     Windows フォーム コントロールは、既定のシステム スタイルで描画されます。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Application.EnableVisualStyles%2A>
- <xref:System.Windows.Forms.VisualStyles>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [visual スタイルが使用されているコントロールのレンダリング](../../winforms/controls/rendering-controls-with-visual-styles.md)
- [チュートリアル: WPF での Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
