---
title: 'チュートリアル: XAML を使用したボタンの作成'
ms.date: 03/30/2017
helpviewer_keywords:
- buttons [WPF]
ms.assetid: 138c41c4-1759-4bbf-8d77-77031a06a8a0
ms.openlocfilehash: a8cc227703e81e5de9dea7e44e10dfecca2cd05c
ms.sourcegitcommit: 62285ec11fa8e8424bab00511a90760c60e63c95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2020
ms.locfileid: "81646474"
---
# <a name="walkthrough-create-a-button-by-using-xaml"></a>チュートリアル: XAML を使用したボタンの作成

このチュートリアルの目的は、Windows Presentation Foundation (WPF) アプリケーションで使用するためのアニメーション化されたボタンを作成する方法を学習することです。 このチュートリアルでは、スタイルとテンプレートを使用して、コードの再利用と、ボタン宣言からのボタン ロジックの分離を可能にする、カスタマイズされたボタン リソースを作成します。 このチュートリアルは、すべて [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] で記述されています。

> [!IMPORTANT]
> このチュートリアルでは、Visual Studio に [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を入力するか、コピーして貼り付けることによって、アプリケーションを作成する手順について説明します。 デザイナーを使用して同じアプリケーションを作成する方法については、[Microsoft Expression Blend を使用してボタンを作成する方法](walkthrough-create-a-button-by-using-microsoft-expression-blend.md)に関する記事を参照してください。

完成したボタンを次の図に示します。

![XAML を使用して作成されたカスタム ボタン](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")

## <a name="create-basic-buttons"></a>基本的なボタンを作成する

まず、新しいプロジェクトを作成し、いくつかのボタンをウィンドウに追加します。

### <a name="to-create-a-new-wpf-project-and-add-buttons-to-the-window"></a>新しい WPF プロジェクトを作成し、ウィンドウにボタンを追加するには

1. Visual Studio を起動します。

2. **新しい WPF プロジェクトを作成する:** **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。 **Windows アプリケーション (WPF)** テンプレートを探し、プロジェクトの名前を "AnimatedButton" に設定します。 これにより、アプリケーションのスケルトンが作成されます。

3. **基本的な既定のボタンを追加する:** このチュートリアルで必要なすべてのファイルは、テンプレートによって提供されます。 ソリューション エクスプローラーで Window1.xaml ファイルをダブルクリックして開きます。 Window1.xaml には <xref:System.Windows.Controls.Grid> 要素が既定で存在します。 <xref:System.Windows.Controls.Grid> 要素を削除し、次の強調表示されているコードを Window1.xaml に入力するか、コピーして貼り付けて、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] ページにいくつかのボタンを追加します。

    ```xaml
    <Window x:Class="AnimatedButton.Window1"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      Title="AnimatedButton" Height="300" Width="300"
      Background="Black">
      <!-- Buttons arranged vertically inside a StackPanel. -->
      <StackPanel HorizontalAlignment="Left">
          <Button>Button 1</Button>
          <Button>Button 2</Button>
          <Button>Button 3</Button>
      </StackPanel>
    </Window>
    ```

     F5 キーを押してアプリケーションを実行します。次の図のような一連のボタンが表示されます。

     ![3 つの基本的なボタン](./media/custom-button-animatedbutton-1.gif "custom_button_AnimatedButton_1")

     これで基本的なボタンが作成されたので、Window1.xaml ファイルでの作業は終了です。 このチュートリアルの残りの部分では、ボタンのスタイルとテンプレートを定義する app.xaml ファイルに注目します。

## <a name="set-basic-properties"></a>基本プロパティを設定する

次に、ボタンの外観とレイアウトを制御するため、これらのボタンにいくつかのプロパティを設定してみましょう。 個々のボタンにプロパティを設定するのではなく、リソースを使用して、アプリケーション全体に対してボタンのプロパティを定義します。 アプリケーション リソースは、概念的には Web ページの外部カスケード スタイル シート (CSS) に似ています。ただし、このチュートリアルの最後にはわかるように、リソースの方がカスケード スタイル シート (CSS) よりはるかに強力です。 リソースの詳細については、[XAML のリソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。

### <a name="to-use-styles-to-set-basic-properties-on-the-buttons"></a>スタイルを使用してボタンの基本プロパティを設定するには

1. **Application.Resources ブロックを定義する:** app.xaml を開き、次の強調表示されているマークアップを追加します (まだ存在していない場合)。

    ```xaml
    <Application x:Class="AnimatedButton.App"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      StartupUri="Window1.xaml"
      >
      <Application.Resources>
        <!-- Resources for the entire application can be defined here. -->
      </Application.Resources>
    </Application>
    ```

     リソースのスコープは、リソースを定義する場所によって決まります。 app.xaml ファイルの `Application.Resources` でリソースを定義すると、アプリケーションのどこでもリソースを使用できるようになります。 リソースのスコープを定義する方法の詳細については、[XAML のリソース](../../../desktop-wpf/fundamentals/xaml-resources-define.md)に関する記事を参照してください。

2. **スタイルを作成し、それを使用して基本的なプロパティ値を定義する:** 次のマークアップを `Application.Resources` ブロックに追加します。 このマークアップで作成される <xref:System.Windows.Style> はアプリケーションのすべてのボタンに適用され、ボタンの <xref:System.Windows.FrameworkElement.Width%2A> が 90 に、<xref:System.Windows.FrameworkElement.Margin%2A> が 10 に設定されます。

    ```xaml
    <Application.Resources>
      <Style TargetType="Button">
        <Setter Property="Width" Value="90" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     <xref:System.Windows.Style.TargetType%2A> プロパティでは、スタイルが <xref:System.Windows.Controls.Button> 型のすべてのオブジェクトに適用されることが指定されます。 各 <xref:System.Windows.Setter> では、<xref:System.Windows.Style> に対して異なるプロパティ値が設定されます。 そのため、この時点では、アプリケーションのすべてのボタンは幅が 90、余白が 10 になっています。  F5 キーを押してアプリケーションを実行すると、次のようなウィンドウが表示されます。

     ![幅 90、余白 10 のボタン](./media/custom-button-animatedbutton-2.gif "custom_button_AnimatedButton_2")

     スタイルを使用すると、さまざまな方法による対象オブジェクトの微調整、複雑なプロパティ値の指定、他のスタイルに対する入力としてのスタイルの使用など、多くのことを行うことができます。 詳しくは、「 [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)」をご覧ください。

3. **リソースにスタイルのプロパティ値を設定する:** リソースを使用すると、一般的に定義されているオブジェクトと値を簡単に再利用できます。 特に、リソースを使用して複雑な値を定義し、コードのモジュール性を高めるのに便利です。 次の強調表示されているマークアップを app.xaml に追加します。

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush" StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
      </Style>
    </Application.Resources>
    ```

     `Application.Resources` ブロックのすぐ下には、"GrayBlueGradientBrush" という名前のリソースを作成してあります。 このリソースでは、水平方向のグラデーションが定義されています。 このリソースは、<xref:System.Windows.Controls.Control.Background%2A> プロパティに対するボタン スタイル セッターの内部など、アプリケーションの任意の場所からプロパティ値として使用できます。 これで、すべてのボタンにこのグラデーションの <xref:System.Windows.Controls.Control.Background%2A> プロパティ値が設定されました。

     F5 キーを押してアプリケーションを実行します。 次のような表示になります。

     ![グラデーション背景を持つボタン](./media/custom-button-animatedbutton-3.gif "custom_button_AnimatedButton_3")

## <a name="create-a-template-that-defines-the-look-of-the-button"></a>ボタンの外観を定義するテンプレートを作成する

このセクションでは、ボタンの外観 (プレゼンテーション) をカスタマイズするテンプレートを作成します。 ボタンのプレゼンテーションは、四角形などの複数のオブジェクトと、ボタンに固有の外観を提供するその他のコンポーネントで構成されています。

これまでのところ、アプリケーションでのボタンの外観の制御は、ボタンのプロパティの変更に限定されています。 ボタンの外観をさらに大きく変更するには、どうすればよいでしょうか。 テンプレートを使用すると、オブジェクトのプレゼンテーションを強力に制御できます。 テンプレートはスタイル内で使用できるため、スタイルが適用されるすべてのオブジェクト (このチュートリアルではボタン) に、テンプレートを適用できます。

### <a name="to-use-the-template-to-define-the-look-of-the-button"></a>テンプレートを使用してボタンの外観を定義するには

1. **テンプレートを設定する:** <xref:System.Windows.Controls.Button> のようなコントロールには <xref:System.Windows.Controls.Control.Template%2A> プロパティがあるため、<xref:System.Windows.Setter> を使用して <xref:System.Windows.Style> で設定した他のプロパティ値と同じように、テンプレート プロパティの値を定義できます。 次の強調表示されたマークアップを、ボタンのスタイルに追加します。

    ```xaml
    <Application.Resources>
      <LinearGradientBrush x:Key="GrayBlueGradientBrush"
        StartPoint="0,0" EndPoint="1,1">
        <GradientStop Color="DarkGray" Offset="0" />
        <GradientStop Color="#CCCCFF" Offset="0.5" />
        <GradientStop Color="DarkGray" Offset="1" />
      </LinearGradientBrush>
      <Style TargetType="{x:Type Button}">
        <Setter Property="Background" Value="{StaticResource GrayBlueGradientBrush}" />
        <Setter Property="Width" Value="80" />
        <Setter Property="Margin" Value="10" />
        <Setter Property="Template">
          <Setter.Value>
            <!-- The button template is defined here. -->
          </Setter.Value>
        </Setter>
      </Style>
    </Application.Resources>
    ```

2. **ボタンのプレゼンテーションを変更する:** この時点で、テンプレートを定義する必要があります。 次の強調表示されたマークアップを追加します。 このマークアップでは、角が丸い 2 つの <xref:System.Windows.Shapes.Rectangle> 要素と、その後で <xref:System.Windows.Controls.DockPanel> が指定されています。 <xref:System.Windows.Controls.DockPanel> は、ボタンの <xref:System.Windows.Controls.ContentPresenter> をホストするために使用されます。 <xref:System.Windows.Controls.ContentPresenter> では、ボタンの内容が表示されます。 このチュートリアルでは、内容はテキスト ("Button 1"、"Button 2"、"Button 3") です。 すべてのテンプレート コンポーネント (四角形と <xref:System.Windows.Controls.DockPanel>) は、<xref:System.Windows.Controls.Grid> の内部にレイアウトされます。

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="Button">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}" ClipToBounds="True">
          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}" RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />
          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch" VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20" Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />
          <!-- Present Content (text) of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20" Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>
      </ControlTemplate>
    </Setter.Value>
    ```

     F5 キーを押してアプリケーションを実行します。 次のような表示になります。

     ![3 個のボタンがあるウィンドウ](./media/custom-button-animatedbutton-4.gif)

3. **テンプレートにガラス効果を追加する:** 次に、ガラスを追加します。 まず、ガラスのグラデーション効果を作成するいくつかのリソースを作成します。 これらのグラデーション リソースを、`Application.Resources` ブロック内の任意の場所に追加します。

    ```xaml
    <Application.Resources>
      <GradientStopCollection x:Key="MyGlassGradientStopsResource">
        <GradientStop Color="WhiteSmoke" Offset="0.2" />
        <GradientStop Color="Transparent" Offset="0.4" />
        <GradientStop Color="WhiteSmoke" Offset="0.5" />
        <GradientStop Color="Transparent" Offset="0.75" />
        <GradientStop Color="WhiteSmoke" Offset="0.9" />
        <GradientStop Color="Transparent" Offset="1" />
      </GradientStopCollection>
      <LinearGradientBrush x:Key="MyGlassBrushResource"
        StartPoint="0,0" EndPoint="1,1" Opacity="0.75"
        GradientStops="{StaticResource MyGlassGradientStopsResource}" />
    <!-- Styles and other resources below here. -->
    ```

     これらのリソースは、ボタン テンプレートの <xref:System.Windows.Controls.Grid> に挿入する四角形の <xref:System.Windows.Shapes.Shape.Fill%2A> として使用されます。 次の強調表示されているマークアップをテンプレートに追加します。

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}" Height="{TemplateBinding Height}"
          ClipToBounds="True">

        <!-- Outer Rectangle with rounded corners. -->
        <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

        <!-- Inner Rectangle with rounded corners. -->
        <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="Transparent" StrokeThickness="20"
          Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20" />

        <!-- Glass Rectangle -->
        <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch"
          StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
          Fill="{StaticResource MyGlassBrushResource}"
          RenderTransformOrigin="0.5,0.5">
          <Rectangle.Stroke>
            <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
              <LinearGradientBrush.GradientStops>
                <GradientStop Offset="0.0" Color="LightBlue" />
                <GradientStop Offset="1.0" Color="Gray" />
              </LinearGradientBrush.GradientStops>
            </LinearGradientBrush>
          </Rectangle.Stroke>
          <!-- These transforms have no effect as they are declared here.
          The reason the transforms are included is to be targets
          for animation (see later). -->
          <Rectangle.RenderTransform>
            <TransformGroup>
              <ScaleTransform />
              <RotateTransform />
            </TransformGroup>
          </Rectangle.RenderTransform>
          <!-- A BevelBitmapEffect is applied to give the button a "Beveled" look. -->
          <Rectangle.BitmapEffect>
            <BevelBitmapEffect />
          </Rectangle.BitmapEffect>
        </Rectangle>

        <!-- Present Text of the button. -->
        <DockPanel Name="myContentPresenterDockPanel">
          <ContentPresenter x:Name="myContentPresenter" Margin="20"
            Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
        </DockPanel>
      </Grid>
    </ControlTemplate>
    </Setter.Value>
    ```

     `x:Name` プロパティが "glassCube" である四角形の <xref:System.Windows.UIElement.Opacity%2A> が 0 であることに注意してください。そのため、サンプルを実行すると、ガラスの四角形が上に重なって表示されません。 これは、ユーザーがボタンを操作したときのためのトリガーを、後でテンプレートに追加するためです。 ただし、<xref:System.Windows.UIElement.Opacity%2A> の値を 1 に変更してアプリケーションを実行すると、ボタンがどのように表示されるかを確認できます。 次の図を参照してください。 次のステップに進む前に、<xref:System.Windows.UIElement.Opacity%2A> を 0 に戻しておきます。

     ![XAML を使用して作成されたカスタム ボタン](./media/custom-button-animatedbutton-5.gif "custom_button_AnimatedButton_5")

