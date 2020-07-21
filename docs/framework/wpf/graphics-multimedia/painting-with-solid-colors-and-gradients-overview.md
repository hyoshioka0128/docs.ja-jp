---
title: 純色およびグラデーションによる塗りつぶしの概要
description: Windows Presentation Foundation (WPF) でオブジェクトを使用して、純色、線状グラデーション、放射状グラデーションで塗りつぶす方法について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- solid colors [WPF], painting with
- painting with gradients [WPF]
- gradients [WPF], painting with
- brushes [WPF], painting with solid colors
- brushes [WPF], painting with gradients
- painting with solid colors [WPF]
ms.assetid: f5b182f3-c5c7-4cbe-9f2f-65e690d08255
ms.openlocfilehash: 957593d758afda06db106c99f6695294d4f84f73
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853664"
---
# <a name="painting-with-solid-colors-and-gradients-overview"></a>純色およびグラデーションによる塗りつぶしの概要

このトピックでは、<xref:System.Windows.Media.SolidColorBrush>、<xref:System.Windows.Media.LinearGradientBrush>、<xref:System.Windows.Media.RadialGradientBrush> オブジェクトを使用して、純色、線状グラデーション、放射状グラデーションで塗りつぶす方法について説明します。

<a name="solidcolor"></a>

## <a name="painting-an-area-with-a-solid-color"></a>領域を純色で塗りつぶす

すべてのプラットフォームで最も一般的な操作の 1 つとして、領域を濃淡のない <xref:System.Windows.Media.Color> で塗りつぶすことがあります。 このタスクを実現するために、[!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] では <xref:System.Windows.Media.SolidColorBrush> クラスが提供されます。 以下のセクションでは、<xref:System.Windows.Media.SolidColorBrush> で塗りつぶすさまざまな方法について説明します。

<a name="solidcolorinxaml"></a>

### <a name="using-a-solidcolorbrush-in-xaml"></a>"XAML" での SolidColorBrush の使用

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] で領域を純色で塗りつぶすには、次のオプションのいずれかを使用します。

- 定義済みの純色のブラシを名前で選択します。  たとえば、ボタンの <xref:System.Windows.Controls.Control.Background%2A> を "Red" または "MediumBlue" に設定できます。  その他の定義済みの純色ブラシの一覧については、<xref:System.Windows.Media.Brushes> クラスの静的プロパティを参照してください。 次に例を示します。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushNamedColor1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushnamedcolor1xaml)]

- 赤、緑、および青の量を指定して単一の純色に結合することで、32 ビット カラー パレットからカラーを選択します。  32 ビット パレットからカラーを指定するための書式は、" *#rrggbb*" です。ここで、*rr* は赤の相対的な量を指定する 2 桁の 16 進数であり、*gg* は緑の量を、*bb*は青の量を指定します。  さらに、カラーは、"#*aarrggbb*" として指定することもできます。ここで、*aa* はカラーの*アルファ*値 (透明度) を指定します。 この方法により、部分的に透明な色を作成することができます。  次の例では、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> は、16 進数表記を使用して完全に不透明な赤に設定されています。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushHex1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushhex1xaml)]

