---
title: イメージングの概要
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- metadata [WPF], images
- displaying images [WPF]
- Imaging API [WPF]
- image metadata [WPF]
- converting images [WPF]
- encoding image formats [WPF]
- format decoding for images [WPF]
- painting with images [WPF]
- stretching images [WPF]
- images [WPF], about imaging
- format encoding for images [WPF]
- cropping images [WPF]
- decoding image formats [WPF]
- rotating images [WPF]
ms.assetid: 72aad87a-e6f3-4937-94cd-a18b7766e990
ms.openlocfilehash: f8686a189883bed782cdde80e56c87ab6dbe404a
ms.sourcegitcommit: 8a0fe8a2227af612f8b8941bdb8b19d6268748e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71835024"
---
# <a name="imaging-overview"></a>イメージングの概要
このトピックでは、[!INCLUDE[TLA#tla_wic](../../../../includes/tlasharptla-wic-md.md)] の概要を説明します。 開発者は、[!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] を使用して、イメージの表示、変換、および形式設定を実行できます。  

## <a name="wpf-imaging-component"></a>WPF Imaging Component  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] は、[!INCLUDE[TLA#tla_win](../../../../includes/tlasharptla-win-md.md)] 内のイメージング機能を大幅に強化します。 ビットマップの表示や一般的なコントロールでのイメージの使用などのイメージング機能は、以前は Microsoft Windows グラフィックスデバイスインターフェイス (GDI) または Microsoft Windows GDI + ライブラリに依存していました。 これらの API は、ベースラインイメージング機能を提供しますが、コーデック拡張機能や忠実度の高いイメージのサポートなどの機能を備えていません。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] は GDI と GDI + の欠点を克服し、アプリケーション内でイメージを表示して使用するための新しい API のセットを提供するように設計されています。  
  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] API にアクセスするには、マネージコンポーネントとアンマネージコンポーネントの2つの方法があります。 アンマネージ コンポーネントは、次の機能を提供します。  
  
- 新規または独自のイメージ形式の機能拡張モデル。  
  
- ビットマップ (BMP)、ジョイント Photographics エキスパートグループ (JPEG)、ポータブルネットワークグラフィックス (PNG)、Tagged Image File Format (TIFF)、@no__t 0、グラフィックスインターチェンジ形式 (GIF)、アイコン (.ico) などのネイティブイメージ形式のパフォーマンスとセキュリティが向上しました。  
  
- チャネルあたり最大 8 ビットのビット深度の高いイメージ データの保存 (ピクセルあたり 32 ビット)。  
  
- 非破壊的なイメージのスケーリング、クロップ、および回転。  
  
- 単純化されたカラー管理。  
  
- ファイル内での専用メタデータのサポート。  
  
- マネージド コンポーネントは、アンマネージド インフラストラクチャを利用して、[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]、アニメーション、グラフィックスなどの他の [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] 機能とイメージをシームレスに統合します。 マネージコンポーネントは、アプリケーションで[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]新しいイメージ形式を自動的に認識できるようにする Windows Presentation Foundation (WPF) イメージングコーデック拡張モデルの利点もあります。  
  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)]マネージ<xref:System.Windows.Controls.Image> API の大部分は<xref:System.Windows.Media?displayProperty=nameWithType> <xref:System.Windows.Media.ImageBrush> <xref:System.Windows.Media.Imaging?displayProperty=nameWithType>名前空間に存在しますが、や<xref:System.Windows.Media.ImageDrawing>などのいくつかの重要な型は名前空間に<xref:System.Windows.Controls?displayProperty=nameWithType>存在し、空間.  
  
 このトピックでは、マネージド コンポーネントに関する追加情報について説明します。 アンマネージ API の詳細については、[アンマネージ WPF イメージングコンポーネント](/windows/desktop/wic/-wic-lh)のドキュメントを参照してください。  
  
