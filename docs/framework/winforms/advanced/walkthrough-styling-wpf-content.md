---
title: 'チュートリアル: スタイル WPF コンテンツ'
ms.date: 03/30/2017
helpviewer_keywords:
- WPF Designer [Windows Forms], styling WPF content
- interoperability [WDF]
- styles [Windows Forms], WPF content
ms.assetid: e574aac7-7ea4-4cdb-8034-bab541f000df
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 07241d41e3fbf270a76bd241765bfa369ee265d5
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646333"
---
# <a name="walkthrough-style-wpf-content"></a>チュートリアル: スタイル WPF コンテンツ

この記事では、Windows フォームでホストされている Windows プレゼンテーションファンデーション (WPF) コントロールにスタイルを適用する方法について説明します。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには Visual Studio が必要です。

## <a name="create-the-project"></a>プロジェクトを作成する

Visual Studio を開き、新しい Windows フォーム アプリケーション プロジェクトを`StylingWpfContent`作成します。

> [!NOTE]
> WPF コンテンツをホストする場合は、C# プロジェクトと Visual Basic プロジェクトのみがサポートされます。

## <a name="create-the-wpf-control-types"></a>WPF コントロール型を作成する

プロジェクトに追加した WPF コントロール型は、<xref:System.Windows.Forms.Integration.ElementHost> コントロールでホストできます。

1. 新しい WPF <xref:System.Windows.Controls.UserControl> プロジェクトをソリューションに追加します。 コントロール型の既定の名前である `UserControl1.xaml` を使用します。 詳細については、「[チュートリアル : デザイン時に Windows フォームで新しい WPF コンテンツを作成する](walkthrough-creating-new-wpf-content-on-windows-forms-at-design-time.md)」を参照してください。

2. デザイン ビューで `UserControl1` が選択されていることを確認します。

3. [**プロパティ]** ウィンドウで、<xref:System.Windows.FrameworkElement.Width%2A>プロパティと<xref:System.Windows.FrameworkElement.Height%2A>プロパティの値を**200**に設定します。

4. にコントロール<xref:System.Windows.Controls.Button?displayProperty=nameWithType>を追加<xref:System.Windows.Controls.UserControl>し、プロパティの値を<xref:System.Windows.Controls.ContentControl.Content%2A> **[キャンセル]** に設定します。

5. に 2<xref:System.Windows.Controls.Button?displayProperty=nameWithType>番目の<xref:System.Windows.Controls.UserControl>コントロールを追加し、プロパティ<xref:System.Windows.Controls.ContentControl.Content%2A>の値を **[OK]** に設定します。

6. プロジェクトをビルドします。

## <a name="apply-a-style-to-a-wpf-control"></a>WPF コントロールにスタイルを適用する

さまざまなスタイルを WPF コントロールに適用することで、外観や動作を変えることができます。

1. Windows フォーム デザイナーで `Form1` を開きます。

1. ツールボックス**で、** をダブルクリック`UserControl1`して フォーム`UserControl1`上の インスタンスを作成します。

   `UserControl1` のインスタンスは、`elementHost1` という名前の新しい <xref:System.Windows.Forms.Integration.ElementHost> コントロールでホストされます。

1. のスマート タグ パネル`elementHost1`で、ドロップダウン リストから **[ホストされたコンテンツの編集**] をクリックします。

   `UserControl1`を開き、WPF デザイナーで開きます。

1. XAML ビューで、次の XAML を `<UserControl>` の開始タグの後に挿入します。 この XAML は、明暗のあるグラデーション境界を持つグラデーションを作成します。 このコントロールをクリックすると、グラデーションが変わり、ボタンを押したような外観が生成されます。 詳しくは、「 [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」をご覧ください。

   ```xaml
   <UserControl.Resources>
    <LinearGradientBrush x:Key="NormalBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#FFF" Offset="0.0"/>
        <GradientStop Color="#CCC" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="PressedBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#BBB" Offset="0.0"/>
        <GradientStop Color="#EEE" Offset="0.1"/>
        <GradientStop Color="#EEE" Offset="0.9"/>
        <GradientStop Color="#FFF" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="NormalBorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#CCC" Offset="0.0"/>
        <GradientStop Color="#444" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="BorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#CCC" Offset="0.0"/>
        <GradientStop Color="#444" Offset="1.0"/>
    </LinearGradientBrush>
    <LinearGradientBrush x:Key="PressedBorderBrush" EndPoint="0,1" StartPoint="0,0">
        <GradientStop Color="#444" Offset="0.0"/>
        <GradientStop Color="#888" Offset="1.0"/>
    </LinearGradientBrush>

    <Style x:Key="SimpleButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="Background" Value="{StaticResource NormalBrush}"/>
        <Setter Property="BorderBrush" Value="{StaticResource NormalBorderBrush}"/>
        <Setter Property="Template">
            <Setter.Value>
                <ControlTemplate TargetType="{x:Type Button}">
                    <Grid x:Name="Grid">
                        <Border x:Name="Border" Background="{TemplateBinding Background}" BorderBrush="{TemplateBinding BorderBrush}" BorderThickness="{TemplateBinding BorderThickness}" Padding="{TemplateBinding Padding}"/>
                        <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalContentAlignment}" Margin="{TemplateBinding Padding}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" RecognizesAccessKey="True"/>
                    </Grid>
                    <ControlTemplate.Triggers>
                        <Trigger Property="IsPressed" Value="true">
                            <Setter Property="Background" Value="{StaticResource PressedBrush}" TargetName="Border"/>
                            <Setter Property="BorderBrush" Value="{StaticResource PressedBorderBrush}" TargetName="Border"/>
                        </Trigger>
                    </ControlTemplate.Triggers>
                </ControlTemplate>
            </Setter.Value>
        </Setter>
    </Style>
   </UserControl.Resources>
   ```

1. 前の`SimpleButton`手順で定義したスタイルを [キャンセル] ボタンの`<Button>`タグに次の XAML を挿入して **[キャンセル]** ボタンに適用します。

   ```xaml
   Style="{StaticResource SimpleButton}
   ```

   ボタンの宣言は、次の XAML のようになります。

   ```xaml
   <Button Height="23" Margin="41,52,98,0" Name="button1" VerticalAlignment="Top"
                Style="{StaticResource SimpleButton}">Cancel</Button>
   ```

1. プロジェクトをビルドします。

1. Windows フォーム デザイナーで `Form1` を開きます。

1. 新しいスタイルが Button コントロールに適用されます。

1. [**デバッグ**] メニューの [**デバッグの開始**] を選択して、アプリケーションを実行します。

1. **[OK] ボタン**と **[キャンセル]** ボタンをクリックして、相違点を表示します。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Forms.Integration.ElementHost>
- <xref:System.Windows.Forms.Integration.WindowsFormsHost>
- [移行と相互運用性](../../wpf/advanced/migration-and-interoperability.md)
- [WPF コントロールの使用](using-wpf-controls.md)
- [Visual Studio で XAML をデザインする](/visualstudio/xaml-tools/designing-xaml-in-visual-studio)
- [XAML の概要 (WPF)](../../../desktop-wpf/fundamentals/xaml.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
