---
title: パス マークアップ構文
description: Windows Presentation Foundation (WPF) でコンパクト パス ジオメトリを指定するために使用できる、強力で複雑なミニ言語について説明します。
ms.date: 03/30/2017
helpviewer_keywords:
- attribute usage in XAML [WPF]
- XAML [WPF], attribute usage
- graphics [WPF], PathGeometry class
- XAML [WPF], object element usage
ms.assetid: b8586241-a02d-486e-9223-e1e98e047f41
ms.openlocfilehash: 6d2778522b622f0b0dcb59673e793a6d772a4b4f
ms.sourcegitcommit: b6a1869f97a37f11a68c90afde1a520a6887dcbc
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85853650"
---
# <a name="path-markup-syntax"></a>パス マークアップ構文
パスについては、「[WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)」と「[ジオメトリの概要](geometry-overview.md)」で説明されていますが、このトピックでは、[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] を使用してパス ジオメトリをよりコンパクトに指定するために使用できる強力で複雑なミニ言語について詳しく説明します。  
  
<a name="prerequisites"></a>
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックを理解するには、<xref:System.Windows.Media.Geometry> オブジェクトの機能についてよく理解している必要があります。 詳細については、「[ジオメトリの概要](geometry-overview.md)」をご覧ください。  
  
<a name="abouthisdocument"></a>
## <a name="streamgeometry-and-pathfigurecollection-mini-languages"></a>StreamGeometry ミニ言語と PathFigureCollection ミニ言語  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] には、ジオメトリック パスを記述するためのミニ言語を提供する <xref:System.Windows.Media.StreamGeometry> と <xref:System.Windows.Media.PathFigureCollection> の2つのクラスが用意されています。  
  
- <xref:System.Windows.Media.StreamGeometry> ミニ言語は、<xref:System.Windows.UIElement> の <xref:System.Windows.UIElement.Clip%2A> プロパティや <xref:System.Windows.Shapes.Path> 要素の <xref:System.Windows.Shapes.Path.Data%2A> プロパティなど、<xref:System.Windows.Media.Geometry> 型のプロパティを設定するときに使用します。 次の例では、属性構文を使用して <xref:System.Windows.Media.StreamGeometry> を作成します。  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMStreamGeometryAttributeSyntaxInline](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmstreamgeometryattributesyntaxinline)]  
  