<a name="_imageformats"></a>   
## <a name="wpf-image-formats"></a>WPF イメージ形式  
 コーデックは、特定のメディア形式をデコードまたはエンコードするために使用されます。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] には、BMP、JPEG、PNG、TIFF、@no__t 1、GIF、および ICON イメージ形式のコーデックが含まれています。 アプリケーションは、これらのコーデックを使用して、対応するイメージ形式をデコードでき、ICON を除くイメージ形式をエンコードできます。  
  
 <xref:System.Windows.Media.Imaging.BitmapSource>は、イメージのデコードとエンコードで使用される重要なクラスです。 それは、[!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] パイプラインの基本ビルディング ブロックであり、ピクセルの単一の定数セットを特定のサイズと解像度で表現します。 には、複数のフレームイメージの個別のフレームを指定する<xref:System.Windows.Media.Imaging.BitmapSource>ことも、に対して実行される変換の結果にすることもできます。<xref:System.Windows.Media.Imaging.BitmapSource> これは、のよう[!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] <xref:System.Windows.Media.Imaging.BitmapFrame>なイメージングで使用される主なクラスの多くの親です。  
  
 は<xref:System.Windows.Media.Imaging.BitmapFrame> 、イメージ形式の実際のビットマップデータを格納するために使用されます。 多くのイメージ形式でサポートされるのは1つの <xref:System.Windows.Media.Imaging.BitmapFrame> だけです。ただし、GIF や TIFF などの形式では、イメージごとに複数のフレームがサポートされます。 フレームは、デコーダーによって入力データとして使用され、イメージ ファイルを作成するためにエンコーダーに渡されます。  
  
 次の例は、@no__t から @no__t 0 が作成され、TIFF イメージに追加される方法を示しています。  
  
 [!code-csharp[BitmapFrameExample#10](~/samples/snippets/csharp/VS_Snippets_Wpf/BitmapFrameExample/CSharp/BitmapFrame.cs#10)]
 [!code-vb[BitmapFrameExample#10](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitmapFrameExample/VB/BitmapFrame.vb#10)]  
  
### <a name="image-format-decoding"></a>イメージ形式のデコード  
 イメージのデコードは、イメージ形式をシステムで使用できるイメージ データに変換する操作です。 変換したイメージ データを使用して、表示、処理、または別の形式へのエンコードを実行できます。 デコーダーの選択は、イメージ形式に基づきます。 コーデックの選択は、特定のデコーダーを指定しない限り、自動的に行われます。 自動デコード操作については、「[WPF でのイメージの表示](#_displayingimages)」セクションの例を参照してください。 アンマネージ [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] インターフェイスを使用して開発し、システムに登録したカスタム形式デコーダーは、デコーダーの選択に自動的に追加されます。 これにより、カスタム形式を [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] アプリケーションに自動的に表示することができます。  
  
 次の例は、ビットマップデコーダーを使用して、BMP 形式のイメージをデコードする方法を示しています。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#5](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#5)]
 [!code-csharp[BmpBitmapDecoderEncoder#5](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#5)]
 [!code-vb[BmpBitmapDecoderEncoder#5](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#5)]  
  
### <a name="image-format-encoding"></a>イメージ形式のエンコード  
 イメージのエンコードは、イメージ データを特定のイメージ形式に変換する操作です。 エンコードされたイメージ データを使用して、新しいイメージ ファイルを作成できます。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] には、上記で説明したイメージ形式用のエンコーダーが用意されています。  
  
 次の例は、エンコーダーを使用して新しく作成されたビットマップ イメージを保存する操作を示しています。  
  
 [!code-cpp[BmpBitmapDecoderEncoder#3](~/samples/snippets/cpp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CPP/anotherfile.cpp#3)]
 [!code-csharp[BmpBitmapDecoderEncoder#3](~/samples/snippets/csharp/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/CSharp/BitmapFrame.cs#3)]
 [!code-vb[BmpBitmapDecoderEncoder#3](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BmpBitmapDecoderEncoder/VB/BitmapFrame.vb#3)]  
  
<a name="_displayingimages"></a>   
## <a name="displaying-images-in-wpf"></a>WPF でのイメージの表示  
 Windows Presentation Foundation (WPF) アプリケーションでイメージを表示するには、いくつかの方法があります。 画像は、 <xref:System.Windows.Controls.Image>コントロールを使用して表示することも、を<xref:System.Windows.Media.ImageBrush>使用してビジュアルに<xref:System.Windows.Media.ImageDrawing>描画することも、を使用して描画することもできます。  
  
### <a name="using-the-image-control"></a>イメージ コントロールの使用  
 <xref:System.Windows.Controls.Image>はフレームワーク要素であり、アプリケーションにイメージを表示する主な方法です。 で[!INCLUDE[TLA2#tla_xaml](../../../../includes/tla2sharptla-xaml-md.md)]は<xref:System.Windows.Controls.Image> 、属性構文とプロパティ構文の2つの方法でを使用できます。 次の例は、属性構文とプロパティ タグ構文の両方を使用して、幅 200 ピクセルのイメージをレンダリングする方法を示しています。 属性構文とプロパティ構文の詳細については、「[依存関係プロパティの概要](../advanced/dependency-properties-overview.md)」を参照してください。  
  
 [!code-xaml[ImageElementExample_snip#ImageSimpleExampleInlineMarkup](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml#imagesimpleexampleinlinemarkup)]  
  
 多くの例では、 <xref:System.Windows.Media.Imaging.BitmapImage>オブジェクトを使用してイメージファイルを参照しています。 <xref:System.Windows.Media.Imaging.BitmapImage>は、読み込み<xref:System.Windows.Media.Imaging.BitmapSource>用に[!INCLUDE[TLA#tla_xaml](../../../../includes/tlasharptla-xaml-md.md)]最適化された特殊なであり、 <xref:System.Windows.Controls.Image>コントロール<xref:System.Windows.Controls.Image.Source%2A>のとしてイメージを表示する簡単な方法です。  
  
 次の例は、コードを使用して幅 200 ピクセルのイメージをレンダリングする方法を示しています。  
  
> [!NOTE]
> <xref:System.Windows.Media.Imaging.BitmapImage>インターフェイスを<xref:System.ComponentModel.ISupportInitialize>実装して、複数のプロパティの初期化を最適化します。 プロパティの変更は、オブジェクトの初期化中にのみ実行できます。 を<xref:System.Windows.Media.Imaging.BitmapImage.BeginInit%2A>呼び出して、初期化が開始さ<xref:System.Windows.Media.Imaging.BitmapImage.EndInit%2A>れたことを通知し、初期化が完了したことを通知します。 初期化の完了後は、プロパティの変更は無視されます。  
  
 [!code-csharp[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageSimpleExample.xaml.cs#imagesimpleexampleinlinecode1)]
 [!code-vb[ImageElementExample_snip#ImageSimpleExampleInlineCode1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/ImageSimpleExample.xaml.vb#imagesimpleexampleinlinecode1)]  
  
#### <a name="rotating-converting-and-cropping-images"></a>イメージの回転、変換、およびクロップ  
 [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)]ユーザーは<xref:System.Windows.Media.Imaging.BitmapImage> 、またはなど<xref:System.Windows.Media.Imaging.BitmapSource> <xref:System.Windows.Media.Imaging.CroppedBitmap>の追加のオブジェクトを使用して、のプロパティを使用してイメージを変換できます。<xref:System.Windows.Media.Imaging.FormatConvertedBitmap> これらのイメージの変換では、イメージの拡大縮小、回転、ピクセル形式の変更、またはクロップを行うことができます。  
  
 イメージの回転は、 <xref:System.Windows.Media.Imaging.BitmapImage.Rotation%2A>の<xref:System.Windows.Media.Imaging.BitmapImage>プロパティを使用して実行されます。 回転は、90 ° 単位でのみ実行できます。 次の例では、イメージが 90 ° 回転します。  
  
 [!code-xaml[ImageElementExample#TransformedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml#transformedxaml2)]  
  
 [!code-csharp[ImageElementExample#TransformedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample/CSharp/TransformedImageExample.xaml.cs#transformedcsharp1)]
 [!code-vb[ImageElementExample#TransformedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample/VB/TransformedImageExample.xaml.vb#transformedcsharp1)]  
  
 画像をグレースケールなどの別のピクセル形式に変換するに<xref:System.Windows.Media.Imaging.FormatConvertedBitmap>は、を使用します。 次の例では、イメージはに<xref:System.Windows.Media.PixelFormats.Gray4%2A>変換されます。  
  
 [!code-xaml[ImageElementExample_snip#ConvertedXAML2](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml#convertedxaml2)]  
  
 [!code-csharp[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/FormatConvertedExample.xaml.cs#convertedcsharp1)]
 [!code-vb[ImageElementExample_snip#ConvertedCSharp1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/FormatConvertedExample.xaml.vb#convertedcsharp1)]  
  
 イメージをトリミングするには、 <xref:System.Windows.UIElement.Clip%2A>または<xref:System.Windows.Controls.Image> <xref:System.Windows.Media.Imaging.CroppedBitmap>のいずれかのプロパティを使用できます。 通常、イメージの一部だけを表示する場合は、を<xref:System.Windows.UIElement.Clip%2A>使用する必要があります。 トリミングされたイメージをエンコードして保存する必要<xref:System.Windows.Media.Imaging.CroppedBitmap>がある場合は、を使用する必要があります。 次の例では、を使用<xref:System.Windows.Media.EllipseGeometry>して、クリッププロパティを使用してイメージをトリミングします。  
  
 [!code-xaml[ImageElementExample_snip#CroppedXAMLUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml#croppedxamlusingclip1)]  
  
 [!code-csharp[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/CroppedImageExample.xaml.cs#croppedcsharpusingclip1)]
 [!code-vb[ImageElementExample_snip#CroppedCSharpUsingClip1](~/samples/snippets/visualbasic/VS_Snippets_Wpf/ImageElementExample_snip/VB/CroppedImageExample.xaml.vb#croppedcsharpusingclip1)]  
  
#### <a name="stretching-images"></a>イメージの引き伸ばし  
 プロパティ<xref:System.Windows.Controls.Image.Stretch%2A>は、コンテナーを埋めるためにイメージをどのように拡大するかを制御します。 プロパティ<xref:System.Windows.Controls.Image.Stretch%2A>は、 <xref:System.Windows.Media.Stretch>列挙体で定義されている次の値を受け入れます。  
  
- <xref:System.Windows.Media.Stretch.None>:イメージは、出力領域に合わせて拡大されません。 イメージが出力領域よりも大きい場合は、出力領域に収まらない部分がクリップされたイメージが出力領域に描画されます。  
  
- <xref:System.Windows.Media.Stretch.Fill>:イメージは、出力領域に合わせて拡大縮小されます。 イメージの高さと幅は個別に拡大縮小されるため、イメージの元の縦横比は保持されないことがあります。 つまり、イメージは、出力コンテナーを完全に埋めるためにゆがんで表示される可能性があります。  
  
- <xref:System.Windows.Media.Stretch.Uniform>:イメージは、出力領域内に完全に収まるようにスケーリングされます。 イメージの縦横比は保持されます。  
  
- <xref:System.Windows.Media.Stretch.UniformToFill>:イメージは、イメージの元の縦横比を維持したまま、出力領域を完全に塗りつぶすようにスケーリングされます。  
  
 次の例では、使用可能<xref:System.Windows.Media.Stretch>な各列挙<xref:System.Windows.Controls.Image>をに適用します。  
  
 次の図は、この例の出力を示しています。 <xref:System.Windows.Controls.Image.Stretch%2A>イメージに適用する場合のさまざまな設定の影響を示しています。  
  
 ![TileBrush のさまざまな Stretch 設定](./media/img-mmgraphics-stretchenum.jpg "img_mmgraphics_stretchenum")  
異なる Stretch 設定  
  
 [!code-xaml[ImageElementExample_snip#ImageStretchExampleWholePage](~/samples/snippets/csharp/VS_Snippets_Wpf/ImageElementExample_snip/CSharp/ImageStretchExample.xaml#imagestretchexamplewholepage)]  
  
### <a name="painting-with-images"></a>イメージによる塗りつぶし  
 画像は、を<xref:System.Windows.Media.Brush>使用してアプリケーションに表示することもできます。 ブラシを使用すると、[!INCLUDE[TLA2#tla_ui](../../../../includes/tla2sharptla-ui-md.md)] オブジェクトを単色で塗りつぶすことも、パターンとイメージの複雑な組み合わせで塗りつぶすこともできます。 イメージで描画するには<xref:System.Windows.Media.ImageBrush>、を使用します。 は、そのコンテンツを<xref:System.Windows.Media.TileBrush>ビットマップイメージとして定義するの一種です。 <xref:System.Windows.Media.ImageBrush> は<xref:System.Windows.Media.ImageBrush> 、 <xref:System.Windows.Media.ImageBrush.ImageSource%2A>プロパティによって指定された1つのイメージを表示します。 イメージがゆがまないようしたり、パターンやその他の効果を作成したりするために、イメージの伸縮、配置、およびタイル表示方法を制御できます。 次の図は、 <xref:System.Windows.Media.ImageBrush>で実現できるいくつかの効果を示しています。  
  
 ![Imagebrush の出力例](./media/wcpsdk-mmgraphics-imagebrushexamples.gif "wcpsdk_mmgraphics_imagebrushexamples")  
イメージ ブラシは、図形、コントロール、テキストなどを塗りつぶすことができる  
  
 次の例は、を使用して<xref:System.Windows.Media.ImageBrush>、イメージでボタンの背景を描画する方法を示しています。  
  
 [!code-xaml[UsingImageBrush#4](~/samples/snippets/csharp/VS_Snippets_Wpf/UsingImageBrush/CS/PaintingWithImages.xaml#4)]  
  
 イメージと画像の描画の詳細については[、「イメージ、描画、およびビジュアルによる塗りつぶし](painting-with-images-drawings-and-visuals.md)」を参照してください。 <xref:System.Windows.Media.ImageBrush>  
  
<a name="_metadata"></a>   
## <a name="image-metadata"></a>イメージのメタデータ  
 一部のイメージ ファイルには、ファイルの内容または特性を記述するメタデータが含まれています。 たとえば、ほとんどのデジタル カメラは、イメージをキャプチャするために使用されるカメラの型番に関するメタデータを含むイメージを作成します。 各イメージ形式は、メタデータを異なる方法で処理しますが、[!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] では、サポートしているイメージ形式のメタデータの格納と取得を一律に実行します。  
  
 メタデータへ<xref:System.Windows.Media.Imaging.BitmapSource>のアクセスは、 <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A>オブジェクトのプロパティを通じて提供されます。 <xref:System.Windows.Media.Imaging.BitmapSource.Metadata%2A>イメージに含まれるすべてのメタデータを含むオブジェクトを返します。<xref:System.Windows.Media.Imaging.BitmapMetadata> このデータは、1 つのメタデータ スキーマでも、異なるスキーマの組み合わせでもかまいません。 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] では、次のイメージメタデータスキーマがサポートされています。イメージファイル (Exif)、テキスト (PNG テキストデータ)、イメージファイルディレクトリ (IFD)、および [!INCLUDE[TLA#tla_xmp](../../../../includes/tlasharptla-xmp-md.md)] を変更できます。  
  
 メタデータの読み取りプロセスを簡略化するために<xref:System.Windows.Media.Imaging.BitmapMetadata> 、には、、などの簡単にアクセス<xref:System.Windows.Media.Imaging.BitmapMetadata.Author%2A> <xref:System.Windows.Media.Imaging.BitmapMetadata.Title%2A> <xref:System.Windows.Media.Imaging.BitmapMetadata.CameraModel%2A>できる名前付きプロパティがいくつか用意されています。 これらの名前付きプロパティの多くは、メタデータを書き込むためにも使用できます。 メタデータを読み取るための追加サポートは、メタデータ クエリ リーダーによって提供されます。 メソッド<xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A>は、 *"/app1/exif/"* などの文字列クエリを指定することによって、メタデータクエリリーダーを取得するために使用されます。 次の例では<xref:System.Windows.Media.Imaging.BitmapMetadata.GetQuery%2A> 、を使用して、 *"/Text/Description"* の場所に格納されているテキストを取得します。  
  
 [!code-cpp[BitmapMetadata#GetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#getquery)]
 [!code-csharp[BitmapMetadata#GetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#getquery)]
 [!code-vb[BitmapMetadata#GetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#getquery)]  
  
 メタデータを書き込むには、メタデータ クエリ ライターが使用されます。 <xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A>クエリライターを取得し、目的の値を設定します。 次の例では<xref:System.Windows.Media.Imaging.BitmapMetadata.SetQuery%2A> 、を使用して、 *"/Text/Description"* の場所に格納されているテキストを書き込みます。  
  
 [!code-cpp[BitmapMetadata#SetQuery](~/samples/snippets/cpp/VS_Snippets_Wpf/BitMapMetadata/CPP/BitmapMetadata.cpp#setquery)]
 [!code-csharp[BitmapMetadata#SetQuery](~/samples/snippets/csharp/VS_Snippets_Wpf/BitMapMetadata/CSharp/BitmapMetadata.cs#setquery)]
 [!code-vb[BitmapMetadata#SetQuery](~/samples/snippets/visualbasic/VS_Snippets_Wpf/BitMapMetadata/VB/BitmapMetadata.vb#setquery)]  
  
<a name="_extensibility"></a>   
## <a name="codec-extensibility"></a>コーデックの機能拡張  
 [!INCLUDE[TLA2#tla_wic](../../../../includes/tla2sharptla-wic-md.md)] の核心的な機能は、新しいイメージ コーデック用の機能拡張モデルです。 これらのアンマネージ インターフェイスによって、コーデック開発者は、コーデックを [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] と統合して、新しいイメージ形式を [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] アプリケーションで自動的に使用できるようにすることができます。  
  
 機能拡張 API のサンプルについては、 [Win32 サンプルコーデック](https://go.microsoft.com/fwlink/?LinkID=160052)を参照してください。 このサンプルは、カスタム イメージ形式用のデコーダーとエンコーダーの作成方法を示しています。  
  
> [!NOTE]
> システムで認識するは、コーデックをデジタル署名する必要があります。  
  
## <a name="see-also"></a>関連項目

- <xref:System.Windows.Media.Imaging.BitmapSource>
- <xref:System.Windows.Media.Imaging.BitmapImage>
- <xref:System.Windows.Controls.Image>
- <xref:System.Windows.Media.Imaging.BitmapMetadata>
- [2D グラフィックスとイメージング](../advanced/optimizing-performance-2d-graphics-and-imaging.md)
- [Win32 サンプル コーデック](https://go.microsoft.com/fwlink/?LinkID=160052)