## <a name="create-button-interactivity"></a>ボタンの操作機能を作成する

このセクションでは、ボタン上のマウス ポインターの移動やクリックなどのユーザーの操作に応じて、プロパティ値を変更してアニメーションを実行するための、プロパティ トリガーとイベント トリガーを作成します。

操作機能 (内部へのマウスの移動、外部へのマウスの移動、クリックなど) を追加する簡単な方法は、テンプレートまたはスタイル内でトリガーを定義することです。 <xref:System.Windows.Trigger> を作成するには、次のようなプロパティの "条件" を定義します: ボタンの <xref:System.Windows.UIElement.IsMouseOver%2A> プロパティの値が `true` と等しい。 次に、トリガー条件が true のときに実行されるセッター (アクション) を定義します。

### <a name="to-create-button-interactivity"></a>ボタンの操作機能を作成するには

1. **テンプレート トリガーを追加する:** 強調表示されたマークアップをテンプレートに追加します。

    ```xaml
    <Setter.Value>
      <ControlTemplate TargetType="{x:Type Button}">
        <Grid Width="{TemplateBinding Width}"
          Height="{TemplateBinding Height}" ClipToBounds="True">

          <!-- Outer Rectangle with rounded corners. -->
          <Rectangle x:Name="outerRectangle" HorizontalAlignment="Stretch"
          VerticalAlignment="Stretch" Stroke="{TemplateBinding Background}"
          RadiusX="20" RadiusY="20" StrokeThickness="5" Fill="Transparent" />

          <!-- Inner Rectangle with rounded corners. -->
          <Rectangle x:Name="innerRectangle" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch" Stroke="Transparent"
            StrokeThickness="20"
            Fill="{TemplateBinding Background}" RadiusX="20" RadiusY="20"
          />

          <!-- Glass Rectangle -->
          <Rectangle x:Name="glassCube" HorizontalAlignment="Stretch"
            VerticalAlignment="Stretch"
            StrokeThickness="2" RadiusX="10" RadiusY="10" Opacity="0"
            Fill="{StaticResource MyGlassBrushResource}"
            RenderTransformOrigin="0.5,0.5">
            <Rectangle.Stroke>
              <LinearGradientBrush StartPoint="0.5,0" EndPoint="0.5,1">
                <LinearGradientBrush.GradientStops>
                  <GradientStop Offset="0.0" Color="LightBlue" />
                  <GradientStop Offset="1.0" Color="Gray" />
                </LinearGradientBrush.GradientStops>
              </LinearGradientBrush>
            </Rectangle.Stroke>

            <!-- These transforms have no effect as they
                 are declared here.
                 The reason the transforms are included is to be targets
                 for animation (see later). -->
            <Rectangle.RenderTransform>
              <TransformGroup>
                <ScaleTransform />
                <RotateTransform />
              </TransformGroup>
            </Rectangle.RenderTransform>

              <!-- A BevelBitmapEffect is applied to give the button a
                   "Beveled" look. -->
            <Rectangle.BitmapEffect>
              <BevelBitmapEffect />
            </Rectangle.BitmapEffect>
          </Rectangle>

          <!-- Present Text of the button. -->
          <DockPanel Name="myContentPresenterDockPanel">
            <ContentPresenter x:Name="myContentPresenter" Margin="20"
              Content="{TemplateBinding  Content}" TextBlock.Foreground="Black" />
          </DockPanel>
        </Grid>

        <ControlTemplate.Triggers>       <!-- Set action triggers for the buttons and define            what the button does in response to those triggers. -->     </ControlTemplate.Triggers>
      </ControlTemplate>
    </Setter.Value>
    ```

