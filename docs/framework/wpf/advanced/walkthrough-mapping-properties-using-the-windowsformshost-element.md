---
title: 'チュートリアル: WindowsFormsHost 要素を使用したプロパティの割り当て'
ms.date: 08/18/2018
dev_langs:
- csharp
- vb
helpviewer_keywords:
- mapping properties [WPF]
- WindowsFormsHost element property mapping [WPF]
ms.assetid: 74809167-bf8e-48b7-a2e7-b4ea08bc7d8c
ms.openlocfilehash: c076937d6431adf1750793d47ece88dc82edf95c
ms.sourcegitcommit: 13e79efdbd589cad6b1de634f5d6b1262b12ab01
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2020
ms.locfileid: "76794100"
---
# <a name="walkthrough-mapping-properties-using-the-windowsformshost-element"></a>チュートリアル: WindowsFormsHost 要素を使用したプロパティの割り当て

このチュートリアルでは、<xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> プロパティを使用して、ホストされている Windows フォーム コントロールの対応するプロパティに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティをマップする方法を示します。

このチュートリアルでは、以下のタスクを行います。

- プロジェクトの作成。

- アプリケーション レイアウトの定義

- 新しいプロパティ マッピングの定義。

- 既定のプロパティ マッピングの削除。

- 既定のプロパティ マッピングの置き換え。

- 既定のプロパティ マッピングの拡張。

