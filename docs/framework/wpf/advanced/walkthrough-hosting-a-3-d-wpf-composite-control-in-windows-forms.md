---
title: 'チュートリアル: Windows フォームでの 3D WPF 複合コントロールのホスト'
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- hosting WPF content in Windows Forms [WPF]
- composite controls [WPF], hosting WPF in
ms.assetid: 486369a9-606a-4a3b-b086-a06f2119c7b0
ms.openlocfilehash: f33adf6bac5efab87fecd9e95437ac8cff6d1f16
ms.sourcegitcommit: f348c84443380a1959294cdf12babcb804cfa987
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2019
ms.locfileid: "73976555"
---
# <a name="walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms"></a>チュートリアル: Windows フォームでの 3D WPF 複合コントロールのホスト

このチュートリアルでは、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 複合コントロールを作成し、<xref:System.Windows.Forms.Integration.ElementHost> コントロールを使用して [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)] コントロールとフォームでホストする方法について説明します。

このチュートリアルでは、2つの子コントロールを含む [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> を実装します。 <xref:System.Windows.Controls.UserControl> には、3次元 (3-d) の円錐が表示されます。 3d オブジェクトのレンダリングは、[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]よりも [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ではるかに簡単になります。 したがって、[!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]に3-d グラフィックスを作成するには、[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> クラスをホストするのが理にかなっています。

このチュートリアルでは、以下のタスクを行います。

- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>を作成しています。

- Windows フォームホストプロジェクトを作成しています。

- [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl>をホストしています。

## <a name="prerequisites"></a>必要条件

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2017

<a name="To_Create_the_UserControl"></a>
## <a name="create-the-usercontrol"></a>UserControl を作成する

1. `HostingWpfUserControlInWf`という名前の**WPF ユーザーコントロールライブラリ**プロジェクトを作成します。

2. WPF デザイナーで UserControl1 を開きます。

3. 生成されたコードを次のコードに置き換えます。

     [!code-xaml[HostingWpfUserControlInWf#1](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/HostingWpfUserControlInWf/ConeControl.xaml#1)]

     このコードは、2つの子コントロールを含む <xref:System.Windows.Controls.UserControl?displayProperty=nameWithType> を定義します。 最初の子コントロールは <xref:System.Windows.Controls.Label?displayProperty=nameWithType> コントロールです。2つ目は、3-d 円錐を表示する <xref:System.Windows.Controls.Viewport3D> コントロールです。

<a name="To_Create_the_Windows_Forms_Host_Project"></a>
## <a name="create-the-host-project"></a>ホストプロジェクトを作成する

1. `WpfUserControlHost` という名前の**Windows フォーム App (.NET Framework)** プロジェクトをソリューションに追加します。

2. **ソリューションエクスプローラー**で、windowsフォーム統合アセンブリへの参照を追加します。このアセンブリには、windowsフォーム integration .dll という名前が付けられています。

3. 次の [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] アセンブリへの参照を追加します。

    - PresentationCore

    - PresentationFramework

    - WindowsBase

4. `HostingWpfUserControlInWf` への参照をプロジェクトに追加します。

5. ソリューションエクスプローラーで、`WpfUserControlHost` プロジェクトをスタートアッププロジェクトとして設定します。

<a name="To_Host_the_Windows_Presentation_Foundation"></a>
## <a name="host-the-usercontrol"></a>UserControl をホストする

1. Windows フォームデザイナーで、Form1 を開きます。

2. プロパティウィンドウで、 **[イベント]** をクリックし、<xref:System.Windows.Forms.Form.Load> イベントをダブルクリックしてイベントハンドラーを作成します。

     コードエディターが開き、新しく生成された `Form1_Load` イベントハンドラーが表示されます。

3. Form1.cs のコードを次のコードに置き換えます。

     `Form1_Load` イベントハンドラーは、`UserControl1` のインスタンスを作成し、それを <xref:System.Windows.Forms.Integration.ElementHost> コントロールの子コントロールのコレクションに追加します。 <xref:System.Windows.Forms.Integration.ElementHost> コントロールが、フォームの子コントロールのコレクションに追加されます。

     [!code-csharp[HostingWpfUserControlInWf#10](~/samples/snippets/csharp/VS_Snippets_Wpf/HostingWpfUserControlInWf/CSharp/WpfUserControlHost/Form1.cs#10)]
     [!code-vb[HostingWpfUserControlInWf#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/HostingWpfUserControlInWf/VisualBasic/WpfUserControlHost/Form1.vb#10)]

4. **F5** キーを押してアプリケーションをビルドし、実行します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: Windows フォームでの WPF 複合コントロールのホスト](walkthrough-hosting-a-wpf-composite-control-in-windows-forms.md)
- [チュートリアル: WPF での Windows フォーム複合コントロールのホスト](walkthrough-hosting-a-windows-forms-composite-control-in-wpf.md)
- [Windows フォームサンプルでの WPF 複合コントロールのホスト](https://go.microsoft.com/fwlink/?LinkID=160001)