2. **プロパティ トリガーを追加する:** 強調表示されたマークアップを `ControlTemplate.Triggers` ブロックに追加します。

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->   <Trigger Property="IsMouseOver" Value="True">     <!-- Below are three property settings that occur when the           condition is met (user mouses over button).  -->     <!-- Change the color of the outer rectangle when user           mouses over it. -->     <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <!-- Sets the glass opacity to 1, therefore, the           glass "appears" when user mouses over it. -->     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />     <!-- Makes the text slightly blurry as though you           were looking at it through blurry glass. -->     <Setter Property="ContentPresenter.BitmapEffect"        TargetName="myContentPresenter">       <Setter.Value>         <BlurBitmapEffect Radius="1" />       </Setter.Value>     </Setter>   </Trigger>

    <ControlTemplate.Triggers/>
    ```

     F5 キーを押してアプリケーションを実行し、ボタンの上にマウス ポインターを置いたときの効果を確認します。

3. **フォーカス トリガーを追加する:** 次に、ボタンにフォーカスが設定された場合 (ユーザーがクリックした後など) に対処する、同様のセッターを追加します。

    ```xaml
    <ControlTemplate.Triggers>

      <!-- Set properties when mouse pointer is over the button. -->
      <Trigger Property="IsMouseOver" Value="True">

        <!-- Below are three property settings that occur when the
             condition is met (user mouses over button).  -->
        <!-- Change the color of the outer rectangle when user          mouses over it. -->
        <Setter Property ="Rectangle.Stroke" TargetName="outerRectangle"
          Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />

        <!-- Sets the glass opacity to 1, therefore, the          glass "appears" when user mouses over it. -->
        <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />

        <!-- Makes the text slightly blurry as though you were          looking at it through blurry glass. -->
        <Setter Property="ContentPresenter.BitmapEffect"       TargetName="myContentPresenter">
          <Setter.Value>
            <BlurBitmapEffect Radius="1" />
          </Setter.Value>
        </Setter>
      </Trigger>
      <!-- Set properties when button has focus. -->   <Trigger Property="IsFocused" Value="true">     <Setter Property="Rectangle.Opacity" Value="1"       TargetName="glassCube" />     <Setter Property="Rectangle.Stroke" TargetName="outerRectangle"       Value="{DynamicResource {x:Static SystemColors.HighlightBrushKey}}" />     <Setter Property="Rectangle.Opacity" Value="1" TargetName="glassCube" />   </Trigger>

    </ControlTemplate.Triggers>
    ```

     F5 キーを押してアプリケーションを実行し、ボタンのいずれかをクリックします。 クリックした後もフォーカスがまだ設定されているため、ボタンが強調表示されたままになることに注意してください。 別のボタンをクリックすると、新しいボタンがフォーカスを取得し、前のボタンは失います。

4. <xref:System.Windows.UIElement.MouseEnter>**と**<xref:System.Windows.UIElement.MouseLeave> **に対するアニメーション** **を追加する:** 次に、トリガーにいくつかのアニメーションを追加します。 `ControlTemplate.Triggers` ブロック内の任意の場所に、次のマークアップを追加します。

    ```xaml
    <!-- Animations that start when mouse enters and leaves button. -->
    <EventTrigger RoutedEvent="Mouse.MouseEnter">
      <EventTrigger.Actions>
        <BeginStoryboard Name="mouseEnterBeginStoryboard">
          <Storyboard>
          <!-- This animation makes the glass rectangle shrink in the X direction. -->
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleX)"
              By="-0.1" Duration="0:0:0.5" />
            <!-- This animation makes the glass rectangle shrink in the Y direction. -->
            <DoubleAnimation
            Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[0].(ScaleTransform.ScaleY)"
              By="-0.1" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    <EventTrigger RoutedEvent="Mouse.MouseLeave">
      <EventTrigger.Actions>
        <!-- Stopping the storyboard sets all animated properties back to default. -->
        <StopStoryboard BeginStoryboardName="mouseEnterBeginStoryboard" />
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     マウス ポインターがボタンの上に移動するとガラスの四角形を小さくし、ポインターが離れると通常のサイズに戻します。

     ポインターがボタンの上に移動するとトリガーされるアニメーションが 2 つあります (<xref:System.Windows.UIElement.MouseEnter> イベントが発生します)。 これらのアニメーションでは、X 軸と Y 軸に沿ってガラスの四角形を縮小します。 <xref:System.Windows.Media.Animation.DoubleAnimation> 要素のプロパティ (<xref:System.Windows.Media.Animation.Timeline.Duration%2A> と <xref:System.Windows.Media.Animation.DoubleAnimation.By%2A>) に注意してください。 <xref:System.Windows.Media.Animation.Timeline.Duration%2A> ではアニメーションを 0.5 秒間実行することが指定されていて、<xref:System.Windows.Media.Animation.DoubleAnimation.By%2A> ではガラスを 10% 縮小することが指定されています。

     2 つ目のイベント トリガー (<xref:System.Windows.UIElement.MouseLeave>) では、最初のトリガーが単に停止されます。 <xref:System.Windows.Media.Animation.Storyboard> を停止すると、アニメーション化されたすべてのプロパティが既定値に戻ります。 このため、ユーザーがポインターをボタンの外に移動すると、ボタンはマウス ポインターがボタンの上に移動する前の状態に戻ります。 アニメーションの詳細については、「[アニメーションの概要](../graphics-multimedia/animation-overview.md)」を参照してください。