- <xref:System.Windows.Media.PathFigureCollection> ミニ言語は、<xref:System.Windows.Media.PathGeometry> の <xref:System.Windows.Media.PathGeometry.Figures%2A> プロパティを設定するときに使用します。 次の例では、属性構文を使用して <xref:System.Windows.Media.PathGeometry> の <xref:System.Windows.Media.PathFigureCollection> を作成します。  
  
     [!code-xaml[GeometrySample_snip_XAML#GraphicsMMPathFigureCollectionAttributeSyntaxInline](~/samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample_snip_XAML/CS/MiniLanguageExample.xaml#graphicsmmpathfigurecollectionattributesyntaxinline)]  
  
 前の例からわかるように、2 つのミニ言語はほとんど同じです。 <xref:System.Windows.Media.StreamGeometry> を使用できる状況であれば常に <xref:System.Windows.Media.PathGeometry> を使用できますが、どちらを使用すればよいでしょうか。 作成後にパスを変更する必要がない場合は <xref:System.Windows.Media.StreamGeometry> を使用し、パスを変更する必要がある場合は <xref:System.Windows.Media.PathGeometry> を使用します。  
  
 <xref:System.Windows.Media.PathGeometry> と <xref:System.Windows.Media.StreamGeometry> オブジェクトの相違点の詳細については、「[ジオメトリの概要](geometry-overview.md)」をご覧ください。  
  
### <a name="a-note-about-white-space"></a>空白についてのメモ  
 簡潔にするために、この後のセクションで示す構文には 1 つの空白が使用されていますが、1 つの空白を使用できるところでは、常に複数の空白スペースも許容されます。  
  
 2 つの数値は、実際にはコンマまたは空白で区切る必要はありません。ただし、これが可能なのは、結果の文字列があいまいにならない場合のみです。 たとえば、`2..3` は実際には 2 つの数値 ("2." と ".3" ) です。 同様に、`2-3` は "2" と "-3" です。 どちらの場合も、コマンドの前後に空白は必要ありません。  
  
### <a name="syntax"></a>構文  
 <xref:System.Windows.Media.StreamGeometry> の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 属性使用構文は、省略可能な <xref:System.Windows.Media.FillRule> 値と 1 つ以上の図の説明で構成されています。  
  
|StreamGeometry XAML 属性使用構文|  
|-----------------------------------------|  
|`<` *object* *property* `="`[ `fillRule`] `figureDescription`[ `figureDescription`]* `" ... />`|  
  
 <xref:System.Windows.Media.PathFigureCollection> の [!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)] 属性使用構文は、1 つ以上の図の説明で構成されています。  
  
|PathFigureCollection XAML 属性使用構文|  
|-----------------------------------------------|  
|`<` *object* *property* `="` `figureDescription`[ `figureDescription`]* `" ... />`|  
  
|用語|説明|  
|----------|-----------------|  
|*fillRule*|<xref:System.Windows.Media.FillRule?displayProperty=nameWithType><br /><br /> <xref:System.Windows.Media.StreamGeometry> が <xref:System.Windows.Media.FillRule.EvenOdd> と <xref:System.Windows.Media.FillRule.Nonzero><xref:System.Windows.Media.PathGeometry.FillRule%2A> のどちらを使用するかを指定します。<br /><br /> -   `F0` は、<xref:System.Windows.Media.FillRule.EvenOdd> の塗りつぶし規則を指定します。<br />-   `F1` は、<xref:System.Windows.Media.FillRule.Nonzero> の塗りつぶし規則を指定します。<br /><br /> このコマンドを省略した場合、サブパスは既定の動作 (<xref:System.Windows.Media.FillRule.EvenOdd>) を使用します。 このコマンドを指定する場合は、先頭に配置する必要があります。|  
|*figureDescription*|移動コマンドと描画コマンド (および省略可能な閉じるコマンド) で構成される図形。<br /><br /> `moveCommand` `drawCommands` `[` `closeCommand` `]`|  
|*moveCommand*|図形の開始位置を指定する移動コマンド。 「[Move コマンド](#themovecommand)」セクションをご覧ください。|  
|*drawCommands*|図の内容を記述する 1 つまたは複数の描画コマンド。 「[描画コマンド](#drawcommands)」セクションをご覧ください。|  
|*closeCommand*|図形を閉じるコマンド (省略可能)。 「[閉じるコマンド](#closecommand)」セクションをご覧ください。|  
  
<a name="themovecommand"></a>
## <a name="move-command"></a>移動コマンド  
 新しい図形の始点を指定します。  
  
|構文|  
|------------|  
|`M` *startPoint*<br /><br /> または<br /><br /> `m` *startPoint*|  
  
|用語|説明|  
|----------|-----------------|  
|*startPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 新しい図形の始点。|  
  
 大文字 `M` は `startPoint` が絶対値であることを示します。小文字 `m` は `startPoint` がその前の点に対するオフセットであることを示します。前の点が存在しない場合は (0,0) になります。 移動コマンドの後ろに複数の点を指定した場合は、直線コマンドを指定した場合でも、これらの点を結ぶ線が描画されます。  
  
<a name="drawcommands"></a>
## <a name="draw-commands"></a>描画コマンド  
 描画コマンドは、さまざまな図形コマンドで構成できます。 次の図形のコマンドを使用できます。直線、水平線、垂直線、3 次ベジエ曲線、2 次ベジエ曲線、スムーズ 3 次ベジエ曲線、スムーズ 2 次ベジエ曲線、および楕円の円弧。  
  
 各コマンドは、大文字または小文字で入力します。大文字は絶対値を、小文字は相対値を表し、そのセグメントの制御点は、前の例の終点を基準とします。 同じ種類の複数のコマンドを続けて入力する場合は、重複するコマンドの入力を省略できます。たとえば、`L 100,200 300,400` は `L 100,200 L 300,400` と同等です。 次の表で、**移動**コマンドと**描画**コマンドを説明します。  
  
### <a name="line-command"></a>直線コマンド  
 現在の点と指定された終点の間に直線を作成します。 `l 20 30` と `L 20,30` は、有効な**直線**コマンドの例です。  
  
|構文|  
|------------|  
|`L` *endPoint*<br /><br /> または<br /><br /> `l` *endPoint*|  
  
|用語|説明|  
|----------|-----------------|  
|*endPoint*|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 線の終点。|  

大文字 `L` は `endPoint` が絶対値であることを示します。小文字 `l` は `endPoint` がその前の点に対するオフセットであることを示します。前の点が存在しない場合は (0,0) になります。

### <a name="horizontal-line-command"></a>水平線コマンド  
 現在の点と指定された x 座標の間に水平線を作成します。 `H 90` は、有効な水平線コマンドの例です。

|構文|  
|------------|  
|`H`  *x*<br /><br /> または<br /><br /> `h`  *x*|  
  
|用語|説明|  
|----------|-----------------|  
|*x*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 直線の終点の x 座標。|  
  
大文字 `H` は `x` が絶対値であることを示します。小文字 `h` は `x` がその前の点に対するオフセットであることを示します。前の点が存在しない場合は (0,0) になります。
  
### <a name="vertical-line-command"></a>垂直線コマンド  
 現在の点と指定された y 座標の間に垂直線を作成します。 `v 90` は、有効な垂直線コマンドの例です。

|構文|  
|------------|  
|`V`  *y*<br /><br /> または<br /><br /> `v`  *y*|  
  
|用語|説明|  
|----------|-----------------|  
|*y*|<xref:System.Double?displayProperty=nameWithType><br /><br /> 直線の終点の y 座標。|  

大文字 `V` は `y` が絶対値であることを示します。小文字 `v` は `y` がその前の点に対するオフセットであることを示します。前の点が存在しない場合は (0,0) になります。  

### <a name="cubic-bezier-curve-command"></a>3 次ベジエ曲線コマンド  
 指定された 2 つの制御点 (`controlPoint`1 と `controlPoint`2) を使用して、現在の点と指定された終点の間に 3 次ベジエ曲線を作成します。 `C 100,200 200,400 300,200` は、有効な曲線コマンドの例です。  
  
|構文|  
|------------|  
|`C` `controlPoint`1`controlPoint`2`endPoint`<br /><br /> または<br /><br /> `c` `controlPoint`1`controlPoint`2`endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`1|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の 1 つ目の制御点。曲線の前半の接線を決定します。|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の 2 つ目の制御点。曲線の後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="quadratic-bezier-curve-command"></a>2 次ベジエ曲線コマンド  
 指定された制御点 (`controlPoint`) を使用して、現在の点と指定された終点の間に 2 次ベジエ曲線を作成します。 `q 100,200 300,200` は、有効な 2 次ベジエ曲線コマンドの例です。  
  
|構文|  
|------------|  
|`Q` `controlPoint` `endPoint`<br /><br /> または<br /><br /> `q` `controlPoint` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の前半と後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="smooth-cubic-bezier-curve-command"></a>スムーズ 3 次ベジエ曲線コマンド  
 現在の点と指定された終点の間に 3 次ベジエ曲線を作成します。 1 つ目の制御点は、現在の点に対する前のコマンドの 2 つ目の制御点のリフレクションと見なされます。 前のコマンドが存在しない場合、または前のコマンドが 3 次ベジエ曲線コマンドまたはスムーズ 3 次ベジエ曲線コマンドでなかった場合、1 つ目の制御点は、現在の点と一致するとみなされます。 2 つ目の制御点 (曲線の後半の制御点) は、`controlPoint`2 で指定されます。 たとえば、`S 100,200 200,300` は有効なスムーズ 3 次ベジエ曲線コマンドです。  
  
|構文|  
|------------|  
|`S` `controlPoint`2`endPoint`<br /><br /> または<br /><br /> `s` `controlPoint`2`endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`2|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の後半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="smooth-quadratic-bezier-curve-command"></a>スムーズ 2 次ベジエ曲線コマンド  
 現在の点と指定された終点の間に 2 次ベジエ曲線を作成します。 制御点は、現在の点に対する前のコマンドの制御点のリフレクションと見なされます。 前のコマンドが存在しない場合、または前のコマンドが 2 次ベジエ曲線コマンドまたはスムーズ 2 次ベジエ曲線コマンドでなかった場合、制御点は、現在の点と一致するとみなされます。  
  
|構文|  
|------------|  
|`T` `controlPoint` `endPoint`<br /><br /> または<br /><br /> `t` `controlPoint` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`controlPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線の制御点。曲線の前半の接線を決定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 曲線が描画される点。|  
  
### <a name="elliptical-arc-command"></a>楕円の円弧コマンド  
 現在の点と指定された終点の間に楕円の円弧を作成します。  
  
|構文|  
|------------|  
|`A` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`<br /><br /> または<br /><br /> `a` `size` `rotationAngle` `isLargeArcFlag` `sweepDirectionFlag` `endPoint`|  
  
|用語|説明|  
|----------|-----------------|  
|`size`|<xref:System.Windows.Size?displayProperty=nameWithType><br /><br /> 円弧の x 半径と y 半径。|  
|`rotationAngle`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 楕円の回転 (度単位)。|  
|`isLargeArcFlag`|円弧の角度を 180 度以上にする場合は 1 に設定します。それ以外の場合は 0 に設定します。|  
|`sweepDirectionFlag`|円弧が正の角度の方向に描画される場合は 1 に設定します。それ以外の場合は 0 に設定します。|  
|`endPoint`|<xref:System.Windows.Point?displayProperty=nameWithType><br /><br /> 円弧が描画される点。|  
  
<a name="closecommand"></a>
## <a name="the-close-command"></a>閉じるコマンド  
 現在の図形を終了し、現在の点と図の開始点を結ぶ線を作成します。 このコマンドは、図形の最初のセグメントと最後のセグメントの間に線結合 (コーナー) を作成します。  
  
|構文|  
|------------|  
|`Z`<br /><br /> または<br /><br /> `z`|  

<a name="pointsyntax"></a>
## <a name="point-syntax"></a>点の構文  
 (0, 0) が左上隅になる点の x 座標と y 座標を記述します。
  
|構文|  
|------------|  
|`x` `,` `y`<br /><br /> または<br /><br /> `x` `y`|  
  
|用語|説明|  
|----------|-----------------|  
|`x`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 点の x 座標。|  
|`y`|<xref:System.Double?displayProperty=nameWithType><br /><br /> 点の y 座標。|  
  
<a name="specialvalues"></a>
## <a name="special-values"></a>特殊な値  
 標準的な数値ではなく、次の特殊な値を使用することもできます。 これらの値では、大文字と小文字が区別されます。  
  
 Infinity  
 <xref:System.Double.PositiveInfinity?displayProperty=nameWithType> を表します。  
  
 -Infinity  
 <xref:System.Double.NegativeInfinity?displayProperty=nameWithType> を表します。  
  
 NaN  
 <xref:System.Double.NaN?displayProperty=nameWithType> を表します。  
  
 指数表記を使用することもできます。 たとえば、`+1.e17` は有効な値です。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Shapes.Path>
- <xref:System.Windows.Media.StreamGeometry>
- <xref:System.Windows.Media.PathGeometry>
- <xref:System.Windows.Media.PathFigureCollection>
- [WPF での図形と基本描画の概要](shapes-and-basic-drawing-in-wpf-overview.md)
- [ジオメトリの概要](geometry-overview.md)
- [方法トピック](geometries-how-to-topics.md)