このチュートリアルで説明されているタスクの完全なコード一覧については、[WindowsFormsHost 要素を使用したプロパティのマッピングのサンプル](https://go.microsoft.com/fwlink/?LinkID=160019)を参照してください。

完了すると、ホストされている Windows フォーム コントロールの対応するプロパティに [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] プロパティをマップできます。

## <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを実行するには、次のコンポーネントが必要です。

- Visual Studio 2017

## <a name="create-and-set-up-the-project"></a>プロジェクトの作成と設定

1. `PropertyMappingWithWfhSample` という名前の **WPF アプリ** プロジェクトを作成します。

2. **ソリューション エクスプローラー**で、WindowsFormsIntegration.dll という名前の WindowsFormsIntegration アセンブリへの参照を追加します。

3. **ソリューション エクスプローラー**で、System.Drawing および System.Windows.Forms アセンブリへの参照を追加します。

## <a name="defining-the-application-layout"></a>アプリケーション レイアウトの定義

[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] ベースのアプリケーションでは、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素を使用して Windows フォーム コントロールをホストします。

### <a name="to-define-the-application-layout"></a>アプリケーションのレイアウトを定義するには

1. WPF デザイナーで Window1.xaml を開きます。

2. 既存のコードを次のコードに置き換えます。

     [!code-xaml[PropertyMappingWithWfhSample#1](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml#1)]

3. コード エディターで Window1.xaml.cs を開きます。

4. ファイルの先頭に、次の名前空間をインポートします。

     [!code-csharp[PropertyMappingWithWfhSample#20](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#20)]
     [!code-vb[PropertyMappingWithWfhSample#20](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#20)]

## <a name="defining-a-new-property-mapping"></a>新しいプロパティ マッピングの定義

<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素には、いくつかの既定のプロパティ マッピングが用意されています。 <xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> に対して <xref:System.Windows.Forms.Integration.PropertyMap.Add%2A> メソッドを呼び出して、新しいプロパティ マッピングを追加します。

### <a name="to-define-a-new-property-mapping"></a>新しいプロパティ マッピングを定義するには

- 次のコードを `Window1` クラスの定義にコピーします。

     [!code-csharp[PropertyMappingWithWfhSample#14](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#14)]
     [!code-vb[PropertyMappingWithWfhSample#14](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#14)]

     `AddClipMapping` メソッドを使用して、<xref:System.Windows.UIElement.Clip%2A> プロパティの新しいマッピングを追加します。

     `OnClipChange` メソッドを使用して、<xref:System.Windows.UIElement.Clip%2A> プロパティを Windows フォーム <xref:System.Windows.Forms.Control.Region%2A> プロパティに変換します。

     `Window1_SizeChanged` メソッドを使用して、ウィンドウの <xref:System.Windows.FrameworkElement.SizeChanged> イベントを処理し、アプリケーション ウィンドウに合わせてクリッピング領域のサイズを変更します。

## <a name="removing-a-default-property-mapping"></a>既定のプロパティ マッピングの削除

<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> に対して <xref:System.Windows.Forms.Integration.PropertyMap.Remove%2A> メソッドを呼び出して、既定のプロパティ マッピングを削除します。

### <a name="to-remove-a-default-property-mapping"></a>既定のプロパティ マッピングを削除するには

- 次のコードを `Window1` クラスの定義にコピーします。

     [!code-csharp[PropertyMappingWithWfhSample#13](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#13)]
     [!code-vb[PropertyMappingWithWfhSample#13](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#13)]

     `RemoveCursorMapping` メソッドを使用して、<xref:System.Windows.FrameworkElement.Cursor%2A> プロパティの既定のマッピングを削除します。

## <a name="replacing-a-default-property-mapping"></a>既定のプロパティ マッピングの置換

既定のプロパティ マッピングを削除するには、既定のマッピングを削除し、<xref:System.Windows.Forms.Integration.WindowsFormsHost> 要素の <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A> に対して <xref:System.Windows.Forms.Integration.PropertyMap.Add%2A> メソッドを呼び出します。

### <a name="to-replace-a-default-property-mapping"></a>既定のプロパティ マッピングを置き換えるには

- 次のコードを `Window1` クラスの定義にコピーします。

     [!code-csharp[PropertyMappingWithWfhSample#12](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#12)]
     [!code-vb[PropertyMappingWithWfhSample#12](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#12)]

     `ReplaceFlowDirectionMapping` メソッドを使用して、<xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティの既定のマップを置き換えます。

     `OnFlowDirectionChange` メソッドを使用して、<xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティを Windows フォーム <xref:System.Windows.Forms.Control.RightToLeft%2A> プロパティに変換します。

     `cb_CheckedChanged` メソッドを使用して、<xref:System.Windows.Forms.CheckBox> コントロールの <xref:System.Windows.Forms.CheckBox.CheckedChanged> イベントを処理します。 <xref:System.Windows.Forms.CheckBox.CheckState%2A> プロパティの値に基づいて <xref:System.Windows.FrameworkElement.FlowDirection%2A> プロパティが割り当てられます

## <a name="extending-a-default-property-mapping"></a>既定のプロパティ マッピングの拡張

既定のプロパティ マッピングを使用できます。また、独自のマッピングを使用して拡張することもできます。

### <a name="to-extend-a-default-property-mapping"></a>既定のプロパティ マッピングを拡張するには

- 次のコードを `Window1` クラスの定義にコピーします。

     [!code-csharp[PropertyMappingWithWfhSample#15](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#15)]
     [!code-vb[PropertyMappingWithWfhSample#15](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#15)]

     `ExtendBackgroundMapping` メソッドを使用して、カスタム プロパティ トランスレーターを既存の <xref:System.Windows.Controls.Control.Background%2A> プロパティ マッピングに追加します。

     `OnBackgroundChange` メソッドを使用して、ホストされているコントロールの <xref:System.Windows.Forms.Control.BackgroundImage%2A> プロパティに特定の画像を割り当てます。 `OnBackgroundChange` メソッドは、既定のプロパティ マッピングが適用された後に呼び出されます。

## <a name="initializing-your-property-mappings"></a>プロパティ マッピングの初期化

前述のメソッドを <xref:System.Windows.FrameworkElement.Loaded> イベント ハンドラーで呼び出して、プロパティ マッピングを設定します。

### <a name="to-initialize-your-property-mappings"></a>プロパティ マッピングを初期化するには

1. 次のコードを `Window1` クラスの定義にコピーします。

     [!code-csharp[PropertyMappingWithWfhSample#11](~/samples/snippets/csharp/VS_Snippets_Wpf/PropertyMappingWithWfhSample/CSharp/PropertyMappingWithWfh/Window1.xaml.cs#11)]
     [!code-vb[PropertyMappingWithWfhSample#11](~/samples/snippets/visualbasic/VS_Snippets_Wpf/PropertyMappingWithWfhSample/VisualBasic/PropertyMappingWithWfh/Window1.xaml.vb#11)]

     `WindowLoaded` メソッドを使用して <xref:System.Windows.FrameworkElement.Loaded> イベントを処理し、次の初期化を実行します。

    - Windows フォーム <xref:System.Windows.Forms.CheckBox> コントロールを作成します。

    - このチュートリアルで前に定義したメソッドを呼び出して、プロパティ マッピングを設定します。

    - マップされたプロパティに初期値を割り当てます。

2. **F5** キーを押してアプリケーションをビルドし、実行します。 チェック ボックスをクリックして、<xref:System.Windows.FrameworkElement.FlowDirection%2A> のマッピングの結果を確認します。 チェック ボックスをクリックすると、レイアウトが左右反転します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.WindowsFormsHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.ElementHost.PropertyMap%2A?displayProperty=nameWithType>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [Windows フォームと WPF プロパティの割り当て](windows-forms-and-wpf-property-mapping.md)
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [チュートリアル: WPF での Windows フォーム コントロールのホスト](walkthrough-hosting-a-windows-forms-control-in-wpf.md)