5. **ボタンがクリックされたときのアニメーションを追加する:** 最後のステップでは、ユーザーがボタンをクリックしたときのトリガーを追加します。 `ControlTemplate.Triggers` ブロック内の任意の場所に、次のマークアップを追加します。

    ```xaml
    <!-- Animation fires when button is clicked, causing glass to spin.  -->
    <EventTrigger RoutedEvent="Button.Click">
      <EventTrigger.Actions>
        <BeginStoryboard>
          <Storyboard>
            <DoubleAnimation Storyboard.TargetName="glassCube"
              Storyboard.TargetProperty=
              "(Rectangle.RenderTransform).(TransformGroup.Children)[1].(RotateTransform.Angle)"
              By="360" Duration="0:0:0.5" />
          </Storyboard>
        </BeginStoryboard>
      </EventTrigger.Actions>
    </EventTrigger>
    ```

     F5 キーを押してアプリケーションを実行し、ボタンのいずれかをクリックします。 ボタンをクリックすると、ガラスの四角形が回転します。

## <a name="summary"></a>まとめ
 このチュートリアルでは、次の演習を行いました。

- <xref:System.Windows.Style> の対象をオブジェクトの種類 (<xref:System.Windows.Controls.Button>) に設定しました。

- <xref:System.Windows.Style> を使用して、アプリケーション全体でボタンの基本プロパティを制御しました。

- <xref:System.Windows.Style> のセッターのプロパティ値に使用する、グラデーションなどのリソースを作成しました。

- ボタンにテンプレートを適用することにより、アプリケーション全体でボタンの外観をカスタマイズしました。

- アニメーション効果など、ユーザーの操作 (<xref:System.Windows.UIElement.MouseEnter>、<xref:System.Windows.UIElement.MouseLeave>、<xref:System.Windows.Controls.Primitives.ButtonBase.Click> など) に応じてボタンの動作をカスタマイズしました。

## <a name="see-also"></a>関連項目

- [Microsoft Expression Blend を使用してボタンを作成する](walkthrough-create-a-button-by-using-microsoft-expression-blend.md)
- [スタイルとテンプレート](../../../desktop-wpf/fundamentals/styles-templates-overview.md)
- [アニメーションの概要](../graphics-multimedia/animation-overview.md)
- [純色およびグラデーションによる塗りつぶしの概要](../graphics-multimedia/painting-with-solid-colors-and-gradients-overview.md)
- [ビットマップ効果の概要](../graphics-multimedia/bitmap-effects-overview.md)
