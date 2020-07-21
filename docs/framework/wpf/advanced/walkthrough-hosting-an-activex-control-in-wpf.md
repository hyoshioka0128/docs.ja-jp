---
title: WPF で ActiveX コントロールをホストする
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ActiveX controls [WPF interoperability]
- hosting ActiveX controls [WPF]
ms.assetid: 1931d292-0dd1-434f-963c-dcda7638d75a
ms.openlocfilehash: 4ca40c0f6e62fd413e7f305649c5c01ddc152b2a
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794147"
---
# <a name="walkthrough-hosting-an-activex-control-in-wpf"></a>チュートリアル: WPF での ActiveX コントロールのホスト
ブラウザーとの対話を強化するために、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションで Microsoft ActiveX コントロールを使用できます。 このチュートリアルでは、Microsoft Windows Media Player を [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ページのコントロールとしてホストする方法について説明します。

 このチュートリアルでは、以下のタスクを行います。

- プロジェクトの作成。

- ActiveX コントロールの作成。

- WPF ページでの ActiveX コントロールのホスト。

 このチュートリアルを完了すると、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションで Microsoft ActiveX コントロールを使用する方法を理解できます。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio がインストールされているコンピューターにインストールされている Microsoft Windows Media Player。

- Visual Studio 2010。

## <a name="creating-the-project"></a>プロジェクトの作成

### <a name="to-create-and-set-up-the-project"></a>プロジェクトを作成し、設定するには

1. `HostingAxInWpf` という名前の WPF アプリケーション プロジェクトを作成します。

2. Windows フォーム コントロール ライブラリ プロジェクトをソリューションに追加し、プロジェクトに `WmpAxLib` という名前を付けます。

3. WmpAxLib プロジェクトで、wmp.dll という名前の Windows Media Player アセンブリへの参照を追加します。

4. **ツールボックス**を開きます。

5. **[ツールボックス]** を右クリックして、 **[アイテムの選択]** をクリックします。

6. **[COM コンポーネント]** タブをクリックし、**Windows Media Player** コントロールを選択して、 **[OK]** をクリックします。

     Windows Media Player コントロールが **[ツールボックス]** に追加されます。

7. ソリューション エクスプローラーで **UserControl1** ファイルを右クリックし、 **[名前の変更]** をクリックします。

8. 言語に応じて、名前を `WmpAxControl.vb` または `WmpAxControl.cs` に変更します。

9. すべての参照の名前を変更するように求められたら、 **[はい]** をクリックします。

## <a name="creating-the-activex-control"></a>ActiveX コントロールの作成
コントロールがデザイン サーフェイスに追加されると、Visual Studio によって Microsoft ActiveX コントロールの <xref:System.Windows.Forms.AxHost> ラッパー クラスが自動的に生成されます。 次の手順では、AxInterop.WMPLib.dll という名前のマネージ アセンブリを作成します。

### <a name="to-create-the-activex-control"></a>ActiveX コントロールを作成するには

1. Windows フォーム デザイナーで WmpAxControl.vb または WmpAxControl.cs を開きます。

2. **[ツールボックス]** から、Windows Media Player コントロールをデザイン サーフェイスに追加します。

3. プロパティ ウィンドウで、Windows Media Player コントロールの <xref:System.Windows.Forms.Control.Dock%2A> プロパティの値を <xref:System.Windows.Forms.DockStyle.Fill> に設定します。

4. WmpAxLib コントロール ライブラリ プロジェクトをビルドします。

## <a name="hosting-the-activex-control-on-a-wpf-page"></a>WPF ページでの ActiveX コントロールのホスト

### <a name="to-host-the-activex-control"></a>ActiveX コントロールをホストするには

1. HostingAxInWpf プロジェクトで、生成された ActiveX 相互運用性アセンブリへの参照を追加します。

     このアセンブリは AxInterop.WMPLib.dll という名前であり、Windows Media Player コントロールをインポートしたときに WmpAxLib プロジェクトのデバッグ フォルダーに追加されたものです。

2. WindowsFormsIntegration.dll という名前の WindowsFormsIntegration アセンブリへの参照を追加します。

3. System.Windows.Forms.dll という名前の Windows フォーム アセンブリへの参照を追加します。

4. WPF デザイナーで MainWindow.xaml を開きます。

5. <xref:System.Windows.Controls.Grid> 要素に `grid1` という名前を付けます。

     [!code-xaml[HostingAxInWpf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml#1)]

6. デザイン ビューまたは XAML ビューで、<xref:System.Windows.Window> 要素を選択します。

7. プロパティ ウィンドウの **[イベント]** タブをクリックします。

8. <xref:System.Windows.FrameworkElement.Loaded> イベントをダブルクリックします。

9. <xref:System.Windows.FrameworkElement.Loaded> イベントを処理する次のコードを挿入します。

     このコードによって、<xref:System.Windows.Forms.Integration.WindowsFormsHost> コントロールのインスタンスが作成され、`AxWindowsMediaPlayer` コントロールのインスタンスがその子として追加されます。

     [!code-csharp[HostingAxInWpf#11](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingAxInWpf/CSharp/HostingAxInWpf/window1.xaml.cs#11)]
     [!code-vb[HostingAxInWpf#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingAxInWpf/VisualBasic/HostingAxInWpf/window1.xaml.vb#11)]  
  
10. F5 キーを押してアプリケーションをビルドし、実行します。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