- プロパティ タグ構文を使用して、<xref:System.Windows.Media.SolidColorBrush> を記述します。 この構文は冗長ですが、ブラシの不透明度などの追加設定を指定することができます。 次の例では、2 つの <xref:System.Windows.Controls.Button> 要素の <xref:System.Windows.Controls.Control.Background%2A> プロパティが完全に不透明な赤に設定されています。 最初のブラシの色は、定義済みの色の名前を使用して記述されています。 2 番目のブラシの色は、16 進表記で記述されています。

  [!code-xaml[BrushOverviewExamples_snip#SolidColorBrushPropertyTag1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/BrushOverviewExamples_snip/XAML/SolidColorBrushExample.xaml#solidcolorbrushpropertytag1xaml)]

<a name="solidcolorsincode"></a>

### <a name="painting-with-a-solidcolorbrush-in-code"></a>コードでの SolidColorBrush による塗りつぶし

コードで領域を純色で塗りつぶすには、次のオプションのいずれかを使用します。

- <xref:System.Windows.Media.Brushes> クラスによって提供される定義済みのブラシのいずれかを使用します。 次の例では、<xref:System.Windows.Controls.Button> の <xref:System.Windows.Controls.Control.Background%2A> が <xref:System.Windows.Media.Brushes.Red%2A> に設定されています。

  [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedBrush1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedbrush1csharp)]

- <xref:System.Windows.Media.SolidColorBrush> を作成し、<xref:System.Windows.Media.Color> 構造体を使用して、その <xref:System.Windows.Media.SolidColorBrush.Color%2A> プロパティを設定します。 <xref:System.Windows.Media.Colors> クラスの定義済みの色を使用することも、静的な <xref:System.Windows.Media.Color.FromArgb%2A> メソッドを使用して <xref:System.Windows.Media.Color> を作成することもできます。

  次の例では、定義済みの色を使用して、<xref:System.Windows.Media.SolidColorBrush> の <xref:System.Windows.Media.SolidColorBrush.Color%2A> プロパティを設定する方法を示しています。

  [!code-csharp[BrushOverviewExamples_snip#SolidColorBrushPredefinedColor1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushpredefinedcolor1csharp)]

静的な <xref:System.Windows.Media.Color.FromArgb%2A> では、色のアルファ、赤、緑、青の値を指定できます。 これらの各値の一般的な範囲は、0 ～ 255 です。 たとえば、アルファ値 0 はカラーが完全に透明であることを示し、値 255 はカラーが完全に不透明であることを示します。 同様に、赤値 0 はカラーに赤が全く含まれないことを示し、値 255 は可能な最大量の赤が含まれることを示します。  次の例では、ブラシのカラーは、アルファ、赤、緑、および青の値を指定することで記述されています。

[!code-csharp[BrushOverviewExamples_snip#SolidColorBrushfromArgbExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/BrushOverviewExamples_snip/CSharp/SolidColorBrushExample.cs#solidcolorbrushfromargbexample1csharp)]

色を指定するその他の方法については、<xref:System.Windows.Media.Color> リファレンス トピックを参照してください。

<a name="gradient"></a>

## <a name="painting-an-area-with-a-gradient"></a>領域をグラデーションで塗りつぶす

グラデーション ブラシは、軸に沿って互いに溶け込む複数の色で領域を塗りつぶします。 これらを使用して、光と影の感じを作り出して、コントロールを立体的に見せることができます。 ガラス、クロム メッキ、水、その他の滑らかな表面をシミュレートするためにも使用できます。  [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] では、<xref:System.Windows.Media.LinearGradientBrush> と <xref:System.Windows.Media.RadialGradientBrush> という 2 種類のグラデーション ブラシが提供されます。

<a name="lineargradientbrush"></a>

## <a name="linear-gradients"></a>線状グラデーション

<xref:System.Windows.Media.LinearGradientBrush> では、直線 ("*グラデーション軸*") に沿って定義されたグラデーションを使用して領域を塗りつぶします。  グラデーションの色とグラデーション軸に沿った位置は、<xref:System.Windows.Media.GradientStop> オブジェクトを使用して指定します。  グラデーション軸を変更することもできます。これにより、水平方向と垂直方向のグラデーションの作成やグラデーションの方向の反転を行うことができます。 グラデーション軸については、次のセクションで説明します。 既定では、対角線方向のグラデーションが作成されます。

次の例では、4 津のカラーを使用して線状グラデーションを作成するコードを示します。

[!code-xaml[GradientBrushExamples_snip#DiagonalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#diagonalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#DiagonalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#diagonalgradient1csharp)]

このコードを実行すると、次のグラデーションが生成されます。

![対角線方向の線状グラデーション](./media/wcpsdk-graphicsmm-diaglgradient-nolabel.jpg "wcpsdk_graphicsmm_diaglgradient_nolabel")

> [!NOTE]
> このトピックのグラデーションの例では、始点と終点の設定で既定の座標系を使用しています。 既定の座標系は、境界ボックスに対して相対的です。0 は境界ボックスの 0% を示し、1 は境界ボックスの 100% を示します。 この座標系は、<xref:System.Windows.Media.GradientBrush.MappingMode%2A> プロパティを <xref:System.Windows.Media.BrushMappingMode.Absolute> の値に設定することで変更できます。 絶対座標系は、境界ボックスに相対しません。 値は、ローカル空間に直接変換されます。

<xref:System.Windows.Media.GradientStop> は、グラデーション ブラシの基本的な構成要素です。  グラデーション境界では、グラデーション軸に沿って <xref:System.Windows.Media.GradientStop.Offset%2A> に <xref:System.Windows.Media.GradientStop.Color%2A> を指定します。

- グラデーション境界の <xref:System.Windows.Media.GradientStop.Color%2A> プロパティでは、グラデーション境界の色を指定します。 色は、定義済みの色 (<xref:System.Windows.Media.Colors> クラスによって提供される) を使用するか、ScRGB または ARGB 値を指定することで設定できます。 [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、16 進表記を使用してカラーを記述することもできます。 詳細については、「<xref:System.Windows.Media.Color> 構造体」を参照してください。

- グラデーション境界の <xref:System.Windows.Media.GradientStop.Offset%2A> プロパティでは、グラデーション軸上のグラデーション境界の位置を指定します。 オフセットは、0 から 1 の範囲の <xref:System.Double> です。 グラデーション境界のオフセット値が 0 に近ければ近いほど、カラーはグラデーションの始まりに近づきます。 グラデーションのオフセット値が 1 に近ければ近いほど、カラーはグラデーションの終わりに近づきます。

グラデーション境界の間の各点のカラーは、2 つのグラデーション境界によって指定されたカラーの混合として線形補間されます。 次の図は、前の例のグラデーション境界を強調しています。 円はグラデーション境界の位置をマークし、破線はグラデーション軸を示しています。

![線状グラデーションのグラデーション境界](./media/wcpsdk-graphicsmm-4gradientstops.png "wcpsdk_graphicsmm_4gradientstops")

最初のグラデーション境界は、オフセット`0.0` に黄色を指定しています。  2 番目のグラデーション境界は、オフセット `0.25` に赤色を指定しています。  これら 2 つの境界の間の点は、グラデーション軸に沿って左から右に移動するにつれて、黄色から徐々に赤色に変化します。  3 番目のグラデーション境界は、オフセット `0.75` に青色を指定しています。  2 番目と 3 番目のグラデーション境界の間の点は、赤から青に徐々に変化します。 4 番目のグラデーション境界は、オフセット `1.0` に緑色を指定しています。 3 番目と 4 番目のグラデーション境界の間の点は、青から緑に徐々に変化します。

<a name="gradientaxis"></a>

### <a name="the-gradient-axis"></a>グラデーション軸

前述のように、線状グラデーション ブラシのグラデーション境界は、直線のグラデーション軸に沿って配置されます。 ブラシの <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> および <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> プロパティを使用して、線の向きとサイズを変更することができます。 ブラシの <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> と <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> を操作することで、水平および垂直グラデーションを作成したり、グラデーションの方向を逆にしたり、グラデーションの広がりを凝縮したりすることができます。

既定では、線状グラデーション ブラシの <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> と <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> は、塗りつぶされる領域に相対的となります。 点 (0, 0) は塗りつぶされる領域の左上隅を、点 (1, 1) は塗りつぶされる領域の右下隅を表します。 <xref:System.Windows.Media.LinearGradientBrush> の既定の <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> は (0,0) で、その既定の <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> は (1,1) です。これにより、塗りつぶされる領域の左上隅から始まり、右下隅に伸びる対角線方向のグラデーションが作成されます。 次の図では、既定の <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> と <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> を使用した線状グラデーション ブラシのグラデーション軸が示されています。

![対角線方向の線状グラデーションのグラデーション軸](./media/wcpsdk-graphicsmm-diagonalgradientaxis.png "wcpsdk_graphicsmm_diagonalgradientaxis")

次の例では、ブラシの <xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> と <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> を指定して、水平グラデーションを作成する方法を示します。 グラデーション境界は前の例と同じであることに注目してください。<xref:System.Windows.Media.LinearGradientBrush.StartPoint%2A> と <xref:System.Windows.Media.LinearGradientBrush.EndPoint%2A> の変更だけで、グラデーションが対角線方向から水平方向に変更されています。

[!code-xaml[GradientBrushExamples_snip#HorizontalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#horizontalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#HorizontalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#horizontalgradient1csharp)]

次の図は、作成されるグラデーションを示しています。 グラデーション軸は破線でマークされ、グラデーション境界は円でマークされています。

![水平方向の線状グラデーションのグラデーション軸](./media/wcpsdk-graphicsmm-horizontalgradient.jpg "wcpsdk_graphicsmm_horizontalgradient")

次の例では、垂直方向のグラデーションを作成する方法を示します。

[!code-xaml[GradientBrushExamples_snip#VerticalGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/LinearGradientBrushExample.xaml#verticalgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#VerticalGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/LinearGradientBrushExample.cs#verticalgradient1csharp)]

次の図は、作成されるグラデーションを示しています。 グラデーション軸は破線でマークされ、グラデーション境界は円でマークされています。

![垂直グラデーションのグラデーション軸](./media/wcpsdk-graphicsmm-verticalgradient.jpg "wcpsdk_graphicsmm_verticalgradient")

<a name="radialgradients"></a>

## <a name="radial-gradients"></a>放射状グラデーション

<xref:System.Windows.Media.LinearGradientBrush> と同様に、<xref:System.Windows.Media.RadialGradientBrush> では、軸に沿ってブレンドされる色で領域を塗りつぶします。 前の例では、線状グラデーション ブラシの軸は直線であることを示しました。 放射状グラデーション ブラシの軸は円によって定義され、そのカラーはその原点から外側に "放射" されます。

次の例では、放射状グラデーション ブラシを使用して、四角形の内側を塗りつぶします。

[!code-xaml[GradientBrushExamples_snip#RadialGradient1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/RadialGradientBrushExample.xaml#radialgradient1xaml)]

[!code-csharp[GradientBrushExamples_snip#RadialGradient1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/RadialGradientBrushExample.cs#radialgradient1csharp)]

次の図は、前の例で作成されるグラデーションを示しています。 ブラシのグラデーション境界が強調されています。 結果は異なっていますが、この例のグラデーション境界は、前の線状グラデーション ブラシの例のグラデーション境界と同じであることに注目してください。

![放射状グラデーションのグラデーション境界](./media/wcpsdk-graphicsmm-4gradientstops-rg.png "wcpsdk_graphicsmm_4gradientstops_rg")

<xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A> では、放射状グラデーション ブラシのグラデーション軸の始点を指定します。 グラデーション軸は、グラデーションの原点からグラデーション円に放射状に広がります。 ブラシのグラデーション円は、その <xref:System.Windows.Media.RadialGradientBrush.Center%2A>、<xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A>、<xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A> プロパティによって定義されます。

次の図には、<xref:System.Windows.Media.RadialGradientBrush.GradientOrigin%2A>、<xref:System.Windows.Media.RadialGradientBrush.Center%2A>、<xref:System.Windows.Media.RadialGradientBrush.RadiusX%2A>、<xref:System.Windows.Media.RadialGradientBrush.RadiusY%2A> の設定が異なる複数の放射状グラデーションが示されています。

![RadialGradientBrush の設定](./media/wcpsdk-graphicsmm-originscirclesandradii.gif "wcpsdk_graphicsmm_originscirclesandradii")GradientOrigin、Center、RadiusX、および RadiusY の設定が異なる RadialGradientBrushes。

<a name="specifyinggradientcolors"></a>

## <a name="specifying-transparent-or-partially-transparent-gradient-stops"></a>透明または部分的に透明なグラデーション境界の指定

グラデーション境界では不透明度プロパティが提供されないため、ARGB の 16 進表記を使用して色のアルファ チャネルをマークアップに指定するか、<xref:System.Windows.Media.Color.FromScRgb%2A?displayProperty=nameWithType> メソッドを使用して透明または部分的に透明なグラデーション境界を作成する必要があります。 以降のセクションで、部分的に透明なグラデーション境界を [!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] とコードで作成する方法を説明します。

<a name="argbsyntax"></a>

### <a name="specifying-color-opacity-in-xaml"></a>"XAML" でのカラーの不透明度の指定

[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)] では、ARGB の 16 進表記を使用して、個々のカラーの不透明度を指定します。 ARGB の 16 進表記では、次の構文を使用します。

`#` **aa** *rrggbb*

前の行の *aa* は、カラーの不透明度を指定するために使用する 2 桁の 16 進値を表します。 *rr*、*gg*、および *bb* は、それぞれ、カラーの赤、緑、および青の量を指定するために使用される 2 桁の 16 進値を表します。 各 16 進数には、0 ～ 9 または A ～ F の値を指定できます。 0 は最小値であり、F は最大値です。 アルファ値 00 は完全に透明なカラーを指定し、アルファ値 FF は完全に不透明なカラーを指定します。  次の例では、2 つの色を指定するために ARGB の 16 進表記が使用されています。 1 つ目は部分的に透明 (アルファ値 x20 ) であり、2 つ目は完全に不透明です。

[!code-xaml[GradientBrushExamples_snip#TransparentGradientStopExample1XAML](~/samples/snippets/xaml/VS_Snippets_Wpf/GradientBrushExamples_snip/XAML/GradientStopsExample.xaml#transparentgradientstopexample1xaml)]

<a name="fromscrgbsyntax"></a>

### <a name="specifying-color-opacity-in-code"></a>コードでのカラーの不透明度の指定

コードを使用する場合、静的な <xref:System.Windows.Media.Color.FromArgb%2A> メソッドを使って、色の作成時にアルファ値を指定できます。 このメソッドでは、<xref:System.Byte> 型の 4 つのパラメーターを受け取ります。 最初のパラメーターはカラーのアルファ チャネルを指定し、その他の 3 つのパラメーターはカラーの赤、緑、および青の値を指定します。 各値は、0 ～ 255 (0 と 255 を含む) の数値にする必要があります。 アルファ値 0 はカラーが完全に透明であることを指定し、アルファ値 255 はカラーが完全に不透明であることを指定します。 次の例では、2 つの色を生成するために <xref:System.Windows.Media.Color.FromArgb%2A> メソッドが使用されています。 1 つ目のカラーは部分的に透明 (アルファ値32) であり、2 つ目のカラーは完全に不透明です。

[!code-csharp[GradientBrushExamples_snip#TransparentGradientStopExample1CSharp](~/samples/snippets/csharp/VS_Snippets_Wpf/GradientBrushExamples_snip/CSharp/GradientStopsExample.cs#transparentgradientstopexample1csharp)]

<xref:System.Windows.Media.Color.FromScRgb%2A> メソッドを使用することもできます。これにより、ScRGB 値を使用して色を作成できます。

<a name="otherbrushes"></a>

## <a name="painting-with-images-drawings-visuals-and-patterns"></a>イメージ、描画、ビジュアル、およびパターンによる塗りつぶし

<xref:System.Windows.Media.ImageBrush>、<xref:System.Windows.Media.DrawingBrush>、<xref:System.Windows.Media.VisualBrush> クラスでは、イメージ、描画、またはビジュアルで領域を塗りつぶすことができます。 イメージ、描画、およびパターンによる塗りつぶしの詳細については、「[イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。

## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Brush>
- <xref:System.Windows.Media.SolidColorBrush>
- <xref:System.Windows.Media.LinearGradientBrush>
- <xref:System.Windows.Media.RadialGradientBrush>
- [イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)
- [ブラシの変換の概要](brush-transformation-overview.md)
- [グラフィックスの描画層](../advanced/graphics-rendering-tiers.md)
