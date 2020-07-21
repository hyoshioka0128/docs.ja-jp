---
title: Windows フォームで 3D WPF 複合コントロールをホストする
titleSuffix: ''
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting WPF content in Windows Forms [WPF]
- composite controls [WPF], hosting WPF in
ms.assetid: 486369a9-606a-4a3b-b086-a06f2119c7b0
ms.openlocfilehash: aaa726ac90fd75a12054c18be6ec08a1372c1128
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794212"
---
# <a name="walkthrough-host-a-3d-wpf-composite-control-in-windows-forms"></a>チュートリアル: Windows フォームで 3D WPF 複合コントロールをホストする

このチュートリアルでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールを作成し、<xref:System.Windows.Forms.Integration.ElementHost> コントロールを使用して Windows フォーム コントロールおよびフォームでホストする方法について説明します。

このチュートリアルでは、2 つの子コントロールを含む [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> を実装します。 <xref:System.Windows.Controls.UserControl> を使用すると、3 次元 (3D) の円錐が表示されます。 3D オブジェクトのレンダリングは、Windows フォームよりも [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] を使用する方がはるかに簡単です。 そのため、Windows フォームで 3D グラフィックを作成するために [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> クラスをホストすることは理にかなっています。

このチュートリアルでは、以下のタスクを行います。

- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> の作成。

- Windows フォーム ホスト プロジェクトの作成。

- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> のホスト。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2017

<a name="To_Create_the_UserControl"></a>
## <a name="create-the-usercontrol"></a>UserControl を作成する

1. `HostingWpfUserControlInWf` という名前の **WPF ユーザー コントロール ライブラリ** プロジェクトを作成します。

2. WPF デザイナーで UserControl1.xaml を開きます。

3. 生成されたコードを次のコードに置き換えます。

     [!code-xaml[HostingWpfUserControlInWf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]

     このコードでは、2 つの子コントロールを含む <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType> を定義します。 1 つ目の子コントロールは <xref:System.Windows.Controls.Label?displayProperty=nameWithType> コントロールです。2 つ目は 3D の円錐を表示する <xref:System.Windows.Controls.Viewport3D> コントロールです。

<a name="To_Create_the_Windows_Forms_Host_Project"></a>
## <a name="create-the-host-project"></a>ホスト プロジェクトを作成する

1. **Windows フォーム アプリ (.NET Framework)** プロジェクトを `WpfUserControlHost` という名前のソリューションに追加します。

2. **ソリューション エクスプローラー**で、WindowsFormsIntegration.dll という名前の WindowsFormsIntegration アセンブリへの参照を追加します。

3. 次の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アセンブリへの参照を追加します。

    - PresentationCore

    - PresentationFramework

    - WindowsBase

4. `HostingWpfUserControlInWf` への参照をプロジェクトに追加します。

5. ソリューション エクスプローラーで、`WpfUserControlHost` プロジェクトをスタートアップ プロジェクトに設定します。

<a name="To_Host_the_Windows_Presentation_Foundation"></a>
## <a name="host-the-usercontrol"></a>UserControl をホストする

1. Windows フォーム デザイナーで、Form1 を開きます。

2. プロパティ ウィンドウで **[イベント]** をクリックし、<xref:System.Windows.Forms.Form.Load> イベントをダブルクリックしてイベント ハンドラーを作成します。

     コード エディターが開き、新しく生成された `Form1_Load` イベント ハンドラーが表示されます。

3. Form1.cs のコードを次のコードに置き換えます。

     `Form1_Load` イベント ハンドラーによって `UserControl1` のインスタンスが作成され、それが <xref:System.Windows.Forms.Integration.ElementHost> コントロールの子コントロールのコレクションに追加されます。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールがフォームの子コントロールのコレクションに追加されます。

     [!code-csharp[HostingWpfUserControlInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/WpfUserControlHost/Form1.cs#10)]
     [!code-vb[HostingWpfUserControlInWf#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWpfUserControlInWf/VisualBasic/WpfUserControlHost/Form1.vb#10)]

4. **F5** キーを押してアプリケーションをビルドし、実行します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [Windows フォームでの WPF 複合コントロールのホストのサンプル](https://go.microsoft.com/fwlink/?LinkID=160001)
